# Risk Register — AWS Cloud Security Risk Assessment (Piedmont Family Clinic)

Assessment date: October 13, 2026 · Environment: AWS, us-east-1 · Baseline CSPM score: **30% (18 passed / 42 failed; 77 findings total)**

**Scoring:** Likelihood (L) and Impact (I) rated 1–5. Risk = L × I. High = 15–25, Medium = 8–14, Low = 1–7.

## Findings

| ID | Asset | Finding | L | I | Score | NIST 800-53 | Treatment |
| --- | --- | --- | --- | --- | --- | --- | --- |
| R-01 | S3 bucket | Bucket policy allows anonymous `s3:GetObject` on patient exports | 4 | 5 | 20 High | AC-3, AC-21 | Mitigate |
| R-02 | EC2 / SG | SSH and RDP open to 0.0.0.0/0 | 5 | 4 | 20 High | SC-7, AC-17 | Mitigate |
| R-03 | IAM | `labadmin` has AdministratorAccess attached directly | 4 | 5 | 20 High | AC-6, AC-2 | Mitigate |
| R-04 | IAM | `labadmin` has no MFA | 4 | 4 | 16 High | IA-2 | Mitigate |
| R-05 | Account | CloudTrail not enabled; no audit trail | 4 | 3 | 12 Medium | AU-2, AU-6, AU-12 | Mitigate |
| R-06 | S3 bucket | No customer-managed KMS key (SSE-S3 only, so no key rotation control or access auditing); bucket access logging disabled | 3 | 3 | 9 Medium | SC-28, AU-2 | Mitigate |
| R-07 | IAM | Long-lived static access key instead of roles | 3 | 3 | 9 Medium | IA-5, AC-6 | Mitigate |
| R-08 | IAM root user | No hardware MFA on root (virtual MFA only) | 2 | 5 | 10 Medium | IA-2 | Accept for lab; hardware key in prod |
| R-09 | EC2 / VPC | Default security group allows inbound and outbound traffic | 3 | 3 | 9 Medium | SC-7 | Mitigate |
| R-10 | EBS | Account-level public access for EBS snapshots not blocked | 2 | 3 | 6 Low | AC-3 | Mitigate |

## Security Hub CSPM validation

The live assessment scored the environment at **30% (18 controls passed, 42 failed; 77 findings total)** — the before-remediation baseline. Every planted finding was independently confirmed by CSPM:

- **R-01** — "S3 general purpose buckets should block public read access" (Critical)
- **R-02** — security-group ingress and public-IPv4 controls (High)
- **R-04** — "MFA should be enabled for all IAM users"
- **R-05** — CloudTrail multi-Region trail control (High)

Three further findings the tool surfaced and worth keeping are recorded above as **R-08 to R-10**. The remaining findings — Amazon Inspector and GuardDuty "enable this service" checks, and SSM document public sharing — were triaged as **out of scope** (services not in use or deliberately not enabled) and noted rather than remediated. That triage — distilling 77 raw findings down to roughly ten that matter — is the core of the assessment.

## Remediation record

Of the ten findings carried forward, **seven were remediated and three accepted** with documented justification. Each fix was verified at the resource level in the console; the post-remediation CSPM score is captured separately once Security Hub finishes re-evaluating (S3, security-group, and VPC default-SG controls cleared within the hour; CloudTrail on the next scheduled pass).

| ID | Status | Remediation and after-state |
| --- | --- | --- |
| R-01 | Remediated | Re-enabled Block Public Access (all four) and deleted the public bucket policy. CSPM control dropped to Informational; the object URL now returns AccessDenied. |
| R-02 | Remediated | Removed 0.0.0.0/0 ingress on ports 22 and 3389; inbound rules now empty. |
| R-03 | Remediated | Detached AdministratorAccess and attached ReadOnlyAccess (least privilege). |
| R-04 | Remediated | MFA not applicable (labadmin has no console access); least privilege enforced. MFA required if console access is later granted. |
| R-05 | Remediated | Created multi-Region CloudTrail trail with management events and log file validation; Logging: On. |
| R-06 | Accepted | S3 applies SSE-S3 by default; residual gap is the absence of a customer-managed KMS key. CMK recommended in production. |
| R-07 | Remediated | Deleted the static access key on labadmin. |
| R-08 | Accepted | Root uses virtual MFA; hardware MFA key not available for the lab. Required in production. |
| R-09 | Remediated | Removed all inbound and outbound rules from the default VPC security group. |
| R-10 | Accepted | No EBS snapshots exist, so no exposure; enable account-level block-public-access in production. |

## Result

| | Before | After |
| --- | --- | --- |
| CSPM score | 30% | _pending re-evaluation_ |
| Public data exposure | Yes | Closed |
| Audit logging | None | Multi-Region CloudTrail |
| Over-privileged IAM user | AdministratorAccess | ReadOnlyAccess |

A raw CSPM score treats accepted risks as failures, so the gap between the final score and 100% is accounted for in this register and the POA&M rather than being an open exposure.
