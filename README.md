<div align="center">

# CrossDiffAction (CrossDiff)

### ☷ Smart Matrix & Diff Comparator for Salesforce

*Colvio Studio Flagship Commercial Utility*

[![Salesforce 2GP](https://img.shields.io/badge/Salesforce-2GP%20Managed%20Package-0176D3?style=flat-square&logo=salesforce)](https://appexchange.salesforce.com)
[![Zero External Business Data Callout](https://img.shields.io/badge/Security-100%25%20Native%20Zero%20Callout-10B981?style=flat-square)](https://colvio.io#security)
[![Enterprise Ready](https://img.shields.io/badge/Enterprise-Audit%20Logs%20%26%20Presets-818CF8?style=flat-square)](docs/customer/ENTERPRISE_CUSTOMIZATION_GUIDE.md)
[![Publisher](https://img.shields.io/badge/Engineered%20by-Colvio%20Studio-4F46E5?style=flat-square)](https://colvio.io)
[![AppExchange Security](https://img.shields.io/badge/AppExchange-Security%20Review%20Ready-06B6D4?style=flat-square)](docs/marketplaces/appexchange/security-review/SECURITY_REVIEW_TESTING_INSTRUCTIONS.md)

<br/>

<img src="docs/images/appexchange_hero_banner_1200x500.png" width="100%" alt="CrossDiffAction Hero Banner" style="border-radius: 8px; box-shadow: 0 10px 25px rgba(0,0,0,0.3);" />

<br/><br/>

**Tired of endless horizontal scrolling in Salesforce standard list views?**<br/>
**Rotate records into a clean vertical matrix, pinpoint discrepancies in seconds, and bulk-edit with zero friction.**

[**Explore on Colvio.io**](https://colvio.io) • [**AppExchange Listing**](https://appexchange.salesforce.com) • [**Admin Setup Guide**](docs/customer/ADMIN_SETUP_GUIDE.md) • [**User Guide**](docs/customer/USER_GUIDE.md) • [**Report an Issue**](https://github.com/colvio-studio/cross-diff-action/issues)

</div>

---

## 💡 Why CrossDiffAction?

Salesforce standard list views force users to scroll horizontally across 30+ columns to compare competing Opportunities, verify duplicate Accounts, audit Case resolutions, or inspect custom objects. Subtle discrepancies often slip through unnoticed, leading to data degradation and lost revenue.

**CrossDiffAction (CrossDiff)** solves this friction by transposing your data: **fields run vertically down the Y-axis, while records align side-by-side along the X-axis**. With instant Diff Finder filtering, baseline comparisons, deep character-level rich text diffs, and client-side Excel exports, CrossDiff turns tedious manual audits into a single-click superpower.

---

## ✨ Key Capabilities & Visual Walkthrough

### 1. ☷ 1-Click Transpose Matrix View (Account & Opportunity Benchmarking)
Rotate any standard or custom Salesforce object into a vertical matrix. Compare up to dozens of records side-by-side without horizontal table clipping. Includes 3-tier multi-column sorting and a pinpoint record search picker.

<div align="center">
  <img src="docs/images/screenshot_01_transpose_matrix.png" width="90%" alt="Transpose Matrix View" style="border-radius: 6px; border: 1px solid #CBD5E1; margin: 12px 0 24px;" />
</div>

---

### 2. ⚡ Smart Diff Finder & Baseline Discrepancy Spotlight
Activate **Diff Only** mode with a single click. Identical rows are instantly collapsed, spotlighting only the divergent values with signature high-contrast amber badges (`#FEF3C7`). Designate any record as the **Baseline (★ Base)** to calculate all variances dynamically.

<div align="center">
  <img src="docs/images/screenshot_02_diff_finder.png" width="90%" alt="Smart Diff Finder" style="border-radius: 6px; border: 1px solid #CBD5E1; margin: 12px 0 24px;" />
</div>

---

### 3. 🔍 Side-by-Side Character & Word Level Diff Modal
Auditing long text, contract clauses, or rich text descriptions? Launch the deep inspection modal to view character-level inline diffs (red for deleted/original text, green for added/new text) computed client-side via our proprietary zero-dependency LCS Diff engine.

<div align="center">
  <img src="docs/images/screenshot_03_character_diff_modal.png" width="90%" alt="Character Diff Modal" style="border-radius: 6px; border: 1px solid #CBD5E1; margin: 12px 0 24px;" />
</div>

---

### 4. ✏️ Matrix Inline Bulk Edit, [Copy from Base], & Atomic DML
Edit picklists, currencies, numbers, and text fields directly within the matrix. Cascade standard values across all comparison records using **Copy from Base**. When saving, atomic DML protections isolate partial-success records and retain unsaved errors with clear red-border highlights and field-level error messages.

<div align="center">
  <img src="docs/images/screenshot_04_matrix_inline_edit.png" width="90%" alt="Matrix Inline Bulk Edit" style="border-radius: 6px; border: 1px solid #CBD5E1; margin: 12px 0 24px;" />
</div>

---

### 5. 📥 Client-Side In-Memory Excel / CSV Export & Enterprise Governance
Download formatted `.xlsx`, legacy `.xls`, or UTF-8 BOM `.csv` spreadsheets generated entirely within your browser sandbox. For Enterprise teams, CrossDiff features **Organization-Wide Locked Presets** (`CrossDiff_Preset__c`) and **Automated Export Audit Logging** (`CrossDiff_Export_Log__c`) with native custom report types.

<div align="center">
  <img src="docs/images/screenshot_05_excel_export_and_presets.png" width="90%" alt="Native Excel Export and Presets" style="border-radius: 6px; border: 1px solid #CBD5E1; margin: 12px 0 24px;" />
</div>

---

## 🛡️ Enterprise Security & Architecture (100% Native)

CrossDiff operates **100% inside your Salesforce Org runtime**. 

- **Zero Business Data Callouts**: CRM records, customer metadata, and export files never leave your Salesforce boundary.
- **Strict FLS & CRUD Enforcement**: Built with Apex `WITH USER_MODE` and programmatic Field-Level Security verification. Unauthorized fields are masked automatically.
- **Cryptographic License Verification**: License entitlements are verified via HMAC-SHA256 signatures with protected custom metadata and dedicated sandbox multi-tenant routing.

```mermaid
graph TD
    subgraph SF_Org ["☁️ Customer Salesforce Org (100% Native Boundary)"]
        UI["🖥️ Lightning Web Component<br/>(crossDiffView)"]
        Controller["⚡ Apex Controller (WITH USER_MODE)<br/>CrossDiffController & Services"]
        DB[("🗄️ Standard & Custom SObjects<br/>(Opportunities / Accounts / Custom)")]
        Audit[("🛡️ Export Audit Log<br/>(CrossDiff_Export_Log__c)")]
        Presets[("📁 Preset Store<br/>(CrossDiff_Preset__c)")]
        MemoryEngine["📊 Client-Side Export Engine<br/>(Pure In-Memory Spreadsheet Generation)"]

        UI <-->|Lightning Data Service / FLS| Controller
        Controller <-->|SOQL / DML User Mode| DB
        Controller -->|Log Audit Event| Audit
        Controller <-->|Load / Save Presets| Presets
        UI -->|Generate XLSX / CSV| MemoryEngine
    end

    subgraph Colvio_Cloud ["🌐 License Verification (Entitlements Only)"]
        Server["🔐 Colvio License Server<br/>(HMAC-SHA256 Signed Verification)"]
    end

    Controller -.->|Org-ID & Tier Sync Only<br/>Via RemoteSiteSetting| Server
```

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Install Package
Click **Get It Now** on the [AppExchange](https://appexchange.salesforce.com) or deploy the 2GP Managed Package into your Sandbox / Production environment:
- **Package ID (04t)**: `04td5000000VuKTAA0` (Version: `0.1.0.1` / `CrossDiffAction@0.1.0-1`)
- **Direct Install Link**: [https://login.salesforce.com/packaging/installPackage.apexp?p0=04td5000000VuKTAA0](https://login.salesforce.com/packaging/installPackage.apexp?p0=04td5000000VuKTAA0)

### Step 2: Assign Permission Sets
Assign one of the bundled permission sets to your users:
- `CrossDiff_Admin`: Full access to preset management, global locking, license configuration, and audit logging.
- `CrossDiff_User`: Standard end-user access to matrix view, diff finder, inline editing, and exports.

### Step 3: Add to Record Page or App
1. Navigate to **Setup** ➔ **App Builder** ➔ Edit any Record Page (e.g. `Opportunity`) or App Page.
2. Drag and drop the **`CrossDiffView`** custom component onto the canvas.
3. (Optional) Configure `allowedObjects` in the component properties panel to restrict comparisons to specific objects.
4. Save and Activate!

---

## 🌍 Global Multi-Language Support

CrossDiffAction comes pre-configured with native translation support across **8 major enterprise languages**:
- 🇺🇸 English (`en_US` - Default)
- 🇯🇵 Japanese (`ja` - 日本語)
- 🇩🇪 German (`de` - Deutsch)
- 🇫🇷 French (`fr` - Français)
- 🇪🇸 Spanish (`es` - Español)
- 🇨🇳 Simplified Chinese (`zh_CN` - 简体中文)
- 🇹🇼 Traditional Chinese (`zh_TW` - 繁體中文)
- 🇰🇷 Korean (`ko` - 한국어)

---

## 📦 Pricing & Commercial Editions

| Edition | Price | Target Audience | Key Features |
| :--- | :--- | :--- | :--- |
| **Standard** | **$9** /user/month | Small Teams & Sales Ops | Transposed Matrix, Diff Finder, Base Record Comparator, CSV Export, Personal Presets |
| **Professional** | **$15** /user/month | Growth Businesses | All Standard features + Character Diff Modal, Inline Bulk Edit, Copy from Base, XLSX Export |
| **Enterprise** | **Custom** (Volume/Contract) | Large Enterprise & Regulated | All Pro features + Organization-Wide Locked Presets, Automated Export Audit Logs, Priority SLA |

---

## 📚 Complete Documentation Sitemap

- **Admin & Setup**:
  - 📋 [**Admin Setup Guide (English)**](docs/customer/ADMIN_SETUP_GUIDE.md)
  - 🇯🇵 [**管理者セットアップガイド（日本語）**](docs/customer/ADMIN_SETUP_GUIDE_JA.md)
- **User Guides**:
  - 👤 [**End User Guide (English)**](docs/customer/USER_GUIDE.md)
  - 🇯🇵 [**エンドユーザー操作マニュアル（日本語）**](docs/customer/USER_GUIDE_JA.md)
- **Enterprise & Governance**:
  - 🛡️ [**Enterprise Customization & Governance Guide (English)**](docs/customer/ENTERPRISE_CUSTOMIZATION_GUIDE.md)
  - 🇯🇵 [**エンタープライズカスタマイズガイド（日本語）**](docs/customer/ENTERPRISE_CUSTOMIZATION_GUIDE_JA.md)
- **Security & Quality**:
  - 🔒 [**AppExchange Security Review Testing Instructions**](docs/marketplaces/appexchange/security-review/SECURITY_REVIEW_TESTING_INSTRUCTIONS.md)
  - 📊 [**Data Flow & Security Architecture**](docs/marketplaces/appexchange/security-review/DATA_FLOW_AND_SECURITY.md)
  - 🛡️ [**Security Policy & Responsible Disclosure (SECURITY.md)**](SECURITY.md)
  - 📄 [**Internal Developer Overview (日本語)**](docs/architecture/INTERNAL_DEVELOPMENT_OVERVIEW_JA.md)

---

## 💬 Support & Inquiries

- **Email Support**: [support@colvio.io](mailto:support@colvio.io) (Guaranteed 24-hour asynchronous SLA)
- **Issue Tracker**: [GitHub Issues](https://github.com/colvio-studio/cross-diff-action/issues)
- **Studio Portal**: [https://colvio.io](https://colvio.io)
- **Privacy Policy**: [https://colvio.io/privacy](https://colvio.io/privacy)
- **Terms of Service**: [https://colvio.io/terms](https://colvio.io/terms)

---

<div align="center">
  <sub>Crafted with boutique precision by <a href="https://colvio.io"><strong>Colvio Studio</strong></a>. Clever Utilities, Frictionless Workflows.</sub>
</div>
