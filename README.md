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
└── README.md
```

---

## Author & Project Leadership
* **Lead Systems Analyst / Software Architect / Project Manager / QA Lead:** **Ritesh Jadhav**
* **Project:** Case Study No. 68 — PharmaCart (Ahmedabad 14-Store Retail Pharmacy Network)
* **Date:** October 2026
