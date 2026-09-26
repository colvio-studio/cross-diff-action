# CrossDiffAction (CrossDiff) — Salesforce 管理者セットアップガイド (Admin Setup Guide)

> **対象読者**: Salesforce システム管理者  
> **製品名**: CrossDiffAction (CrossDiff) — Smart Matrix & Diff Comparator for Salesforce  
> **バージョン**: v0.1.0 (2GP Managed Package)  
> **パッケージバージョンID (04t)**: `04td5000000VuKTAA0`  
> **最終更新日**: 2026-09-06  

---

## 1. はじめに

CrossDiffAction（以下、CrossDiff）は、Salesforceの標準リストビューでは難しかった「複数レコードの横並び突き合わせ」「ワンクリック縦横反転（マトリクス表示）」「項目の値差分抽出（Diff Finder）」「Side-by-Side詳細比較」「インライン一括編集」を提供する AppExchange 認定マネージドパッケージです。

本ガイドでは、Salesforce組織へのパッケージインストールから、権限セットの割り当て、Lightning アプリケーションへのタブ追加、Lightning アプリケーションビルダーによるページ配置までの初期セットアップ手順を説明します。

---

## 2. システム要件 & 前提条件

- **Salesforce Edition**:
  - Enterprise Edition
  - Unlimited Edition
  - Performance Edition
  - Developer Edition / Scratch Org
  - Professional Edition (※APIアクセス権限不要のネイティブパッケージ)
- **ユーザーライセンス**:
  - Salesforce Standard License
  - Salesforce Platform License
- **ブラウザ**:
  - Google Chrome（最新版推奨）
  - Microsoft Edge（最新版推奨）
  - Mozilla Firefox / Apple Safari
- **外部インフラ・通信**:
  - **同梱のリモートサイト設定で完結**。日常業務（レコード比較、差分表示、インライン編集、Excel/CSV出力等）は 100% Salesforce Org 内部完結。システム管理者によるオンラインライセンス同期用の Remote Site Setting (`CrossDiff_License_Server`) はパッケージに同梱済みのため、顧客側での追加ネットワーク設定や Named Credential の構築は不要です。

---

## 3. インストール手順

### 3.1. インストールリンクからの実行
1. 管理者権限を持つユーザーで Salesforce 組織にログインします。
2. 以下のインストール URL にアクセスします：
   ```text
   https://login.salesforce.com/packaging/installPackage.apexp?p0=04td5000000VuKTAA0
   ```
   *(Sandbox または Scratch Org にインストールする場合は `login.salesforce.com` を `test.salesforce.com` に置き換えてください)*
3. インストール対象を選択します：
   - **推奨**: **「すべてのユーザーのインストール」** または **「管理者のみのインストール」**（後から権限セットで柔軟に制御可能）
4. **「インストール」** をクリックします。
5. インストール完了メッセージを確認します。

---

## 4. 権限セット (Permission Sets) の割り当て

CrossDiff には、用途に応じた2種類の権限セットが標準同梱されています。

| 権限セット名 (API参照名) | 表示ラベル | 対象ユーザー | 付与される主な権限 |
| :--- | :--- | :--- | :--- |
| `crossdiff__CrossDiff_Admin` | **CrossDiff Admin** | システム管理者 / リーダー | ・CrossDiffView タブ・FlexiPageの利用<br/>・オブジェクトスキーマのDescribe & 読取/更新<br/>・全社プリセット（`CrossDiff_Preset__c`）の作成・全社ロック権限<br/>・エクスポート監査ログ（`CrossDiff_Export_Log__c`）の追跡およびカスタムレポート参照<br/>・ライセンス設定（`CrossDiff_License__c`）の管理権限 |
| `crossdiff__CrossDiff_User` | **CrossDiff User** | 一般エンドユーザー / 営業・サポート | ・CrossDiffView タブ・FlexiPageの利用<br/>・自身がアクセス権を持つオブジェクト・レコードの比較・閲覧<br/>・個人の比較プリセット保存・呼出（全社ロックプリセットの適用）<br/>・エクスポート実行（監査ログの自動記録）<br/>・インライン編集（オブジェクトのFLS/CRUD範囲内） |

