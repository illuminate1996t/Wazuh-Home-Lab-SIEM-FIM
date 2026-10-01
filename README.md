# Wazuh Home Lab — SIEM & File Integrity Monitoring

A practical home-lab project for learning **Wazuh SIEM**, Windows agent monitoring, and **File Integrity Monitoring (FIM)**.

## Lab Architecture

```text
                    Home / Lab Network
                           |
             +-------------+-------------+
             |                           |
     Ubuntu Server VM              Windows Host
     Wazuh Manager                 Wazuh Agent
     Wazuh Indexer                 Logs / Events
     Wazuh Dashboard                     |
             |                           |
             +---------- Wazuh ----------+
                         Agent data
```

The reference lab uses a Wazuh Manager on Ubuntu running in VirtualBox and a Wazuh Agent on the Windows host. Bridged networking places the Ubuntu VM on the same network as the host.

## Objectives

- Deploy a Wazuh Manager.
- Access the Wazuh Dashboard.
- Register a Windows endpoint.
- Monitor a Windows directory with Syscheck/FIM.
- Generate file create/modify/delete events.
- Verify alerts in the dashboard.
- Troubleshoot common agent, network, and FIM problems.

## Prerequisites

- VirtualBox
- Ubuntu Server 20.04+
- Internet access on the Ubuntu VM
- Windows administrative access
- Basic Linux/Windows administration knowledge

## 1. Configure the Ubuntu VM

In VirtualBox, use **Bridged Adapter** networking so the Ubuntu VM and Windows host can communicate.

Find the Ubuntu IP:

```bash
ifconfig
```

If `ifconfig` is unavailable, use:

```bash
ip addr
```

## 2. Install Wazuh

The supplied lab guide uses the Wazuh 4.12 installation script.

Add the package signing key:

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh-archive-keyring.gpg
```

Download and run the installation script:

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
sudo bash ./wazuh-install.sh -a -i
```

`-a` installs the all-in-one components and `-i` runs the interactive installation.

> Version note: the commands above reproduce the supplied lab guide. For a new deployment, check the current Wazuh documentation and adapt the version as necessary.

## 3. Open the Dashboard

From a browser:

```text
https://<ubuntu-vm-ip>
```

Accept the browser warning if the installation uses a self-signed certificate.

Use the credentials displayed by the installation process.

## 4. Install the Windows Agent

Install the Wazuh Agent MSI on the Windows host using the normal installation process.

The supplied guide instructs you to obtain the current Windows agent from Wazuh's official documentation.

## 5. Register the Windows Agent

On Ubuntu:

```bash
sudo /var/ossec/bin/manage_agents
```

Then:

1. Select `A` to add an agent.
2. Give it a name, such as `WindowsHost`.
3. Leave the IP blank unless a static assignment is required.
4. Select `E` to extract the agent key.
5. Copy the generated key.

On Windows:

1. Open Wazuh Agent Manager.
2. Paste the key.
3. Save/apply the key.
4. Enter the Ubuntu Wazuh Manager IP.
5. Restart the Wazuh Agent service.

The agent should become **Active** in the Wazuh Dashboard.

## 6. Configure File Integrity Monitoring

Edit:

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Add a monitored directory inside the appropriate configuration area:

```xml
<directories realtime="yes">C:\Users\i_Node\Desktop\Wazuh\Test</directories>
```

Replace `C:\Users\abc\Test` with the directory you actually want to monitor.

Restart the Wazuh Agent after saving the configuration.

## 7. Test FIM

In the monitored directory:

- Create a file.
- Modify the file.
- Delete the file.

Then open the Wazuh Dashboard and check **Integrity Monitoring** for the resulting events/alerts.

## Troubleshooting

See [`docs/TROUBLESHOOTING.md`](docs/TROUBLESHOOTING.md).

## Verification Checklist

See [`docs/VERIFICATION.md`](docs/VERIFICATION.md).

## Suggested Repository Structure

```text
Wazuh-Home-Lab-SIEM-FIM/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── ARCHITECTURE.md
│   ├── LEARNED.md
│   ├── VERIFICATION.md
│   └── WINDOWS-FIM.md
└── config/
│    └── fim-example.xml
└── screnshots/
│
└── /Troublesooting
    ├── Troubleshooting.md
    └── Other Troubleshooting issue.md

```

## Disclaimer

Use this project only on systems and networks you own or are authorized to administer. This is a learning lab, not a production hardening guide.
