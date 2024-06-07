## Initial Setup for Debian based LINUX

This software was designed and run on Ubuntu. It might be possible to install and run it on other OS like Windows or MacOS, but we can't guarantee it will perform the same way, or that there won't be any issue.<br>

If you want to host it externally, preferably on a secured (https) domain, you will require an independent ssl certificate for every instance of every app you install on your server. 
This guide doesn't cover the installation and management of ssl certificates in case of an external domain.<br> 

For this installation you will need to create a local domain to make the services available; this is why we do all the dns setup below. <br>
To install and use the BIBBOX software please follow these instructions:

### Install Docker Engine, Docker-compose, Dnsmasq, Git and prepatory Steps, Linux

Run the following commands:
```
sudo apt-get update
sudo apt-get install -y ca-certificates curl git
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker network create bibbox-default-network
sudo usermod -aG docker $USER
```
Dnsmasq is used to create a local domain to resolve your requests towards the internal Proxy-Server operated by the bibbox. Otherwise installation and app usage will not work.

### DNS service setup for UBUNTU 20+, These steps will replace your current systemd-resolved with dnsmasq.
Note: if you do something wrong your internet will not work anymore.

#### Installing and configuring dnsmasq:<br>
```
sudo apt install dnsmasq -y
```
Uninstall `systemd-resolved` package. It isn’t necessary to have.
```
sudo systemctl disable systemd-resolved
sudo systemctl stop systemd-resolved
sudo apt purge systemd-resolved
```
<br>Disable dnsmasq in the `/etc/NetworkManager/NetworkManager.conf`. Also, ensure to have the `dns=none` line:<br> `sudo nano /etc/NetworkManager/NetworkManager.conf`

```
[main]
dns=none
plugins=ifupdown,keyfile

[ifupdown]
managed=false

[device]
wifi.scan-rand-mac-address=no
```
<br>Restart NetworkManager:
```
sudo systemctl restart NetworkManager
```
<br>Remove the current `/etc/resolv.conf` file and install dnsmasq:
```
unlink /etc/resolv.conf
sudo apt-get install dnsmasq -y
```
<br>Config your upstream dns:
```
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.dnsmasq
echo "nameserver 8.8.8.8" | sudo tee -a /etc/resolv.dnsmasq
```
<br>Backing up the default configuration file dnsmasq creates:
```
sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```
<br>Config your `dnsmasq.conf` file. Use a cache-size parameter.
If you for example choose `bibbox.local.test` as the domain name the contents of this file will look like:
```
sudo tee /etc/dnsmasq.conf << EOF
listen-address=127.0.0.1
expand-hosts
domain=bibbox.local.test
address=/bibbox.local.test/127.0.0.1
resolv-file=/etc/resolv.dnsmasq
cache-size=2048
EOF
```
<br>Use the dnsmasq as main dns provider:
```
echo "nameserver 127.0.0.1" | sudo tee /etc/resolv.conf
```
<br>Testing if everything is fine:
```
dnsmasq --test
```
If you get the following answer everything is good: `dnsmasq: syntax check OK`, if not there is a mistake in `dnsmasq.conf`.<br>
<br>Restart dnsmasq service
```
sudo systemctl restart dnsmasq
sudo systemctl enable dnsmasq
```
<br>Testing the newly created domain:
```
dig bibbox.local.test
```
<br>Output should look like in the example bellow; if it's working it will have an `ANSWER SECTION`
```
; <<>> DiG 9.16.1-Ubuntu <<>> bibbox.local.test
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36047
;; flags: qr aa rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;bibbox.local.test.		IN	A

;; ANSWER SECTION:
bibbox.local.test.	0	IN	A	127.0.0.1

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Di Okt 19 14:23:19 CEST 2021
;; MSG SIZE  rcvd: 62
```
<br>We can also use:
```
nslookup bibbox.local.test
```
<br>Output should look like:
```
Server:		127.0.0.1
Address:	127.0.0.1#53

Name:	bibbox.local.test
Address: 127.0.0.1
```
<br>* NOTE: The domain used here `bibbox.local.test` is just an example. You can use a domain name of your choice.
* For more information about the topic visit: <a href="https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/" target="_blank">setup a dns-dhcp-server/</a>

## Install the BIBBOX (in the Beta only Debian based Linux Distributions are featured)

**Create the bibbox location folder:**
```
cd /opt
sudo mkdir bibbox
cd bibbox
```
<br>**Clone the bibbox system repository to opt bibbox and run the installation script.**
```
sudo git clone https://github.com/bibbox/sys-bibbox.git
cd sys-bibbox
```
```
sudo bash INSTALL.sh
```
<br>Warning using INSTALL.sh will reinstall nvm and set the nodejs version used by npm to 14.16.0

### URL/Domain-Settings
<br>When asked for a domain name we will use the one we created above: <br>
```
Specify domainname + TLD (e.g. silicolabv4.bibbox.org):
```
<br>Afterwards everything should be working as intended.<br>
<br>Thank you and have a nice day!

## Install BIBBOX Apps
### Installation within BIBBOX
To install an App within the BIBBOX just select an App and click install. Futher instructions are given in the install instruction (INSTALL.md) of each App.
### Standalone Installation
A standalone version is also provided for each App. An installation guide for the standalone version is present in the README.md of each App. And usually include the following commands:
```
git clone <repo_url>
cd <repo_directory>
docker network create bibbox-default-network
docker-compose up -d
```
#### Hint for Mac's
If the standalone version does not work on Mac, please try this command to set a default docker platfrom before running `docker-compose up -d`
```
export DOCKER_DEFAULT_PLATFORM=linux/amd64
```
