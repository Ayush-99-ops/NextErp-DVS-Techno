# ERPNext Implementation Playbook for DVS Technosoft

## Purpose

This playbook keeps ERPNext implementation knowledge, client operating assumptions, setup decisions, and delivery steps in one place so that once DVS Technosoft confirms requirements, implementation can start without re-learning the basics.

Confirmed correction: the open-source base is **ERPNext**, not a separate "NextERP" product.

## Current Client Context

- Client: DVS Technosoft
- Approximate employee count: 50-55
- First discovery meeting: 2 June 2026
- Delivery expectation: production-ready phase-1 ERP within a 5-month window
- Hosting preference: AWS
- Initial infrastructure idea: `m6a.large` with 50 GB storage
- Field requirement: engineers should be able to clock in from mobile with coordinates captured at punch/site-visit events
- Mobile expectation: Android and iOS access
- Onsite expectation: implementation partner should visit the Kalewadi office once a week
- Key stakeholder context: the owner/contact may live in the US and may not always be physically present in India; company presence exists in both India and the US

## ERPNext Ecosystem to Use

Core open-source projects:

- ERPNext: <https://github.com/frappe/erpnext>
- Frappe Framework: <https://github.com/frappe/frappe>
- Frappe HR / HRMS: <https://github.com/frappe/hrms>
- Official Docker deployment: <https://github.com/frappe/frappe_docker>

Recommended project apps:

- `frappe`
- `erpnext`
- `hrms`
- `india_compliance`, if DVS needs Indian GST/e-invoicing/e-way bill support inside ERPNext
- `dvs_custom`, a project-specific custom app for upgrade-safe DVS customizations

## Core ERPNext Modules to Understand

### Setup

Used for foundational configuration:

- Company
- Fiscal year
- Currency
- Letterhead
- Email accounts
- Numbering series
- Departments and branches where needed
- Role profiles
- Users and permissions

Questions for DVS:

- Is there one company or multiple legal entities?
- Does the US company need to be represented in the same ERP?
- Are India and US operations separate companies, branches, or cost centers?
- Which users should have admin rights?

### Frappe HR / HRMS

Likely important for phase 1.

Relevant features:

- Employee master
- Department/designation
- Leave management
- Attendance
- Shift management
- Employee Checkin
- Mobile check-in through `/hrms` PWA
- Geolocation tracking
- Shift Location geofencing
- Expense claims
- Payroll, if included later

Recommended phase-1 stance:

- Implement employee master, leave, attendance, and mobile check-in first.
- Defer full payroll unless DVS explicitly makes it a must-have.

### CRM

Used for:

- Leads
- Opportunities
- Customers
- Sales follow-ups
- Communication history

Questions for DVS:

- Do they currently track leads in Excel, email, WhatsApp, or another CRM?
- Do they need lead-to-quotation tracking?
- Who owns sales follow-ups?

### Selling

Used for:

- Customer master
- Quotations
- Sales orders
- Delivery notes
- Sales invoices, if accounting is in ERPNext
- Print formats

Likely DVS customizations:

- Quotation format
- Terms and conditions
- Project/service-specific quotation fields
- Approval before sending quotation

### Projects

Used for:

- Projects/jobs
- Tasks
- Timesheets
- Project costing
- Project dashboards

Likely useful for DVS because their work includes automation, robotics, commissioning, engineering, manufacturing, and service activities.

Questions for DVS:

- Does every customer PO become a project/job?
- What are the standard stages from PO to handover?
- Do engineers log time against projects?
- Are field visits project-linked or ticket-linked?

### Support

Used for:

- Issues / service tickets
- Customer support workflows
- Assignment and status tracking

Likely DVS customizations:

- Field visit details
- Engineer assignment
- Site visit checklist
- Customer sign-off
- Service report PDF
- Photo attachments

### Buying

Used for:

- Supplier master
- Material requests
- Supplier quotations
- Purchase orders
- Purchase receipts
- Purchase invoices

Questions for DVS:

- Do they want purchase approvals in phase 1?
- Are purchases project-specific?
- Do they need vendor outstanding reports in ERPNext or Tally?

### Stock

Used for:

- Item master
- Warehouses
- Stock ledger
- Material receipt/issue/transfer
- Reorder levels
- Project-wise material movement, with configuration/customization

Questions for DVS:

- Do they maintain physical stores?
- Do they track PLCs, drives, panels, spares, cables, and sensors?
- Do they need serial numbers?
- Is barcode/QR needed now or later?

### Manufacturing

Used for:

- BOM
- Work orders
- Production planning
- Job cards
- Subcontracting integration

Phase-1 caution:

- Manufacturing can become large quickly. For DVS, start with project/panel-shop tracking and basic BOM only if needed.

