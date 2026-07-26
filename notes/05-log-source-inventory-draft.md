# Log Source Inventory Draft

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

| Source | Security questions it answers | Likely integration method | Key event types to capture | What you lose if it breaks | Health-check method |
|---|---|---|---|---|---|
| AWS / CloudTrail | Who changed IAM, created keys, launched resources, or disabled logging? | Native connector or API pull | IAM changes, ConsoleLogin, CreateAccessKey, StopLogging, policy changes | No visibility into cloud control plane activity | Alert if no new events arrive within a set time window |
| HubSpot | Was data exported, were permissions changed, or was API access abused? | API pull | Bulk export, user permission changes, API auth events | Loss of SaaS business-system visibility | Monitor last event time and ingestion lag |
| Canvas | Were accounts changed, content exported, or login anomalies observed? | API pull / connector | Logins, role changes, export activity | Loss of education-platform visibility | Check for recent auth and activity events |
| MacBook endpoints via Mosyle and Bitdefender | Is the endpoint compliant, infected, or tampered with? | Agent / connector | Device compliance, malware detections, profile changes, process activity | Loss of endpoint visibility and device control | Confirm latest check-in and policy sync |
| M365 and Entra ID | Are there sign-in anomalies, MFA changes, mailbox rules, or OAuth abuse? | Native connector / API pull | Sign-in logs, MFA events, mailbox forwarding, consent grants | Loss of identity and email visibility | Alert on missing sign-in and audit events |

## Self-check

1. Where does my work end and the Huntress SOC’s work begin?
   - My work is source setup, verification, normalization, tuning, and health monitoring. The SOC handles 24/7 monitoring, triage, and escalation.

2. What is the difference between a false positive and a benign true positive?
   - A false positive is a bad alert. A benign true positive is real activity that was authorized.

3. How would I detect that a log source stopped sending data?
   - Use last-seen timestamps, ingestion-lag alerts, and a rule for no events within a defined time window.