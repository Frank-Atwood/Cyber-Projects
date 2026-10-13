# Executive Summary — AWS Cloud Security Risk Assessment

**Prepared for:** Piedmont Family Clinic (clinic director)

**Prepared by:** Frank Atwood

**Date:** October 13, 2026

## Overview

We reviewed the clinic's small cloud environment on Amazon Web Services (AWS) for security weaknesses. The review found several serious problems; including patient export files that anyone on the internet could download without a password. We corrected the most dangerous issues the same day and documented the remainder with a plan to address them.

## What we assessed

The clinic's cloud footprint. Online file storage, a server, and the user accounts that administer them, were measured against two widely used security standards (the AWS Foundational Security Best Practices and the CIS benchmarks) using AWS's built-in assessment tool, Security Hub. The findings are also mapped to the NIST SP 800-53 control framework used across healthcare and government.

## Starting posture: 30%

The automated assessment passed 18 of 60 security checks, a score of 30%, with 42 failing. Not every failure was equally important: after review, about ten findings critically applied to the clinic's environment. The rest were checks for optional services the clinic does not use, and were set aside as out of scope.

## The three most serious risks

1. **Patient data was publicly readable.** A storage location holding patient export files was open to the entire internet with no password required. This was the single highest risk, because it exposed sensitive information directly.
2. **A server was exposed to the internet.** A server was reachable from any address in the world on its remote-access ports, inviting automated attack.
3. **An administrator account was over-powered and unprotected.** A user account held full administrative control it did not need, secured only by a permanent access key and no second-factor (two-step) login.

## What was fixed

All three top risks were corrected:

- The storage location was made private, and the public download path now returns "access denied."
- The server's open internet access was closed.
- The over-powered account was reduced to read-only access, and its permanent access key was removed.
- Account-wide activity logging was switched on, so future actions are recorded and can be reviewed.

In total, seven of the ten relevant findings were fully remediated.

## What remains, and why

Three lower-priority findings were formally accepted rather than fixed, each with a documented reason. For example, the top-level "root" account is protected by an app-based two-step login rather than a physical security key. This is acceptable for this environment (since this is a lab), but worth strengthening in a live clinic. Every accepted item is tracked, with an owner and a target date, in the accompanying Plan of Action & Milestones (POA&M).

## Bottom line and recommendations

The environment moved from an exposed state, with sensitive data publicly readable, to one where the critical exposures are closed and the remaining items are documented and scheduled. Post-remediation security score: ___% (score will be updated once the scan is complete, takes 12-24 hours).

Recommended next steps:

- Adopt a customer-managed encryption key for patient data, with regular rotation.
- Require a hardware security key for two-step login on the root account.
- Schedule quarterly reviews of user access and overall security posture.
