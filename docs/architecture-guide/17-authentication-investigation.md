# 17. Authentication Investigation

## Purpose

This document explains how authentication events are investigated within a Security Information and Event Management (SIEM) platform. Authentication activity represents one of the highest-value telemetry sources because nearly every security incident involves the use or misuse of identities.

This guide demonstrates how authentication events collected from Linux systems can be analyzed using Splunk to identify suspicious behavior, support incident investigations, and develop future security detections.

## Business Perspective

Identity has become the primary security perimeter for modern organizations. As businesses adopt cloud services, remote work, and zero trust architectures, authentication events provide critical visibility into user activity and potential security threats.

Monitoring authentication events enables organizations to:

* Detect unauthorized access attempts
* Identify compromised accounts
* Reduce incident response time
* Support compliance requirements
* Improve audit readiness
* Protect privileged accounts
* Validate security controls
* Detect insider threats

Authentication telemetry is valuable because it often provides the earliest indication of malicious activity.

## Why Authentication Events Matter

Nearly every successful attack begins with an attempt to obtain or abuse credentials.

Authentication logs provide evidence of activities such as:

* Successful logins
* Failed logins
* Invalid usernames
* Privilege escalation
* Service account usage
* Remote access
* Administrative actions

Analyzing these events enables analysts to identify abnormal behavior before an attacker achieves their objectives.

## Common Threat Scenarios

Authentication monitoring supports the detection of numerous attack techniques.

Examples include:

* Brute-force attacks
* Password spraying
* Credential stuffing
* Stolen credentials
* Privilege escalation
* Lateral movement
* Unauthorized administrative access
* Suspicious remote logins
* Service account abuse

Many of these techniques align with the MITRE ATT&CK framework and form the basis for production detection rules.

## Current Lab Environment

The current laboratory environment consists of:

* Splunk Enterprise
* Dedicated security index named `security_lab`
* Linux authentication logs
* Source: `/var/log/auth.log`
* Sourcetype: `linux_secure`

The searches contained within this document use this environment as the investigative data source.

## Investigation Methodology

Authentication investigations should follow a structured process.

### Identify the Question

Determine what you are attempting to discover.

Examples include:

* Has someone attempted to access the system?
* Were there repeated authentication failures?
* Was privileged access used?
* Did authentication activity occur outside expected hours?

### Locate Relevant Events

Identify the appropriate index, sourcetype, host, and time range.

### Review Raw Events

Validate that the returned events accurately represent the activity being investigated.

### Identify Patterns

Look for repeated activity, unusual behavior, or deviations from established baselines.

### Develop Findings

Determine whether the observed activity is expected, suspicious, or malicious.

### Document Conclusions

Record the investigation, supporting evidence, assumptions, and recommended actions.

## Retrieve All Authentication Events

Retrieve all Linux authentication events.

```spl
index=security_lab sourcetype=linux_secure
```

This search establishes the initial investigative dataset.

## Display Key Metadata

Display the most important event metadata.

```spl
index=security_lab sourcetype=linux_secure
| table _time host source sourcetype _raw
```

This confirms event quality and validates successful parsing.

## Failed Authentication Attempts

Search for failed password attempts.

```spl
index=security_lab sourcetype=linux_secure "Failed password"
```

Repeated authentication failures may indicate:

* User error
* Password guessing
* Brute-force attacks
* Automated attack tools

Investigators should consider the frequency, timing, originating IP address, and targeted accounts.

## Successful Authentication

Retrieve successful login events.

```spl
index=security_lab sourcetype=linux_secure "Accepted password"
```

Successful authentication should be reviewed alongside failed attempts to determine whether an attacker eventually gained access.

## Invalid User Activity

Retrieve invalid username attempts.

```spl
index=security_lab sourcetype=linux_secure "Invalid user"
```

Attempts against nonexistent accounts frequently indicate automated scanning or password guessing.

## Root Login Activity

Search for root authentication activity.

```spl
index=security_lab sourcetype=linux_secure root
```

Privileged account activity should receive additional scrutiny because compromise of privileged credentials significantly increases organizational risk.

## Sudo Activity

Retrieve sudo events.

```spl
index=security_lab sourcetype=linux_secure sudo
```

Sudo activity may indicate:

* Administrative maintenance
* Privilege escalation
* Unauthorized administrative actions

Context is required to determine whether the activity is expected.

## Authentication Activity Over Time

Visualize authentication volume.

```spl
index=security_lab sourcetype=linux_secure
| timechart count
```

Time-based visualizations help identify spikes, anomalies, and periods of unusual activity.

## Event Counts by Host

Determine which hosts generated authentication activity.

```spl
index=security_lab sourcetype=linux_secure
| stats count by host
| sort - count
```

This identifies systems generating the highest authentication volume.

## Top Authentication Sources

Identify frequently occurring sources.

```spl
index=security_lab sourcetype=linux_secure
| top source
```

