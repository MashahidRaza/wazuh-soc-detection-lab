# Network Port Scan Detection

## Objective

Detect and investigate network reconnaissance activity against the Wazuh server.

## Lab Environment

- Attacker/Test Host: Parrot OS
- Source IP: 192.168.64.14
- Target: Wazuh Server
- Destination IP: 192.168.64.6
- Detection Platform: Wazuh + Suricata

## Attack Simulation

The following Nmap SYN scan was performed from the authorized lab machine:

```bash
sudo nmap -sS -p 1-1000 -T3 192.168.64.6
