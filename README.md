# Crime Evidence Management System (CEMS) — Linked List DSA Edition

A browser-based criminal investigation and evidence chain-of-custody management system implemented in vanilla JavaScript using C-style Data Structure and Algorithm (DSA) principles.

The system manages case records as a **Singly Linked List** (`CaseNode`) where each case node maintains an internal linked sub-list of physical, digital, document, and testimonial evidence (`EvidenceNode`).

---

## 🏛️ System Overview

- **Architecture:** Zero external dependencies, single-file HTML5 application (`index.html`).
- **Data Structure:** Singly Linked List with pointer-based node traversal, relinking, and Bubble Sort.
- **Persistence:** Browser `localStorage` engine (Key: `cems.v2`).
- **Visual Design:** Editorial police registry theme retaining dark forest green (`#101916`, `#26372e`), cream/paper tones (`#f2f0e9`, `#fbfaf6`), and lime accents (`#d7f36a`, `#dce8c8`).

---

## 🧩 Core Data Structures (DSA)

### 1. `CaseNode`
Represents an individual criminal case in memory:
```javascript
class CaseNode {
  constructor({ id, type, location, date, priority, status, officer, description, evidence }) {
    this.id = Number(id);           // Unique identifier
    this.type = type;               // Crime category (Theft, Assault, etc.)
    this.location = location;       // Crime scene location
    this.date = date;               // Date reported
    this.priority = priority;       // High, Medium, Low
    this.status = status;           // Open, Under Investigation, Evidence Review, Closed, Solved
    this.officer = officer;         // Investigating officer in charge
    this.description = description; // Case notes
    this.next = null;               // Pointer to next CaseNode
    this.evidenceHead = null;       // Head pointer to EvidenceNode linked list
  }
}
```

### 2. `EvidenceNode`
Sub-linked list node attached to each case:
```javascript
class EvidenceNode {
  constructor({ id, type, description, date, location, collectedBy }) {
    this.id = id;                   // e.g. E001
    this.type = type;               // Physical, Digital, Witness, Document
    this.description = description; // Detailed description
    this.date = date;               // Date collected
    this.location = location;       // Location found / secured
    this.collectedBy = collectedBy; // Forensics officer or technician
    this.next = null;               // Pointer to next EvidenceNode in sub-list
  }
}
```

### 3. Linked List Operations
- **Append `O(n)`:** Inserts new case or evidence node at the end of the list.
- **Linear Traversal Search `O(n)`:** Traverses through node pointers matching queries across Case ID, Crime Type, Location, Officer, and Evidence descriptions.
- **Node Deletion & Relinking `O(n)`:** Traverses to find target node and executes pointer relink:
  ```javascript
  prev.next = curr.next;
  ```
- **In-Memory Bubble Sort `O(n²)`:** Sorts the linked list by swapping node payload attributes and sub-list head references without breaking the linked chain.

---

## ⚡ Key Features

1. **Investigation Dashboard:**
   - Real-time statistics: Total Cases, Active/Open Cases, Solved Cases, Evidence Count, and Assigned Officers.
   - Performance trend indicators.

2. **Case Records & Docket Management:**
   - **Add New Case:** Modal form with inline field validation, required indicator checks, and duplicate Case ID prevention.
   - **Edit Case:** Pre-populated form to update metadata while preserving list structure.
   - **Delete Case:** Confirmation modal detailing the case to be removed before unlinking.
   - **Badges:** Color-coded status badges (Open = Blue, Under Investigation = Amber, Evidence Review = Purple, Closed = Gray, Solved = Green) and priority badges (High = Red, Medium = Amber, Low = Green).

3. **Per-Case Evidence Chain of Custody:**
   - Expandable table rows allowing investigators to inspect attached evidence items.
   - Add new evidence items (`EvidenceNode`) directly to any case.
   - Delete individual evidence nodes with pointer relinking.
   - Evidence count badge displayed directly on each case row.

4. **Live Linked List Visualizer:**
   - Interactive panel showing the live linked list nodes (`HEAD → Node 1 → Node 2 → ... → NULL`).
   - Click any node in the visualizer to jump directly to and highlight that case in the main table.
   - Live updates whenever cases are appended, edited, sorted, or removed.

5. **Search & Multi-Criteria Filtering:**
   - Real-time search across all case and evidence fields.
   - Dropdown filters for Crime Type, Status, and Priority.
   - "Clear Filters" button to reset all criteria.

6. **Linked List Sorting:**
   - Clickable column headers (Case ID, Date Reported, Priority, Status) executing bubble sort on the linked list.

7. **Audit Activity Log:**
   - Keeps track of the last 8 operations (case created, updated, deleted, evidence added, sorted, exported) with timestamps.

8. **Export to CSV:**
   - One-click export downloading all case dockets and attached evidence sub-lists as a formatted `.csv` file.

9. **Keyboard Shortcuts:**
   - `Escape`: Close all open dialogs/modals.
   - `Ctrl+N` / `Cmd+N`: Open "Register New Case" modal from anywhere.

---

## 📋 Default Benchmark Sample Dataset

The system initializes with 6 pre-loaded benchmark cases:
- **Case #101:** Theft (MG Road, Pune) — High Priority — Under Investigation (Officer R. Sharma)
  - *Evidence E001 (Physical):* Broken window glass and footprints near entrance
- **Case #102:** Vandalism (Sector 7, Nashik) — Low Priority — Evidence Review (Officer P. Deshmukh)
  - *Evidence E002 (Digital):* CCTV footage recovered from boundary surveillance
  - *Evidence E003 (Physical):* Spray paint marks on wall and discarded aerosol cans
- **Case #103:** Assault (Camp Area, Pune) — High Priority — Under Investigation (Officer A. Patil)
  - *Evidence E004 (Document):* Witness statement and emergency medical triage report
- **Case #104:** Burglary (College Road, Nashik) — Medium Priority — Open (Officer S. Jadhav)
  - *Evidence E005 (Physical):* Latent fingerprints dusted from door handle and cash drawer
- **Case #105:** Cybercrime (IT Park, Pune) — High Priority — Solved (Officer K. Joshi)
  - *Evidence E006 (Digital):* Server logs, API access keys, and IP transaction traces
- **Case #106:** Drug Trafficking (Highway NH-60) — Medium Priority — Closed (Officer M. Verma)
  - *Evidence E007 (Physical):* Seized contraband samples in sealed chemical pouches

*(You can restore this default dataset at any time using the "Reset Samples" button in the top action bar).*

---

## 🚀 How to Run

1. Open `index.html` in any modern web browser (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari).
2. No local web server, npm packages, build steps, or internet connection are required.
3. All changes are automatically preserved in the browser's `localStorage` under key `cems.v2`.