Understanding event distribution supports operational awareness and capacity planning.

## Reviewing Raw Events

Investigators should always review representative raw events before relying on extracted fields.

Raw events provide valuable context that may not appear within summarized reports.

Examples include:

* Process identifiers
* Original log formatting
* Service names
* Authentication methods
* Error messages

Validation of raw events improves confidence in search results and detection logic.

## Investigation Questions

During an authentication investigation, analysts should consider:

* Who authenticated?
* Which account was used?
* Which system generated the event?
* Was authentication successful?
* Were there repeated failures?
* Was privileged access involved?
* Did activity occur during expected hours?
* Was the originating system expected?
* Does the behavior differ from normal activity?

These questions help determine whether additional investigation is required.

## Detection Opportunities

Authentication events support numerous future detections.

Examples include:

* Multiple failed logins within a short period
* Excessive authentication failures
* Successful login following repeated failures
* Privileged login outside business hours
* Authentication from unusual hosts
* Authentication from unexpected locations
* Excessive sudo activity
* Service account misuse

These detections will be developed in later phases of the project.

## MITRE ATT&CK Alignment

Authentication monitoring supports detection of techniques including:

* Valid Accounts
* Brute Force
* Password Spraying
* Credential Access
* Privilege Escalation
* Lateral Movement

Mapping detections to ATT&CK improves reporting, threat coverage analysis, and security program maturity.

## Security Considerations

Authentication data contains sensitive information.

Organizations should protect:

* Usernames
* Hostnames
* Administrative activity
* Privileged accounts
* Authentication history
* Access patterns

Access to authentication data should follow least-privilege principles.

## Operational Considerations

Operational authentication monitoring requires:

* Accurate timestamps
* Reliable log collection
* Consistent parsing
* Appropriate retention
* Alert tuning
* Regular review of detection logic
* Investigation procedures
* Clear ownership

Authentication monitoring should be integrated into daily security operations rather than performed only after incidents occur.

## Architecture Considerations

Security architects should evaluate:

* Authentication coverage
* Data quality
* Time synchronization
* Parsing accuracy
* Field extraction
* Detection fidelity
* Search performance
* Storage requirements
* Retention policies
* Scalability

High-quality authentication telemetry enables reliable investigations and stronger detections.

## Tradeoffs

Collecting excessive authentication events increases storage and processing requirements.

Collecting insufficient authentication telemetry creates investigative blind spots.

Architects should balance:

* Visibility
* Performance
* Cost
* Retention
* Detection quality
* Operational complexity

The objective is to maximize security value while maintaining an efficient and scalable architecture.

## Best Practices

* Monitor all authentication activity.
* Validate timestamps during ingestion.
* Review raw events before creating detections.
* Monitor privileged accounts separately.
* Investigate repeated failures.
* Correlate successful and failed logins.
* Establish behavioral baselines.
* Continuously tune authentication detections.
* Document investigative procedures.
* Review authentication coverage regularly.

## Interview Questions

### Why are authentication logs considered high-value telemetry?

Authentication events provide visibility into identity usage and often represent the earliest indicators of compromise.

### Why investigate both failed and successful logins?

Repeated failures followed by a successful login may indicate that an attacker successfully guessed or obtained valid credentials.

### Why should privileged authentication receive additional attention?

Compromise of privileged accounts significantly increases organizational risk because those accounts provide elevated access to critical systems.

### Why review raw events?

Raw events validate parsing, provide additional investigative context, and ensure that detection logic is based on accurate data.

### How do authentication investigations support detection engineering?

Investigations reveal patterns of malicious behavior that can later be automated through alerts, correlation searches, and detection rules.

## Lessons Learned

Authentication events provide some of the most valuable telemetry within a SIEM.

Successful investigations depend upon high-quality timestamps, reliable parsing, accurate field extraction, and disciplined analytical processes.

Authentication monitoring forms the foundation for future dashboards, alerts, detections, and threat hunting activities.

## Architect's Perspective

Security architects should view authentication telemetry as a strategic security capability rather than simply another log source.

Identity remains one of the most frequently targeted attack surfaces, making authentication monitoring essential for reducing organizational risk.

Architectural decisions regarding data collection, parsing, retention, search performance, and detection quality directly influence the organization's ability to identify compromised accounts, investigate incidents, and respond effectively.

The value of authentication monitoring is measured not by the number of events collected, but by the organization's ability to rapidly distinguish legitimate activity from malicious behavior and take appropriate action.

## Key Takeaways

* Authentication events are among the highest-value security telemetry sources.
* Identity-based attacks often begin with authentication activity.
* Structured investigations improve consistency and reduce response time.
* Authentication searches support reports, dashboards, alerts, and detections.
* High-quality telemetry enables reliable investigations.
* Authentication monitoring should be continuously refined as new threats emerge.
* Effective security architecture prioritizes detection quality over event volume.
