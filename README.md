# CBShandbook
Corebankingsystemhandbook
# AmberBank Fineract / Mifos Handbook

## Table of contents
1. System overview & purpose  
2. Main features  
3. Access points & management  
4. Who uses what  
5. Default credentials (exercise)  
6. Ports in use  
7. Key requirements  
8. Operational guidelines  
9. Quick start (common tasks)  
10. Troubleshooting & tips  
11. Additional resources

---
<img width="1300" height="715" alt="image" src="https://github.com/user-attachments/assets/beb30d72-68ac-4ae3-b484-0d76d2c3ee99" />

## 1) System overview & purpose

### Apache Fineract (Core Banking Server)
- Purpose: Core transactional engine (clients, loans, savings, accounting). Exposes a secure REST API.
- Use cases: Product setup, accounting integration, tenant configuration, back‑office operations via API, single source of truth.

### Mifos WebApp (Back‑Office UI)
- Purpose: Staff console layered on Fineract for day‑to‑day operations.
- Use cases: Client onboarding, product configuration, approvals, collections, accounting, reports, admin.

### Self Service UI (Online Banking)
- Purpose: Client‑facing portal for end users.
- Use cases: View balances/schedules, make repayments/transfers, manage beneficiaries. Shows only client‑visible data (no internal notes or approval workflows).

---

## 2) Main features

### Fineract (Core)
- Multi‑tenant modular REST API: clients, groups, loans, savings, charges, fees, penalties.
- Loan engine: scheduling, interest, arrears, rescheduling, write‑offs, refinances.
- Savings & deposits: interest posting, standing instructions, transfers.
- Accounting: COA, GL entries, trial balance, closures, financial reports.
- Security: RBAC, maker‑checker, audit trails.
- Integrations: web/mobile apps, payment hubs/gateways, reporting tools.

### Mifos WebApp (Back Office)
- Client & group management, KYC, documents, photos.
- Loan and savings lifecycle management.
- Accounting workspace and admin (offices, staff, roles, templates).
- Dashboards & reports for portfolio/risk.

### Self Service UI (Online Banking)
- Client login and role‑appropriate access.
- View accounts, statements, schedules, charges; perform repayments/transfers.
- Profile management and basic notifications.
- Strictly limited to client’s own data.

---

## 3) Access points & management

| Component | Primary URL | IP | Notes |
|---|---|---:|---|
| Fineract Core (API + DB) | | 100.10x.3.33:8443  | Ensure HTTPS; reachable from AmberBank subnet |
| Mifos WebApp (Back Office) | http://adm.amberbank.x.lab | 100.10x.3.33:80 | Staff console; check static assets & API base URL |
| Self Service UI (Online) | http://ib.amberbank.x.lab | 100.10x.3.33:8080 | Client portal; verify CORS/API connectivity |

Note: AmberBank subnet access required. Verify routing, DNS and firewall rules.

---

## 4) User access — who uses what?
- System Administrators: Fineract API/admin, SSH to servers. Manage tenants, products, users, integrations.
- Back‑Office Staff / Loan Officers: Mifos WebApp for onboarding, approvals, collections, accounting, reports.
- Clients (End Users): Self Service UI for their own accounts and transactions.

---

## 5) Default credentials.

Fineract  
- Admin: root / changeme

Mifos Web UI  
- Admin: Mifos / password  
- Employees (amberbank AD/DC): {name.lastname} / Pa5w0rd123456*

Self Service UI  
- Admin: Mifos / password  
- Employees (amberbank AD/DC): {name.lastname} / Pa5w0rd123456*

(Important: rotate these credentials.)

---

## 6) Ports in use

| Component | Ports |
|---|---|
| Fineract | 8443 (HTTPS), 22 (SSH) |
| Mifos WebApp | 8080 (HTTP), 22 (SSH) |
| Self Service | 80 (HTTP), 22 (SSH) |

---

## 7) Key requirements
- Accessibility: reachable from AmberBank subnet.  
- Web UI readiness: static assets, environment config, API base URLs must load.  
- Admin access: admin interfaces available to authorized admins.  
- Content integrity: prevent unauthorized tampering with products, GL, or client data.

---

## 8) Operational guidelines

### System stability
- Monitor processes, logs, CPU/RAM, DB connections.

### Security monitoring
- Collect and review API, application, and SSH logs.
- Review roles/permissions; apply least privilege.

### SSH & remote management
- SSH on port 22. Exercise default: Username: root / Password: abcd.1234.

---

## 9) Quick start (common tasks)

### Back Office (Mifos WebApp)
1. Open http://ib.amberbank.x.lt and sign in.  

### Self Service (Client)
1. Open http://adm.amberbank.x.lt and sign in.  


---

## 10) Troubleshooting & tips
- Cant't login through self-service/web-app: access https://100.10x.3.33:8443 and accept the risk.
- UI won’t load / API 401: verify credentials, roles, and UI environment API origin.  
- Connectivity: confirm ports 8443/80/8080 reachable from AmberBank subnet; check DNS, firewalls, proxies.

---

## 11) Additional resources
- Mifos & Fineract API Overview: https://mifos.readme.io/reference/overview-1  
- Mifos X — Getting Started: https://mifosforge.jira.com/wiki/spaces/docs/pages/107479067/Getting+started

