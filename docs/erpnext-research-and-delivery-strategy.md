# ERPNext Research and DVS Delivery Strategy

## Executive Summary

The open-source ERP base we should validate with the client is most likely **ERPNext by Frappe**. The name is often confused in conversation as "NextERP", but the well-known open-source project is:

- ERPNext: <https://github.com/frappe/erpnext>
- Frappe Framework: <https://github.com/frappe/frappe>
- Frappe HR / HRMS: <https://github.com/frappe/hrms>
- Official Docker deployment: <https://github.com/frappe/frappe_docker>

ERPNext already includes many of the business modules DVS Technosoft may need. Frappe HR already includes employee check-in/check-out, mobile PWA access, geolocation capture, and geofencing via Shift Location. This means the phase-1 goal should be to configure and extend existing ERPNext/Frappe capabilities before building custom features from scratch.

If the client actually means a different open-source product named "NextERP", we need the exact repository URL before implementation starts.

## Core Product Stack

ERPNext is built on the Frappe Framework.

Typical stack:

- Python backend on Frappe Framework
- JavaScript frontend
- MariaDB database
- Redis for cache and queues
- Background workers for async jobs
- Scheduler for scheduled tasks
- Socket.IO/websocket service for real-time behavior
- Nginx or Traefik as reverse proxy
- Bench CLI for development and site/app management
- Docker Compose recommended for production-style deployment

## ERPNext Built-In Modules

ERPNext version 15 module list includes:

- Accounts
- CRM
- Buying
- Projects
- Selling
- Setup
- Manufacturing
- Stock
- Support
- Utilities
- Assets
- Portal
- Maintenance
- Regional
- ERPNext Integrations
- Quality Management
- Communication
- Telephony
- Bulk Transaction
- Subcontracting
- EDI

Frappe HR / HRMS adds:

- HR
- Payroll

Frappe HR feature areas include:

- Employee management
- Employee lifecycle
- Leave and attendance
- Shift management
- Expense claims and advances
- Hiring
- Performance management
- Fleet management
- Training
- Payroll
- Taxation
- Compensation
- Analytics

## Field Attendance and Mobile App Findings

Frappe HR already supports the core DVS requirement.

Relevant built-in settings and fields:

- HR Settings has `Allow Employee Checkin from Mobile App`.
- HR Settings has `Allow Geolocation Tracking`.
- Employee Checkin has:
  - Employee
  - Log Type: IN / OUT
  - Time
  - Shift
  - Location / Device ID
  - Geolocation
  - Latitude
  - Longitude
  - Fetch Geolocation button
- Frappe HR v15 ships with a mobile frontend as a PWA at:
  - `https://<site-domain>/hrms`

Mobile installation:

- Android: open `/hrms` in Chrome and install/add to home screen.
- iOS: open `/hrms` in Safari and use Add to Home Screen.

Geofencing:

- Frappe HR includes Shift Location.
- Shift Location can store latitude, longitude, and check-in radius.
- If geolocation tracking is enabled and the employee is assigned to a shift location, check-in can be restricted to the configured radius.

Recommended DVS position:

- Do not build native Android/iOS apps in phase 1 unless DVS explicitly requires branded store apps.
- First use Frappe HR PWA/mobile frontend.
- Test Android Chrome and iPhone Safari with real devices.
- Use coordinate capture only during check-in/check-out, not continuous tracking.
- Customize only if DVS needs extra flows such as site visit linkage, photo proof, customer/project reference, approval exceptions, or map-based manager reports.

Third-party app note:

- Generic URL/browser apps and Frappe mobile wrapper apps exist, but they should not be the primary dependency for phase 1.
- PWA is cleaner because it is tied directly to the ERP domain and Frappe HR app.
- A wrapper/native app can be evaluated later if DVS wants branding, push notifications, device binding, stronger native GPS controls, or app-store distribution.

## Recommended Customization Strategy

Avoid modifying ERPNext, Frappe, or HRMS core source files directly.

Use a separate custom Frappe app for DVS-specific logic, for example:

