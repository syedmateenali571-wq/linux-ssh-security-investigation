# Linux SSH Security Investigation

## Project Overview

This project is a small SOC-style security investigation performed on a Kali Linux virtual machine.

The objective was to investigate the SSH service, identify its configuration, analyze authentication activity, review active connections, and examine host-level firewall and logging configuration.

The investigation was performed in a controlled lab environment.

## Objectives

- Investigate the SSH service status
- Verify SSH port 22
- Analyze SSH authentication logs
- Identify successful and failed authentication attempts
- Review SSH effective configuration
- Examine authentication security controls
- Check current SSH connections
- Review firewall configuration
- Review SSH logging configuration
- Document findings using a SOC investigation approach

## Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Environment | VirtualBox |
| Service Investigated | OpenSSH |
| Protocol | SSH |
| Port | TCP/22 |
| Logging | systemd journal |
| Investigation Type | SOC / Blue Team |

## Investigation Methodology

The investigation followed this process:

1. Check SSH service status
2. Verify whether port 22 is listening
3. Start the SSH service for the lab
4. Review SSH service logs
5. Generate a legitimate local SSH authentication event
6. Analyze failed and successful authentication
7. Check active users and connections
8. Review effective SSH configuration
9. Review authentication controls
10. Review firewall configuration
11. Review SSH logging configuration
12. Document findings

## Tools and Commands Used

### SSH Service

```bash
systemctl status ssh
sudo systemctl start ssh
