# Changelog

All notable changes to the LogTide hardware agent are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0]

### Added

- `hw.host.info` carries the operating system from `os-release`: `os.name`, `os.version` and `os.description` (for example `Debian GNU/Linux 12 (bookworm)`). LogTide 1.8 shows it on the host page instead of the bare kernel version.
- `system.cpu.logical.count` (unit `{cpu}`): online logical CPUs from `/sys/devices/system/cpu/online`, falling back to `/proc/cpuinfo`. Sent with the host information, so it does not depend on the `system` collector.

## [1.1.0]

### Added

- `system` collector (enabled by default, switch it off by leaving it out of `LOGTIDE_HW_COLLECTORS`): host resource metrics with OpenTelemetry names read from `/proc` and `statvfs`. CPU utilization per state and total, load average, memory and swap usage and utilization, filesystem usage and utilization for real filesystems, disk and network throughput as per-second rates, and uptime. See the README for the full list.
- `system` appears in `hw.agent.collector.status` like the other collectors.

## [1.0.0]

First release, for LogTide 1.7.0.

### Added

- Collectors for SMART (HDD, SSD and NVMe through smartctl), ECC memory errors per controller and DIMM (EDAC), temperatures, fans and voltages (hwmon and IPMI sensors), power supply state and redundancy (IPMI), CPU thermal throttling, physical NIC counters, host information and virtualization detection.
- Hardware events from the kernel log (`/dev/kmsg`) and the BMC event log (SEL), sent as logs with service `hardware`.
- OTLP JSON metrics (`hw.*`) to `/v1/otlp/metrics` with the project API key; retries with backoff on 408, 429 and 5xx.
- Time budgets for every external command, SMART in its own thread, abandoned probes for disks hung in D-state.
- Clock skew warning based on the server `Date` header.
- Docker image (`logtide/hw-agent`), systemd unit, `--once` and dry run mode.
