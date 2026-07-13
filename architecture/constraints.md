# Constraints

## Purpose

Every solution is influenced by technical, financial, operational, and business constraints. Identifying these constraints early helps ensure architectural decisions are practical, supportable, and aligned with project objectives.

---

## Budget Constraints

- The solution should minimize implementation costs.
- The project should leverage free or community editions where practical.
- Ongoing cloud costs should be avoided unless they provide significant architectural value.

---

## Infrastructure Constraints

- The solution will be deployed on local hardware.
- The environment should coexist with other development projects.
- Hardware resources (CPU, memory, and storage) are limited compared to enterprise environments.

---

## Technology Constraints

- Splunk Enterprise will be used as the primary SIEM platform.
- Windows and Ubuntu Linux will serve as the initial monitored systems.
- Additional integrations may be added in future phases.

---

## Operational Constraints

- The environment should be easy to rebuild.
- Documentation should accompany every major implementation step.
- Changes should be version controlled using Git.

---

## Learning Constraints

- The project is intended to develop architectural understanding rather than product administration expertise.
- The focus is on design decisions, security monitoring concepts, and detection engineering.

---

## Assumptions

The project assumes:

- A single-user lab environment.
- No production data.
- Simulated attack scenarios.
- Limited daily log volume.
