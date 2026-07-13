# ADR-001 – SIEM Platform Selection

## Status

Accepted

---

## Context

This project requires a Security Information and Event Management (SIEM) platform capable of collecting security telemetry, supporting search and analysis, enabling dashboard creation, and demonstrating enterprise security monitoring concepts in a local lab environment.

The selected platform should support interview preparation while minimizing ongoing operational costs.

---

## Decision

Splunk Enterprise has been selected as the SIEM platform for this project.

---

## Decision Drivers

- Industry recognition
- Interview relevance
- Enterprise adoption
- Local deployment capability
- Strong documentation
- SPL search language
- Dashboard capabilities
- Security monitoring features

---

## Alternatives Considered

### Splunk Enterprise

Pros

- Industry standard
- Extensive documentation
- Strong search capabilities
- Excellent dashboards
- Valuable interview experience

Cons

- Commercial licensing
- Free license ingestion limits
- Vendor-specific language

---

### Wazuh

Pros

- Open source
- No licensing cost
- Excellent detection capabilities
- MITRE ATT&CK integration

Cons

- Less market recognition
- Smaller enterprise footprint

---

### Elastic Security

Pros

- Flexible
- Powerful search
- Strong visualization

Cons

- Greater configuration complexity
- Less common in many enterprise SIEM deployments

---

### Microsoft Sentinel

Pros

- Cloud native
- Strong Microsoft integration
- Excellent automation

Cons

- Azure dependency
- Cloud costs
- Less suitable for an offline local lab

---

## Consequences

Positive

- Develop hands-on Splunk experience.
- Improve interview readiness.
- Learn enterprise SIEM concepts.
- Build reusable SPL knowledge.

Negative

- Limited by the free license.
- Some enterprise features are unavailable.
- Knowledge is partially vendor specific.

---

## Architecture Lens Evaluation

| Category | Assessment |
|-----------|------------|
| Business Value | High |
| Security | High |
| Cost | Medium |
| Operational Complexity | Medium |
| Scalability | Medium |
| Maintainability | High |
| Vendor Lock-In | Medium |
| Reliability | High |
| Overall Recommendation | Recommended |

Splunk was selected because the primary objective of this project is to develop practical SIEM knowledge that aligns with technologies commonly encountered in enterprise environments. While other platforms may offer lower cost or additional open-source flexibility, interview relevance and market recognition were prioritized for this learning project. This decision reflects the project's goals and constraints rather than suggesting Splunk is universally the best SIEM solution.
