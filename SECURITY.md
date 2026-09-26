# Security Policy for CrossDiffAction

> **Logos Agent Co., Ltd. / Colvio Studio**  
> **Product**: CrossDiffAction (CrossDiff)  

---

## 1. Security Architecture & Principles

CrossDiffAction is designed under the **Zero Trust & Zero External Dependency** security framework:
1. **100% Org-Internal**: No customer data, metadata, or queries are ever transmitted outside the customer's Salesforce organization.
2. **Strict CRUD / FLS Enforcement**: All Apex controllers operate with `WITH USER_MODE` and `Security.stripInaccessible`.
3. **No External JavaScript Libraries**: Zero risk of supply-chain attacks or third-party tracking.

---

## 2. Reporting a Vulnerability

If you discover a security issue or vulnerability, please notify our security team immediately:
- **Email**: `security@logosagent.com` / `sfpartner@logosagent.com`
- **Response SLA**: Initial acknowledgement within 24 hours; remediation patch plan within 72 hours.
- **Coordinated Disclosure**: We follow responsible disclosure guidelines and will credit reporters in our security advisories.
