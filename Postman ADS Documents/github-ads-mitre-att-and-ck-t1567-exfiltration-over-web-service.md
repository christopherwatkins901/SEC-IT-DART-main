---
description: This is for all Github ADS Wiki's
---

# Github ADS-MITRE ATT\&CK: T1567 - Exfiltration Over Web Service

## Alerting and Detection Strategy (ADS) Template

### Goal

The goal is to detect potentially unauthorized or suspicious mass downloads of GitHub repositories, which could be indicative of data exfiltration or reconnaissance activities.

### Categorization

* MITRE ATT\&CK: [T1567 - Exfiltration Over Web Service](https://attack.mitre.org/techniques/T1567/)

### Strategy Abstract

The alert leverages Scanner.dev to aggregate GitHub audit logs, focusing on various types of download-related actions like ZIP downloads, Git clones, API-based downloads, release downloads, package downloads, and forks. The alert groups these activities by actor, repository name, IP address, and user agent to provide a comprehensive view of the activities.

### Technical Context

The detection query used in Scanner.dev is as follows:

```plaintext
(
  (%ingest.match_rule_name:"github" and action:"repo.download_zip") or
  (%ingest.match_rule_name:"github" and action:"git_clone") or
  (%ingest.match_rule_name:"github" and action:"api_download") or
  (%ingest.match_rule_name:"github" and action:"release_download") or
  (%ingest.match_rule_name:"github" and action:"package_download") or
  (%ingest.match_rule_name:"github" and action:"fork")
) | groupbycount actor, repo_name, actor_ip, user_agent
```

### Blind Spots and Assumptions

* Assumes that GitHub audit logs are being ingested into Scanner.dev.
* Does not account for legitimate use-cases where multiple repositories may be downloaded by a single actor for valid reasons.

### False Positives

* Development or CI/CD pipelines that clone or download multiple repositories.
* Legitimate administrative actions.

### Validation

To validate, simulate the download or clone of more than 3 GitHub repositories within a 5-minute window by a single actor. Ensure that the activities are logged and ingested into Scanner.dev, and confirm that the alert is triggered.

### Priority

* High: If more than 3 repositories are downloaded within a 5-minute window by a single actor.

### Response

1. Investigate the actor's identity and intent.
2. Review the repositories involved for sensitive data.
3. Check the originating IP address for other associated activities.
4. Validate the user agent for any anomalies.
5. If malicious intent is confirmed, revoke the actor's access and initiate incident response procedures.

### Additional Resources

* [MITRE ATT\&CK Technique T1567](https://attack.mitre.org/techniques/T1567/)
* [GitHub Audit Log Documentation](https://docs.github.com/en/organizations/keeping-your-organization-secure/reviewing-the-audit-log-for-your-organization)
* [Scanner.dev Documentation](https://docs.scanner.dev/scanner/using-scanner/query-syntax)
