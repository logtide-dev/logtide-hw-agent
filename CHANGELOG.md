# Changelog

All notable changes to the LogTide hardware agent are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0]

First release, for LogTide 1.7.0.

### Added

- Collectors for SMART (HDD, SSD and NVMe through smartctl), ECC memory errors per controller and DIMM (EDAC), temperatures, fans and voltages (hwmon and IPMI sensors), power supply state and redundancy (IPMI), CPU thermal throttling, physical NIC counters, host information and virtualization detection.
- Hardware events from the kernel log (`/dev/kmsg`) and the BMC event log (SEL), sent as logs with service `hardware`.
- OTLP JSON metrics (`hw.*`) to `/v1/otlp/metrics` with the project API key; retries with backoff on 408, 429 and 5xx.
- Time budgets for every external command, SMART in its own thread, abandoned probes for disks hung in D-state.
- Clock skew warning based on the server `Date` header.
- Docker image (`logtide/hw-agent`), systemd unit, `--once` and dry run mode.
