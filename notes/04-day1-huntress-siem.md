# Day 1 — Huntress and the SIEM Mental Model

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

## Core idea

Huntress is the center of gravity for this role. The job is not to build a SIEM from scratch, but to make sure the right logs flow in, are parsed correctly, and remain healthy over time.

## Log source onboarding lifecycle

1. Identify the source and the security questions it can answer.
2. Choose the integration method.
3. Authenticate with least privilege.
4. Confirm parsing and normalization.
5. Validate ingestion with a known test event.
6. Build or enable detections.
7. Monitor ingestion health as an ongoing control.

## Triage vocabulary

- True positive: real and unauthorized.
- False positive: the detection logic misfired.
- Benign true positive: the event really happened, but it was authorized.

## Tuning order

1. Fix the detection logic.
2. Adjust the threshold.
3. Add a scoped exception.
4. Suppress only as a last resort.

## Why the data matters

- AWS CloudTrail: IAM changes, key creation, unusual API calls, disabled logging.
- M365 and Entra ID: sign-in anomalies, MFA changes, mailbox rules, OAuth consent grants.
- HubSpot: bulk export, permission changes, unusual API use.
- macOS endpoints: process execution, persistence, malware detections.
- Mosyle: compliance drift, profile removal, unenrollment.

## Self-check

1. Where does my work end and the Huntress SOC’s work begin?
   - My work is source setup, validation, context, and tuning. The SOC handles continuous monitoring, triage, and escalation.

2. What is the difference between a false positive and a benign true positive?
   - A false positive is an incorrect alert. A benign true positive is real activity that was authorized.

3. How would I detect that a log source stopped sending data?
   - Use last-seen timestamps, ingestion-lag monitoring, and no-event alerts over a defined time window.