SOC LAB for mimicing the SOC-analyst everyday-job
============================================================================================================================================================================================================



This architecture is actually very good for a practical SOC lab.

We already have separated VMs(See the PDF):
    <ul>
      <li>attacker</li>
      <li>victim</li>
      <li>SIEM</li>
    </ul>

which is exactly how many real environments are structured.

The lab flow is basically:

    Kali Linux (attacker)
            |
            v
    Windows VM (victim + logs)
            |
            v
    Wazuh Server on DigitalOcean (SIEM/SOC)

That’s our solid setup.


<h1>1. What To Configure Inside Windows VM</h1>

We need:

vulnerable target(s)
Wazuh agent

The Windows VM acts as:

victim machine
monitored endpoint



A. Install Wazuh Agent

Install:

Wazuh Agent

on:

Windows 10 Enterprise LTSC 2021

This agent will:

collect Windows Event Logs
monitor processes
detect malware indicators
send logs to Wazuh server
generate alerts
Configure Agent To Connect To Our Wazuh Server

Inside agent config:

<address>YOUR_SERVER_IP</address>

Usually in:

C:\Program Files (x86)\ossec-agent\ossec.conf

Then restart the service.

B. Install Sysmon (VERY IMPORTANT)

This is one of the biggest improvements

Install:

Sysmon

bECAUSE Windows default logs are weak.

Sysmon gives:

process creation
PowerShell activity
network connections
DLL loading
persistence detection
parent/child process chains

This dramatically improves Wazuh visibility.

Recommended Sysmon Config

Use:

SwiftOnSecurity Sysmon config

It’s widely used in SOC labs.
