# wazuh-ubnutu-ct
Wazuh in LXC container in Proxmox


ssh into your proxmox server.
```
pveam update
pveam availale
pveam download local ubuntu-22.04-standard_22.04-1_amd64.tar.zst
```

Log into the web interface and create a new container.

Download pre-requisites:
```
sudo apt install vim curl apt-transport-https unzip wget libcap2-bin software-properties-common lsb-release gnupg2
```

Download install script and run it:
```
curl -sO https://packages.wazuh.com/4.3/wazuh-install.sh
sudo bash ./wazuh-install.sh -a -i
```

Output:
```
24/01/2024 05:38:01 INFO: Starting Wazuh installation assistant. Wazuh version: 4.3.11
24/01/2024 05:38:01 INFO: Verbose logging redirected to /var/log/wazuh-install.log
24/01/2024 05:38:03 WARNING: Hardware and system checks ignored.
24/01/2024 05:38:10 INFO: Wazuh repository added.
24/01/2024 05:38:10 INFO: --- Configuration files ---
24/01/2024 05:38:10 INFO: Generating configuration files.
24/01/2024 05:38:12 INFO: Created wazuh-install-files.tar. It contains the Wazuh cluster key, certificates, and passwords necessary for installation.
24/01/2024 05:38:12 INFO: --- Wazuh indexer ---
24/01/2024 05:38:12 INFO: Starting Wazuh indexer installation.
24/01/2024 05:39:00 INFO: Wazuh indexer installation finished.
24/01/2024 05:39:00 INFO: Wazuh indexer post-install configuration finished.
24/01/2024 05:39:00 INFO: Starting service wazuh-indexer.
24/01/2024 05:39:34 INFO: wazuh-indexer service started.
24/01/2024 05:39:34 INFO: Initializing Wazuh indexer cluster security settings.
24/01/2024 05:40:05 INFO: Wazuh indexer cluster initialized.
24/01/2024 05:40:05 INFO: --- Wazuh server ---
24/01/2024 05:40:05 INFO: Starting the Wazuh manager installation.
24/01/2024 05:41:21 INFO: Wazuh manager installation finished.
24/01/2024 05:41:21 INFO: Starting service wazuh-manager.
24/01/2024 05:41:45 INFO: wazuh-manager service started.
24/01/2024 05:41:45 INFO: Starting Filebeat installation.
24/01/2024 05:42:20 INFO: Filebeat installation finished.
24/01/2024 05:42:21 INFO: Filebeat post-install configuration finished.
24/01/2024 05:42:21 INFO: Starting service filebeat.
24/01/2024 05:42:24 INFO: filebeat service started.
24/01/2024 05:42:24 INFO: --- Wazuh dashboard ---
24/01/2024 05:42:24 INFO: Starting Wazuh dashboard installation.
24/01/2024 05:42:24 INFO: Starting Wazuh dashboard installation.
24/01/2024 05:47:17 INFO: Wazuh dashboard installation finished.
24/01/2024 05:47:17 INFO: Wazuh dashboard post-install configuration finished.
24/01/2024 05:47:17 INFO: Starting service wazuh-dashboard.
24/01/2024 05:47:17 INFO: wazuh-dashboard service started.

```


```
curl -so wazuh-agent-4.3.11.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.3.11-1_amd64.deb && sudo WAZUH_MANAGER='localhost' WAZUH_AGENT_GROUP='default' dpkg -i ./wazuh-agent-4.3.11.deb
```

```
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

https://computingforgeeks.com/how-to-install-wazuh-server-on-ubuntu/
