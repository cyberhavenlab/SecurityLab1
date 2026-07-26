# AWS Sandbox Setup

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

This note captures the account setup, cost controls, and least-privilege access needed for the AWS lab environment.

## Pre-flight checklist

- Create a dedicated AWS sandbox account.
- Use a separate lab email or alias for recovery and billing.
- Enable MFA on the root user immediately.
- Set a billing alarm / AWS Budget at $5.
- Create a read-only IAM user for scripting.
- Store credentials in a password manager.
- Use a Mac or macOS VM for local testing if available.
- Create a Python 3.11+ virtual environment with boto3 and requests.
- Keep all deliverables in the notes repository.

## AWS account setup

1. Sign in to the AWS console as root.
2. Enable MFA on the root user.
3. Turn on billing access for IAM if needed.
4. Create a budget with a $5 alert threshold.
5. Confirm billing notifications go to the lab email.
6. Create a read-only IAM user for scripts and inventory work.
7. Attach the AWS managed policy `ReadOnlyAccess`.
8. Create an access key for CLI / boto3 use.
9. Store the access key and secret securely.
10. Test the credentials with a harmless read-only AWS CLI command.

## IAM user design

- Root user: account setup only.
- Read-only user: scripting, inventory, and audit-style work.
- Admin user later: changes, provisioning, and destructive work.

## Mac / Python environment

1. Confirm Python 3 is installed.
2. Create a virtual environment.
3. Activate the environment.
4. Install `boto3` and `requests`.
5. Install the AWS CLI if needed.
6. Configure the CLI with the read-only IAM user.
7. Confirm the CLI returns the expected account identity.

## Notes and decisions

- Keep the sandbox separate from personal accounts.
- Prefer least privilege for all access.
- Use `json` as the default AWS CLI output format.
- Keep all lab artifacts in the notes repo.

## Self-check

1. Why is root MFA the first AWS security step?
   - Because root has full account power and should be protected before anything else.

2. Why use a read-only IAM user for scripting?
   - To reduce risk while still allowing inventory and verification tasks.

3. How do I know the billing alert works?
   - By confirming the budget is created and the notification target is correct.