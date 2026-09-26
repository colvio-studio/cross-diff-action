# CrossDiffAction — Version 0.1.0 Release Notes (Initial 2GP Build)

> **Release Version**: `0.1.0.1` (`CrossDiffAction@0.1.0-1`)  
> **Milestone**: Stage 1 Commercial Release Build for Colvio Studio  
> **Subscriber Package Version ID (04t)**: `04td5000000VuKTAA0`  
> **Release Date**: August 2026  
> **Target Editions**: Enterprise, Unlimited, Performance, Developer, Professional  

---

## What is New in v0.1.0

### 1. Core Matrix & Difference Engine
- **Instant Transpose View**: Rotate standard and custom CRM records into a vertical matrix view.
- **Smart Diff Finder**: Highlights data discrepancies across records and provides a "Diff Only" filter.
- **Base Record Comparison**: Set any record as a baseline to highlight divergent field values.
- **Side-by-Side Detail Diff Modal**: Character-level diff comparison for long text and rich text fields.

### 2. Productivity & Inline Actions
- **Matrix Inline Editing**: Edit multiple records directly within the matrix table.
- **Bulk DML Save**: One-click transactional update with `Security.stripInaccessible` protection.
- **Copy from Base (Bulk Propagate)**: One-click copying of baseline record field values across all compared records.
- **Proprietary Excel (.xlsx) & CSV Export**: Zero-external-dependency spreadsheet generator built directly in native JavaScript.
- **Comparison Presets**: Save, overwrite, and recall custom comparison views.

### 3. Global Multi-Language Support (i18n)
- Comprehensive translation across 8 languages: English, Japanese, German, French, Spanish, Simplified Chinese, Traditional Chinese, and Korean.

### 4. Security & Compliance
- 100% Salesforce Org-Internal Native Execution for CRM data (Zero External Business Data Callouts).
- Packaged RemoteSiteSetting (`CrossDiff_License_Server`) for cryptographically signed HMAC-SHA256 online license verification.
- Fully compliant with Salesforce AppExchange Security Review standards (CRUD/FLS in user mode, SOQL injection immunity).