### Quality Management

Useful for:

- Inspection templates
- Quality inspections
- FAT/checklists

Likely DVS customizations:

- Factory Acceptance Testing templates
- Commissioning checklists
- Panel inspection checklists

### Accounts

Used for:

- Chart of accounts
- Sales/purchase invoices
- Payments
- Journal entries
- Receivables/payables
- Financial statements
- Cost centers
- Project accounting

Phase-1 caution:

- If DVS already uses Tally and accountants/auditors depend on it, avoid replacing accounting immediately.
- Start with operational workflows and either export summaries to Tally or plan integration later.

### Assets

Useful for:

- Company assets
- Tools/instruments
- Laptops
- Calibration equipment, if applicable

### Portal

Useful later for:

- Customer portal
- Vendor portal
- Ticket status
- Documents

Phase-1 caution:

- Defer portal unless DVS explicitly needs external access in first release.

## Mobile Attendance Strategy

ERPNext + Frappe HR already covers the core requirement.

Built-in capabilities:

- Frappe HR PWA at `https://<domain>/hrms`
- Android install through Chrome
- iOS install through Safari Add to Home Screen
- Employee Checkin from mobile app/PWA
- Geolocation tracking
- Latitude and longitude on Employee Checkin
- Shift Location geofencing

Recommended phase-1 approach:

1. Deploy ERPNext + HRMS behind HTTPS.
2. Configure HR Settings:
   - Allow Employee Checkin from Mobile App
   - Allow Geolocation Tracking
3. Configure employees, shifts, and optionally Shift Locations.
4. Test on real Android and iPhone devices.
5. Use the PWA instead of building a native app.

Customize only if DVS needs:

- Customer/site/project reference during clock-in
- Selfie/photo proof
- Attendance exception approval
- Manager map/report view
- Travel reimbursement link
- Site visit log separate from attendance
- Fake/mock location detection controls
- Offline check-in behavior

Privacy rule:

- Capture coordinates only when the user performs a clock-in, clock-out, or site-visit action.
- Do not propose continuous background tracking unless the client explicitly requests it and accepts privacy implications.

## AWS and Domain Checklist

Before production setup, DVS should confirm:

- AWS account ownership
- AWS region
- Subdomain, for example `erp.dvstechnosoft.com`
- DNS control and ability to create A/CNAME records
- SSL certificate approach
- Admin email for Let's Encrypt/alerts
- SMTP/email sending provider
- Backup retention
- Whether database should be local MariaDB container or AWS RDS
- Whether files should be local storage, S3 backup, or S3-backed storage

Recommended starting architecture for controlled budget:

- EC2 `m6a.large`
- 50 GB gp3 volume initially
- Docker Compose deployment
- MariaDB container
- Redis containers
- ERPNext/Frappe backend, frontend, workers, scheduler, websocket
- HTTPS via Traefik or Nginx + Let's Encrypt
- Daily off-server backups to S3
- CloudWatch monitoring

Upgrade path:

- RDS MariaDB for managed database
- S3 for document storage/backups
- Larger gp3 volume
- More workers if background jobs/data imports increase

## Customization Rules

Do not modify ERPNext, Frappe, or HRMS core code unless there is no practical alternative.

Use a separate app:

- App name: `dvs_custom` or `dvs_technosoft`
- Store all DVS-specific code and fixtures there.

Use the simplest safe tool for each need:

- Standard configuration for built-in ERPNext behavior
- Custom Fields for extra fields
- Property Setters for form behavior changes
- Workflows for approval flow
- Print Formats for quotation/service/FAT PDFs
- Custom Reports for management reporting
- Client Scripts for lightweight UI logic
- Server Scripts for simple backend automation where acceptable
- Python hooks/controllers in custom app for serious business logic
- Fixtures to version-control custom fields, workflows, scripts, roles, reports, and print formats
- Data patches for repeatable migrations

## Weekly Kalewadi Office Visit Operating Model

Since DVS expects a weekly office visit at Kalewadi, use visits for high-value activities that are harder to complete remotely.

Recommended onsite agenda pattern:

1. Confirm open decisions from previous week.
2. Meet department owners: HR, accounts, projects, service, stores, sales, and management as needed.
3. Review current process examples: Excel sheets, registers, quotation formats, project trackers, service reports, attendance records.
4. Demo configured/customized ERPNext workflows.
5. Collect UAT feedback from real users.
6. Validate data migration templates.
7. Train a small group of key users.
8. Record decisions and action items in Notion before leaving.

Because the main stakeholder may live in the US:

- Send a pre-visit agenda before each Kalewadi visit.
- Identify an India-side decision owner for each department.
- Record decisions in Notion and share a short summary after each visit.
- Keep US stakeholder review async-friendly.
- Schedule remote calls for decisions that need the US stakeholder.
- Avoid accepting verbal scope changes without written confirmation.

