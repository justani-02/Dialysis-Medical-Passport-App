
# 🏥 Medical Passport: Global Dialysis Freedom

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Tech: FHIR](https://img.shields.io/badge/Health%20Standards-FHIR%20/%20HL7-green)](https://www.hl7.org/fhir/)
[![Security: HMAC-SHA256](https://img.shields.io/badge/Security-HMAC--SHA256-red)](https://en.wikipedia.org/wiki/HMAC)

**Medical Passport** is a secure, digital "travel visa" for dialysis patients. It restores travel freedom by providing a tamper-proof, hospital-verified record of life-sustaining dialysis prescriptions ($Q_b$, $Q_d$) and viral serology.

---

## 💡 Inspiration
Our inspiration came from a teammate’s experience in a nephrology clinic, observing the immense difficulty travel poses for people on chronic dialysis. Even short trips demand weeks of coordination and anxiety due to fragmented, slow, and paper-dependent medical sharing. We realized that "data logistics" shouldn't be a barrier to a normal life.


## 📋 What it does
Medical Passport stores a concise, hospital-verified summary of a patient’s essential dialysis information. 
- **For Patients:** A digital card and QR code for easy, offline-ready travel.
- **For Clinics:** A "Scan & Verify" tool that confirms the integrity of the prescription ($Q_b$ and $Q_d$ rates) and recent labs (HIV/HepB/HepC).
- **Goal:** Eliminate the "Information Silo" and reduce clinical risk during cross-border handovers.



## 🛠️ System Architecture & Logic
The system is built on a "Trust, but Verify" model using cryptographic hashing to ensure medical data cannot be altered by the bearer or third parties.

### High-Level User Flow
```mermaid
graph TD
    subgraph Origin [Stage 1: Home Clinic]
    A[Nephrologist Inputs Data] --> B[HMAC-SHA256 Signing]
    B --> C[Encrypted Record Created]
    end

    subgraph Bearer [Stage 2: Patient App]
    C --> D[Secure QR Code Generation]
    D --> E[Offline-Ready Passport]
    end

    subgraph Receiver [Stage 3: Overseas Clinic]
    E --> F[Scan & Recalculate Hash]
    F --> G{Integrity Match?}
    G -- Yes --> H[Safe Dialysis Setup]
    G -- No --> I[Tamper Alert]
    end

```

## 🛡️ Technical Specifications

To ensure this passport is "clinical-grade," we focused on three technical pillars:

* **Data Integrity (HMAC-SHA256):** Every prescription is signed with a secret key. If a value (like Blood Flow Rate $Q_b$) is modified by even one digit, the hash verification fails instantly.
* **Interoperability (FHIR/HL7):** Data is structured using JSON-based FHIR resources (ServiceRequest/Observation) to ensure it can be read by modern hospital EHRs globally.
* **Safety Guardrails:** The system includes a logic layer that flags prescriptions falling outside KDOQI safety guidelines (e.g., ensuring needle gauge matches the $Q_b$ flow rate).

## 🚧 Challenges we ran into

* **Clinical Realism:** Balancing complex medical regulations with a fast-paced development cycle. We had to ensure we didn't oversimplify safety for the sake of the UI.
* **Data Sovereignty:** Designing a model where patients own their data while ensuring it remains "Clinician-Trusted" and unalterable.
* **Cross-Border Standards:** Navigating the lack of a universal standard for dialysis-specific data fields across different healthcare jurisdictions.

## 🏆 Accomplishments that we're proud of

* **Empathetic Tech:** Turning a complex clinical workflow into a simple, user-friendly mobile experience.
* **Zero-Knowledge Potential:** Creating a system where a clinic can verify data without needing a direct, live connection back to the originating hospital's database.

## ⚙️ Built With

* **Design:** Figma
* **Frontend:** React, TypeScript
* **Backend:** Python (FastAPI), Supabase
* **Standards:** FHIR (Fast Healthcare Interoperability Resources), HL7
* **Security:** HMAC-SHA256 Cryptographic Hashing

---

© 2026 Medical Passport Team | Restoring Freedom to the Dialysis Community.
