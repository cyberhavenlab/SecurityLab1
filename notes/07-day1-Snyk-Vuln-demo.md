# Snyk Vulnerable Demo Scan

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

This note records the results of scanning the intentionally vulnerable Python demo in `vuln-python-demo`.

## Scan summary

- Project type: Python 3.7.17
- Imported from: cyberhavenlab@proton.me
- Total issues: 19
- Critical: 1
- High: 7
- Medium: 11
- Low: 0
- Fixable: 19
- Partially fixable: 0
- No supported fix: 0

## Key findings

- `requests@2.19.1` had 5 direct issues.
- `urllib3@1.23` had 15 transitive issues.
- `idna@2.7` had 2 transitive issues.
- The scan showed available fixed versions for all findings.

## Remediation path

- Upgrade `requests` to a supported fixed version.
- Upgrade `urllib3` to a patched version recommended by Snyk.
- Upgrade `idna` to a patched version recommended by Snyk.

## Why this matters

This demo shows how a single outdated dependency can create multiple direct and transitive vulnerabilities. It also shows why dependency hygiene and repeated scanning are part of the lab workflow.

## Self-check

1. What was the main vulnerable dependency?
   - `requests@2.19.1`.

2. Why did one package produce many more issues than expected?
   - Because transitive dependencies like `urllib3` and `idna` also inherited risk.

3. What is the first remediation step?
   - Upgrade to the fixed package versions Snyk recommends.

   # Snyk Fix PR Result

Snyk created and merged a fix pull request for the intentionally vulnerable Python demo in `vuln-python-demo`.

## Result

- `requests` was upgraded from `2.19.1` to `2.20.0`.
- `urllib3` was upgraded from `1.23` to `1.24.2`.
- `idna` was upgraded from `2.7` to `3.7`.
- The pull request was merged into `main`.

## Observations

- Snyk reported 19 total issues before the fix.
- The fix PR reduced the vulnerable dependency set by upgrading the affected package chain.
- Snyk warned about potential compatibility risk from the `idna` major version change, so major upgrades should always be tested.

## Self-check

1. What did Snyk fix?
   - The vulnerable dependency chain in `vuln-python-demo/requirements.txt`.

2. Why did Snyk warn about compatibility?
   - Because `idna 2.7` to `3.7` is a major version change with stricter validation behavior.

3. Why is this useful in the lab?
   - It shows how dependency scanning, fix PRs, and review workflows work together.

   ## Retest result

Snyk retested the vulnerable Python demo after the first fix PR. The project now shows 11 open issues instead of 19.

### Current findings
- `urllib3@2.0.7`: 7 direct issues.
- `requests@2.20.0`: 4 direct issues.
- `idna@3.10`: 1 direct issue.
- Severity mix: 0 Critical, 4 High, 7 Medium.

### Interpretation
The first Snyk fix PR reduced the overall risk, but the dependency chain still contains vulnerable versions. The latest retest shows that additional upgrades are needed, especially for `urllib3`, `requests`, and `idna`.

### Remediation
- Upgrade `idna` to `3.15` or later. [web:194][web:195]
- Continue moving `requests` and `urllib3` to the safest versions supported by the package chain.

After applying the second Snyk fix PR and retesting, the project dropped from 11 issues to 9 issues. The remaining findings are still fixable, but they now center on urllib3@2.0.7, requests@2.31.0, and idna@3.10, with Snyk recommending further upgrades such as urllib3@1.26.19, requests@2.32.2 or 2.32.4, and idna@3.15. This shows that Snyk’s automated fixes are incremental and compatibility-aware, so multiple remediation cycles may be needed before a dependency tree is fully clean.