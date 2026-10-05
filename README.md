# PharmaCart — Omni-Channel Online Ordering & Inventory Platform
## Software Engineering & Project Management (SEPM) Comprehensive Package

[![Author](https://img.shields.io/badge/Author-Ritesh%20Jadhav-blue.svg)](https://github.com/RiteshJadhav283)
[![Project](https://img.shields.io/badge/Case%20Study-No.%2068-emerald.svg)](#)
[![Methodology](https://img.shields.io/badge/Methodology-Agile%20%2F%20Scrum%20%2B%20IEEE%20Standards-purple.svg)](#)
[![Release](https://img.shields.io/badge/Release-Core%20MVP%20v1.0-orange.svg)](#)

---

### Executive Overview
**PharmaCart** is an enterprise-grade omni-channel pharmacy ordering, prescription verification, and real-time inventory aggregation platform engineered for a 14-store retail pharmacy network across Ahmedabad, Gujarat. 

This repository contains the complete, industry-standard **Software Engineering and Project Management (SEPM)** documentation suite authored and managed by **Ritesh Jadhav** (*Lead Systems Analyst, Software Architect, Project Manager, QA Lead, and CCB Chair*).

---

## Deliverables Directory & Documentation Suite

| Deliverable Folder | Primary Specification | Core Topics & Artifacts Covered |
| :--- | :--- | :--- |
| [**01_SRS_Document/**](./01_SRS_Document/01_SRS_Document.md) | **Software Requirements Specification (IEEE Std 830-1998)** | System Context Model, 12 Detailed Functional Requirements (`FR-01` to `FR-12`), 8 Measurable NFRs (`NFR-01` to `NFR-08`), Regulatory Compliance (Drugs & Cosmetics Act, Schedule H/H1, GSPC), MoSCoW Scoping, and Requirements Traceability Matrix (RTM). |
| [**02_UML_Package/**](./02_UML_Package/02_UML_Package.md) | **UML Object Design & Architecture Package** | Use Case Model (`UC-05` Verification Specification), Domain Class Diagram, Sequence Diagram (*"Upload Rx and Place Order"*), Concurrent Order Fulfillment Activity Diagram, `Order` Lifecycle State Machine, Inter-Model Consistency Matrix, and Loose Coupling / High Cohesion Architectural Assessment. |
| [**03_Project_and_Budget_Plan/**](./03_Project_and_Budget_Plan/03_Project_and_Budget_Plan.md) | **Agile Estimation, Project Schedule & Budget Runway** | Backlog Sizing (118 Wishlist SP vs. 72 Core MVP SP), Runway Calculations (₹14.0L Capital, ₹2.4L/mo Burn, 5.16 Months Runway), Cone of Uncertainty, Work Breakdown Structure (WBS), Critical Path Method (CPM Network Analysis, 60-Day Critical Path), 12-Week Mermaid Gantt Chart, and Month-by-Month Cash Burn Ledger. |
| [**04_Test_Plan_and_Evidence/**](./04_Test_Plan_and_Evidence/04_Test_Plan_and_Evidence.md) | **Master Test Plan, Verification Evidence & QA Metrics** | IEEE Std 829 Test Strategy, Boundary Value Analysis (BVA for [1–30] quantities and [₹50–₹500] coupons), Equivalence Partitioning, 8-Rule Decision Table for Schedule H/H1 and Stock Rules, 18-Item Execution Defect Log, Defect Density (0.25 defects/SP; 1.44 defects/KLOC), and Defect Removal Efficiency (DRE = 90.0%). |
| [**05_Risk_Register_and_Closure_Note/**](./05_Risk_Register_and_Closure_Note/05_Risk_Register_and_Closure_Note.md) | **Risk Register, RMMM Action Plans & Project Retrospective** | $5 \times 5$ Probability-Impact Matrix, Exposure-Ranked Risk Register ($RE = P \times I$), In-Depth Risk vs. Issue Case Study (resolving physical store stock mismatch via 2-unit safety buffers and 30-min soft holds), Full RMMM Plans for Top 3 Risks, and Engineering Lessons Learned Retrospective. |
| [**06_Change_Management/**](./06_Change_Management/06_Change_Management.md) | **Change Management Plan & Change Control Governance** | Change Control Board (CCB) Charter & Voting Rules, 6-Step Formal Change Control Lifecycle, Marketing Request Walkthrough (`CR-01: Chronic Auto-Refill & Coupons`, 28 SP funded from ₹5.20L contingency), Master Change Request Log (`CR-01` to `CR-04`), Anti-Scope Creep Guidelines, and Formal CCB Sign-Off Table. |
| [**07_BRD/**](./07_BRD/07_BRD_Document.md) | **Business Requirements Document (BRD)** | Strategic Business Context (14 Ahmedabad Outlets), As-Is vs. To-Be Process Models, 5 Strategic KPIs, Stakeholder Personas (Chronic Caregiver, Store Pharmacist, Tele-Pharmacist), 10 High-Level Business Requirements (`BR-01` to `BR-10`), and Commercial Financial Feasibility / Break-Even ROI Analysis. |
| [**08_SOW/**](./08_SOW/08_SOW_Document.md) | **Statement of Work (SOW)** | Legally Binding Commercial Scope, Contractual Milestones (M1 to M6 across 12 Weeks), Milestone Billing & Payment Schedule (₹8.80L Core MVP + ₹5.20L Contingency), RACI Governance Matrix, NFR Acceptance Quality Gates, Scope Trade-In Rules, and IP/Warranty Terms. |

---

## Stitch Interactive UI & High-Fidelity Prototype Suite

All core UML diagrams, workflows, and functional requirements have been translated into a complete, responsive, medical-grade interactive UI suite on **Stitch**. The user experience employs a crisp **Clinical Clarity Light Scheme** (Hygienic Canvas `#FAF8FF` / `#FFFFFF`, Deep Clinical Teal `#0D9488`, Cerulean Blue `#0284C7`, Slate `#0F172A`, and Regulatory Amber `#D97706`).

* **Stitch Project Name:** `projects/17457897745948134773`
* **Project Title:** *PharmaCart - Omni-Channel Pharmacy Platform*
* **Design Theme:** `Clinical Clarity Omnichannel` (Light Mode, Manrope + Inter Typography, 8px Rounded Architecture)

| Screen & Device | Screen Identifier | Mapped UML & Requirements | Key Architectural & Interaction Features |
| :--- | :--- | :--- | :--- |
| **1. Customer Omni-Channel Storefront & Rx Vault**<br>*(Desktop)* | `58ea020efed84776bdd6d39d5fa5ad7f` | • System Context Model<br>• Use Case Diagram (`UC-01` to `UC-04`)<br>• Sequence Diagram (*"Upload Rx and Place Order"* Steps 1–8)<br>• `FR-01`, `FR-03` | • 14 Ahmedabad retail outlet switcher with live driving distance & stock flags.<br>• Real-time 2-unit safety buffer display (`Max(0, Physical - 2)`).<br>• Drag-and-drop Prescription Vault with real-time OCR validation preview.<br>• 30-minute soft reservation countdown cart drawer holding inventory in Redis. |
| **2. Duty Pharmacist Clinical Verification Portal**<br>*(Desktop)* | `f5f30f3af6ae4503bb4ba3dc5a64f114` | • Use Case `UC-05` (Prescription Verification)<br>• Sequence Diagram (*"PharmacistReview"* Steps 9–15)<br>• Class Diagram (`Prescription`, `PharmacistReview`)<br>• `FR-02` (Schedule H/H1 Compliance) | • Dual-pane clinical inspection workstation.<br>• Left pane: High-resolution Rx pan/zoom viewer with Gujarat Pharmacy Council (GSPC) doctor credential verification.<br>• Right pane: Side-by-side line-item medicine dosage matching, generic substitution alerts, and Schedule H regulatory chips.<br>• Tele-pharmacy SLA countdown timer (<= 15 min) and 4-digit digital signing PIN authorization. |
| **3. Express Counter Pickup & OTP Handover Terminal**<br>*(Tablet / Kiosk)* | `eeea772ba9b74557bb1e183fa901802f` | • `Order` Lifecycle State Machine (`READY_FOR_PICKUP` ➔ `COMPLETED`)<br>• Activity Diagram (In-Store Pickup Branch)<br>• `FR-08` (Counter Collection Handover) | • Ergonomic high-contrast touchscreen terminal optimized for store clerks.<br>• 6-digit cryptographic customer OTP numeric keypad.<br>• Real-time laser barcode scanner input hook.<br>• Tamper-evident sealed bag shelf/cubby locator (`Bin A-14`).<br>• 90-second express handover SLA badge and instant local POS receipt release. |
| **4. Central Multi-Store Inventory & Routing Dashboard**<br>*(Desktop)* | `872e882315154562850421287306e5f7` | • Domain Class Diagram (`StoreInventory`, `OrderRoutingEngine`)<br>• Activity Diagram (Split-Fulfillment Fork)<br>• `FR-04`, `FR-05`, `FR-06`<br>• Risk Register Mitigation (`RSK-01`) | • Network-wide aggregate inventory grid across all 14 Ahmedabad pharmacies.<br>• Real-time POS daemon sync latency telemetry (`<= 30s`).<br>• Customer proximity routing visualizer with nearest sister-store automated failover.<br>• Distributed lock monitor, stock threshold alerts, and real-time Kafka event audit logs. |
| **5. PharmaCart Consumer Mobile App (Storefront & Camera Rx Scan)**<br>*(Mobile iOS/Android)* | `49ac67717dc3434fa3a3b9ea38c8c1b6` | • Mobile Context Model<br>• Use Case Diagram (`UC-01` to `UC-04`)<br>• Sequence Diagram (Mobile Customer Flow)<br>• `FR-01`, `FR-03`, `FR-11` | • Native mobile shell with GPS-driven Ahmedabad store switcher (e.g., Satellite Branch 1.2km away).<br>• One-tap Camera OCR prescription scan hero card (<= 15 min verification SLA).<br>• Medicine product feed with 2-unit safety buffer protection and Schedule H/H1 tags.<br>• Floating soft-hold cart reservation bar (28:14 mins Redis countdown timer).<br>• Ergonomic 5-tab bottom navigation with elevated center Rx action button. |
| **6. Mobile Order Tracking & Express Counter Pickup OTP Pass**<br>*(Mobile iOS/Android)* | `e0cc0974efc24bbab4abbb40698938f5` | • Order State Machine (`SUBMITTED` ➔ `READY_FOR_PICKUP` ➔ `COMPLETED`)<br>• Sequence Diagram (Counter Pickup Flow)<br>• `FR-08` (90s Express Handover SLA) | • Digital pickup pass card with optical QR code for fast laser barcode checkout.<br>• Large cryptographic 6-digit handover OTP (`8 4 9 2 0 1`) displayed to customer.<br>• Complete UML state machine vertical visual timeline with pharmacist GSPC signature stamp.<br>• Turn-by-turn driving directions to nearest outlet (850m) and store phone hook.<br>• Downloadable verified Schedule H prescription PDF and itemized GST receipt. |

---

## Key Project Engineering Metrics

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        PHARMACART METRICS AT A GLANCE                  │
├────────────────────────────────────────────────────────────────────────┤
│ Total Backlog Wishlist:        118 Story Points (9 Sprints / 18 Wks)   │
│ Selected Core MVP Scope:        72 Story Points (6 Sprints / 12 Wks)   │
│ Team Velocity:                  14 Story Points per 2-Week Sprint      │
│ Total Capital Cap:             ₹14.00 Lakh                             │
│ Baseline MVP Expenditure:      ₹8.80 Lakh (Labor: ₹7.20L + Infra: ₹1.6L│
│ Unallocated Contingency Buffer:₹5.20 Lakh (Funded 2-Month Runway)     │
│ Critical Path Duration:         60 Business Days (12 Working Weeks)    │
│ Physical Stock Safety Buffer:   2 Units Reserve (Available = Count - 2)│
│ Cart Soft Reservation Hold:     30 Minutes Fixed Expiry Window         │
│ Tele-Pharmacy Verification SLA: <= 15 Minutes                          │
│ POS Distributed Sync Latency:   <= 30 Seconds                          │
│ Defect Removal Efficiency (DRE):90.0% Pre-Release Containment          │
└────────────────────────────────────────────────────────────────────────┘
```

---

## Repository Structure

```text
.
├── 01_SRS_Document/
│   ├── 01_SRS_Document.md
│   └── 01_SRS_Document.pdf
├── 02_UML_Package/
│   ├── 02_UML_Package.md
│   └── 02_UML_Package.pdf
├── 03_Project_and_Budget_Plan/
│   ├── 03_Project_and_Budget_Plan.md
│   └── 03_Project_and_Budget_Plan.pdf
├── 04_Test_Plan_and_Evidence/
│   ├── 04_Test_Plan_and_Evidence.md
│   └── 04_Test_Plan_and_Evidence.pdf
├── 05_Risk_Register_and_Closure_Note/
│   ├── 05_Risk_Register_and_Closure_Note.md
│   └── 05_Risk_Register_and_Closure_Note.pdf
├── 06_Change_Management/
│   ├── 06_Change_Management.md
│   └── 06_Change_Management.pdf
├── 07_BRD/
│   └── 07_BRD_Document.md
├── 08_SOW/
│   └── 08_SOW_Document.md
└── README.md
```

---

## Author & Project Leadership
* **Lead Systems Analyst / Software Architect / Project Manager / QA Lead:** **Ritesh Jadhav**
* **Project:** Case Study No. 68 — PharmaCart (Ahmedabad 14-Store Retail Pharmacy Network)
* **Date:** October 2026
