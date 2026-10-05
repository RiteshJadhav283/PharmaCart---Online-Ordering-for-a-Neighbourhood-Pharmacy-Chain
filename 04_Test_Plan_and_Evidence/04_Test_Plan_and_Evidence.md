# TEST PLAN, QUALITY ASSURANCE & DEFECT ANALYSIS SPECIFICATION
## For PharmaCart - Omni-Channel Pharmacy Ordering Platform
### Document Reference: QA-TEST-PC-2026-V1.0

---

### Document Control & Metadata
* **Project Name:** PharmaCart — Online Ordering for Neighbourhood Pharmacy Chain
* **Case Study Reference:** Case Study No. 68
* **Document Standard:** IEEE Std 829-2008 (Standard for Software and System Test Documentation) & ISO/IEC/IEEE 29119
* **Author / Lead QA & Test Architect:** Ritesh Jadhav
* **Engineering Organization:** PharmaCart Project Delivery Team
* **Target Network:** 14 Retail Pharmacies across Ahmedabad, Gujarat, India
* **Date of Issue:** October 2026
* **Status:** Baseline Approved (Approved by Lead Architect & Head Pharmacist)

---

### Revision History

| Version | Date | Author | Description of Change | Approved By |
| :--- | :--- | :--- | :--- | :--- |
| **0.1** | 2026-10-02 | Ritesh Jadhav | Initial test strategy and test case design | QA Team Lead |
| **0.6** | 2026-10-04 | Ritesh Jadhav | BVA, Decision tables, and equivalence partitioning | Software Architecture Lead |
| **1.0** | 2026-10-05 | Ritesh Jadhav | Execution defect log, DRE and Defect Density metrics | Head Pharmacist & Delivery Manager |

---

