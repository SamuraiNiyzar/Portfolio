[← Back to portfolio home](../README.md)

# Home Lab — Keycloak (Ubuntu) + Windows Server Active Directory

**Objective:** Self-directed IAM lab outside the AZ-500 curriculum — stand up a Windows Server domain controller with a realistic Active Directory structure, and deploy Keycloak on Ubuntu Server as an external Identity Provider, federated to that AD via LDAP.

**Architecture:**
```
┌─────────────────────────────┐          LDAP (389/636)         ┌──────────────────────────┐
│  Windows Server VM           │ <──────────────────────────────>│  Ubuntu Server VM         │
│  Active Directory Domain     │   bind: svc-keycloak account    │  Keycloak (Docker/local)  │
│  Services — domain: lab.local│                                  │  User Federation → AD LDAP│
└─────────────────────────────┘                                  └──────────────────────────┘
```

**Part 1 — Windows Server: Active Directory Domain Services**

- Configured a Windows Server VM as a domain controller for `lab.local`, including networking mode changes (NAT → Bridged) for proper lab connectivity between VMs
- Built out an OU structure to mirror a real organizational hierarchy:
  ```
  DC=lab,DC=local
  └── OU=IAM-Lab
      ├── OU=Users
      ├── OU=Groups
      └── OU=Service Accounts
  ```
- Created test user accounts (`alice`, `bob`) and security groups (`IAM-Admins`, `IAM-Users`), with group membership assignments reflecting a real-world admin/standard-user separation
- Created a dedicated **service account** (`svc-keycloak`) with a non-expiring password — this is the bind account Keycloak uses to query AD over LDAP, following the principle of using scoped service accounts rather than domain admin credentials for application integrations
- Diagnosed and resolved an `ADPasswordComplexityException` when creating accounts with `New-ADUser`, aligning generated passwords to the domain's default password policy
- Verified the full AD structure using `Get-ADUser`, `Get-ADGroup`, and `Get-ADOrganizationalUnit`

**Part 2 — Ubuntu Server: Keycloak deployment & AD federation**

- Deployed a second VM running **Ubuntu Server**, provisioned as the host for **Keycloak**
- Planned integration: configure Keycloak's **User Federation** provider to bind against `lab.local` using the `svc-keycloak` service account, over LDAP, so that AD users (`alice`, `bob`) and groups (`IAM-Admins`, `IAM-Users`) become available as Keycloak-managed identities — enabling centralized SSO for downstream applications without duplicating user records

**Challenges & fixes:**

| Issue | Root Cause | Fix |
|---|---|---|
| Server Manager showed a benign-looking cached-server-list error after switching network adapter from NAT to Bridged | Server Manager caches a server list that becomes invalid when the network adapter/context changes | Cleared the cache (`Remove-Item ServerList.xml`) and restarted Server Manager; confirmed AD itself was unaffected via `Get-ADDomain` |
| `New-ADUser` failed with `ADPasswordComplexityException` | Supplied password didn't meet the domain's default complexity policy | Verified policy with `Get-ADDefaultDomainPasswordPolicy`; used a compliant password |
| `svc-keycloak` account missing from `Get-ADUser -Filter *` results | Account had failed silently on first creation attempt | Re-ran `New-ADUser` explicitly and verified with a targeted `-SearchBase` query scoped to the IAM-Lab OU |

**Skills demonstrated:** Windows Server / Active Directory Domain Services, OU design, Group Policy password requirements, PowerShell AD administration (`New-ADUser`, `New-ADGroup`, `Add-ADGroupMember`), service account provisioning for LDAP-based application integration, Ubuntu Server administration, Keycloak deployment, LDAP federation design, Hyper-V/VM networking troubleshooting.

**Status:** ✅ AD domain, OU structure, users, groups, and service account complete and verified · 🔜 Keycloak LDAP User Federation configuration in progress

<p>
  <img src="../screenshots/homelab-1.png" width="45%" alt="Active Directory Users and Computers showing IAM-Lab OU structure" />
  <img src="../screenshots/homelab-2.png" width="45%" alt="PowerShell output verifying users, groups, and OUs" />
</p>
<p>
  <img src="../screenshots/homelab-3.png" width="45%" alt="Ubuntu Server terminal showing Keycloak installation/service status" />
  <img src="../screenshots/homelab-4.png" width="45%" alt="Keycloak admin console User Federation LDAP configuration" />
</p>
