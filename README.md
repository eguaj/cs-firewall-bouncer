<p align="center">
<img src="https://github.com/crowdsecurity/cs-firewall-bouncer/raw/main/docs/assets/crowdsec_linux_logo.png" alt="CrowdSec" title="CrowdSec" width="280" height="250" />
</p>
<p align="center">
<img src="https://img.shields.io/badge/build-pass-green">
<img src="https://img.shields.io/badge/tests-pass-green">
</p>
<p align="center">
&#x1F4DA; <a href="#installation">Documentation</a>
&#x1F4A0; <a href="https://hub.crowdsec.net">Hub</a>
&#128172; <a href="https://discourse.crowdsec.net">Discourse </a>
</p>


# cs-firewall-bouncer
Crowdsec bouncer written in golang for firewalls.

cs-firewall-bouncer will fetch new and old decisions from a CrowdSec API to add them in a blocklist used by supported firewalls.

Supported firewalls:
 - iptables (IPv4 :heavy_check_mark: / IPv6 :heavy_check_mark: )
 - nftables (IPv4 :heavy_check_mark: / IPv6 :heavy_check_mark: )

## Installation

### Assisted

First, download the latest [`cs-firewall-bouncer` release](https://github.com/crowdsecurity/cs-firewall-bouncer/releases).

```sh
$ tar xzvf cs-firewall-bouncer.tgz
$ sudo ./install.sh
```

### From source

Run the following commands:

```bash
git clone https://github.com/crowdsecurity/cs-firewall-bouncer.git
cd cs-firewall-bouncer/
make release
tar xzvf cs-firewall-bouncer.tgz
cd cs-firewall-bouncer-v*/
sudo ./install.sh
```


## Configuration

Before starting the `cs-firewall-bouncer` service, please edit the configuration to add your API url and key.
The default configuration file is located under : `/etc/crowdsec/cs-firewall-bouncer/`

```sh
$ vim /etc/crowdsec/cs-firewall-bouncer/cs-firewall-bouncer.yaml
```

```yaml
mode: iptables
piddir: /var/run/
update_frequency: 10s
daemonize: true
log_mode: file
log_dir: /var/log/
log_level: info
api_url: <API_URL>  # when install, default is "localhost:8080"
api_key: <API_KEY>  # Add your API key generated with `cscli bouncers add --name <bouncer_name>`
```

You can then start the service:

```sh
sudo systemctl start cs-firewall-bouncer
```
