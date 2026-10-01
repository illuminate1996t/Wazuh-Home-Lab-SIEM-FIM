\## 1. Other Possible Issues



\### Dashboard Does Not Open



Check the Ubuntu IP:



```bash

ip addr

```



Open:



```text

https://<ubuntu-vm-ip>

```



Test connectivity from Windows:



```powershell

ping <ubuntu-vm-ip>

```



Confirm VirtualBox uses \*\*Bridged Adapter\*\*.



\### Windows Agent Not Active



Check:



\- Agent key

\- Manager IP

\- Agent service

\- Network connectivity



```powershell

Get-Service | Where-Object {$\_.Name -like "\*wazuh\*"}

```



\### FIM Events Not Appearing



Check:



```text

C:\\Program Files (x86)\\ossec-agent\\ossec.conf

```



Example:



```xml

<directories realtime="yes">C:\\Users\\i\_Node\\Desktop\\Wazuh\\Test</directories>

```



Restart the agent and test:



```text

Create → Modify → Delete → Check Dashboard

```



\### Configuration Problems



Check `ossec.conf` for incorrect XML or paths. Keep a backup before editing.



\### Diagnostic Order



```text

Manager → Network → Agent → Registration → ossec.conf → FIM → Dashboard

```

```



