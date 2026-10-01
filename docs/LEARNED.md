# Wazuh Home Lab — Lessons Learned

## What I Learned

This lab helped me understand the basic workflow of using Wazuh as a SIEM and for File Integrity Monitoring (FIM).

### 1. Wazuh Manager

I learned that the Wazuh Manager must be active for the Wazuh environment and API connection to work correctly.

```bash
sudo systemctl status wazuh-manager
```

If inactive:

```bash
sudo systemctl restart wazuh-manager
```

### 2. Wazuh Agent

I learned how to register a Windows endpoint with the Wazuh Manager using an agent key and the Manager's IP address.

### 3. File Integrity Monitoring

I learned how Wazuh can monitor files and directories for changes using Syscheck.

```xml
<directories realtime="yes">C:\Users\i_Node\Desktop\Wazuh\Test</directories>
```

Creating, modifying, or deleting files in a monitored directory can generate events in the Wazuh Dashboard.

### 4. Troubleshooting

The main problem I experienced was that the Wazuh API connection was down because the Wazuh Manager was not active.

I learned to check the Manager service first:

```bash
sudo systemctl status wazuh-manager
```

Then restart it when necessary:

```bash
sudo systemctl restart wazuh-manager
```

### 5. Network Configuration

I learned that the Ubuntu VM and Windows host need network connectivity.

The VirtualBox VM used:

```text
Bridged Adapter
```

Check the Ubuntu IP:

```bash
ip addr
```

Test connectivity from Windows:

```powershell
ping <ubuntu-vm-ip>
```

## Key Skills Gained

- Wazuh SIEM setup
- Wazuh Manager administration
- Windows Agent registration
- File Integrity Monitoring
- Linux service management
- Network troubleshooting
- Wazuh Dashboard verification
- Security event troubleshooting

## Key Lesson

I learned to troubleshoot systematically by checking the Manager, network connectivity, agent status, configuration, and FIM events step by step.

