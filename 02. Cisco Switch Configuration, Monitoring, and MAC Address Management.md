# Cisco Switch Configuration, Monitoring, and MAC Address Management

# 📘 Introduction

This document provides standardized procedures for managing and monitoring Cisco switches within an enterprise network environment.

The guide covers:

* Remote access to Cisco switches
* Interface and port status verification
* MAC address table lookup and monitoring
* Configuration saving procedures
* Operational verification and troubleshooting

This documentation is intended for:

* Network Administrators
* IT Support Engineers
* Infrastructure Teams
* System Administrators

---

# 🎯 Purpose

The purpose of this manual is to establish:

* Consistent operational procedures
* Standardized network administration
* Improved troubleshooting efficiency
* Accurate infrastructure management
* Better operational documentation practices

---

# 🌐 Environment Information

| Parameter         | Value          |
| ----------------- | -------------- |
| **Device Type**   | Cisco Switch   |
| **Management IP** | `192.168.1.20` |
| **Access Method** | SSH / Telnet   |
| **Client Tool**   | PuTTY          |
| **Username**      | `admin`        |
| **Password**      | `*****`   |

> ⚠️ **Security Notice**
> Administrative credentials must be stored securely according to organizational security policies.

---

# ✅ Prerequisites

Before proceeding, ensure the following requirements are met:

* PuTTY is installed on the workstation
* Network connectivity to the switch is available
* Authorized administrative access is approved
* Valid Cisco switch credentials are available
* SSH or Telnet communication is permitted through the firewall

---

# 🔐 Accessing the Cisco Switch

## Step 1 — Launch PuTTY

Open the **PuTTY** application.

---

## Step 2 — Enter the Management IP Address

Use the Cisco switch management IP address:

```bash
192.168.1.20
```

### Example Configuration

| Setting         | Value          |
| --------------- | -------------- |
| Host Name       | `192.168.1.20` |
| Connection Type | `SSH`          |
| Port            | `22`           |

---

## Step 3 — Open the Session

Click **Open** to initiate the connection.

---

## Step 4 — Authenticate

Enter the administrative credentials.

### Example Login

```text
login as: admin
password: ********
```

---

## Step 5 — Continue the Session

If terminal output pauses, press:

```text
Ctrl + C
```

---

# 📡 Interface Verification & Monitoring

This section explains how to monitor switch interfaces and verify operational status.

---

## Display Interface Descriptions

### Command

```bash
show interfaces description
```

### Purpose

Displays:

* Interface identifiers
* Port descriptions
* Operational state
* Protocol status

### Example Output

```text
Interface        Status         Protocol Description
Gi1/0/1          up             up       Uplink-CoreSW
Gi1/0/2          up             up       Finance-PC01
Gi1/0/3          administratively down down
```

### Status Definitions

| Status                  | Description                                |
| ----------------------- | ------------------------------------------ |
| `up/up`                 | Interface operating normally               |
| `down/down`             | Cable disconnected or endpoint unavailable |
| `administratively down` | Interface manually disabled                |

---

## Stop Command Output

```text
Ctrl + C
```

---

## Display Interface Status

### Command

```bash
show interfaces status
```

### Purpose

Displays:

* VLAN assignments
* Interface operational state
* Duplex settings
* Speed configuration
* Device connectivity status

### Example Output

```text
Port      Name               Status       Vlan       Duplex  Speed Type
Gi1/0/1   Uplink-CoreSW      connected    trunk      a-full  a-1000
Gi1/0/2   Finance-PC01       connected    10         a-full  a-100
Gi1/0/3                      notconnect   1          auto    auto
```

### Important Fields

| Field  | Description             |
| ------ | ----------------------- |
| Status | Current interface state |
| VLAN   | Assigned VLAN           |
| Duplex | Duplex mode             |
| Speed  | Interface speed         |

---

## Stop Command Output

```text
Ctrl + C
```

---

# 🔍 MAC Address Table Operations

The MAC address table is used to identify devices connected to switch interfaces.

---

## Display Complete MAC Address Table

### Command

```bash
show mac address-table
```

### Purpose

Displays all MAC addresses learned by the Cisco switch.

### Example Output

