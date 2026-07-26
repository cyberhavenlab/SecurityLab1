# Day 1 Self-Check

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

## Questions

1. Where does my work end and the Huntress SOC’s work begin?
   - My work is onboarding sources, verifying data flow, checking normalization, tuning noise, and monitoring health. The Huntress SOC handles continuous monitoring, triage, and escalation.

2. What is the difference between a false positive and a benign true positive, and why does it matter for metrics?
   - A false positive is an alert that should not have fired. A benign true positive is a real event that was authorized. They must be tracked separately so metrics and tuning decisions stay accurate.

3. How would I detect that a log source stopped sending data?
   - Use a last-event timestamp, ingestion lag checks, and an alert for missing data over a defined time window.

## Notes

- Ingestion health is a security control, not just an operations task.
- Every tuning decision should have a written reason.
- A read-only user is the safest default for scripting and inventory work.