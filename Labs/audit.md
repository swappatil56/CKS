Enable Audit Logging for giving Audit Policy

Configure the Apiserver for Audit Logging.

The log path should be /etc/kubernetes/audit-logs/audit.log on the host and inside the container.

The existing Audit Policy to use is at /etc/kubernetes/audit-policy/policy.yaml . The path should be the same on the host and inside the container.

Set argument --audit-log-maxsize=7

Set argument --audit-log-maxbackup=2


