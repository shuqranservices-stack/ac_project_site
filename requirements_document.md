# System Requirements for HVAC Project Management Platform (Restaurants and Cafes)

## Overview
The objective of this project is to build a professional web‑based platform to manage HVAC (heating, ventilation and air conditioning) projects for restaurants and cafés.  The system replaces disparate Excel workbooks with a unified interface that makes it easy for operations teams and project managers to track purchase orders, compressors, other equipment, additional works and service requests.  It should provide a modern, clean user experience similar to the reference design (`equiptrack‑central.lovable.app`).

## Stakeholders
- **Maintenance Department:** responsible for issuing purchase orders, scheduling maintenance and approving requests.
- **Project Managers (PMs):** oversee installation and maintenance projects; need a high‑level overview of project status and ability to add records.
- **Store Owners / Managers:** submit service requests and track progress.
- **Finance / Accounting:** track payment status of purchase orders and invoices.
- **Administrators:** manage user accounts and configure system settings.

## Functional Requirements

### Data Management
1. **Datasets:** the platform must support the following core datasets:
   - **Master Sheet (Main Data):** contains purchase order (PO) information such as PO number, store name, project manager, region, city, request status, request priority, payment status, date and amount.  Additional columns hold attachments (copies of purchase orders, invoices, etc.).
   - **Compressors:** inventory of compressor units, including model, capacity, unit count and store details.
   - **Others:** other equipment or spare parts not covered by compressors, with similar attributes.
   - **Additional Work:** records for extra work, modifications or upgrades beyond the original scope.
   - **Service Requests:** maintenance or repair requests submitted by stores.

2. **Unique purchase orders:** if a PO number appears more than once because multiple items were ordered, the system must group these records together.  The main table should show a single summary row per PO number, displaying high‑level information (store, region, PM, request status, payment status, date and total amount).  Details of the individual items must not clutter the main table but should be shown in a modal when the user clicks the row.

3. **Details modal:** when a row in any table is clicked, a modal window opens showing all details for that record.  For grouped purchase orders, the modal must include:
   - A summary table listing the high‑level fields (PO number, store, PM, region, request status, payment status, date, total amount).
   - A separate item table listing each item’s specific fields (e.g., unit type, capacity, quantity, brand).  Attachments must be represented by clickable icons instead of long URLs.
   - Color‑coded badges for payment status (e.g., green for `Paid`, blue for `Submitted`, yellow for `Pending`, dark blue for `Approved`).

4. **Record addition:** each dataset page must include an “Add record” button that opens a form in a modal.  The form fields must reflect the dataset’s schema.  After submission the record appears in the appropriate table.

5. **Filtering and search:** provide filters at the top of the main pages (e.g., by request status, request priority, payment status) and a search box to quickly find records.  Changing a filter or entering search text updates the table without reloading the page.

### User Interface
1. **Responsive layout:** the site must be fully responsive and support right‑to‑left (RTL) languages.  It should display correctly on phones, tablets and desktop screens.

2. **Navigation:** a sidebar on the right contains icons and labels for each section (Dashboard, Main Data, Compressors, Others, Additional Work, Service Requests, Reports, Users).  The active section should be highlighted.  A top bar includes a search field and user information.

3. **Dashboard:** the home page shows summary cards with counts of unique purchase orders in each dataset.  The counts must reflect only unique POs, not all item rows.  For example, if one PO has three items, it counts as one.  The dashboard can also include basic charts (e.g., number of requests by region or status) for quick insight.

4. **Tables:** data is presented in paginated, scrollable tables with clean typography and alternating row shading.  Long URLs must be replaced with the company logo as a hyperlink so they do not clutter the table.  Column headings should be translated to Arabic and arranged in a logical order.

5. **Modals:** all dialogs (add record forms and details views) appear as centered modals with a light backdrop.  The modal width should be wide enough to accommodate RTL text (e.g., 600px or more).  The close button is located at the top left and the cancel/save buttons at the bottom.

6. **Colour palette:** use a soft, professional colour scheme (light greys and blues) consistent across the entire interface.  Avoid harsh or saturated colours; aim for high contrast for readability.  Icons and badges should use appropriate accent colours to convey status (e.g., green for success, red for danger).

### Non‑Functional Requirements
1. **Performance:** page load times should be minimised.  Use local CSS and JavaScript files rather than external CDNs to avoid network delays.  When filtering or searching, update tables via JavaScript rather than reloading the page.

2. **Maintainability:** the codebase must be modular and well‑documented.  Common functions should be placed in a shared JavaScript file (`common.js`) and reused across pages.  Data should be defined in a separate file (`data.js`) to allow easy replacement with a database in the future.

3. **Extensibility:** the system must be designed so that additional datasets, filters or pages can be added without breaking existing functionality.

4. **Accessibility:** ensure all interactive elements have appropriate ARIA roles and labels.  Use semantic HTML and ensure keyboard navigation works for modals and tables.

5. **Security:** when the platform is connected to a backend, proper validation and sanitisation must be implemented to prevent SQL injection or cross‑site scripting.  User authentication should be added, with sessions or JWT tokens to protect data.  File uploads for attachments should be stored securely and validated.

### Future Enhancements (not yet implemented)
- **User authentication:** integrate a sign‑in system so that each user has their own account.  This allows storing conversation history, customising the dashboard, or restricting access to certain sections.
- **Database integration:** replace the current static `data.js` with a real database (e.g., Firebase Firestore) to persist data and support multiple concurrent users.
- **Role‑based access control:** allow administrators to manage roles (e.g., viewer, editor, manager) with different permissions.
- **Export and import:** add functionality to export tables to Excel/PDF and import data from spreadsheets.
- **Notifications:** send notifications (email or in‑app) when a new service request is created or when a purchase order is completed.
- **Analytics and reporting:** include advanced charts and reports (e.g., spend per region, average completion time) on a dedicated Reports page.

## Deployment and Version Control
- **Hosting:** the site is currently deployed on Netlify at [https://jovial-hotteok-438066.netlify.app](https://jovial-hotteok-438066.netlify.app).  Each change must be uploaded to Netlify to go live.  In the future, continuous deployment can be set up to automatically publish changes from a version control repository.
- **Version control:** all source code should be stored in a GitHub repository.  Each feature or bug fix should be committed with a meaningful message.  Whenever a change is made locally, it must be pushed to GitHub and then redeployed to Netlify.
- **Repository structure:** the repository root should contain separate folders for the web pages and assets.  For example:

```
ac_project_site/
├── index.html
├── master.html
├── compressors.html
├── others.html
├── additional.html
├── service.html
├── assets/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   ├── data.js
│   │   ├── common.js
│   │   └── script.js
│   └── images/
│       ├── logo.png
│       └── alshgran-logo.png
└── README.md
```

This document describes both the existing functionality already implemented and additional requirements identified during analysis.  It should serve as a guide for developers and stakeholders to understand what the system must deliver and to track future enhancements.
