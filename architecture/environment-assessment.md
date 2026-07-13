# Environment Assessment

## Assessment Date

July 12, 2026

## Purpose

This assessment verifies that the local environment has sufficient capacity and compatibility to host a single-instance Splunk Enterprise SIEM laboratory.

## Environment

| Component | Assessment |
|---|---|
| Host platform | Windows 11 with WSL2 |
| Linux distribution | Ubuntu 22.04.5 LTS |
| Architecture | x86_64 |
| Kernel | Microsoft WSL2 Linux 6.6.87.2 |
| Logical processors | 16 |
| Available memory | Approximately 29 GiB |
| Swap | 8 GiB |
| WSL filesystem capacity | Approximately 1 TiB |
| WSL filesystem available | Approximately 950 GiB |
| Docker | Available |
| Docker Compose | Available |

## Capacity Assessment

The environment provides sufficient CPU, memory, and storage for a local, single-instance Splunk Enterprise deployment and a controlled volume of Windows and Linux security telemetry.

The available resources exceed the anticipated needs of the initial laboratory. Resource consumption will still be monitored because indexed security data can grow significantly over time.

## Deployment Decision

Splunk Enterprise will initially be installed directly in Ubuntu under WSL2 rather than deployed as a Docker container.

This approach was selected because it:

- Exposes Splunk's native directory and configuration structure.
- Provides direct experience with Splunk command-line administration.
- Simplifies access to local Linux logs.
- Avoids coupling the SIEM lab to the Docker environment used by other projects.
- Supports easier troubleshooting during the learning phases.

## Limitations and Risks

- WSL2 is not representative of a production Linux server.
- The lab is a single-instance deployment without high availability.
- Host resource contention may occur when other local projects are running.
- Large ingestion volumes could consume substantial storage.
- Windows telemetry will require a separate forwarding mechanism.
- The environment must not ingest sensitive or production data.

## Conclusion

The environment is suitable for the planned local Splunk SIEM Detection Lab.

**Assessment result: Approved to proceed**