- `dvs_custom`
- `dvs_technosoft`

Use the custom app for:

- Custom fields on standard DocTypes
- Custom DocTypes
- Workflows and approval rules
- Custom reports
- Custom dashboards
- Print formats
- Client scripts
- Server scripts where suitable
- Python hooks for deeper business logic
- Fixtures to version-control UI customizations
- Data patches for controlled migrations

This keeps the implementation more upgrade-safe and easier to deploy across development, staging, and production.

## AWS Deployment Direction

The proposed `m6a.large` with 50 GB storage is a reasonable starting point for a 50-55 employee phase-1 deployment if scope and document storage are controlled. Final sizing should be validated after module scope, file upload volume, data migration volume, and concurrent users are known.

### Practical Phase-1 Architecture

Option A: single EC2 instance, lower initial complexity

- EC2: `m6a.large`
- Storage: 50 GB gp3 initially, with monitoring and expansion plan
- Docker Compose running ERPNext/Frappe services
- MariaDB container
- Redis containers
- Frappe backend/frontend/workers/scheduler/websocket
- HTTPS via Traefik or Nginx + Let's Encrypt
- Backups pushed to S3

Option B: more reliable production architecture

- EC2 for ERPNext/Frappe containers
- RDS MariaDB for managed database backups and reliability
- S3 for file backups and optional document storage
- CloudWatch monitoring and alerts
- Optional ElastiCache later if needed

Recommended starting point:

- Use Option A for controlled budget if DVS accepts it.
- Use Option B if DVS wants stronger reliability, easier backups, and reduced database maintenance.
- Regardless of option, configure off-server backups from day one.

## Subdomain and Client Prerequisites

Ask DVS to confirm:

- ERP subdomain, for example `erp.dvstechnosoft.com`.
- Who controls DNS.
- Whether they can create an A record pointing to the AWS public IP.
- Whether they want ERP under their AWS account or managed by implementation team.
- AWS region preference.
- Admin email for SSL/alerts.
- SMTP/email sending details.
- Expected users and concurrent users.
- Data migration files.
- Current attendance process.
- Whether Frappe HR PWA is acceptable for Android/iOS attendance.

For PWA/mobile location features, HTTPS is required. A real domain/subdomain is strongly preferred over raw IP access.

## Setup Path to Validate

Development/staging setup:

1. Set up bench or Docker-based development environment.
2. Install Frappe/ERPNext version 15 or stable version selected for project.
3. Install HRMS app.
4. Optionally install India Compliance app if GST/e-invoicing/GSTR features are required.
5. Create a site such as `staging.erp.dvstechnosoft.com`.
6. Configure company, users, roles, departments, employees, shifts, and attendance settings.
7. Enable mobile check-in and geolocation settings.
8. Test `/hrms` PWA on Android and iOS.
9. Identify gaps requiring DVS custom app.

Typical bench commands for a manual setup are:

```bash
bench init frappe-bench --frappe-branch version-15
cd frappe-bench
bench new-site erp.example.com
bench get-app --branch version-15 erpnext
bench get-app --branch version-15 hrms
bench --site erp.example.com install-app erpnext
bench --site erp.example.com install-app hrms
```

Production should preferably use the official Docker deployment path from `frappe/frappe_docker`, not an improvised server setup.

## DVS Module Mapping

Likely built-in or mostly configurable:

- Employee master: Frappe HR
- Attendance and leave: Frappe HR
- Mobile check-in: Frappe HR PWA
- GPS coordinates: Frappe HR Employee Checkin
- Geofencing: Frappe HR Shift Location
- CRM/leads/opportunities: ERPNext CRM
- Quotations and sales: ERPNext Selling
- Purchase/vendor: ERPNext Buying
- Inventory/stores: ERPNext Stock
- Projects/jobs: ERPNext Projects
- Support/service tickets: ERPNext Support
- Manufacturing/panel shop basics: ERPNext Manufacturing
- Asset tracking: ERPNext Assets
- Quality/FAT checklists: ERPNext Quality Management, possibly customized
- Portal: ERPNext Portal
- Accounts/invoicing: ERPNext Accounts

