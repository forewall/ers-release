---
layout: default
title: ERS Agent Downloads
---

# ERS Agent Downloads

Latest version: v1.0.3a (Released on 2025-05-18)

## Download ERS Agent for your platform

### Windows

| Architecture | Download | Checksum | Size | Notes |
|-------------|----------|----------|------|-------|
| Windows x64 | [ers-agent-windows-amd64.exe](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-amd64.exe) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-amd64.exe.sha256) | ~7MB | UPX compressed |
| Windows x86 | [ers-agent-windows-386.exe](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-386.exe) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-386.exe.sha256) | ~6MB | UPX compressed |
| Windows ARM64 | [ers-agent-windows-arm64.exe](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-arm64.exe) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-windows-arm64.exe.sha256) | ~12MB | Standard build |

### Linux

| Architecture | Download | Checksum | Size | Notes |
|-------------|----------|----------|------|-------|
| Linux x64 | [ers-agent-linux-amd64](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-amd64) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-amd64.sha256) | ~7MB | UPX compressed |
| Linux x86 | [ers-agent-linux-386](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-386) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-386.sha256) | ~6MB | UPX compressed |
| Linux ARM64 | [ers-agent-linux-arm64](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-arm64) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-arm64.sha256) | ~12MB | Standard build |
| Linux ARM | [ers-agent-linux-arm](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-arm) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-linux-arm.sha256) | ~11MB | Standard build |

### macOS

| Architecture | Download | Checksum | Size | Notes |
|-------------|----------|----------|------|-------|
| macOS Intel | [ers-agent-darwin-amd64](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-darwin-amd64) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-darwin-amd64.sha256) | ~13MB | Standard build |
| macOS Apple Silicon | [ers-agent-darwin-arm64](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-darwin-arm64) | [SHA256](https://github.com/forewall/ers-release/releases/download/v1.0.3a/ers-agent-darwin-arm64.sha256) | ~12MB | Standard build |

> **Note about UPX compression**: Some binaries are compressed with UPX to reduce file size (up to 50% smaller). This provides faster downloads but doesn't affect performance. The executable decompresses automatically at runtime.

## Quick Start Guide

### Linux/macOS

1. Download the appropriate binary for your platform.
2. Make it executable:
   ```bash
   chmod +x ers-agent-*
   ```
3. Move to a directory in your PATH:
   ```bash
   sudo mv ers-agent-* /usr/local/bin/ers-agent
   ```
4. Run the agent:
   ```bash
   ers-agent --help
   ```
5. Configure with your server and agent key:
   ```bash
   ers-agent -s wss://your-server.com/ws -k your-agent-key
   ```

### Windows

1. Download the appropriate .exe file for your platform.
2. Move to a desired location (e.g., C:\Program Files\ERS).
3. Run the agent from Command Prompt or PowerShell:
   ```
   ers-agent.exe --help
   ```
4. Configure with your server and agent key:
   ```
   ers-agent.exe -s wss://your-server.com/ws -k your-agent-key
   ```

## Running as a Service

### Linux (systemd)

Create a systemd service file:

```bash
sudo nano /etc/systemd/system/ers-agent.service
```

Add the following content:

```ini
[Unit]
Description=ERS Agent Service
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/ers-agent -k YOUR_AGENT_KEY -s YOUR_SERVER_URL
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Enable and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable ers-agent
sudo systemctl start ers-agent
sudo systemctl status ers-agent
```

### Windows

#### Using NSSM (recommended)

1. Download [NSSM](https://nssm.cc/)
2. Open Command Prompt as Administrator
3. Run the following command:
   ```
   nssm.exe install ERSAgent "C:\Path\To\ers-agent.exe" "-k YOUR_AGENT_KEY -s YOUR_SERVER_URL"
   nssm.exe set ERSAgent Description "Easy Remote System Agent"
   nssm.exe set ERSAgent Start SERVICE_AUTO_START
   nssm.exe start ERSAgent
   ```

#### Using Windows Services

1. Open Command Prompt as Administrator
2. Create a Windows service:
   ```
   sc create ERSAgent binPath= "C:\Path\To\ers-agent.exe -k YOUR_AGENT_KEY -s YOUR_SERVER_URL"
   sc description ERSAgent "Easy Remote System Agent"
   sc config ERSAgent start= auto
   sc start ERSAgent
   ```

## Troubleshooting

### Common Issues

- **Connection Problems**: Make sure your server URL is correct and includes the WebSocket protocol (wss:// or ws://)
- **Permission Denied**: Ensure the binary has execute permissions on Linux/macOS
- **Agent Key Invalid**: Verify you are using the correct agent key from your ERS management console

For more detailed troubleshooting, use the debug log level:

```bash
ers-agent -l debug -s YOUR_SERVER_URL -k YOUR_AGENT_KEY
```

## Previous Versions

Visit the [Releases page](https://github.com/forewall/ers-release/releases) to download previous versions.

## Release Notes

## ERS Agent v1.0.3a

Released on 2025-05-18

### 🚀 New Features

- Add fallback release creation and repo initialization steps

### ⚡ Improvements

- Update deploy workflow to use environment variables for defaults

### 📋 All Changes

<details>
<summary>View all changes</summary>

- Update deploy workflow to use environment variables for defaults (526db2b)
- Add fallback release creation and repo initialization steps (af84f11)
- Add GitHub Actions workflow for release and deployment (bd21f34)
- Update default branch detection in CI workflow (c5b76d3)
</details>

## Installation

Download the appropriate binary for your platform from the assets below or visit our [Download Page](https://forewall.github.io/ers-release/).