## Table of Contents
1. [Test Strategy & Quality Objectives](#1-test-strategy--quality-objectives)
2. [Boundary Value Analysis (BVA)](#2-boundary-value-analysis-bva)
   - 2.1 Order Quantity Input Boundary Testing (Min: 1, Max: 30)
   - 2.2 Coupon Value & Discount Threshold Boundary Testing
3. [Equivalence Class Partitioning (ECP)](#3-equivalence-class-partitioning-ecp)
4. [Comprehensive Decision Table: Prescription & Stock Rules](#4-comprehensive-decision-table-prescription--stock-rules)
   - 4.1 Condition & Action Definitions
   - 4.2 Tabular Decision Truth Matrix
   - 4.3 Test Case Derivation from Decision Rules
5. [Systematic Test Case Suite](#5-systematic-test-case-suite)
6. [Comprehensive Defect Log (Execution Results)](#6-comprehensive-defect-log-execution-results)
7. [Quantitative Defect Metrics & Formulas](#7-quantitative-defect-metrics--formulas)
   - 7.1 Defect Density Computation (per Story Point & KLOC)
   - 7.2 Defect Removal Efficiency (DRE) Computation
   - 7.3 Benchmark Evaluation & Quality Gate Assessment

---

## 1. Test Strategy & Quality Objectives

The testing suite for PharmaCart enforces statutory patient safety, zero dispensing errors for Schedule H/X pharmaceuticals, and accurate synchronization with 14 disconnected retail POS installations across Ahmedabad.

| Quality Objective | Operational Target Metric | Verification Method |
| :--- | :--- | :--- |
| **Zero Schedule Drug Breaches** | 100% block of Schedule H/X drugs without verified Rx | Automated Regression & Negative Testing |
| **Stock Accuracy at Counter** | >= 98.0% fulfillment without stockout cancellation | Concurrency & Race-Condition Testing |
| **Defect Removal Efficiency (DRE)**| >= 90.0% defects filtered prior to production release | Defect Log Mathematical Analysis |
| **Defect Density** | <= 0.30 Defects / Story Point (<= 2.0 Defects / KLOC) | Codebase & Defect Tracking Audit |
| **Verification SLA Adherence** | 90% of prescriptions audited within <= 15 minutes | Performance & Latency Stress Testing |

---

## 2. Boundary Value Analysis (BVA)

Boundary Value Analysis (BVA) targets the edges of input domains where software bugs cluster due to relational operator errors (`<` vs `<=`, or `>` vs `>=`).

### 2.1 Order Quantity Input Boundary Testing (Min: 1, Max: 30)
* **Domain Specification:** A customer may purchase a minimum of **1 unit** (single strip/bottle) up to a statutory retail maximum of **30 units** per order to prevent hoarding and illicit bulk redistribution.
* **Input Domain:** Valid Integer range [1, 30].
* **Testing Values:**
  * Minimum Boundary: Min - 1 = 0, Min = 1, Min + 1 = 2.
  * Nominal Value: Nominal = 15.
  * Maximum Boundary: Max - 1 = 29, Max = 30, Max + 1 = 31.
  * Extreme Robustness Values: -1, 100, Non-numeric (`"ten"`), Decimal (`2.5`).

| Test Case ID | Test Parameter | Input Value | Boundary Category | Expected System Behavior | Actual Result | Status |
| :---: | :--- | :---: | :--- | :--- | :--- | :---: |
| **TC-BVA-QTY-01** | Order Quantity | `-1` | Extreme Lower Invalid | Block input; display: "Quantity must be at least 1" | Blocked with validation error | **PASS** |
| **TC-BVA-QTY-02** | Order Quantity | `0` | Lower Boundary (Min - 1) | Block input; cart rejects zero items | Blocked; cart button disabled | **PASS** |
| **TC-BVA-QTY-03** | Order Quantity | `1` | Lower Boundary (Min) | Accept; minimum permissible order line item | Added to cart (Qty = 1) | **PASS** |
| **TC-BVA-QTY-04** | Order Quantity | `2` | Lower Boundary (Min + 1) | Accept; standard multi-unit purchase | Added to cart (Qty = 2) | **PASS** |
| **TC-BVA-QTY-05** | Order Quantity | `15` | Nominal Valid Value | Accept; typical monthly chronic prescription | Added to cart (Qty = 15) | **PASS** |
| **TC-BVA-QTY-06** | Order Quantity | `29` | Upper Boundary (Max - 1) | Accept; high-volume retail purchase | Added to cart (Qty = 29) | **PASS** |
| **TC-BVA-QTY-07** | Order Quantity | `30` | Upper Boundary (Max) | Accept; maximum permissible retail order | Added to cart (Qty = 30) | **PASS** |
| **TC-BVA-QTY-08** | Order Quantity | `31` | Upper Boundary (Max + 1) | Block input; display: "Maximum allowed retail limit is 30 units" | Blocked; alert rendered | **PASS** |
| **TC-BVA-QTY-09** | Order Quantity | `2.5` | Fractional / Decimal | Block input; integer enforcement rejects fractional strips | Auto-rounded or blocked | **PASS** |
| **TC-BVA-QTY-10** | Order Quantity | `"ABC"` | Non-numeric String | Sanitization rejects string; retains previous state | Rejected; field reset to 1 | **PASS** |

---

### 2.2 Coupon Value & Discount Threshold Boundary Testing
* **Domain Specification:** 
  * Cart minimum subtotal threshold for coupon eligibility: **₹500.00**.
  * Discount calculation: **10% of OTC items**, subject to a maximum cap of **₹100.00**.
  * Absolute statutory rule: Prescription (Schedule H/X) items are excluded from discount computations.
* **Testing Values for Cart Subtotal:**
  * Cart Min Boundary: ₹499.00 (Min - 1), ₹500.00 (Min), ₹501.00 (Min + 1).
* **Testing Values for Calculated Discount:**
  * Discount Cap Boundary: ₹990 cart (10% = ₹99.00), ₹1,000 cart (10% = ₹100.00), ₹1,010 cart (10% = ₹101.00 capped to ₹100.00).

| Test Case ID | Cart Subtotal (OTC) | Coupon Code | Boundary Category | Expected System Behavior | Actual Result | Status |
| :---: | :---: | :---: | :--- | :--- | :--- | :---: |
| **TC-BVA-CPN-01** | ₹499.00 | `PHARMA10` | Subtotal Boundary (Min - 1) | Reject coupon; "Add ₹1.00 more to apply coupon" | Coupon rejected; message displayed | **PASS** |
| **TC-BVA-CPN-02** | ₹500.00 | `PHARMA10` | Subtotal Boundary (Min) | Accept coupon; discount = ₹50.00 (10% of ₹500) | Applied discount: ₹50.00 | **PASS** |
| **TC-BVA-CPN-03** | ₹501.00 | `PHARMA10` | Subtotal Boundary (Min + 1) | Accept coupon; discount = ₹50.10 | Applied discount: ₹50.10 | **PASS** |
| **TC-BVA-CPN-04** | ₹990.00 | `PHARMA10` | Discount Cap (Cap - 1) | Accept coupon; discount = ₹99.00 | Applied discount: ₹99.00 | **PASS** |
| **TC-BVA-CPN-05** | ₹1,000.00 | `PHARMA10` | Discount Cap (Cap) | Accept coupon; discount = ₹100.00 (Exact max cap) | Applied discount: ₹100.00 | **PASS** |
| **TC-BVA-CPN-06** | ₹1,500.00 | `PHARMA10` | Discount Cap (Cap + 1) | Accept coupon; discount capped at exactly ₹100.00 | Applied discount: ₹100.00 | **PASS** |
| **TC-BVA-CPN-07** | ₹800 (Rx only) | `PHARMA10` | Schedule Drug Exclusion | Reject coupon; "Coupons apply exclusively to OTC products" | Coupon rejected | **PASS** |

---

## 3. Equivalence Class Partitioning (ECP)

Equivalence Partitioning divides input data into classes of equivalent data from which test cases can be derived, assuming all members of a partition are processed identically.

| Partition ID | Input Field / Parameter | Valid Equivalence Classes (VEC) | Invalid Equivalence Classes (IEC) |
| :--- | :--- | :--- | :--- |
| **ECP-01** | Order Quantity | **VEC-1:** Integers in [1, 30] | **IEC-1:** Integers < 1<br>**IEC-2:** Integers > 30<br>**IEC-3:** Floats / Decimals<br>**IEC-4:** Non-numeric characters |
| **ECP-02** | Prescription File Upload | **VEC-2:** Formats: JPEG, PNG, PDF<br>**VEC-3:** File Size <= 10 MB | **IEC-5:** Executables (.exe, .sh, .bat)<br>**IEC-6:** Corrupted images (0 bytes)<br>**IEC-7:** File Size > 10 MB |
| **ECP-03** | Prescription Issue Date | **VEC-4:** Date issued within <= 30 days | **IEC-8:** Date issued > 30 days (Expired)<br>**IEC-9:** Future date (> Today) |
| **ECP-04** | Store Physical Stock | **VEC-5:** Physical Count > 2 units (Available > 0) | **IEC-10:** Physical Count <= 2 units (Buffer Lock)<br>**IEC-11:** Physical Count = 0 (Total Stockout) |
| **ECP-05** | Customer Pickup OTP | **VEC-6:** Exactly 6 numeric digits matching hash | **IEC-12:** String length != 6<br>**IEC-13:** Alphanumeric / Special characters<br>**IEC-14:** Expired OTP (> 24 hours) |

---

## 4. Comprehensive Decision Table: Prescription & Stock Rules

### 4.1 Condition & Action Definitions

To test the complex combinatorial business logic governing prescription compliance and multi-store inventory reservation, we construct a formal Decision Table.

#### Conditions (Inputs):
* **C1: Schedule Drug?** Does the basket contain at least one Schedule H, H1, or X medication? (Y / N)
* **C2: Prescription Uploaded?** Has the customer provided a readable doctor prescription document? (Y / N)
* **C3: Pharmacist Approved?** Has a licensed pharmacist validated doctor seal, reg number, and approved the order? (Y / N)
* **C4: Store Stock Available?** Does the target store have sufficient stock after applying the 2-unit safety buffer (`Physical - 2 >= OrderQty`)? (Y / N)

#### Actions (System Outputs):
* **A1: Allow Instant Checkout.** Proceed directly to checkout without pharmacist gate.
* **A2: Prompt Prescription Upload.** Block checkout and render mandatory upload screen.
* **A3: Enqueue to Pharmacist Desk.** Route ticket to central FIFO tele-pharmacy verification portal.
* **A4: Reject Order with Clinical Alert.** Cancel order, notify customer of rejection reason, and provide re-upload link.
* **A5: Soft Reserve Stock (30 Mins).** Place 30-minute reservation lock on store POS inventory.
* **A6: Route to Sister Branch.** Automatically re-route order to the next closest Ahmedabad store with available stock.
* **A7: Issue Picking Slip & OTP.** Confirm order, alert store staff to pack, and generate customer pickup OTP.

---

### 4.2 Tabular Decision Truth Matrix

The 2^4 = 16 possible logical permutations are collapsed into 8 discrete, mutually exclusive business decision rules.

| Rule Category | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 | Rule 6 | Rule 7 | Rule 8 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Condition Evaluation** | | | | | | | | |
| **C1: Schedule H/X Drug in Cart?** | **N** | **N** | **Y** | **Y** | **Y** | **Y** | **Y** | **Y** |
| **C2: Prescription Uploaded?** | — | — | **N** | **Y** | **Y** | **Y** | **Y** | **Y** |
| **C3: Pharmacist Approved?** | — | — | — | **N** | **Y** | **Y** | **Y** | **Y** |
| **C4: Stock Available (Phys - 2 >= Qty)?**| **Y** | **N** | — | — | **Y** | **N (Local)** | **N (All 14)** | **Y (High Vol)** |
| **Action Execution** | | | | | | | | |
| **A1: Allow Instant Checkout** | **X** | | | | | | | |
| **A2: Prompt Prescription Upload** | | | **X** | | | | | |
| **A3: Enqueue to Pharmacist Desk** | | | | | **X** | **X** | **X** | **X** |
| **A4: Reject Order with Clinical Alert**| | | | **X** | | | | |
| **A5: Soft Reserve Stock (30 Mins)** | **X** | | | | **X** | | | **X** |
| **A6: Route to Sister Branch** | | **X** | | | | **X** | | |
| **A7: Issue Picking Slip & OTP** | **X** | | | | **X** | | | |
| **Expected System Behavior** | **OTC Fast Checkout** | **OTC Sister Re-route** | **Rx Blocked at Cart** | **Rx Legally Rejected** | **Standard Rx Approved** | **Sister Store Failover** | **Chain-wide Out of Stock** | **Split-Order Exception** |

---

### 4.3 Test Case Derivation from Decision Rules

* **Test Case realization for Rule 1 (OTC Fast Path):**
  Customer adds 2 strips of Paracetamol (OTC) at Navrangpura store; stock is 10 (`10 - 2 = 8 >= 2`). Cart proceeds directly to payment without prompting for prescription.
* **Test Case realization for Rule 4 (Prescription Rejected):**
  Customer orders Amoxicillin 500mg (Schedule H) and uploads prescription dated 45 days ago. Pharmacist clicks "Reject: Expired Rx". Order immediately transitions to `RX_REJECTED`; zero store inventory is locked.
* **Test Case realization for Rule 6 (Sister Store Re-route):**
  Customer orders Metformin 500mg at Satellite branch; store physical stock is 3 (`3 - 2 = 1 < 2 ordered`). System detects shortage, verifies Bodakdev store (2.1 km away) has 20 units, and automatically reallocates order to Bodakdev.

---

## 5. Systematic Test Case Suite

The test cases below validate end-to-end trace realization linking directly to the SRS requirements matrix.

| Test Case ID | Requirement Ref | Test Description & Objective | Test Input Data | Expected Result | Execution Result |
| :---: | :---: | :--- | :--- | :--- | :---: |
| **TC-RX-01** | FR-01 | Upload valid prescription image (PNG) | 2.4 MB clear JPG prescription | Prescription encrypted AES-256; unique `Rx_ID` generated | **PASS** |
| **TC-RX-02** | FR-01 | Upload malicious executable payload | `exploit.pdf.exe` (Renamed PE) | File type scanner detects MIME mismatch; blocks upload | **PASS** |
| **TC-VR-01** | FR-02 | Pharmacist approval workflow with Council ID | Valid Rx; Pharmacist PIN = `4491` | Approval stamped with Council ID `GPC-44910`; order unblocked | **PASS** |
| **TC-VR-02** | FR-02 | Pharmacist rejection with audit reason code | Blurred Rx image | Rejection recorded; SMS alert dispatched to customer | **PASS** |
| **TC-INV-01** | FR-04 | Ingest 14-store delta POS sync stream | JSON stream from 14 store clients | Central stock ledger updated in <= 30 seconds | **PASS** |
| **TC-BUF-01** | FR-05 | Enforce 2-unit safety buffer rule | Physical Stock = 2; Order Qty = 1 | System reports "Out of Stock" (Effective stock = 0) | **PASS** |
| **TC-BUF-02** | FR-05 | 30-minute soft reservation timeout | Unpaid order held for 30m 01s | Soft lock released automatically; shelf units restored | **PASS** |
| **TC-RT-01** | FR-06 | Multi-store geodesic distance routing | Delivery to Pincode 380009 | Routed to Navrangpura store (Distance = 1.2 km) | **PASS** |
| **TC-OTP-01** | FR-08 | Counter pickup verification with valid OTP | Correct 6-digit OTP entered | Terminal confirms match; prints GST tax invoice | **PASS** |
| **TC-OTP-02** | FR-08 | Brute-force protection on pickup OTP | 3 consecutive incorrect OTPs | Terminal locks OTP entry for 15 minutes; alerts store manager | **PASS** |

---

## 6. Comprehensive Defect Log (Execution Results)

The defect log records all software defects identified, classified, and resolved during Sprint 4 and Sprint 5 testing cycles across the 14-store testbed.

| Defect ID | Severity | Module / Component | Defect Description | Root Cause | Status | Resolution Sprint |
| :---: | :---: | :--- | :--- | :--- | :---: | :---: |
| **BUG-01** | Critical | `ReservationManager` | Race condition allowed 2 online orders for last 3 units concurrently | Soft hold lacked database row-level locking (`SELECT FOR UPDATE`) | Closed | Sprint 4 |
| **BUG-02** | Critical | `PrescriptionService` | Prescriptions uploaded without doctor registration number were accepted | Regex parser failed on non-standard state council registration prefixes | Closed | Sprint 4 |
| **BUG-03** | Major | `StoreSyncDaemon` | POS sync daemon crashed when store Windows terminal rebooted | Daemon lacked auto-restart Windows Service wrapper | Closed | Sprint 4 |
| **BUG-04** | Major | `PromotionEngine` | 10% coupon applied across both OTC and Schedule H prescription items | Subtotal query failed to filter by `is_prescription_mandatory = false` | Closed | Sprint 5 |
| **BUG-05** | Major | `RoutingEngine` | Sister store routing failed if customer address lacked latitude/longitude | Geocoder fallback to Ahmedabad 6-digit pincode was unhandled | Closed | Sprint 5 |
| **BUG-06** | Medium | `PharmacistPortal` | Dual-pane image viewer failed to rotate vertical mobile photos | EXIF orientation metadata was stripped during WebP compression | Closed | Sprint 4 |
| **BUG-07** | Medium | `AuthService` | Pickup OTP SMS delayed by > 5 minutes during peak evening hours | Karix SMS gateway priority queue was set to promotional instead of transactional | Closed | Sprint 5 |
| **BUG-08** | Medium | `OrderService` | Cancelled order failed to release inventory lock on Store #07 POS | Missing exception handler on payment gateway cancellation webhook | Closed | Sprint 5 |
| **BUG-09** | Minor | `CustomerUI` | Cart badge did not increment dynamically without page refresh | React query cache invalidator missing on `addToCart` event | Closed | Sprint 4 |
| **BUG-10** | Minor | `StoreTerminal` | Thermal receipt printer cut line truncated patient doctor name | Receipt template width configured for 58mm instead of 80mm roll | Closed | Sprint 5 |
| **BUG-11** | Major | `ReservationManager` | Safety buffer deducted twice when order was edited in cart | Idempotency token was regenerated on cart quantity update | Closed | Sprint 5 |
| **BUG-12** | Medium | `CatalogService` | Search query for generic "Paracetamol" failed to return "Crocin" | Full-text search index lacked pharmaceutical synonym dictionary | Closed | Sprint 4 |
| **BUG-13** | Minor | `CustomerUI` | Date-picker allowed selecting past birthdates greater than 120 years | Missing boundary validation on patient profile age field | Closed | Sprint 5 |
| **BUG-14** | Critical | `PaymentService` | User double-clicking "Pay" charged credit card twice | UI submit button lacked debounce handler; backend lacked idempotency key | Closed | Sprint 5 |
| **BUG-15** | Medium | `LogisticsService` | Runner manifest listed delivery addresses in random non-geodesic sequence | Missing traveling-salesperson route optimization sort | Closed | Sprint 5 |
| **BUG-16** | Major | `PrescriptionService` | PDF prescriptions containing multiple pages only uploaded page 1 | PDF-to-image converter failed to loop through document page array | Closed | Sprint 5 |
| **BUG-17** | Minor | `StoreTerminal` | Barcode scanner beeped error on valid EAN-13 barcodes with leading zeros | String parser trimmed leading zero character | Closed | Sprint 5 |
| **BUG-18** | Medium | `NotificationService` | WhatsApp notification template failed for non-English customer names | Character encoding set to ASCII instead of UTF-8 | Closed | Sprint 5 |

---

## 7. Quantitative Defect Metrics & Formulas

### 7.1 Defect Density Computation (per Story Point & KLOC)
Defect Density measures the residual defects relative to software size, providing an objective metric of architectural quality and test thoroughness.

#### Metric Definitions:
* **Total Defects Discovered in Testing (D_internal):** 18 Defects.
* **Core MVP Scope Size:** 72 Story Points.
* **Codebase Size (KLOC):** 12.5 Thousand Lines of Code (KLOC) across microservices.

#### Calculation 1: Defect Density per Story Point
* **Formula:**
  ```text
  Defect Density (per Story Point) = Total Internal Defects / Total Story Points
  ```
* **Step-by-Step Calculation:**
  ```text
  Defect Density (SP) = 18 / 72 = 0.25 Defects / Story Point
  ```

#### Calculation 2: Defect Density per KLOC
* **Formula:**
  ```text
  Defect Density (per KLOC) = Total Internal Defects / Codebase Size in KLOC
  ```
* **Step-by-Step Calculation:**
  ```text
  Defect Density (KLOC) = 18 / 12.5 = 1.44 Defects / KLOC
  ```

---

### 7.2 Defect Removal Efficiency (DRE) Computation

Defect Removal Efficiency (DRE) quantifies the quality team's ability to filter out defects prior to customer exposure.

#### Metric Definitions:
* **E (Internal Defects):** Defects caught and resolved by the QA engineering team prior to production deployment = **18 Defects**.
* **D (Escaped Defects):** Defects reported by real users / store clerks during the initial 3-store production pilot in Ahmedabad = **2 Defects** (Defect 1: Minor UI alignment on low-res POS monitor; Defect 2: Thermal printer font size).

#### DRE Formula:
```text
DRE (%) = [ E / (E + D) ] * 100
```

#### Step-by-Step Intermediate Calculation:
```text
Step 1: Calculate Total Identified Defects
Total_Defects = E + D = 18 + 2 = 20 Defects

Step 2: Compute Removal Quotient
DRE_Quotient = 18 / 20 = 0.9000

Step 3: Convert to Percentage
DRE = 0.9000 * 100 = 90.0%
```

---

### 7.3 Benchmark Evaluation & Quality Gate Assessment

| Quality Metric | Measured Value | Industry Standard Benchmark | Compliance Assessment |
| :--- | :---: | :---: | :--- |
| **Defect Removal Efficiency (DRE)**| **90.0%** | 85.0% – 90.0% | **EXCELLENT**: Meets high-reliability industry benchmark. |
| **Defect Density (per KLOC)** | **1.44** | 1.00 – 3.00 Defects/KLOC | **OPTIMAL**: Indicates clean code architecture and low technical debt. |
| **Defect Density (per Story Point)**| **0.25** | 0.20 – 0.40 Defects/SP | **CONTROLLED**: Sits well within acceptable commercial thresholds. |
| **Critical Defect Escapes** | **0** | Strict 0 Tolerance | **PERFECT**: Zero regulatory or medical safety defects escaped to pilot. |

---

### Formal Quality Assurance Sign-Off

*The undersigned confirm that the testing procedures, boundary analyses, decision models, and mathematical defect evaluations documented herein have been executed in compliance with IEEE Std 829. Release 1.0 achieves all required quality thresholds for chain-wide commercial launch.*

**Executed & Documented By:**  
`Ritesh Jadhav`  
Lead QA & Test Architect  
PharmaCart Engineering Team  
Date: October 5, 2026  

**Clinical Safety Endorsement By:**  
`Head Pharmacist-in-Charge`  
Chief Pharmacist, Ahmedabad Central Outlets  
Date: October 5, 2026  

**Approved for Release By:**  
`Head of Software Engineering`  
PharmaCart Project Delivery Team  
Date: October 5, 2026  
