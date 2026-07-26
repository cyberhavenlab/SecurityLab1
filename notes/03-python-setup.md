# Python Setup

Date:
Objective:
Time spent:
Links:
Decisions:
Open questions:

## Environment check

- Confirm whether a Mac is available.
- If not, note that macOS-specific labs will be adapted to read/write only.
- Verify Python 3.11+ is installed.
- Verify `pip` is available.
- Verify the AWS CLI is installed.

## Virtual environment setup

1. Create a project virtual environment.
2. Activate the environment.
3. Upgrade `pip`.
4. Install `boto3`.
5. Install `requests`.

Example commands:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install boto3 requests
```

## AWS CLI setup

1. Run `aws configure`.
2. Enter the read-only IAM user access key.
3. Enter the read-only IAM user secret key.
4. Set the default region, such as `us-east-1`.
5. Set the output format to `json`.

Example:

```bash
aws configure
```

## Validation

- Check `python --version`.
- Check `pip --version`.
- Check `aws --version`.
- Confirm the virtual environment is active.
- Confirm AWS CLI uses the read-only identity.

## Notes and decisions

- Use `json` as the AWS CLI output format.
- Keep scripts read-only until a later admin user is introduced.
- Use the notes repo as the single source of truth for lab artifacts.

## Self-check

1. Why create a virtual environment?
   - To isolate lab dependencies from the system Python install.

2. Why use `boto3` and `requests`?
   - `boto3` for AWS API work and `requests` for general HTTP/API calls.

3. Why use a read-only AWS identity here?
   - To prevent accidental changes while testing and inventorying.