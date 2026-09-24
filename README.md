# Cloud-Threat-Detection (AWS - Splunk)


Phase 0 — Setup & Safety

- Create a dedicated AWS account (isolated from anything real)
- Set a billing alarm and a budget cap
- Confirm Splunk is running and licensed (free tier = 500MB/day, plan around it)
- Create an IAM user/role for Splunk with least-privilege read access to logs

Phase 1 — Log Sources (get data flowing)

- Enable CloudTrail (management + data events)
- Enable VPC Flow Logs
- Turn on GuardDuty
- Enable S3 access logging on a target bucket
- Optionally: IAM Access Analyzer, Config

Phase 2 — Ingestion (AWS → Splunk)

- Install the Splunk Add-on for AWS
- Configure inputs (SQS-based S3 pull is the standard path for CloudTrail/flow logs)
- Verify each source is indexed and fields are parsing correctly (CIM compliance)
- Build a simple "data health" check search

Phase 3 — Attack Simulation

- Install Stratus Red Team
- Run scenarios one at a time, e.g.:
- IAM backdoor user / access key creation
- Privilege escalation
- S3 data exfiltration
- CloudTrail tampering (stop/delete trail)
- Console login from unusual location
- Log the timestamp of each attack so you can confirm detection

Phase 4 — Detection Engineering

- Write an SPL detection for each attack scenario
- Tune out false positives
- Map every detection to a MITRE ATT&CK technique (build a coverage table)
- Save each as a Splunk alert with severity + description

Phase 5 — Dashboards & Investigation

- Build a SOC-style dashboard (alerts over time, top source IPs, attacker activity, MITRE coverage)
- Write an incident report per scenario: what happened, how you detected it, timeline, impact, response

Phase 6 — Package for Recruiters

- GitHub repo with README: architecture diagram, detection→MITRE table, dashboard screenshots, incident reports
- Store detections as code (SPL/Sigma files)
Optional: Terraform to make the whole lab reproducible
3–5 min demo video + LinkedIn post + resume bullet
