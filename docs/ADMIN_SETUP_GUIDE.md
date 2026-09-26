# CrossDiffAction (CrossDiff) — Administrator Setup Guide (Admin Setup Guide)

> **Target Audience**: Salesforce System Administrators  
> **Product**: CrossDiffAction (CrossDiff) — Smart Matrix & Diff Comparator for Salesforce  
> **Package Version**: v0.1.0 (2GP Managed Package)  
> **Package Version ID (04t)**: `04td5000000VuKTAA0`  
> **Publisher**: Colvio (`https://colvio.io`)  

---

## 1. Introduction

CrossDiffAction (CrossDiff) is an AppExchange certified 2GP managed package designed to overcome standard Salesforce ListView limitations. It delivers one-click transposed matrix viewing, automated field-level difference finding (Diff Finder), side-by-side character diffs, and inline bulk editing.

This guide provides step-by-step instructions for package installation, permission set assignment, navigation setup, and Lightning App Builder page configuration.

---

## 2. System Requirements & Prerequisites

- **Supported Salesforce Editions**:
  - Enterprise Edition
  - Unlimited Edition
  - Performance Edition
  - Developer Edition / Scratch Org
  - Professional Edition (native package operation without requiring custom API permissions)
- **User Licenses**:
  - Salesforce Standard License
  - Salesforce Platform License
- **Supported Browsers**:
  - Google Chrome (latest)
  - Microsoft Edge (latest)
  - Mozilla Firefox / Apple Safari
- **External Network Infrastructure**:
  - **Pre-configured Remote Site Setting Included**. Routine operations (record comparison, difference finding, inline editing, Excel/CSV export) require zero external infrastructure (100% Org-internal). Administrative online license verification communicates solely with the packaged Remote Site Setting (`CrossDiff_License_Server`). No customer-side network configuration or Named Credentials required.

---

## 3. Installation Guide

### 3.1. Installing via AppExchange Link
1. Log in to your Salesforce environment with administrative privileges.
2. Navigate to the package install URL:
   ```text
   https://login.salesforce.com/packaging/installPackage.apexp?p0=04td5000000VuKTAA0
   ```
   *(For Sandbox or Scratch Org environments, replace `login.salesforce.com` with `test.salesforce.com`)*
3. Select an installation audience:
   - **Recommended**: **Install for All Users** or **Install for Admins Only** (access is cleanly governed via Permission Sets).
4. Click **Install**.
5. Wait for the confirmation notification.

---

## 4. Permission Set Assignment

CrossDiffAction includes two packaged permission sets out of the box:

| Permission Set Name | Label | Target Users | Included Permissions |
| :--- | :--- | :--- | :--- |
| `crossdiff__CrossDiff_Admin` | **CrossDiff Admin** | System Administrators / Leads | Access to CrossDiffView tab and FlexiPages, full schema describe & read/edit access, organization-wide global preset management & locking (`CrossDiff_Preset__c`), export compliance audit log tracking & reports (`CrossDiff_Export_Log__c`), and license administration (`CrossDiff_License__c`). |
| `crossdiff__CrossDiff_User` | **CrossDiff User** | Standard Users (Sales, Support) | Access to CrossDiffView tab and FlexiPages, viewing & comparing authorized records, personal preset management, export audit logging, and inline editing within user FLS/CRUD boundaries. |

### Assignment Steps:
1. In Salesforce **Setup**, navigate to **Users** ➔ **Permission Sets**.
2. Select **CrossDiff Admin** or **CrossDiff User**.
3. Click **Manage Assignments** ➔ **Add Assignment**.
4. Select the designated users and click **Assign**.

---

## 5. Navigation & Application Setup

### Adding CrossDiff to Lightning App Navigation
1. Go to **Setup** ➔ **Apps** ➔ **App Manager**.
2. Locate your active Lightning App (e.g., *Sales* or *Service*), click the dropdown arrow ➔ **Edit**.
3. In the left navigation, select **Navigation Items**.
4. In the Available Items list, select **`CrossDiff`** and click **Add** to move it to Selected Items.
5. Adjust order as desired and click **Save**.

---

## 6. Lightning App Builder Configuration

The `crossDiffView` LWC can be embedded directly onto any Lightning Home Page, Record Page, or App Page.

### Embedding into Pages:
1. Open the target page, click the gear icon ➔ **Edit Page**.
2. Drag **`crossDiffView`** from the Custom - Managed component palette onto the canvas.
3. Configure component properties in the right-hand panel:

| Property | Type | Default | Description |
| :--- | :---: | :---: | :--- |
| **Allowed Objects (`allowedObjects`)** | String | *(Empty: all allowed)* | Comma-separated list of SObject API names permitted in the object selector (e.g., `Account,Opportunity,Contact`). |
| **Default Record Limit (`defaultLimit`)** | Integer | `10` | Maximum number of records fetched upon initial query (recommended: 5 to 30). |
| **Default Sort Order (`defaultSortOrder`)** | String | `CreatedDate DESC` | Default SOQL `ORDER BY` clause. |

4. Click **Save** and **Activate**.

---

## 7. Security & Governance

- **100% Org-Internal Core Execution**: Routine operations (record comparison, difference calculation, inline editing, Excel/CSV export, presets, audit logs) perform zero HTTP callouts. Customer business records never leave the Salesforce boundary.
- **Controlled License Verification**: The only outbound network communication is an optional, administrator-initiated license verification callout to the dedicated license server, securely enabled by the pre-configured Remote Site Setting (`CrossDiff_License_Server`).
- **Strict CRUD & FLS Enforcement**: All SOQL queries run `WITH USER_MODE`. All updates pass through `Security.stripInaccessible(AccessType.UPDATABLE)`.
- **Zero Vulnerable Dependencies**: No third-party tracking scripts or external CDN JavaScript dependencies.

---

## 8. Support & Legal

- **Publisher**: Colvio (Logos Agent Co., Ltd.)
- **Support Inquiries**: `support@colvio.io`
- **Official Website**: `https://colvio.io`
- **Privacy Policy**: `https://colvio.io/privacy`
- **Terms of Service**: `https://colvio.io/terms`
