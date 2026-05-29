# DVS Technosoft NextERP Discovery Questionnaire

Meeting date: 2 June 2026  
Client: DVS Technosoft  
Purpose: Identify the ERP modules, workflows, deployment expectations, and customization scope needed for the first implementation phase.

## 1. Meeting Goals

- Understand DVS Technosoft's current business processes and pain points.
- Confirm which ERP modules are required in phase 1.
- Identify workflows that need customization in NextERP.
- Confirm AWS hosting expectations, security needs, backup needs, and storage requirements.
- Capture requirements for mobile attendance with GPS coordinates for engineers working at customer or project sites.
- Agree on decision makers, approval flows, and next steps after the discovery meeting.

## 2. Company and User Context

### Basic Details

- Total employees: 50-55 currently.
- Expected employee growth in the next 12-24 months:
- Number of office users:
- Number of field/site engineers:
- Number of management users:
- Number of admin/HR/accounts users:
- Number of external customer/vendor portal users, if any:

### Departments / Teams

Ask which departments should use the ERP:

- Management
- HR / administration
- Accounts / finance
- Sales / business development
- Purchase / procurement
- Inventory / stores
- Projects
- Engineering / design
- Manufacturing / panel shop
- Service / commissioning
- Field support
- IT
- Other:

### Current Tools

- What tools are currently used?
  - Excel / Google Sheets
  - Tally or accounting software
  - WhatsApp
  - Email
  - Paper registers
  - Existing ERP / CRM
  - Project management tools
  - Attendance machine / biometric system
  - Other:
- What are the biggest problems with the current process?
- Which reports are difficult or time-consuming today?
- Which workflows currently depend on manual follow-up?

## 3. Module Discovery

For each module, confirm:

- Required in phase 1? Yes / No / Later
- Current process
- Pain points
- Required approvals
- Reports needed
- Data migration needed
- Users and permissions

### HR and Employee Management

- Do they need an employee master?
- What employee data should be stored?
  - Name, employee code, department, designation
  - Joining date, work location, reporting manager
  - Contact details
  - Documents
  - Salary details
  - Emergency contact
- Do they need role-based access by department?
- Who can create, update, or deactivate employee records?

### Attendance and Leave

- Do they need regular office attendance?
- How is office attendance captured today?
  - Manual
  - Biometric
  - Web app
  - Mobile app
  - Other:
- Do they need shift management?
- Do they need late mark, half-day, overtime, or comp-off rules?
- Do they need leave management?
  - Leave types
  - Leave balance
  - Leave approval flow
  - Holiday calendar
- Should attendance connect to payroll?

### Field Engineer Attendance with GPS Coordinates

Important clarification: this is not live tracking. The ERP should only capture location coordinates at the time of clock-in / clock-out or site visit marking.

Questions:

- Should field engineers clock in from:
  - Android app
  - iOS app
  - Mobile browser
  - All of the above
- Is a native mobile app required on both Android and iOS, or is a mobile-friendly web/PWA acceptable for phase 1?
- Should GPS coordinates be captured on:
  - Clock-in only
  - Clock-out only
  - Both clock-in and clock-out
  - Every site visit entry
- Should the system capture:
  - Latitude and longitude
  - Address resolved from coordinates
  - Time and date
  - Customer/site name
  - Project/job reference
  - Selfie/photo proof
  - Remarks
  - Device details
- Should attendance be allowed only within a customer/site geofence?
- If geofencing is required:
  - What radius is acceptable? Example: 100 meters, 250 meters, 500 meters
  - Who maintains customer/site coordinates?
  - Should exceptions be allowed?
- What should happen if GPS is unavailable or permission is denied?
  - Block attendance
  - Allow with manager approval
  - Allow manual reason entry
- Who approves field attendance exceptions?
- Should managers see the punch location on a map?
- Should HR/admin be able to export field attendance with coordinates?
- Should field attendance connect to:
  - Project costing
  - Timesheets
  - Service tickets
  - Payroll
  - Travel reimbursement
- Do engineers need offline mode if network is unavailable at site?
- Should the app prevent fake GPS/mock location usage if technically feasible?
- Do they need customer/site visit logs separate from attendance?

### CRM and Sales

- Do they need lead management?
- Sources of leads:
  - Website
  - Phone
  - Email
  - Referral
  - Existing customers
  - Other:
- Do they need opportunity/deal tracking?
- Quotation process:
  - Who prepares quotations?
  - Who approves quotations?
  - Are quotation templates required?
  - Do they need revision tracking?
