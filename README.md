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
| Fineract Core (API + DB) | https://cbs.amberbank.x.lt| 100.10x.3.33:8443  | Ensure HTTPS; reachable from AmberBank subnet |
| Mifos WebApp (Back Office) | http://bankwebadm.amberbank.x.lt | 100.10x.3.76:4200 | Staff console; check static assets & API base URL |
| Self Service UI (Online) | http://bankwebcli.amberbank.x.lt | 100.10x.3.77:3000 | Client portal; verify CORS/API connectivity |

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
| Mifos WebApp | 4200 (HTTP), 22 (SSH) |
| Self Service | 3000 (HTTP), 22 (SSH) |

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
- SSH on port 22. Exercise default: Username: root / Password: changeme.

---

## 9) Quick start (common tasks)

### Back Office (Mifos WebApp)
1. Open http://bankwebadm.amberbank.x.lt:4200 and sign in.  

### Self Service (Client)
1. Open http://bankwebcli.amberbank.x.lt:3000 and sign in.  

### Core API (Fineract)
1. Use https://cbs.amberbank.x.lt:8443 with curl/Postman.  
2. Call endpoints (e.g., GET /clients, GET /loans).  
3. Confirm authentication, tenant headers and request format.

---

## 10) Troubleshooting & tips
- CORS errors: ensure API/reverse proxy returns Access‑Control‑Allow‑Origin for UI origins and UI uses correct API base URL (HTTPS for 8443).  
- HTTP 400 with HTML body: check path, method, headers (Content-Type: application/json), and JSON body.  
- TLS / EPROTO issues: match HTTPS, validate cert chain; avoid forcing HTTP/2 with self‑signed certs.  
- UI won’t load / API 401: verify credentials, roles, and UI environment API origin.  
- Connectivity: confirm ports 8443/4200/3000 reachable from AmberBank subnet; check DNS, firewalls, proxies.

---

## 11) Additional resources
- Mifos & Fineract API Overview: https://mifos.readme.io/reference/overview-1  
- Mifos X — Getting Started: https://mifosforge.jira.com/wiki/spaces/docs/pages/107479067/Getting+started

