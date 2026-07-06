# 🔐 Nazarii Savon — Security & IAM Lab Portfolio

Aspiring **Identity & Access Management (IAM) / Cybersecurity** professional. IT technician background, currently completing Microsoft's **AZ-500: Azure Security Technologies**, plus a self-built on-prem IAM home lab (Keycloak + Windows Server AD).

📧 nazarij77777@gmail.com · 📍 Warsaw, Poland · [LinkedIn](#) *(add your link)*

---

## ⚡ At a glance

| | |
|---|---|
| **Cloud identity & access** | RBAC, Microsoft Entra ID, Just-in-Time VM access, Conditional Access/MFA |
| **Network security** | NSGs, Azure Firewall, service endpoints, network segmentation |
| **Data protection** | Key Vault, SQL Always Encrypted, data classification, auditing |
| **SIEM/SOAR** | Microsoft Sentinel, KQL, Logic Apps automation |
| **On-prem IAM** | Windows Server Active Directory, Keycloak (LDAP federation) |
| **Scripting** | PowerShell, Azure CLI, ARM templates |

---

## 📋 Labs completed — all 11 official AZ-500 labs + 1 self-directed home lab

| # | Lab | Outcome | Details |
|---|---|---|---|
| 01 | Role Based Access Control | Built 3-tier Entra ID group structure, assigned RBAC roles, verified via CLI/PowerShell | [→](./labs/lab01.md) |
| 02 | NSGs & Application Security Groups | Configured web/RDP inbound rules, verified IIS reachable as designed | [→](./labs/lab02.md) |
| 03 | Azure Firewall | Deployed firewall, confirmed unauthorized outbound traffic correctly blocked | [→](./labs/lab03.md) |
| 04 | Securing ACR & AKS | Diagnosed empty registry via `kubectl`, fixed with `az acr import`, verified pod-to-pod networking | [→](./labs/lab04.md) |
| 05 | Securing Azure SQL Database | Applied data classification (15 columns), configured & verified SQL auditing | [→](./labs/lab05.md) |
| 06 | Service Endpoints & Storage | Proved network segmentation: private VM ✅storage/❌internet, public VM reverse | [→](./labs/lab06.md) |
| 07 | Key Vault — Always Encrypted | Built working Always Encrypted demo app querying encrypted SQL columns via Key Vault | [→](./labs/lab07.md) |
| 08 | Log Analytics, Storage, DCR | Deployed monitoring foundation (DCR, workspace, VM) reused by Labs 09 & 11 | [→](./labs/lab08.md) |
| 09 | Defender for Cloud | Enabled Defender for Servers Plan 2, unlocking JIT VM access | [→](./labs/lab09.md) |
| 10 | Just-in-Time VM Access | Configured & used time-boxed RDP access, verified prerequisites | [→](./labs/lab10.md) |
| 11 | Microsoft Sentinel (SIEM/SOAR) | Built full detection→automation pipeline: KQL rule → incident → playbook, verified end-to-end | [→](./labs/lab11.md) |
| 🏠 | **Home Lab:** Keycloak + Windows AD | Built AD domain (OUs, users, groups, service account) + Keycloak on Ubuntu for LDAP federation | [→](./labs/homelab.md) |

*Each link opens a detailed write-up: objective, what was done, challenges & fixes, and screenshots.*

---

## 🧰 Full skills list

**Identity & Access:** Microsoft Entra ID · RBAC · Conditional Access/MFA · Windows AD DS · Keycloak (LDAP/SSO) · Just-in-Time VM access
**Network Security:** VNets · NSGs · Azure Firewall · Service Endpoints
**Data Protection:** Azure Key Vault · Always Encrypted · SQL Data Classification & Auditing
**Cloud/Containers:** AKS · ACR · Kubernetes (`kubectl`)
**Monitoring & SOC:** Microsoft Sentinel · KQL · Azure Monitor · Log Analytics · Logic Apps
**Cloud Security Posture:** Microsoft Defender for Cloud
**Systems Admin:** Windows Server · Ubuntu Server
**Scripting/IaC:** PowerShell · Azure CLI · ARM templates

---

## 🚀 Deploying this portfolio (GitHub Pages)

See [DEPLOY.md](./DEPLOY.md) for step-by-step instructions.

## 📸 Adding screenshots

Each lab file references images like `../screenshots/lab01-1.png`. Add your PNG/JPG files to the `screenshots/` folder using matching filenames — they'll render automatically on GitHub.