Suggested recurring onsite outputs:

- Decision log updates
- Requirement clarifications
- UAT feedback list
- Training attendance/notes
- New risks/blockers
- Next-week priorities

## Five-Month Delivery Plan

The delivery window is workable if scope is controlled and ERPNext built-ins are used first.

### Month 1: Discovery, Blueprint, and Technical Baseline

Focus:

- Run discovery meeting.
- Confirm phase-1 modules.
- Confirm AWS, subdomain, and ownership.
- Confirm PWA/mobile attendance approach.
- Stand up staging ERPNext + HRMS.
- Prepare fit-gap analysis.
- Create signed blueprint.

Outputs:

- Confirmed scope
- Module priority list
- Data migration list
- Staging ERP URL
- Initial users/roles
- Implementation backlog

### Month 2: Core Configuration

Focus:

- Company setup
- Employees/departments/designations
- Role profiles and permissions
- HRMS attendance/leave/shift setup
- CRM/customer/vendor/project masters
- Initial print formats
- Basic dashboards

Outputs:

- Working core ERP flows
- HR attendance PWA configured
- First round of user demos
- Data import templates

### Month 3: Custom Workflows and Reports

Focus:

- Build `dvs_custom` app.
- Add confirmed custom fields.
- Configure workflows and approval rules.
- Customize quotations, project/job flow, service visits, and documents as required.
- Build key reports and dashboards.

Outputs:

- Version-controlled custom app
- Custom workflows
- Initial reports
- UAT-ready modules

### Month 4: Mobile Attendance, Data Migration, and UAT

Focus:

- Test Android/iOS `/hrms` PWA.
- Validate GPS and geofencing.
- Build any attendance exception/report customizations.
- Run data migration dry run.
- Conduct department-wise UAT.
- Fix UAT issues.

Outputs:

- UAT sign-offs by module
- Migration validation
- Mobile attendance guide
- Admin/user training drafts

### Month 5: Production, Training, and Go-Live

Focus:

- Production AWS deployment
- Domain and SSL
- Backups and monitoring
- Final migration
- Role-based training
- Go-live rehearsal
- Production cutover
- Hypercare support

Outputs:

- Production ERP live
- Trained users
- Go-live checklist completed
- Support process active

## Requirement Intake Checklist

When DVS gives requirements, classify each item:

- Standard ERPNext configuration
- Standard HRMS configuration
- Custom field
- Workflow/approval
- Print format
- Report/dashboard
- Data migration
- Integration
- Custom app development
- Defer to later phase

For each requirement capture:

- Department owner
- Business reason
- Current process
- Desired process
- Frequency of use
- Required fields
- Approval flow
- Reports/exports
- Data migration dependency
- Acceptance criteria
- Priority: must-have, important later, nice-to-have, out of scope

## Meeting Questions to Keep Ready

### Company / Governance

- Who is the final scope approver?
- Who is the India-side decision owner when the US stakeholder is unavailable?
- Will India and US operations use one ERP or separate company records?
- Who will be ERP admin after go-live?

### Technical

- Can DVS create `erp.dvstechnosoft.com` or another subdomain?
- Who will manage DNS?
- Which AWS account will be used?
- What email/SMTP provider will send ERP emails?
- Is public internet access acceptable, or do they need VPN/IP restriction?

### Modules

- Which modules are required for first release?
- Which modules can wait?
- What are the daily pain points today?
- Which reports does management need every week?

### Mobile Attendance

- Is `/hrms` PWA acceptable for Android and iOS?
- Should GPS be captured on IN, OUT, or both?
- Do they need site/customer/project reference during check-in?
- Do they need geofencing?
- Do they need photo proof?
- Who approves exceptions?

### Data Migration

- What data is available in Excel/Tally/current systems?
- Who will clean and approve import files?
- Do they need historical transactions or only current/open records?

## Key Risks to Manage

- Scope creep from trying to implement too many modules in first release.
- Confusion between ERPNext built-in capabilities and custom requirements.
- Native app expectation when PWA is enough.
- Tally/accounting integration becoming bigger than expected.
- Poor-quality data migration files.
- US stakeholder unavailable for decisions.
- Weekly onsite feedback not being formally captured.
- AWS/domain/DNS delays blocking mobile PWA and SSL testing.

## Immediate Preparation Tasks

- Keep ERPNext/HRMS module notes ready.
- Prepare staging environment plan.
- Prepare subdomain/AWS checklist for DVS.
- Prepare weekly Kalewadi visit agenda template.
- Prepare requirement intake format.
- After 2 June meeting, convert confirmed requirements into implementation tasks in Notion.