- Do they need follow-up reminders?
- Do they need customer communication history?

### Projects and Job Tracking

- Do they need project/job creation after PO confirmation?
- What project types should be tracked?
  - Automation
  - Robotics
  - IT / IIoT
  - Cybersecurity
  - Energy solutions
  - Engineering design
  - Manufacturing / panel shop
  - Commissioning
  - Field service
- Required project stages:
  - Requirement gathering
  - Design
  - Procurement
  - Manufacturing
  - FAT
  - Dispatch
  - Installation
  - Commissioning
  - Handover
  - Support
- Do they need task assignment by project?
- Do they need timesheets by project?
- Do they need project costing?
- Do they need document storage per project?
- Do they need milestone tracking and alerts?

### Service Tickets / Field Service

- Do customers raise service requests?
- Who creates tickets?
  - Customer portal
  - Internal team
  - Email
  - Phone
- Ticket fields needed:
  - Customer
  - Site
  - Machine / panel / system
  - Issue type
  - Priority
  - Assigned engineer
  - Visit date
  - Status
  - Resolution notes
  - Photos / attachments
- Do engineers need to update service tickets from mobile?
- Do service tickets need customer sign-off?
- Do they need service reports generated as PDF?

### Purchase and Vendor Management

- Do they need vendor master?
- Do they need purchase requisitions?
- Approval flow for purchase:
  - Requester
  - Department head
  - Management
  - Purchase team
  - Accounts
- Do they need purchase order generation?
- Do they need GRN / material receipt?
- Do they need vendor payment tracking?

### Inventory / Stores

- Do they maintain inventory for automation parts, panels, cables, sensors, drives, PLCs, spares, etc.?
- Do they need item master with categories?
- Do they need serial number or batch tracking?
- Do they need stock in / stock out?
- Do they need project-wise material issue?
- Do they need minimum stock alerts?
- Do they need multi-location inventory?
- Do they need barcode / QR support?

### Manufacturing / Panel Shop

- Do they need panel shop work order tracking?
- Do they need BOM management?
- Do they need material planning?
- Do they need inspection and quality checklists?
- Do they need FAT checklist templates?
- Do they need dispatch readiness tracking?

### Finance / Accounts

- Will accounting remain in Tally or move into ERP?
- If Tally remains primary, is integration required?
- Do they need:
  - Invoice generation
  - Payment tracking
  - Expense tracking
  - Project costing
  - Tax/GST reports
  - Customer outstanding reports
  - Vendor outstanding reports
- Who approves invoices and expenses?

### Document Management

- What documents should be stored in the ERP?
  - Customer POs
  - Quotations
  - Technical drawings
  - CAD files
  - FAT reports
  - Commissioning reports
  - Service reports
  - Employee documents
  - Vendor documents
- Do they need version control?
- Do they need access restrictions by project/customer?
- Approximate current document size to migrate:
- Expected monthly document upload size:

### Reports and Dashboards

Ask management which dashboards matter most:

- Sales pipeline
- Quotation status
- Project status
- Pending approvals
- Engineer attendance
- Field visit summary
- Service ticket status
- Inventory stock
- Purchase status
- Project cost summary
- Revenue / billing summary
- Department performance
- Custom reports:

## 4. Mobile App Requirements

Because DVS requested clock-in from both iOS and Android, clarify the exact mobile expectation early.

### App Scope

- Is mobile required only for attendance, or also for:
  - Leave requests
  - Task updates
  - Project updates
  - Service ticket updates
  - Photo uploads
  - Customer sign-off
  - Travel expense claims
  - Notifications
- Should the app support both employees and managers?
- Should managers approve attendance/leave/tickets from mobile?

### Platform Decision

- Is a native Android and iOS app mandatory?
- Would a responsive mobile web app or PWA be acceptable for phase 1?
- Is App Store / Play Store publishing required, or can the app be distributed privately?
- Who will own developer accounts if store publishing is needed?

### Mobile Security

- Login method:
  - Email/password
  - Mobile OTP
  - Company SSO
  - Other:
- Should biometric unlock be supported?
- Should the app enforce device binding?
- Should users be logged out after inactivity?
- What data can be stored locally on the device?

### Notifications

- Do they need push notifications for:
  - Attendance reminders
  - Leave approvals
  - Task assignment
  - Service ticket assignment
  - Approval requests
  - Project alerts

## 5. AWS Deployment Discovery

