# SOC Identity Analytics – Pre-Work

This repository contains reusable XSIAM playbooks and automation aligned with the "Identity Analytics" use case in the SOC Framework. It enhances triage and response for suspicious identity-based alerts — helping SOC teams quickly evaluate authentication anomalies, suspicious user behavior, and cloud identity misuse.

## 📌 Overview

This use case focuses on alerts tied to the **MITRE ATT&CK tactic: Initial Access**, particularly identity-related scenarios. The playbooks leverage Cortex XSIAM’s native enrichment, user investigation, and verdict-handling capabilities to streamline incident response and reduce manual overhead.

## 🚀 Getting Started

### Step 1: Configure the Playbook Trigger

Set up a **Playbook Trigger** to automatically run the identity analytics playbook logic when relevant alerts are detected.

Go To: **Incident Response → Incident Configuration → Playbook Triggers**

- **Trigger Name:** `EP_InitialAccess`
- **Type:** Entry Point Playbook
- **Playbook to Trigger:** `EP_InitialAccess`
- **Filter Criteria:**
    - Alert Field: `Mitre ATT&CK Tactic`
    - Condition: Equals `TA0001 - Initial Access`

### Step 2: Entry Point Playbook Structure

The `EP_InitialAccess` playbook routes identity-related alerts into the **Identity Analytics – Alert Handling** playbook, which performs the following stages:


## 🧪 Validation Tips

To confirm the configuration is working as expected:

- Trigger an alert mapped to `TA0001 - Initial Access` tied to a known user/IP
- Confirm enrichment pulls identity and IP context into the case
- Review verdict and ensure appropriate playbook actions (block, revoke, or close) are taken
- Track outcome metrics in the **SOC Framework Value Dashboard**

## 🧩 Dependencies

- SOC Optimization Framework (for auto-triage, scoring, and layout handling)
- Identity provider integrations (e.g., Okta, Azure AD) configured and ingesting events
- Alerts must include `username`, `source IP`, and `MITRE Tactic` for full workflow execution

---

For enhancement suggestions or integration support, contact your Palo Alto Networks Field team or the SOC Framework maintainers.
