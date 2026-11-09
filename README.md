# Employee Raise Issue – Record Producer & Service Portal Integration in ServiceNow

A custom **ServiceNow Scoped Application (`Employee Center`)** built to standardize enterprise employee issue reporting, enforce automated form validations and category-to-subcategory dependencies, and provide a self-service intake experience through a custom **Service Portal (`/employee_request`)** and **Record Producer (`Raise Employee Issue`)**.

- **Developer / Project Owner:** Abdul Khadarvali (`Individual`)
- **Program / Track:** [SkillWallet ServiceNow Global Certification Capstone Project](https://myskillwallet.ai/dashboard/skillwallet/module/servicenow-global-certification-lendi-6a38ca70d0c5068d7d216761/projects/6a4b6939daf22dccbaf90e40/Employee-Raise-Issue-Record-Producer-Service-Portal-Integration-Guide-6ab39ea8211fa4fd5d28ac30)
- **Structural Reference:** [Metro Ticket Generating System in ServiceNow](https://github.com/manasa-pothina/Metro-Ticket-Generating-System-in-ServiceNow)
- **Service Portal Endpoint:** [`/employee_request`](https://dev280178.service-now.com/employee_request)
- **Project Timeline:** 19 October 2026 – 07 November 2026 (Completed on ServiceNow PDI on **07 November 2026**)

## 📌 Overview of Sections
- Project Overview
- Problem Statement
- Key Features
- Repository Folder Structure & Phase-Wise Deliverables
- Architecture & Data Model (`Employee raises issue` Table)
- Application Governance (UI Policies & Dictionary Dependency)
- Service Catalog Intake (`Raise Employee Issue` Record Producer)
- Service Portal (`/employee_request`) & Custom `6*6` Widgets
- Agile Sprint Schedule & Velocity (`19 Oct 2026 – 07 Nov 2026`)
- Setup & Installation Instructions
- Project Demo
- Functional, Performance & UAT Testing Summary (`TC01–TC09`)
- Future Enhancements

## 🚀 Project Overview
In large enterprise organizations, employees frequently encounter workplace-related issues such as network/VPN outages, hardware/laptop malfunctions, software/server errors, or account/password access blocks. Raising these issues through unstructured emails or informal chat messages leads to missing diagnostic fields, misrouted requests, delayed resolution, and zero status visibility.

The **[Employee Raise Issue – Record Producer & Service Portal Integration Guide](https://myskillwallet.ai/dashboard/skillwallet/module/servicenow-global-certification-lendi-6a38ca70d0c5068d7d216761/projects/6a4b6939daf22dccbaf90e40/Employee-Raise-Issue-Record-Producer-Service-Portal-Integration-Guide-6ab39ea8211fa4fd5d28ac30)** replaces ad-hoc requests with a dedicated **ServiceNow Service Portal** ([`/employee_request`](https://dev280178.service-now.com/employee_request)). Employees interact with a responsive **`6*6` two-column widget layout** (**`Commercial widget`** on the left and **`Link redirect`** on the right) that routes them directly to the **`Raise Employee Issue`** Record Producer (`Service Catalog -> Service`). Submitting the form creates a validated, auto-numbered ticket in the custom **`Employee raises issue`** table inside the **`Employee Center`** scoped application.

## 🎯 Problem Statement
Traditional email- and chat-based employee issue reporting causes five major operational bottlenecks:
- **Lack of Standardized Data Capture:** Informal messages omit critical details such as requester reference, category, subcategory, or issue summary.
- **Mismatched Category & Subcategory Selection:** Without dictionary-level dependency rules, users select incompatible category/subcategory pairs (e.g., pairing `Network` with `Laptop`).
- **Missing Descriptions on New Tickets:** Support teams receive blank or incomplete tickets when mandatory field rules are not enforced at intake.
- **Unprotected Ticket Identifiers:** Without read-only enforcement, auto-generated ticket numbers can be accidentally edited or overwritten.
- **No Centralized Self-Service Portal:** Employees struggle to locate the proper catalog item without a dedicated portal landing page and single-click redirect card.

## ✨ Key Features
- **Scoped Application Isolation (`Phase 1`):** Encapsulates all tables, form layouts, UI policies, catalog items, and portal widgets inside the **`Employee Center`** Scoped Application created in **ServiceNow Studio** (`All menus -> App Engine -> ServiceNow Studio`).
- **Auto-Numbered 8-Field Custom Table (`Phase 2`):** Automatically generates sequential, unique ticket IDs on the **`Employee raises issue`** table (`System Definition -> Tables`) with `Auto number` enabled in Table Controls.
- **Automated Form Governance via UI Policies (`Phase 3`):**
  - Enforces `Short description` as **Mandatory** whenever `State is New` (*`When the state changes to new then short description is mandatory`*).
  - Locks `Number` as **Read-only** across all states (*`Number field will read only`*).
- **Dynamic Category-to-Subcategory Dependency (`Phase 3`):** Filters `Subcategory` choices (`VPN`, `Laptop`, `Server`, `Forgot password`) dynamically based on the selected `Category` (`Network`, `Hardware`, `Software`, `Access`) via Dictionary Dependency (`Dependent = Category`).
- **5-Variable Record Producer Intake (`Phase 4`):** Exposes the **`Raise Employee Issue`** Record Producer under `Service Catalog -> Service` with 5 variables (`Orders 100–500`) mapped 1:1 to target columns on `Employee raises issue`.
- **Branded Service Portal & Custom `6*6` Widgets (`Phases 5 & 6`):** Launches the **`Requesting portal`** at URL suffix [`/employee_request`](https://dev280178.service-now.com/employee_request) with the **`Employee Center Coral Theme`**, custom page **`Employee Center Portal Page`** (`employee_center_portal_page`), **`Commercial widget`** (left 6 columns with 135-degree tri-color CSS linear gradient), and **`Link redirect`** widget (right 6 columns with AngularJS `$location.url` redirect).

## 📂 Repository Folder Structure & Phase-Wise Deliverables

This repository follows the 5-phase SDLC structure modeled on the [ServiceNow Capstone Reference Repository](https://github.com/manasa-pothina/Metro-Ticket-Generating-System-in-ServiceNow):

```text
Employee-Raise-Issue-Service-Portal-in-ServiceNow/
├── README.md
├── 1. Ideation Phase/
│   ├── Brainstorming_Idea_Generation_Prioritization.pdf                                (19 October 2026)
│   ├── Brainstorm_and_Idea_Prioritization_Template_-_Employee_Raise_Issue_System.pdf   (19 October 2026)
│   ├── Define_Problem_Statements.pdf                                                   (19 October 2026)
│   └── Empathy_Map_Canvas.pdf                                                          (20 October 2026)
├── 2. Requirement Analysis/
│   ├── Customer_Journey_Map.pdf                                                        (21 October 2026)
│   ├── Data_Flow_Diagrams_and_User_Stories.pdf                                         (22 October 2026)
│   ├── Solution_Requirements.pdf                                                       (23 October 2026)
│   └── Technology_Stack.pdf                                                            (24 October 2026)
├── 3. Project Design Phase/
│   ├── Problem-Solution_Fit_-_Employee_Raise_Issue_System.pdf                          (26 October 2026)
│   ├── Proposed_Solution_-_Employee_Raise_Issue_System.pdf                             (27 October 2026)
│   └── Solution_Architecture_-_Employee_Raise_Issue_System.pdf                         (28 October 2026)
├── 4. Project Planning Phase/
│   ├── Project_Planning_-_Employee_Raise_Issue_System.pdf                              (29 October 2026)
│   └── Planning_Logic_-_Employee_Raise_Issue_System.pdf                                (29 October 2026)
└── 5. Project Development & Testing Phase/
    ├── Performance_Testing_-_Employee_Raise_Issue_System.pdf                           (06 November 2026)
    ├── Functional_and_Performance_Testing_-_Employee_Raise_Issue_System.pdf            (06 November 2026)
    ├── UAT_Report_-_Employee_Raise_Issue_System.pdf                                    (07 November 2026)
    └── User_Acceptance_Testing_-_Employee_Raise_Issue_System.pdf                       (07 November 2026)
```

## 🏗 Architecture & Data Model

### Scoped Application & Custom Table
1. **Application Scope:** `Employee Center` (`ServiceNow Studio`)
2. **Table Label:** `Employee raises issue` (`System Definition -> Tables`, `Auto number` enabled in Controls)

### Table Schema (`Employee raises issue` — 8 Custom Fields)

| S.No. | Field Label | Field Type | Reference / Choice Options | Governance & Behavior |
| :---: | :--- | :--- | :--- | :--- |
| 1 | `Number` | Auto-Number | System auto-generated sequential ID | Locked as **Read-only** across all states via UI Policy |
| 2 | `Requester` | Reference | `User [sys_user]` | Identifies the employee raising the issue (Mapped to Order `100`) |
| 3 | `Category` | Choice | `Network`, `Hardware`, `Software`, `Access` | Controlling parent field for `Subcategory` (Mapped to Order `200`) |
| 4 | `Subcategory` | Choice | `VPN`, `Laptop`, `Server`, `Forgot password` | Dependent on `Category` dictionary configuration (Mapped to Order `300`) |
| 5 | `Short description` | String | Single-line summary of the issue | **Mandatory** when `State is New` via UI Policy (Mapped to Order `500`) |
| 6 | `State` | Choice | `New`, `In progress`, `Resolved`, `Closed` | Tracks end-to-end ticket lifecycle (Mapped to Order `400`) |
| 7 | `Priority` | Choice | `Critical`, `High`, `Medium`, `Low` | Defines urgency for support SLA handling |
| 8 | `Assignment Group` | Reference | `Group [sys_user_group]` | Routes the ticket to the responsible IT/HR support group |

### Category to Subcategory Dependency Matrix

| Selected Category (`Parent Choice`) | Filtered Subcategory (`Dependent Choice`) | Typical Support Routing |
| :--- | :--- | :--- |
| `Network` | `VPN` | Network / Infrastructure Support (`sys_user_group`) |
| `Hardware` | `Laptop` | Hardware / Desktop Support (`sys_user_group`) |
| `Software` | `Server` | Application / Server Support (`sys_user_group`) |
| `Access` | `Forgot password` | Identity & Access Management (`sys_user_group`) |

## ⚙ Application Governance (UI Policies & Dictionary Dependency)

### 1. UI Policy 1 — Mandatory Short Description on New Issues
- **Table:** `Employee raise issue`
- **Short Description:** `When the state changes to new then short description is mandatory`
- **When to Apply (Condition):** `State is New`
- **UI Policy Action:** Field name = `Short description` | `Mandatory = true`

### 2. UI Policy 2 — Read-Only Ticket Number Lock
- **Table:** `Employee raise issue`
- **Short Description:** `Number field will read only`
- **When to Apply (Condition):** Global (No filter condition — applies on all new and existing records)
- **UI Policy Action:** Field name = `Number` | `Read only = true`

### 3. Dictionary Choice Dependency
- **Navigation:** Right-click `Subcategory` -> `Configure Dictionary` -> Switch to `Advanced view` -> `Dependent Field` tab -> Check `Use dependent field` -> Set `Dependent on field = Category`.

## 📝 Service Catalog Intake (`Raise Employee Issue` Record Producer)

- **Name:** `Raise Employee Issue`
- **Table Name:** `Employee Raise issue`
- **Accessibility:** Catalogs = `Service Catalog` | Category = `Service` | Meta = Table name
- **Mapped Variables (`Orders 100–500`):**

| Order | Question / Label | Variable Type | Reference / Choices | Mapped Table Column (`Map to field = true`) |
| :---: | :--- | :--- | :--- | :--- |
| `100` | `What is the Requester name` | `Reference` | `User [sys_user]` | `Requester` |
| `200` | `Which Category` | `Choice` | `Network`, `Software`, `Hardware`, `Access` | `Category` |
| `300` | `What is Subcategory` | `Choice` | `VPN`, `Laptop`, `Server`, `Forgot password` | `Subcategory` |
| `400` | `Which State is this issue` | `Choice` | `New`, `In progress`, `Resolved`, `Closed` | `State` |
| `500` | `Short description` | `Single line text` | Free-text string input | `Short description` |

## 🖥 Service Portal (`/employee_request`) & Custom `6*6` Widgets

### Service Portal Configuration (`Service Portal -> Portals -> New`)
- **Title:** `Requesting portal`
- **URL Suffix:** `employee_request` ([`https://dev280178.service-now.com/employee_request`](https://dev280178.service-now.com/employee_request))
- **Homepage:** `ec_standard_home`
- **Custom Portal Page:** `Employee Center Portal Page` (`ID: employee_center_portal_page`)
- **KB Home Page:** `esc_knowledge_home`
- **Login Page:** `login` | **404 Page:** `404`
- **Main Menu:** `Employee Center Menu`
- **Theme:** `Employee Center Coral Theme`

### Widget 1 (Left Column in `6*6` Grid): `Commercial widget`

**Body HTML Template:**
```html
<div class="service-box">
  <h2>Our Services</h2>
  <p class="intro">
    We provide a centralized platform to help users raise issues, track requests,
    and get faster resolutions with complete transparency.
  </p>
  <ul class="service-list">
    <li><strong>24/7 Customer Support</strong> – Raise issues anytime, anywhere</li>
    <li><strong>Faster Issue Resolution</strong> – Automated routing to the right team</li>
    <li><strong>Transparent Tracking</strong> – Real-time status updates</li>
    <li><strong>Secure &amp; Reliable</strong> – Enterprise-grade data protection</li>
  </ul>
  <p class="footer-note">
    Click on <strong>Raise an Issue</strong> to submit your request and our support team
    will get back to you shortly.
  </p>
</div>
```

**CSS:**
```css
.service-box {
  height: 100%;
  padding: 30px;
  border-radius: 14px;
  background: linear-gradient(135deg, #1db954 0%, #ffffff 50%, #0b5ed7 100%);
  color: #0f172a;
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.15);
}
.service-box h2 {
  font-size: 26px;
  font-weight: 700;
  margin-bottom: 12px;
  color: #0b5ed7;
}
.service-box .intro {
  font-size: 15px;
  margin-bottom: 18px;
  color: #1e293b;
}
.service-list {
  list-style: none;
  padding-left: 0;
  margin-bottom: 20px;
}
.service-list li {
  font-size: 14.5px;
  margin-bottom: 10px;
  padding-left: 22px;
  position: relative;
  color: #0f172a;
}
.service-list li::before {
  content: "✔";
  position: absolute;
  left: 0;
  color: #1db954;
  font-weight: bold;
}
.footer-note {
  font-size: 14px;
  font-weight: 500;
  color: #0b5ed7;
}
```

### Widget 2 (Right Column in `6*6` Grid): `Link redirect`

**Body HTML Template:**
```html
<div class="issue-card" ng-click="c.openRecordProducer()">
  <h3>Raise an Issue</h3>
  <p>Click here to submit a ticket</p>
  <span class="action">Raise Ticket →</span>
</div>
```

**CSS:**
```css
.issue-card {
  cursor: pointer;
  padding: 25px;
  border-radius: 10px;
  background: linear-gradient(135deg, #2b5876, #4e4376);
  color: #fff;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.issue-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.25);
}
.action {
  display: inline-block;
  margin-top: 10px;
  font-weight: bold;
  text-decoration: underline;
}
```

**Client Script:**
```javascript
api.controller = function($location) {
  var c = this;

  // Record Producer sys_id for "Raise Employee Issue"
  var RECORD_PRODUCER_SYS_ID = 'ae2cd61183433210de6fc590ceaad3a4';

  c.openRecordProducer = function() {
    $location.url('sp?id=sc_cat_item&sys_id=' + RECORD_PRODUCER_SYS_ID);
  };
};
```

## 📅 Agile Sprint Schedule & Velocity (`19 Oct 2026 – 07 Nov 2026`)

| Sprint | Epic / Core Milestone | User Stories | Story Points | Duration | Start Date | End / Release Date |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: |
| **Sprint-1** | Scoped App & 8-Field Custom Table (`Phases 1 & 2`) | `USN-1` (3), `USN-2` (3), `USN-3` (4) | **10** | 5 Days | 19 Oct 2026 | 23 Oct 2026 |
| **Sprint-2** | UI Policies & Dictionary Dependency (`Phase 3`) | `USN-4` (3), `USN-5` (3), `USN-6` (4) | **10** | 5 Days | 24 Oct 2026 | 28 Oct 2026 |
| **Sprint-3** | Record Producer & Service Portal Setup (`Phases 4 & 5`) | `USN-7` (5), `USN-8` (3), `USN-9` (2) | **10** | 5 Days | 29 Oct 2026 | 02 Nov 2026 |
| **Sprint-4** | Custom `6*6` Widgets, QA & UAT Closure (`Phases 6–8`) | `USN-10` (3), `USN-11` (4), `USN-12` (2), `USN-13` (1) | **10** | 5 Days | 03 Nov 2026 | 07 Nov 2026 |
| **Total** | **All 8 SkillWallet Phases Completed** | **13 User Stories (`USN-1` to `USN-13`)** | **40 SP** | **20 Days** | **19 Oct 2026** | **07 Nov 2026** |

- **Project Velocity:** `40 Story Points / 4 Sprints = 10 Story Points per Sprint` (`2.00 Story Points per Day`).

## 🛠 Setup & Installation Instructions

1. **Create Scoped Application:** Log in to your ServiceNow Personal Developer Instance (PDI), navigate to `All menus -> App Engine -> ServiceNow Studio`, and create the **`Employee Center`** scoped application.
2. **Create Custom Table & 8 Fields:** Navigate to `System Definition -> Tables -> New`, create **`Employee raises issue`** with `Auto number` enabled in Controls, and configure the 8 fields via `Form Design`.
3. **Configure UI Policies & Dependency:** Under `System UI -> UI Policies`, create the mandatory `Short description` policy (`State is New`) and read-only `Number` policy. Configure Dictionary Dependency on `Subcategory` (`Dependent = Category`).
4. **Create Record Producer:** Navigate to `Service Catalog -> Catalog Definition -> Record Producers -> New`, create **`Raise Employee Issue`** under `Service Catalog -> Service`, add the 5 mapped variables (`Orders 100–500`), and copy its `sys_id`.
5. **Configure Service Portal & `6*6` Widgets:** Create **`Requesting portal`** (`/employee_request`) with **`Employee Center Coral Theme`**, create **`Commercial widget`** and **`Link redirect`**, and place them side by side in a `6*6` layout on **`Employee Center Portal Page`** in Service Portal Designer.

## 🎥 Project Demo

Watch the complete demonstration of the **Employee Raise Issue – Record Producer & Service Portal Integration** project:

- **Live Portal Endpoint (PDI):** [`https://dev280178.service-now.com/employee_request`](https://dev280178.service-now.com/employee_request)
- **SkillWallet Project Workspace:** [Employee Raise Issue – Record Producer & Service Portal Integration Guide](https://myskillwallet.ai/dashboard/skillwallet/module/servicenow-global-certification-lendi-6a38ca70d0c5068d7d216761/projects/6a4b6939daf22dccbaf90e40/Employee-Raise-Issue-Record-Producer-Service-Portal-Integration-Guide-6ab39ea8211fa4fd5d28ac30)

## 🧪 Functional, Performance & UAT Testing Summary (`TC01–TC09`)

All 9 test cases were executed between **03 November 2026 and 07 November 2026** with a **100% pass rate (9/9 Passed, 0 Defects)**:

| Test Case ID | Scenario Tested | Expected Result | Measured / Actual Result | Status |
| :---: | :--- | :--- | :--- | :---: |
| `TC01 (FT-01)` | Scoped Application & 8-Field Table Schema | `Employee raises issue` active in `Employee Center` with 8 fields & `Auto number` | All 8 fields, references (`sys_user`, `sys_user_group`), & auto-number verified | **Pass** |
| `TC02 (FT-02)` | Category & Dependent Subcategory Filtering | `Network -> VPN`, `Hardware -> Laptop`, `Software -> Server`, `Access -> Forgot password` | Dynamic subcategory filtering verified 4/4 | **Pass** |
| `TC03 (FT-03)` | Mandatory `Short description` UI Policy (Negative Test) | Blocks save when `State is New` and `Short description` is blank | Mandatory alert shown; save blocked until populated | **Pass** |
| `TC04 (FT-04)` | Read-Only `Number` Field UI Policy | Auto-generated ticket `Number` is locked across all states | `Number` field remained non-editable on all forms | **Pass** |
| `TC05 (FT-05)` | Service Portal (`/employee_request`) & `6*6` Widgets | `Commercial widget` (left) and `Link redirect` (right) render in `6*6` grid | Both custom widgets rendered with Coral Theme & CSS gradient | **Pass** |
| `TC06 (FT-06)` | Record Producer Redirect & Ticket Creation | Clicking `Raise Ticket ->` opens `Raise Employee Issue` & inserts mapped record | Redirected via `$location.url` and mapped all 5 variables (`Orders 100–500`) | **Pass** |
| `TC07 (PT-01)` | Portal & Custom Widget Load Speed | Render `/employee_request` & both widgets within `2.0 seconds` | Rendered in **`1.1–1.5 seconds`** average | **Pass** |
| `TC08 (PT-02)` | Redirect & Ticket Submission Speed | Client redirect & database insert complete within `3.0 seconds` | Redirect `< 0.6s`; record insert **`1.4–1.8 seconds`** | **Pass** |
| `TC09 (PT-03)` | Repeated Consecutive Ticket Submissions | 10 consecutive submissions generate unique sequential IDs without lag | 10/10 sequential ticket numbers generated with zero collision | **Pass** |

## 🔮 Future Enhancements
- Automated `Assignment Group` routing rules triggered by `Category` and `Subcategory`.
- Flow Designer email/SMS notifications to the `Requester` (`sys_user`) and `Assignment Group` (`sys_user_group`) on status transitions (`New -> In progress -> Resolved -> Closed`).
- SLA (Service Level Agreement) timers bound to `Priority` (`Critical`, `High`, `Medium`, `Low`).
- Real-time "My Submitted Issues" status tracker widget embedded on `/employee_request`.
