# Wazuh SOC Detection & Incident Investigation Lab

## Overview

A hands-on Security Operations Center (SOC) laboratory built to
practice security monitoring, threat detection, alert investigation,
MITRE ATT&CK mapping, and incident response.

The project uses Wazuh as the central SIEM/XDR platform with
Sysmon for Windows endpoint telemetry and Suricata for network
threat detection.

## Lab Architecture

```text
                    Parrot OS
                 192.168.64.14
                       |
                       | Nmap / Network Traffic
                       ↓
                Windows 11 Endpoint
                 192.168.64.12
                     Sysmon
                       |
                       | Windows Events
                       ↓
                 Wazuh Server
                  192.168.64.6
                       |
              ┌────────┴────────┐
              ↓                 ↓
          Wazuh SIEM        Suricata
              ↓                 ↓
          Dashboard       Network Alerts
