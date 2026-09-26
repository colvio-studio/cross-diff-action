# CrossDiffAction (CrossDiff) — End User Guide (User Guide)

> **Target Audience**: Salesforce End Users (Sales Operations, Account Executives, Customer Success, Managers)  
> **Product**: CrossDiffAction (CrossDiff) — Smart Matrix & Diff Comparator for Salesforce  
> **Package Version**: v0.1.0  
> **Publisher**: Colvio (`https://colvio.io`)  

---

## 1. Introduction

Comparing multiple records in Salesforce (Opportunities, Accounts, Quotes, Contracts, Cases) using standard list views has always required endless horizontal scrolling and manual squinting to find subtle discrepancies.

**CrossDiffAction (CrossDiff)** solves this friction by transposing records into a vertical matrix view and spotlighting field-level differences with instant Diff Finder and inline editing.

---

## 2. Interface Layout & Navigation

```text
+-----------------------------------------------------------------------------------+
|  [CrossDiff Logo]  [Object Selector ▼]  [Record Search 🔍]  [Presets ▼]  [Lang]   |  <-- Control Bar
+-----------------------------------------------------------------------------------+
|  [Diff Only Filter 🔘]  [Base Record ▼]  [Edit Mode ✏️]  [Export Excel 📥]        |  <-- Action Bar
+-----------------------------------------------------------------------------------+
|  Field Name (Y-axis) | Record A (Base)   | Record B          | Record C           |  <-- Transposed Matrix
|  --------------------+-------------------+-------------------+--------------------+
|  Account Name        | Acme Corp         | Acme Corp         | Acme Corp          |
|  Annual Revenue      | $5,000,000        | $3,000,000 (Diff) | $8,000,000 (Diff)  |
|  Stage               | Proposal          | Negotiation (Diff)| Proposal           |
+-----------------------------------------------------------------------------------+
|  [Selected: 3]  [Diff Fields: 2]  [Copy Summary 📋]                               |  <-- Status Bar
+-----------------------------------------------------------------------------------+
```

---

## 3. Core Feature Guide

### 3.1. Object Selection & Fast Field Search
- Use the primary dropdown to choose any supported Standard or Custom SObject (e.g., `Opportunity`, `Account`).
- Type keywords into the field search bar to instantly filter down the displayed attributes.

### 3.2. Multi-Column Sorting & Pinpoint Record Picker
- **Multi-Sort**: Chain up to 3 sorting rules (e.g., `CloseDate ASC`, `Amount DESC`).
- **Record Picker**: Search and select specific records across your entire Org to compare in a focused session.

### 3.3. Smart Diff Finder
- **Diff Only Toggle**: When activated, hides all matching rows and displays **only fields where values diverge** across the selected records. Reduces comparison review time from minutes to seconds.

### 3.4. Baseline Record Comparison (Base Record Diff)
- Designate any record as the baseline. The matrix automatically highlights cells in yellow that differ from the selected standard.

### 3.5. Side-by-Side Character Diff Modal
- Click on long text or rich text cells to open a side-by-side inspection modal showing exact inline word and character differences (green for added, red for deleted text).

### 3.6. Matrix Inline Editing, Copy from Base & Bulk DML Save
- Toggle **Edit Mode** to turn matrix cells into active input fields.
- Use **Copy from Base** on any row to instantly cascade standard values from your baseline record across all comparison records.
- Click **Save** in the top or bottom action bar to commit all edits in a secure transaction.
- **Partial-Success Error Retain**: If a record fails validation rules, valid records are saved, while erroneous cells are highlighted with red borders (`#EA001E`) and contextual error popovers so you can correct values and retry without losing drafts.

### 3.7. 100% Native In-Memory Excel / CSV Export
- Click **Export Excel (XLSX)**, **XLS**, or **Export CSV** to download a formatted spreadsheet reflecting your exact matrix view.
- **Pure Native Execution**: Generated entirely in your browser's memory without external server processing or data exfiltration. Every export event is recorded to the organization audit log (`CrossDiff_Export_Log__c`).

### 3.8. Saving & Loading Comparison Presets
- Save frequent comparison configurations (object, selected records, fields, sort rules) as named personal presets for one-click recall.
- **Organization-Wide Global Presets**: Presets marked with `🔒 GLOBAL` are distributed by administrators for standardized team audits (e.g. Executive Pipeline Review). These presets can be loaded by all users and are protected against accidental overwriting.

### 3.9. Multi-Language Support
- Switch seamlessly between 8 international languages using the language toggle in the control bar.

---

## 4. Frequently Asked Questions (FAQ)

**Q. Why are some fields read-only with a lock icon?**  
A. Formula fields, auto-numbers, system audit timestamps (`CreatedDate`), and fields where your profile lacks edit permissions under Field-Level Security (FLS) are automatically protected as read-only.

**Q. Is my data safe when exporting to Excel?**  
A. Yes. CrossDiff generates export files entirely inside your browser sandbox. No records or telemetry are transmitted to Colvio or any third-party server.
