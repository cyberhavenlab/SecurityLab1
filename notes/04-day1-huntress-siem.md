# Day 1 — Huntress and the SIEM Mental Model

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

Huntress is the center of gravity for this role. The job is not to build a SIEM from scratch, but to make sure the right logs flow in, are parsed correctly, and remain healthy over time.

## Log source onboarding lifecycle

Use this as the repeatable playbook for every source:

1. Identify the source and what security questions it can answer.
2. Choose the integration method: native connector, API pull, HTTP event collector, syslog, or agent.
3. Authenticate with least-privilege, read-only credentials scoped to the needed data.
4. Confirm parsing and field normalization: timestamps, usernames, hostnames, and event types.
5. Validate ingestion with a known test event.
6. Build or enable detections against it.
7. Monitor ingestion health as an ongoing control.

Step 7 is critical. A log source that silently stops is a blind spot that looks like quiet. Ingestion health monitoring is itself a security control.

## Why the data matters

For each source, explicitly name the attacker behavior it would reveal:

- AWS CloudTrail: IAM changes, key creation, unusual API calls, disabled logging.
- M365 and Entra ID: sign-in anomalies, MFA changes, mailbox forwarding rules, OAuth consent grants.
- HubSpot: bulk contact export, permission changes, unusual API access.
- macOS endpoints: process execution, persistence mechanisms, malware detections.
- Mosyle: device compliance drift, profile removal, unenrollment.

This maps directly to MITRE ATT&CK behaviors and makes the inventory useful, not just a list.

## Triage vocabulary

Use three verdicts, not two:

- True positive: real and unauthorized.
- False positive: the detection logic misfired.
- Benign true positive: the event really happened, but it was authorized.

This matters because incident metrics become misleading if benign true positives are counted as attacks. Auditors also care about why alerts were tuned or suppressed.

## Tuning order

When something is noisy or misfiring, tune in this order:

1. Fix the detection logic.
2. Adjust the threshold.
3. Add a scoped exception.
4. Suppress only as a last resort.

Every tuning decision should have a written rationale: what changed, why, who approved it, and when it should be reviewed.

## Self-check

1. Where does my work end and the Huntress SOC’s work begin?
   - My work is onboarding, validation, tuning, and health monitoring. The Huntress SOC handles 24/7 monitoring, triage, and escalation.

2. What is the difference between a false positive and a benign true positive?
   - A false positive is an incorrect alert. A benign true positive is real activity that was authorized.

3. How would I detect that a log source stopped sending data?
   - Use last-seen timestamps, ingestion-lag alerts, and a rule for no events within a defined time window.