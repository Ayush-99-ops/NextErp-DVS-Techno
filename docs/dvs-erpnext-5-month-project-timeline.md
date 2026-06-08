# DVS Technosoft ERPNext Implementation - 5 Month Project Timeline

Prepared for: DVS Technosoft Management  
Project: ERPNext Deployment, Configuration, and Customization  
Platform: Open-source ERPNext with Frappe HR / HRMS  
Hosting: AWS  

## 1. Project Objective

The objective is to deploy and customize ERPNext for DVS Technosoft so that the company has a centralized ERP system for daily operations, employee management, attendance, field engineer coordination, CRM, projects, documents, and management reporting.

The first release should focus on practical modules that DVS teams will use every day. Advanced or lower-priority features can be planned as later enhancements after the core ERP is stable.

## 2. Proposed Phase-1 Scope

The final scope will be confirmed after the requirement discovery meeting. The recommended first-release scope is:

- Company setup and ERP branding
- User roles and permissions
- Employee master
- Attendance and leave management
- Field engineer mobile check-in with GPS coordinates
- CRM / lead tracking
- Customer and vendor master
- Quotation tracking
- Project / job tracking
- Service ticket or field visit tracking
- Document management
- Basic dashboards and reports
- AWS production deployment with SSL, backups, and monitoring

## 3. Scope Items Recommended for Later Phase

To keep the first release practical and deliverable, the following should be taken up only if DVS marks them as critical:

- Full payroll processing
- Full accounting replacement
- Real-time Tally integration
- Advanced inventory automation
- Barcode / QR workflows
- Full manufacturing and BOM automation
- Customer portal
- Vendor portal
- Native Android and iOS apps
- Advanced BI dashboards

For mobile attendance, the recommended first approach is to use the Frappe HR mobile PWA, which works through the ERP domain on Android and iOS. A branded native app can be considered later if required.

## 4. High-Level 5 Month Timeline

| Month | Phase | Main Outcome |
| --- | --- | --- |
| Month 1 | Discovery, Blueprint, and Technical Foundation | Confirm requirements, finalize phase-1 scope, prepare staging ERPNext environment |
| Month 2 | Core ERP Configuration | Configure company, users, roles, HR, attendance, CRM, projects, and basic masters |
| Month 3 | Customization and Reports | Build DVS-specific workflows, fields, print formats, reports, and dashboards |
| Month 4 | Mobile Attendance, Data Migration, and UAT | Validate GPS attendance, migrate trial data, conduct department-wise testing |
| Month 5 | Production Deployment, Training, and Go-Live | Deploy on AWS production, train users, import final data, and go live |

## 5. Month-by-Month Plan

### Month 1 - Discovery, Blueprint, and Technical Foundation

Purpose: understand the business clearly before customization starts.

Key activities:

- Conduct requirement discovery with DVS management and department owners.
- Confirm phase-1 modules and later-phase modules.
- Map current processes for HR, attendance, sales, projects, service, purchase, inventory, and documents.
- Confirm AWS ownership, region, domain/subdomain, and email requirements.
- Confirm whether the ERP will use a subdomain such as `erp.dvstechnosoft.com`.
- Confirm mobile attendance expectations for Android and iOS.
- Prepare ERPNext fit-gap analysis.
- Set up a staging ERPNext + HRMS environment.
- Prepare the implementation backlog.

Deliverables:

- Requirement summary
- Signed phase-1 scope / blueprint
- AWS and domain checklist
- Staging ERPNext environment
- Initial module configuration plan
- Data migration template list

DVS inputs required:

- Department-wise process details
- Existing Excel sheets/registers/reports
- Current quotation/project/service formats
- AWS and domain decision
- India-side decision owners
- Final approval on phase-1 scope

Decision gate:

- Development-heavy customization starts only after DVS confirms the phase-1 scope.

### Month 2 - Core ERP Configuration

Purpose: configure the standard ERPNext foundation before custom development.

Key activities:

- Configure company profile, letterhead, branding, and basic settings.
- Configure users, roles, role profiles, and permissions.
- Configure departments, designations, employees, and reporting structure.
- Configure attendance, leave, shifts, and HR settings.
- Enable mobile check-in and geolocation settings in Frappe HR.
- Configure customer, vendor, project, and item masters as required.
- Configure CRM, quotation, and project/job basics.
- Prepare initial dashboards and standard reports.
- Prepare first round of user demos.

Deliverables:

- Working core ERP configuration
- User and permission structure
- HR and attendance setup
- Initial CRM/project setup
- Mobile attendance base setup
- Initial dashboards/reports
- Data import templates

DVS inputs required:

- Employee list
- Department/designation list
- User access list
- Leave/attendance rules
- Customer/vendor/project master samples
- Approval hierarchy

Decision gate:

- DVS validates whether standard ERPNext flows are acceptable or need customization.

### Month 3 - Customization and Reports

