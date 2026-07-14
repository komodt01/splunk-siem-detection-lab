# 14. Security Operations Lifecycle

## Purpose

This document explains the end-to-end Security Operations (SecOps) lifecycle and the role a Security Information and Event Management (SIEM) platform plays within it. While Splunk provides powerful capabilities for collecting, analyzing, and detecting security events, it represents only one component of a broader security operations ecosystem.

Understanding this lifecycle enables security architects to design solutions that improve visibility, reduce response times, and continuously strengthen an organization's security posture.

## Business Perspective

Security operations is a continuous process rather than a single technology or product. Organizations must collect security telemetry, detect malicious activity, investigate incidents, respond appropriately, and improve their defenses based on lessons learned.

A mature Security Operations Center (SOC) relies on repeatable processes supported by people, technology, and governance. The SIEM acts as the central analytical platform that brings these elements together.

The objective is not simply to collect logs—it is to reduce organizational risk by transforming security data into actionable intelligence.

## Security Operations Lifecycle

The lifecycle can be represented as follows:

```
+----------------------+
|    Data Sources      |
+----------+-----------+
           |
           v
+----------------------+
|     Collection       |
+----------+-----------+
           |
           v
+----------------------+
| Parsing &            |
| Normalization        |
+----------+-----------+
           |
           v
+----------------------+
|   Indexing & Storage |
+----------+-----------+
           |
           v
+----------------------+
| Search & Analytics   |
+----------+-----------+
           |
           v
+----------------------+
| Detection & Alerts   |
+----------+-----------+
           |
           v
+----------------------+
| Investigation        |
+----------+-----------+
           |
           v
+----------------------+
| Response             |
+----------+-----------+
           |
           v
+----------------------+
| Continuous           |
| Improvement          |
+----------------------+
```

Each stage builds upon the previous one. Weaknesses introduced early in the process affect every downstream capability.

## Stage 1 – Data Sources

Every investigation begins with security telemetry.

Common data sources include:

- Linux servers
- Windows Event Logs
- Sysmon
- Active Directory
- Microsoft Entra ID
- AWS CloudTrail
- Azure Activity Logs
- Google Cloud Audit Logs
- Firewalls
- VPN appliances
- Endpoint Detection and Response (EDR)
- Web servers
- DNS
- Email security platforms

The quality and relevance of these data sources directly influence detection effectiveness.

## Stage 2 – Collection

Security events must be reliably collected from each source.

Collection methods may include:

- Universal Forwarders
- Syslog
- APIs
- Cloud-native integrations
- Event streaming platforms

Architectural considerations include:

- Reliability
- Encryption in transit
- Bandwidth
- Latency
- High availability
- Data loss prevention

Reliable collection is the foundation of an effective SIEM.

## Stage 3 – Parsing and Normalization

Raw log data is transformed into structured events.

Parsing identifies event boundaries and extracts meaningful fields such as:

- Username
- IP address
- Host
- Process
- Event type
- Timestamp

Normalization allows different technologies to be analyzed consistently.

Without proper parsing, security analytics become significantly less effective.

## Stage 4 – Indexing and Storage

Once events are parsed, they are indexed for efficient searching and long-term retention.

Architectural decisions include:

- Index strategy
- Retention periods
- Storage tiers
- Compression
- Performance optimization

Balancing storage costs with investigative needs is a key architectural responsibility.

## Stage 5 – Search and Analytics

Security analysts search indexed data to answer investigative questions.

Examples include:

- Who logged in?
- From where?
- When?
- Which systems were accessed?
- What happened immediately before and after?

Search capabilities transform stored data into operational intelligence.

## Stage 6 – Detection and Alerting

Rather than relying solely on manual searches, organizations develop detection logic that continuously evaluates incoming events.

Examples include:

- Brute-force attacks
- Privilege escalation
- Suspicious PowerShell activity
- Malware execution
- Impossible travel
- Excessive authentication failures

Alerts notify analysts when predefined conditions are met.

Detection engineering focuses on maximizing fidelity while minimizing false positives.

## Stage 7 – Investigation

Once an alert is generated, analysts determine:

- Is the activity malicious?
- Which assets are affected?
- What is the scope?
- What evidence supports the conclusion?
- How did the attack progress?

Investigations often involve correlating events across multiple systems and time periods.

## Stage 8 – Response

Response actions may include:

- Disabling user accounts
- Blocking IP addresses
- Isolating endpoints
- Updating firewall rules
- Rotating credentials
- Escalating incidents

Many organizations automate portions of the response process using Security Orchestration, Automation, and Response (SOAR) platforms.

## Stage 9 – Continuous Improvement

Every incident provides opportunities to strengthen security.

Organizations should continuously:

- Improve detections
- Tune alert thresholds
- Add new telemetry
- Refine correlation logic
- Enhance dashboards
- Update documentation
- Improve response playbooks

Continuous improvement is what transforms a reactive SOC into a mature security program.

## Architectural Considerations

Security architects should evaluate:

- Scalability
- Data quality
- High availability
- Performance
- Compliance
- Retention requirements
- Operational costs
- Integration complexity
- Detection coverage

Each design decision influences the effectiveness of downstream security operations.

## Common Challenges

Organizations frequently encounter:

- Excessive log volume
- Alert fatigue
- Poor-quality telemetry
- Missing data sources
- Inconsistent parsing
- Limited storage
- Staffing shortages
- Detection gaps

A successful architecture addresses these challenges proactively rather than reacting after incidents occur.

## Security Architect Perspective

A SIEM should not be viewed as the beginning or the end of security operations. It is the analytical engine within a much larger operational process.

Security architects are responsible for designing an ecosystem where data flows reliably from source systems to analysts, enabling accurate detections, efficient investigations, and effective incident response.

The true measure of success is not the number of alerts generated, but the organization's ability to identify, understand, contain, and learn from security events while continuously reducing overall business risk.

## Key Takeaways

- Security operations is a continuous lifecycle.
- Data quality affects every downstream capability.
- SIEM platforms enable centralized analysis but are only one component of the SOC ecosystem.
- Effective detection depends on reliable collection, parsing, and normalization.
- Continuous improvement is essential for maintaining an effective security operations program.
