# Incident Timeline — Suspicious dllhost.exe Activity

## Case Summary

This timeline reconstructs the suspicious `dllhost.exe` activity observed on the Windows endpoint using Wazuh and Sysmon telemetry.

The investigation focused on understanding the process creation event, its execution context, and the evidence associated with the COM Surrogate process.

---

## Timeline

| Time (UTC) | Source | Event | Analyst Interpretation |
|---|---|---|---|
| 2026-08-07 16:06:59 | Wazuh / Sysmon | `dllhost.exe` process creation detected | Wazuh generated Rule 61638 |
| 2026-08-07 16:06:59 | Wazuh / Sysmon | Second `dllhost.exe` event observed | Repeated detection required investigation |
| 2026-08-09 14:44:02 | Wazuh / Sysmon | `dllhost.exe` process detected again | Same detection pattern observed |
| 2026-08-11 17:38:19 | Wazuh / Sysmon | `dllhost.exe` process detected again | Repeated activity observed |

---

## Process Evidence

The Sysmon Event ID 1 telemetry identified:

- Image: `C:\Windows\SysWOW64\dllhost.exe`
- Description: `COM Surrogate`
- Company: `Microsoft Corporation`
- Integrity Level: `High`
- Process ID: `11184`
- Parent Process ID: `744`
- User: `WIN-VTU7D3FFVFH\user`
- Command Line: `C:\WINDOWS\SysWOW64\DllHost.exe /Processid:{6A695947-B2C3-457C-9B12-800EE815E4BF}`

---

## Investigation Sequence

The investigation followed this sequence:

1. Wazuh generated Rule 61638.
2. The alert was correlated with Sysmon Event ID 1.
3. The `dllhost.exe` executable path was examined.
4. The command line and COM process identifier were examined.
5. Process ID and Parent Process ID were investigated.
6. The executable publisher and file information were checked.
7. The SHA256 hash was collected.
8. The COM registration associated with the identifier was investigated.
9. The available evidence was evaluated before assigning a verdict.

---

## Analyst Assessment

The repeated `dllhost.exe` detections justified investigation because Wazuh classified the process as suspicious.

However, the presence of `dllhost.exe` alone does not establish malware.

The investigation found evidence consistent with a legitimate Windows `COM Surrogate` process, including the Microsoft executable path and Microsoft Corporation publisher information.

### Final Verdict

**Suspicious activity investigated — no confirmed malware identified.**

The case demonstrates the importance of correlating SIEM alerts with endpoint telemetry and investigating the surrounding process context before declaring an incident malicious.

## Evidence

### Wazuh Alert Overview

![Wazuh dllhost alert](../screenshots/wazuh-dllhost-alert.png)

### Detailed Sysmon Event

![Wazuh dllhost event details](../screenshots/Details_wazuh-dllhost-alert.png)