Likely customization areas:

- DVS-specific project stages and terminology.
- Field site visit linked to customer/project/service ticket.
- Attendance exception workflow.
- Manager map/report view for field check-ins.
- Customer-specific service report PDF.
- FAT/commissioning checklist formats.
- Quotation print formats.
- Role profiles and permission tuning.
- Management dashboards.
- Data import templates.
- Tally integration, if required.

## Five-Month Delivery Window Strategy

The delivery window can work if phase 1 remains controlled and we use ERPNext/Frappe built-ins wherever possible.

### Phase 1: Discovery, Scope Lock, and Technical Baseline

Outputs:

- Confirm exact upstream software: ERPNext/Frappe or another NextERP repository.
- Confirm phase-1 modules.
- Confirm AWS/subdomain ownership.
- Confirm mobile attendance approach.
- Confirm data migration scope.
- Confirm approval workflows and reports.
- Stand up a working ERPNext + HRMS staging instance.
- Prepare gap analysis against DVS requirements.

### Phase 2: Core ERP Setup

Outputs:

- Company setup.
- Departments, designations, employees, roles, and permissions.
- HR, attendance, leave, shift, and geolocation settings.
- CRM/customer/vendor/project masters.
- Initial print formats and branding.
- Baseline dashboards.

### Phase 3: DVS Custom App and Workflow Customization

Outputs:

- Custom app created and version-controlled.
- Custom fields, workflows, reports, and print formats exported as fixtures.
- Project/job flow customized for DVS operations.
- Service/field visit flow customized if confirmed.
- Document management structure configured.
- Data import templates prepared.

### Phase 4: Mobile Attendance, Reports, and UAT Hardening

Outputs:

- Android/iOS PWA check-in tested.
- GPS and geofencing tested with real locations.
- Attendance exception handling finalized.
- Manager/admin field attendance reports.
- Required dashboards and exports.
- Data migration dry run.
- User acceptance testing by module.

### Phase 5: Production Cutover and Training

Outputs:

- Production AWS environment ready.
- Domain/subdomain, SSL, backups, monitoring configured.
- Final approved data imported.
- Admin and user training completed.
- Field engineer mobile attendance guide prepared.
- Go-live checklist completed.
- Post-go-live issue tracker active.

## Scope Control

Recommended phase-1 must-haves:

- Employee master
- Roles and permissions
- Attendance and leave
- Field/mobile GPS attendance
- CRM and quotation tracking
- Project/job tracking
- Service/field visit tracking if DVS confirms it is operationally critical
- Documents
- Basic dashboards
- AWS deployment, backups, and monitoring

Defer unless critical:

- Full payroll
- Deep accounting replacement
- Tally real-time integration
- Advanced inventory automation
- Barcode/QR flows
- Full manufacturing/BOM automation
- Customer/vendor portals
- Native Android/iOS app
- Advanced BI

## Questions for the Client

Critical questions for the 2 June meeting:

1. Do you mean ERPNext by Frappe, or a different open-source project called NextERP?
2. Can you create a subdomain such as `erp.dvstechnosoft.com`?
3. Who will control AWS: DVS account or implementation team account?
4. Is Frappe HR PWA acceptable for Android/iOS attendance?
5. Should attendance capture GPS at check-in only, check-out only, or both?
6. Do you need geofencing by office/customer/site?
7. Do you need selfie/photo proof?
8. Which modules are must-have for first release?
9. Will accounting remain in Tally?
10. Do you need ERPNext-to-Tally integration or only exports/imports?
11. What data needs to be migrated before go-live?
12. Who will approve scope and UAT?

## Immediate Next Steps

1. Confirm the exact upstream ERP repository.
2. Set up a staging ERPNext + HRMS instance.
3. Validate HRMS PWA check-in with GPS on Android and iOS.
4. Run the DVS discovery meeting using the questionnaire.
5. Convert confirmed requirements into a Notion task backlog.
6. Create the DVS custom app only after gaps are confirmed.