```text
Vlan    Mac Address       Type        Ports
10      A1:B2:C3:D4:E5:F6:G7   DYNAMIC     Gi1/0/6
20      0050.56ab.cd11   DYNAMIC     Gi1/0/10
```

---

## Stop Output

```text
Ctrl + C
```

---

## Search MAC Address by Interface

Use this command to identify devices connected to a specific switch port.

### Example Interface

```text
GigabitEthernet1/0/6
```

### Command

```bash
show mac address-table interface GigabitEthernet1/0/6
```

### Example Output

```text
Vlan    Mac Address       Type        Ports
10      A1:B2:C3:D4:E5:F6:G7   DYNAMIC     Gi1/0/6
```

### Operational Use Cases

Useful for:

* Identifying connected endpoints
* Troubleshooting user connectivity
* Tracking unauthorized devices
* Verifying endpoint location

---

## Search Interface by MAC Address

Use this procedure when the MAC address is already known.

### Example MAC Address

```text
A1:B2:C3:D4:E5:F6:G7
```

### Cisco MAC Address Format

Cisco switches commonly display MAC addresses in dotted notation:

```text
A1:B2:C3:D4:E5:F6:G7
```

---

### Command

```bash
show mac address-table | include A1:B2:C3:D4:E5:F6:G7
```

### Example Output

```text
10      A1:B2:C3:D4:E5:F6:G7   DYNAMIC     Gi1/0/6
```

### Result Interpretation

| Field       | Description                     |
| ----------- | ------------------------------- |
| VLAN        | VLAN associated with the device |
| MAC Address | Device hardware address         |
| Port        | Connected interface             |

---

# 💾 Save Configuration

After making configuration changes, save the running configuration to prevent data loss after reboot.

---

## Save Running Configuration

### Command

```bash
write memory or wr
```

### Alternative Command

```bash
copy running-config startup-config
```

### Example Output

```text
Building configuration...
[OK]
```

> ✅ Configuration successfully saved.

---

# ✔️ Verification Procedures

Always verify switch operations and configurations after changes are applied.

---

## Verify Interface Status

```bash
show interfaces status
```

---

## Verify Interface Descriptions

```bash
show interfaces description
```

---

## Verify MAC Address Learning

```bash
show mac address-table
```

---

## Verify Specific Interface MAC Entries

```bash
show mac address-table interface GigabitEthernet1/0/6
```

---

# 🛡️ Best Practices

Follow these recommended operational standards:

* Use SSH instead of Telnet whenever possible
* Save configurations immediately after modifications
* Verify all configuration changes
* Maintain regular configuration backups
* Restrict administrative access permissions
* Disable unused interfaces
* Monitor switch logs regularly
* Document all production environment changes

---

# 🧰 Troubleshooting Guide

| Issue                                          | Possible Cause                  | Recommended Action                        |
| ---------------------------------------------- | ------------------------------- | ----------------------------------------- |
| Unable to connect via SSH                      | SSH disabled or network issue   | Verify SSH configuration and connectivity |
| Interface status shows `down/down`             | Physical connection issue       | Check cable and endpoint device           |
| Interface status shows `administratively down` | Interface manually disabled     | Enable interface if authorized            |
| MAC address not visible                        | Device inactive or disconnected | Verify endpoint connectivity              |
| Configuration changes lost after reboot        | Configuration not saved         | Execute `write memory`                    |

---

# ⚡ Quick Command Reference

## Connection

```bash
ssh admin@192.168.1.20
```

---

## Interface Monitoring

```bash
show interfaces description
show interfaces status
```

---

## MAC Address Operations

```bash
show mac address-table
show mac address-table interface GigabitEthernet1/0/6
show mac address-table | include A1:B2:C3:D4:E5:F6:G7
```

---

## Save Configuration

```bash
write memory or wr
```

---

# 📌 Document Control

| Item           | Details                |
| -------------- | ---------------------- |
| Document Owner | IT Infrastructure Team |
| Last Updated   | May 2026               |
| Review Cycle   | Quarterly              |
| Classification | Internal Use Only      |

---

# ✅ Conclusion

This guide provides standardized operational procedures for Cisco switch access, interface monitoring, MAC address lookup, and configuration management.

Following this documentation helps ensure:

* Consistent network administration
* Faster troubleshooting
* Improved operational efficiency
* Better infrastructure visibility
* Enhanced network management practices

---
