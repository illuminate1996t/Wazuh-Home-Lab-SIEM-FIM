# Verification Checklist

## Ubuntu Manager

- [ ] Ubuntu VM has network connectivity.
- [ ] Ubuntu and Windows can communicate.
- [ ] Wazuh installation completed.
- [ ] Wazuh services are running.
- [ ] Dashboard opens at `https://<ubuntu-vm-ip>`.

## Windows Agent

- [ ] Wazuh Agent is installed.
- [ ] Agent key was generated.
- [ ] Key was applied to Windows.
- [ ] Manager IP is configured.
- [ ] Agent service was restarted.
- [ ] Dashboard shows the agent as Active.

## FIM

- [ ] `ossec.conf` contains the monitored directory.
- [ ] `realtime="yes"` is configured for the test directory.
- [ ] Agent was restarted after configuration.
- [ ] A test file was created.
- [ ] A test file was modified.
- [ ] A test file was deleted.
- [ ] Integrity Monitoring shows the activity.

## Evidence

Record:

```text
Ubuntu Manager IP:
Windows Agent Name:
Monitored Directory:
Agent Status:
FIM Test Date:
Observed Alerts:
```
