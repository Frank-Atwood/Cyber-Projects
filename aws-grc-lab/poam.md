# Plan of Action & Milestones (POA&M)

**Assessment:** AWS Cloud Security Risk Assessment — Piedmont Family Clinic

**Prepared by:** Frank Atwood

**Date:** October 13, 2026

A POA&M records findings that were **accepted** rather than remediated during the assessment, along with the justification for accepting the risk, any compensating control already in place, and a scheduled action to close the gap in a production environment.

## Accepted findings

| ID | Weakness | Risk owner | Justification & compensating control | Planned action | Target date |
| --- | --- | --- | --- | --- | --- |
| R-06 | No customer-managed KMS key on the S3 bucket (default SSE-S3 encryption only) | IT Manager | Data is already encrypted at rest with AWS-managed keys (SSE-S3); the residual gap is the lack of key rotation control and access auditing that a customer-managed key provides | Create a customer-managed KMS key and apply it to the bucket; enable key rotation | Q1 2027 |
| R-08 | Root account protected by virtual (app-based) MFA rather than a hardware security key | IT Manager | Virtual MFA is enabled on root; root sign-in is rare and every use is recorded in CloudTrail | Procure a hardware security key (e.g. FIDO2) and register it as the root MFA device | Q1 2027 |
| R-10 | Account-level public access for EBS snapshots is not blocked | IT Manager | No EBS snapshots currently exist in the account, so there is no actual exposure; the finding reflects a default account setting | Enable account-level "block public access for snapshots" as a preventive control | Q4 2026 |

## Review cadence

Accepted risks are not permanent decisions. Each item above is scheduled for review on a quarterly basis, and will be re-evaluated sooner if the environment changes in a way that increases its likelihood or impact — for example, if EBS snapshots are created (R-10), or if patient data volume grows (R-06).

## Out-of-scope findings

Several additional findings raised by the assessment tool were determined to be out of scope for this environment and were neither remediated nor tracked as accepted risks, because they relate to optional services that are not in use:

- Amazon Inspector vulnerability scanning (EC2, ECR, Lambda) — not enabled; no workloads of these types in use
- Amazon GuardDuty threat detection — not enabled for this engagement
- SSM document public sharing — no Systems Manager documents in use

These would be reconsidered if the corresponding services were adopted.
