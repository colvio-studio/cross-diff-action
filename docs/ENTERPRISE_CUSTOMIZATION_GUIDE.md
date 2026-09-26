# CrossDiffAction (CrossDiff) — Enterprise Customization & Governance Guide

> **Target Audience**: System Administrators, Salesforce Architects, Center of Excellence (CoE) Teams  
> **Package Version**: v0.1.0 (2GP Managed Package)  
> **Publisher**: Colvio (`https://colvio.io`)  

---

## 1. Overview

This guide explains how to configure and customize CrossDiffAction for specific departments, business processes, compliance auditing, and enterprise governance requirements within Enterprise and Unlimited Edition Salesforce environments.

---

## 2. Department-Specific Comparison Views (FlexiPage Customization)

By leveraging the `allowedObjects` design attribute in Lightning App Builder, administrators can tailor the comparison workspace to the exact records each team works with, reducing visual noise and enforcing data scoping:

### Configuration Examples:
- **Sales Operations Page**: `allowedObjects = "Opportunity,Account,Quote"`
- **Customer Support & Field Service Page**: `allowedObjects = "Case,Asset,Contact,WorkOrder"`
- **Procurement & Legal Page**: `allowedObjects = "Contract,Order,Quote"`
- **Custom SObject Audit**: `allowedObjects = "Invoice__c,Shipment__c,Payment_Log__c"`

### Deployment Steps:
1. Navigate to **Setup** ➔ **User Interface** ➔ **Lightning App Builder**.
2. Open or create a Lightning Page (App Page or Record Page).
3. Select the **`CrossDiffView`** component canvas.
4. In the right-side properties panel, enter the comma-separated API names into **Allowed Objects**.
5. Save and activate the page to targeted profiles or apps.

---

## 3. Governance & Inherited Field-Level Security (FLS)

CrossDiffAction adheres strictly to native Salesforce platform sharing and object security models:
- **Sharing Architecture**: Organization-Wide Defaults (OWD), role hierarchies, manual sharing, and Criteria-Based Sharing Rules are 100% respected.
- **Apex USER_MODE Enforcement**: All SOQL read operations execute under `WITH USER_MODE`. If a user does not have read access to a specific field or record, it is never retrieved.
- **Dynamic FLS Stripping**: All bulk DML updates pass through `Security.stripInaccessible(AccessType.UPDATABLE)`. Read-only or restricted fields are locked on the client side and protected at the database tier.
- **Zero Dual-Maintenance**: No duplicate security rules or custom permission silos to configure or maintain.

---

## 4. Organization-Wide Presets & Centralized Locking

Enterprise teams often require standardized comparison templates (e.g., standard field lists and sorting orders for quarterly executive reviews) that regular end-users cannot accidentally overwrite or corrupt.

### 4.1. Global Preset Architecture (`CrossDiff_Preset__c`)
- **Global Flag (`Is_Global__c`)**: When enabled, the comparison preset appears in the preset picker for all users across the organization.
- **Admin Lock Flag (`Is_Locked__c`)**: When locked, end-users can load and inspect the preset, but cannot overwrite or modify the saved configuration.

### 4.2. Role-Based Permissions for Preset Governance
| Action | Standard User (`CrossDiff_User`) | Administrator (`CrossDiff_Admin`) |
| :--- | :---: | :---: |
| **Create Personal Preset** | ✅ Allowed | ✅ Allowed |
| **Update Personal Preset** | ✅ Allowed | ✅ Allowed |
| **Create Global Preset** | ❌ Blocked | ✅ Allowed |
| **Lock / Unlock Preset** | ❌ Blocked | ✅ Allowed |
| **Delete Global Preset** | ❌ Blocked | ✅ Allowed |

---

## 5. Export Compliance & Automated Audit Logging

Data loss prevention (DLP) and compliance auditing are critical requirements when users export CRM data into spreadsheets. CrossDiffAction provides built-in enterprise audit logging for every export event.

### 5.1. Audit Record Architecture (`CrossDiff_Export_Log__c`)
Whenever a user initiates an export (Excel `.xlsx`, `.xls`, or `.csv`), CrossDiff automatically writes an immutable audit record to the `CrossDiff_Export_Log__c` custom object:
- **Exported By (`User__c`)**: Lookup to the initiating Salesforce User.
- **Export Timestamp (`Export_Time__c`)**: Exact UTC date and time of file generation.
- **Target SObject (`Object_Api_Name__c`)**: API name of the compared object (e.g., `Opportunity`).
- **Record Count (`Record_Count__c`)**: Total number of records included in the spreadsheet.
- **Field Count (`Field_Count__c`)**: Total number of transposed attribute columns exported.
- **Export Format (`Export_Format__c`)**: `XLSX`, `XLS`, or `CSV`.
- **Client Execution Context**: 100% In-Memory client-side generation verified (Zero Data Exfiltration).

### 5.2. Packaged Custom Report Type (`CrossDiff_Export_Logs`)
Administrators can build real-time compliance reports and dashboards immediately after installation:
1. Navigate to the **Reports** tab in Salesforce.
2. Click **New Report** ➔ Search for **`CrossDiff Export Logs`** (Packaged Report Type).
3. Group by `Object_Api_Name__c` or `User__c` to visualize data export frequency and monitor bulk data activity across your enterprise.

---

## 6. Atomic Bulk DML & Partial-Success Fault Tolerance

CrossDiffAction includes enterprise-grade transactional resilience during matrix inline editing:

- **Top Docked Unsaved Changes Bar**: Sticky notification displaying total draft count and affected records with one-click Save / Cancel buttons.
- **Partial-Success Isolation**: If 3 out of 4 records save successfully but 1 record fails due to a custom validation rule or trigger error (`FIELD_CUSTOM_VALIDATION_EXCEPTION`), CrossDiff commits the 3 valid records, keeps the invalid record in draft state, highlights the erroneous cells in high-contrast red (`#EA001E`), and displays the exact platform error message in a contextual tooltip.
- **Copy from Base Cascade**: Replicate standard baseline values across multiple records simultaneously with immediate client-side validation prior to DML submission.
