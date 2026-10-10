# doctor-labs

Offline security **doctors** for embedded and hardware targets. Each tool answers one
question about one kind of artifact, runs without network or telemetry, points every
finding at evidence, and speaks one shared machine contract (`doctor/1`) so agents and
CI can read them all the same way.

| Tool | What it examines | Language |
|------|------------------|----------|
| [**lua-doctor**](https://github.com/doctor-labs/lua-doctor) | RCE and backdoors in embedded Lua (LuCI / OpenWrt / CGI) | Lua |
| [**pcap-doctor**](https://github.com/doctor-labs/pcap-doctor) | `.pcap`/`.pcapng` captures — who talked to whom, what crypto, what leaks | Python + tshark |
| [**android-doctor**](https://github.com/doctor-labs/android-doctor) | Android OTA / firmware images — debuggable, rooted or unsigned builds | Rust |
| [**sim-doctor**](https://github.com/doctor-labs/sim-doctor) | SIM / UICC / eUICC cards over PC/SC | Rust |
| [**ble-doctor**](https://github.com/doctor-labs/ble-doctor) | Bluetooth Low Energy devices and captures | Rust |

## The shared contract (`doctor/1`)

Every tool's `--json` emits the same envelope — `{schema, tool, version, exit_code, score, findings, data}` —
with a 0–100 health score (`good` / `needs work` / `critical`), stable finding fingerprints,
SARIF output, baseline diffing, and an MCP server that returns the same JSON as the CLI.
Exit codes are uniform: `0` clean, `1` findings, `2` error, `3` new-vs-baseline.

Defensive / CTF / own-gear use. No telemetry. Secrets found are reported, never repeated.