Initial thought: m6a.large with 50 GB storage may be a reasonable starting point for 50-55 employees, but final sizing should depend on stack, database choice, document uploads, concurrent users, and backup retention.

### Hosting Questions

- Preferred AWS region:
- Domain name to use:
- Who controls DNS?
- Public internet access or VPN/private access?
- Any customer/security requirement for data residency?
- Required uptime expectation:
- Expected concurrent users:
- Expected number of mobile users:

### Proposed Starting Architecture to Validate

- EC2: m6a.large
- Storage: 50 GB gp3 initially
- Database:
  - Option A: Database on same EC2 for lower initial cost
  - Option B: AWS RDS for better backup, reliability, and maintenance
- File storage:
  - Local storage for low initial complexity
  - S3 for scalable document storage and backups
- Reverse proxy: Nginx
- SSL: Let's Encrypt or AWS Certificate Manager depending on architecture
- Monitoring: CloudWatch
- Backups: automated daily backups with retention policy

### Backup and Recovery

- Backup frequency:
  - Daily
  - Twice daily
  - Hourly
- Retention period:
  - 7 days
  - 15 days
  - 30 days
  - Longer
- Should backups include:
  - Database
  - Uploaded files
  - Configuration
  - Application code
- Who should receive backup/monitoring alerts?
- Recovery time expectation:

### Security

- Who should have server/admin access?
- Is MFA required for admin accounts?
- Should ERP admin access be restricted by IP/VPN?
- Do they need audit logs for key actions?
- Do they need role-based access per department?
- Do they need data export restrictions?

## 6. Data Migration

- What existing data should be imported?
  - Employees
  - Customers
  - Vendors
  - Items/materials
  - Projects
  - Open service tickets
  - Inventory stock
  - Leave balances
  - Documents
  - Financial opening balances
- Source format:
  - Excel
  - Tally
  - Existing software export
  - Manual entry
- Who will clean and approve the data before import?
- Is historical data required, or only current/open records?

## 7. Roles and Permissions

Identify user roles:

- Super admin
- Management
- HR admin
- Accounts
- Sales
- Purchase
- Stores
- Project manager
- Engineer
- Field engineer
- Service manager
- Customer portal user
- Vendor portal user

For each role, confirm:

- What can they view?
- What can they create?
- What can they edit?
- What can they approve?
- What reports can they export?

## 8. Phase 1 Prioritization

Use this table during the meeting.

| Module | Phase 1 | Later | Not Required | Notes |
| --- | --- | --- | --- | --- |
| Employee master |  |  |  |  |
| Attendance |  |  |  |  |
| Mobile GPS attendance |  |  |  |  |
| Leave management |  |  |  |  |
| CRM / leads |  |  |  |  |
| Quotations |  |  |  |  |
| Projects / jobs |  |  |  |  |
| Service tickets |  |  |  |  |
| Purchase |  |  |  |  |
| Inventory |  |  |  |  |
| Manufacturing / panel shop |  |  |  |  |
| Finance / invoicing |  |  |  |  |
| Document management |  |  |  |  |
| Dashboards / reports |  |  |  |  |
| Customer portal |  |  |  |  |
| Vendor portal |  |  |  |  |
| Tally/accounting integration |  |  |  |  |

## 9. Decisions to Capture in Meeting

- Confirm phase 1 modules:
- Confirm mobile app approach:
  - Native Android/iOS
  - PWA/mobile web
  - Hybrid app
- Confirm GPS attendance rules:
- Confirm AWS architecture:
- Confirm database choice:
- Confirm document storage approach:
- Confirm backup policy:
- Confirm data migration scope:
- Confirm first admin users:
- Confirm approval owners from DVS:

## 10. Recommended Phase 1 Discussion Focus

For a 50-55 employee company, a practical first phase may focus on:

- Employee master
- Attendance and leave
- Field engineer mobile clock-in with GPS coordinates
- CRM and quotation tracking
- Project/job tracking
- Service ticket or field visit tracking
- Document management
- Basic dashboards
- AWS deployment, backups, SSL, and admin roles

Final scope should be decided only after DVS confirms business priorities and current pain points.

## 11. Follow-Up Items After Meeting

- Prepare finalized module scope.
- Prepare gap analysis between standard NextERP features and required customizations.
- Prepare AWS architecture and estimated monthly cost.
- Prepare implementation backlog.
- Prepare data migration template files.
- Confirm whether native mobile apps are required or whether PWA/mobile web is acceptable.
- Confirm timeline, testing approach, and go-live expectations.