### 権限セットの割り当て手順
1. Salesforce の **[設定] (歯車アイコン)** ➔ **[ユーザー]** ➔ **[権限セット]** を開きます。
2. **`CrossDiff Admin`** または **`CrossDiff User`** をクリックします。
3. **[割り当ての管理]** ➔ **[割り当てを追加]** をクリックします。
4. 対象のユーザーを選択し、**[割り当て]** をクリックします。

---

## 5. アプリケーション & ナビゲーションへの追加

### 5.1. Lightning アプリケーションのナビゲーションバーへの追加
ユーザーがいつでもワンクリックで CrossDiff を開けるよう、標準・カスタムアプリケーション（例: 「セールス」「サービス」）のナビゲーションバーにタブを追加します。

1. **[設定]** ➔ **[アプリケーション]** ➔ **[アプリケーションマネージャー]** を開きます。
2. 追加先のアプリアプリケーション（例: `セールス (Lightning)`）の右端の下矢印 ➔ **[編集]** をクリックします。
3. 左側メニューの **[ナビゲーション項目]** を選択します。
4. 利用可能な項目から **`CrossDiff`** を探し、**[追加]** 矢印をクリックして選択済みの項目へ移動します。
5. 表示順序を好みの位置に調整し、**[保存]** をクリックします。

---

## 6. Lightning アプリケーションビルダーでの配置 & プロパティ設定

CrossDiff の LWC コンポーネント（`crossDiffView`）は、スタンドアロンタブとしてだけでなく、**任意の Lightning ページ（ホームページ、レコードページ、アプリケーションページ）** にコンポーネントとして埋め込むことができます。

### 6.1. ホームページ / アプリケーションページへの埋め込み手順
1. 対象のページを開き、右上の **[設定] (歯車アイコン)** ➔ **[編集ページ]** をクリックします。
2. 左側のコンポーネントパレットの **[カスタム - 管理]** セクションから **`crossDiffView`** をドラッグし、ページの任意の領域に配置します。
3. 右側のプロパティパネルで以下の設定を行います：

| プロパティ名 | 型 | デフォルト値 | 説明 |
| :--- | :---: | :---: | :--- |
| **対象オブジェクト絞り込み (`allowedObjects`)** | String | *(空: 全CRMオブジェクト許可)* | 画面上に表示・選択を許可するオブジェクトAPI名をカンマ区切りで指定（例: `Account,Opportunity,Contact`）。 |
| **デフォルト表示件数 (`defaultLimit`)** | Integer | `10` | 初期ロード時に取得・表示する最大レコード数（推奨: 5〜30件）。 |
| **デフォルトソート順 (`defaultSortOrder`)** | String | `CreatedDate DESC` | 初期表示時のSOQLソート基準。 |

4. **[保存]** ➔ **[有効化]** をクリックします。

---

## 7. セキュリティ & ガバナンス仕様

- **業務データの完全な Org 内部完結 (Zero Business Data Callout)**:
  日常のレコード比較、差分検出、インライン編集、Excel/CSV出力、プリセット管理、監査ログ記録などの通常業務は 100% Salesforce Org 内で完結し、外部通信は一切行われません。顧客データが外部ネットワークに送信されることはありません。
- **管理者限定のライセンスオンライン同期**:
  システム管理者がライセンス管理画面から明示的に同期を実行した場合にのみ、同梱の Remote Site Setting (`CrossDiff_License_Server`) を通じて Cloudflare ライセンスサーバーへの HTTPS 通信（HMAC-SHA256 署名検証付き）が行われます。送信されるデータはライセンス検証に必要な最小限の識別子（Org ID、管理者メールアドレス）のみに限定されます。
- **Salesforce CRUD & FLS 厳格遵守**:
  すべての SOQL および DML は `WITH USER_MODE` および `Security.stripInaccessible` を介して実行されます。ユーザーが Salesforce 上で参照・編集権限を持たない項目は、画面上に表示されず、更新も遮断されます。
- **データストレージの完全性**:
  比較プリセットや監査ログ、ライセンス設定は、Salesforce 標準のカスタムオブジェクト（`CrossDiff_Preset__c`、`CrossDiff_Audit_Log__b`）および保護された階層カスタム設定（`CrossDiff_License__c`）に安全に保存されます。

---

## 8. サポート & お問い合わせ

- **開発・提供元**: Logos Agent Co., Ltd. (d.b.a. Colvio)
- **サポート窓口**: `support@colvio.io`
- **公式サイト**: `https://colvio.io`
