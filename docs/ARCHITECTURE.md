# Lab Architecture

## Components

| Component | Platform | Role |
|---|---|---|
| Wazuh Manager | Ubuntu VM | Collects, analyzes, and stores agent data |
| Wazuh Agent | Windows host | Sends logs and system events to the manager |
| Wazuh Dashboard | Ubuntu/Wazuh installation | Provides the monitoring interface |
| VirtualBox | Host hypervisor | Runs the Ubuntu server VM |

## Network

The supplied lab uses **Bridged Adapter** networking.

```text
Windows Host
    |
    | Wazuh Agent
    |
    +---------------- LAN ----------------+
                                         |
                                  Ubuntu VM
                                  Wazuh Manager
                                  Dashboard
```

The Windows agent needs network connectivity to the Ubuntu Wazuh Manager.

## Data Flow

```text
Windows file/system activity
          |
          v
     Wazuh Agent
          |
          v
    Wazuh Manager
          |
          v
       Analysis
          |
          v
      Dashboard
```