Purpose: implement DVS-specific business workflows without modifying ERPNext core.

Key activities:

- Create and maintain a dedicated DVS custom app.
- Add approved custom fields.
- Configure workflows and approvals.
- Customize quotation format and document templates.
- Customize project/job stages based on DVS operations.
- Configure service ticket or field visit workflow if included in phase 1.
- Build required reports and dashboards.
- Configure document management structure.
- Conduct demos with department owners.

Deliverables:

- DVS custom app
- Custom fields and workflows
- Quotation / service / project print formats
- Project/job workflow
- Service/field visit workflow, if confirmed
- Management reports and dashboards
- Updated UAT checklist

DVS inputs required:

- Approved print format samples
- Approval rules
- Report format expectations
- Project stage confirmation
- Service/field visit process confirmation

Decision gate:

- Department owners approve customized workflows for UAT.

### Month 4 - Mobile Attendance, Data Migration, and UAT

Purpose: validate the system with real users and real business scenarios.

Key activities:

- Test mobile attendance on Android and iOS.
- Validate GPS coordinate capture during check-in/check-out.
- Validate geofencing if DVS requires site/location restrictions.
- Add attendance exception flow if required.
- Run trial data migration.
- Conduct department-wise UAT.
- Fix UAT issues.
- Prepare user training material.
- Prepare go-live checklist.

Deliverables:

- Tested mobile attendance workflow
- GPS/geofencing validation report
- Trial migrated data
- UAT feedback and issue tracker
- UAT fixes
- Training material draft
- Go-live checklist draft

DVS inputs required:

- Real Android and iPhone test users
- Field engineer test scenarios
- Cleaned import files
- UAT users from each department
- Feedback and sign-off from department owners

Decision gate:

- DVS gives module-wise UAT approval before production cutover.

### Month 5 - Production Deployment, Training, and Go-Live

Purpose: deploy the approved system on production AWS and transition DVS users to ERPNext.

Key activities:

- Prepare production AWS environment.
- Configure domain/subdomain, SSL, backups, and monitoring.
- Deploy ERPNext production environment.
- Import approved final data.
- Configure production users and permissions.
- Conduct role-based training.
- Perform go-live rehearsal.
- Complete final cutover.
- Provide initial post-go-live support.

Deliverables:

- Production ERPNext environment
- SSL-enabled ERP domain
- Backup and monitoring setup
- Final imported data
- Trained users
- Admin guide and user guide
- Mobile attendance guide
- Go-live sign-off
- Post-go-live support tracker

DVS inputs required:

- Final approved data
- Final production user list
- Domain/DNS access or coordination
- AWS access or coordination
- Training attendance from key users
- Go-live approval

Decision gate:

- ERP goes live only after final data, access, backup, and UAT approvals are complete.

## 6. Weekly Working Model

DVS has requested weekly office visits at Kalewadi. These visits should be used for decisions, demos, UAT, training, and clarification.

Recommended weekly rhythm:

- Pre-visit agenda shared before the visit
- Onsite meeting with department owners
- Demo of completed ERP workflows
- Review of open decisions and blockers
- Collection of user feedback
- Training or UAT session where required
- Notion/project tracker update after the visit
- Summary shared with management and remote stakeholders

Because the CEO/key stakeholder may be based in the US, written decision logs are important. Any major scope or approval decision should be recorded and confirmed in writing.

## 7. Client Responsibilities

To keep the project on track, DVS should provide:

- Timely scope approval
- India-side department decision owners
- AWS account or access confirmation
- Domain/subdomain and DNS support
- Clean master data for import
- Existing document/report formats
- UAT users from each department
- Feedback within agreed review cycles
- Final approval for go-live

## 8. Implementation Principles

- Use standard ERPNext functionality wherever possible.
- Customize only confirmed business gaps.
- Keep phase 1 focused on daily operational needs.
- Avoid modifying ERPNext core code.
- Use a separate DVS custom app for custom fields, workflows, reports, and print formats.
- Keep mobile attendance as punch-event coordinate capture, not live tracking.
- Maintain weekly decision and issue tracking.

## 9. Success Criteria

The phase-1 implementation will be considered successful when:

- DVS users can log into ERPNext with correct roles.
- HR, attendance, and mobile GPS check-in work for office and field users.
- Approved CRM, quotation, project, service, and document workflows are usable.
- Required phase-1 reports and dashboards are available.
- Production system is hosted on AWS with SSL, backups, and monitoring.
- Approved data is migrated.
- Key users are trained.
- DVS signs off on go-live.

## 10. Notes and Assumptions

- The timeline assumes prompt approval of scope, AWS/domain readiness, and availability of clean data.
- Major additions after scope approval may affect delivery and should be treated as change requests.
- Native mobile apps are not assumed in phase 1 because Frappe HR already provides a mobile PWA for Android and iOS.
- Tally/accounting integration should be confirmed separately because it can become a large workstream.
