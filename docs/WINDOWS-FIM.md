# Windows File Integrity Monitoring

Wazuh uses Syscheck for file integrity monitoring.

## Configuration File

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
```

## Example

```xml
<directories realtime="yes">C:\Users\i_Node\Desktop\Wazuh\Test</directories> 
```

Change the path to a directory that exists on your Windows system.

## Test Procedure

1. Create a test directory.
2. Add the directory to `ossec.conf`.
3. Restart the Wazuh Agent.
4. Create a test file.
5. Modify the file.
6. Delete the file.
7. Review the Wazuh Dashboard.

## Important

Keep the monitored directory dedicated to testing. Avoid experimenting with system-critical Windows directories until you understand the configuration.

If events do not appear, use `docs/TROUBLESHOOTING.md`.
