# Install and Configure Prometheus
These instructions were tested on **Ubuntu Server 24.04 LTS**. For other operating systems, consult the relevant documentation.

---
### Step 1: Check for latest version on website
Visit the Prometheus downloads on their [website](https://prometheus.io/download/) and make a note of the most recent release.

I am using the latest LTS at time of this edit is `prometheus-2.53.4.linux-amd64.tar.gz`.

---
### Step 2: Download Prometheus
Use `wget` to download Prometheus to the monitoring server.

*Use `sudo` for commands requiring elevated privileges on systems with security restrictions (e.g., Ubuntu, RHEL, or enterprise environments).*
```bash
# edit the following according to your selected version
$ wget https://github.com/prometheus/prometheus/releases/download/v2.53.4/prometheus-2.53.4.linux-amd64.tar.gz
```
---
### Step 3: Extract the archived files to path and verify installation
- Extract the archived Prometheus files.
- (Optional) delete the archive to free space
```bash
$ tar xvfz prometheus-*.tar.gz
$ rm prometheus-*.tar.gz    # Optional
```
- The `/etc/prometheus` directory stores the Prometheus configuration files. 
- The `/var/lib/prometheus` directory holds application data.
```bash
$ sudo mkdir /etc/prometheus /var/lib/prometheus
```
- Move into the main directory
- Move the prometheus and promtool directories to the `/usr/local/bin/` directory. *This makes Prometheus accessible to all users.*
- Move the configuration file `prometheus.yml` to the `/etc/prometheus` directory.
```bash
$ cd prometheus-2.53.4.linux-amd64
$ sudo mv prometheus promtool /usr/local/bin/
$ sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```
- The files under directories `consoles` and `console_libraries` should be moved to the `etc/prometheus` directory.
- *These directories contains necessary resources for customized consoles.*
```bash
$ sudo mv consoles/ console_libraries/ /etc/prometheus/
```

- Verify that Prometheus is successfully installed
```bash
$ prometheus --version
------------------------------------
prometheus, version 2.53.4 (branch...)
```

### Step 4: Configure Prometheus as a Service
- Create a system user named `prometheus`
- Assign `prometheus` ownership of resource directories
```bash
$ sudo useradd -rs /bin/false prometheus
$ sudo chown -R prometheus: /etc/prometheus /var/lib/prometheus
```
- Create a `prometheus.service` file, 
- Contents under `prometheus/prometheus.service` from left pane
```bash
$ sudo vi /etc/systemd/system/prometheus.service
```
- Reload `systemctl` daemon
- Enable prometheus autostart on reboot
```bash
$ sudo systemctl daemon-reload
$ sudo systemctl enable prometheus
```
- Start the prometheus service and review the status.
```bash
$ sudo systemctl start prometheus
$ sudo systemctl status prometheus
---------------------------------------
o prometheus.service - Prometheus
    Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; vendor preset: enabled)
    Active: active (running) since Mon 2025-05-03 13:06:50 UTC; 7s ago
```

