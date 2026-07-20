# 20. Authentication Correlation and Investigation

## Purpose
The final phase of the Splunk SIEM Detection Lab demonstrates how multiple security events can be correlated into a single investigative record. Rather than analyzing individual authentication events independently, security analysts often need to understand the complete sequence of activity occurring within a defined period. Splunk's transaction command allows related authentication events to be grouped together, providing greater context for security investigations.

## Business Perspective
Organizations rarely investigate isolated authentication failures without additional context. Security teams need to determine whether repeated failed authentication attempts were followed by successful access, whether activity originated from the same system, and whether the sequence represents legitimate user behavior or a potential compromise. Correlation reduces investigation time and improves analyst decision making by presenting related events together.

## What Was Implemented
Authentication correlation was implemented using Linux authentication events previously collected into the security_lab index. Failed and successful SSH authentication events occurring on the same host within a five-minute period were combined into a single transaction. The resulting investigation view provides analysts with the complete authentication sequence rather than requiring manual reconstruction across multiple log entries.

## Detection Logic
The correlation search retrieves both failed and successful SSH authentication events from the Linux authentication logs. Events are grouped by host using the transaction command with a maximum correlation window of five minutes. Transactions containing more than one authentication event are returned for analyst review along with timestamps, event counts, transaction duration, and the original authentication log entries.

## SPL Search

    index=security_lab sourcetype=linux_secure earliest=-15m
    ("Failed password" OR "Accepted password")
    | transaction host maxspan=5m
    | search eventcount>1
    | table _time host eventcount duration _raw

## Security Value
Authentication correlation enables analysts to identify suspicious authentication sequences that may otherwise appear unrelated when viewed individually. Multiple failed logins followed by successful authentication may indicate password guessing, credential stuffing, brute force activity, or compromised credentials. Presenting the entire sequence improves analyst efficiency and reduces investigation time.

## Architecture Considerations
The transaction command provides valuable investigative context by grouping related events into logical sessions. While effective for smaller datasets and investigations, transaction operations consume more memory than statistical aggregation commands. Large production environments frequently implement correlation using stats, streamstats, or accelerated data models to improve scalability. The transaction approach remains appropriate for learning environments and investigative demonstrations because it clearly illustrates event relationships.

## Operational Considerations
Correlation windows should be selected carefully to balance detection accuracy against unnecessary grouping of unrelated events. Short correlation periods may fail to associate legitimate attack sequences, while excessive time windows may combine unrelated authentication events. Production implementations often tune these values based on authentication patterns, user behavior, and organizational risk tolerance.

## Results
The completed correlation successfully identified multiple authentication events occurring on the same Linux host within the configured investigation window. The transaction output displayed the host name, total correlated events, transaction duration, and complete authentication sequence, demonstrating successful event correlation across multiple SSH authentication attempts.

## Tradeoffs
The transaction command offers excellent investigative visibility but requires additional system resources compared to aggregation commands. It is best suited for forensic investigations, proof-of-concept demonstrations, and environments with moderate event volumes. High-volume enterprise deployments generally favor more scalable correlation techniques while preserving equivalent detection capability.

## Lessons Learned
Building a detection pipeline extends beyond collecting log data. Effective detection engineering requires understanding authentication behavior, creating repeatable searches, tuning alert thresholds, validating detections using controlled events, and correlating related activity into meaningful investigations. The project demonstrates the complete lifecycle from data ingestion through investigation-ready detection.

## Interview Questions
Why would you use transaction instead of stats for authentication correlation?
How would you tune the correlation window in a production environment?
What limitations exist when using transaction against high-volume log sources?
How would you detect successful logins following repeated authentication failures?
How would this detection integrate into an enterprise SOC workflow?

## Architect's Perspective
Security architecture focuses on transforming large volumes of telemetry into actionable intelligence that supports business risk reduction. Correlation represents the transition from simple log collection to meaningful detection engineering by combining related events into investigations that security analysts can quickly interpret. This project demonstrates the architectural principles of centralized logging, detection engineering, alerting, correlation, and investigation within a modern SIEM platform.
