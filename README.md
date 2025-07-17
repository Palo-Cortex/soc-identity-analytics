# SOC Identity Analytics – Pre-Work

This repository contains reusable XSIAM playbooks and automation aligned with the "Identity Analytics" use case in the SOC Framework. It enhances triage and response for suspicious identity-based alerts — helping SOC teams quickly evaluate authentication anomalies, suspicious user behavior, and cloud identity misuse.

## 📌 Overview

This use case focuses on alerts tied to the **MITRE ATT&CK tactic: Initial Access**, particularly identity-related scenarios. The playbooks leverage Cortex XSIAM’s native enrichment, user investigation, and verdict-handling capabilities to streamline incident response and reduce manual overhead.

### Step 2: Entry Point Playbook Structure

The `EP_InitialAccess` playbook routes identity-related alerts into the **Identity Analytics – Alert Handling** playbook, which performs the following stages:

#### 🧪 Analysis
- Enriches the associated **IP address** and **account username**
- Provides context such as known risk history, user attributes, and asset value

#### 🔍 Investigation
- Retrieves and evaluates related **XDR alerts** for the same user by MITRE tactic
- Executes cloud-specific sub-playbooks:
    - **Okta User Investigation** for suspicious SSO behavior or session misuse
    - **Azure User Investigation** for anomalous login or privilege escalation attempts

#### ✅ Verdict
- Determines whether the behavior is **malicious** or **benign** based on enrichment and correlation

#### 🛡️ Verdict Handling
- **Malicious:** Blocks IP, revokes sessions, and clears tokens
- **Non-malicious:** Annotates alert and completes case handling without escalation

## 🧠 Why This Matters

This playbook supports the XSIAM FieldOps Model’s value drivers:

| Value Driver          | Capability Delivered                                                |
|----------------------|---------------------------------------------------------------------|
| Transformation        | Analysts are presented with enriched, context-rich identity cases   |
| Risk & Resiliency     | Identity anomalies tied to Initial Access are handled proactively    |
| Automation & Efficacy | Triage, enrichment, and verdict handling are streamlined and scalable |

## 🧪 Validation Tips

To confirm the configuration is working as expected:

- Trigger an alert mapped to `TA0001 - Initial Access` tied to a known user/IP
- Confirm enrichment pulls identity and IP context into the case
- Review verdict and ensure appropriate playbook actions (block, revoke, or close) are taken
- Track outcome metrics in the **SOC Framework Value Dashboard**

## 🧩 Dependencies

- SOC Optimization Framework (for auto-triage, scoring, and layout handling)
- Identity provider integrations (e.g., Okta, Azure AD) configured and ingesting events
- Alerts must include `username`, `source IP`, and `mitre_tactic_id` for full workflow execution

---

For enhancement suggestions or integration support, contact your Palo Alto Networks Field team or the SOC Framework maintainers.
