## Initial Setup for Debian based LINUX

This software was designed and run on Ubuntu. It might be possible to install and run it on other OS like Windows or MacOS, but we can't guarantee it will perform the same way, or that there won't be any issue.<br>

To install and use the BIBBOX software please follow these instructions:

### Install Docker Engine, Docker-compose, Dnsmasq, Git and prepatory Steps, Linux

Run the following commands:
```
sudo apt-get update
sudo apt install docker.io -y
sudo apt-get install docker.io -y
sudo apt-get install docker-compose -y
sudo apt-get install dnsmasq -y
sudo apt install git -y
sudo docker network create bibbox-default-network
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
Dnsmasq is used to create a local domain to resolve your requests towards the internal Proxy-Server operated by the bibbox. Otherwise installation and app usage will not work.

### DNS service setup

#### Configuring dnsmasq:<br>
Backing up the default configuration file dnsmasq creates:
```
sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```
Editing the dnsmasq config file:
```
sudo nano /etc/dnsmasq.conf
```
If you for example choose `bibbox.local.test` as the domain name the contents of this file will look like:

```
listen-address=127.0.0.1
expand-hosts
domain=bibbox.local.test
server=8.8.8.8
server=8.8.4.4
address=/bibbox.local.test/127.0.0.1
```

* The `server=` parts are there to allow traffic not directed at our domain to be resolved to an public DNS server (googles DNS server in this case)
  
Testing if everything is fine:<br>
```
dnsmasq --test
```

If you get the following answer everything is good, if not there is a mistake in `dnsmasq.conf`:<br>  

`dnsmasq: syntax check OK`

In order to make the computer use the created DNS-Server, we need to set the namespace to the IP-Adress we provided in `listen-address`.<br> 
```
sudo nano /etc/resolv.conf
```
We replace the line:<br>
```
nameserver 127.0.0.53
```
with
```
nameserver 127.0.0.1
```
* NOTE: There could be more `nameserver=` directives present. In order for dnsmasq to work, all of those need to be commented out with an `\#` in front of them.

As the warning states to make this changes permanent we would have to add write protection towards this file:<br>
```
sudo chmod 544 /etc/resolv.conf
```

Adding `dnsmasq` to your hosts file, since all the information about DNS-Hosts will be read from there:<br>
```
sudo nano /etc/hosts
```

Add this line: <br> 
```
127.0.0.1	dnsmasq
```

Restart the dnsmasq service for all changes to take effect:
```
sudo systemctl restart dnsmasq
```

Testing the newly created domain:
```
dig bibbox.local.test
```
Output should look like in the example bellow; if it's working it will have an `ANSWER SECTION`

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

We can also use:
```
nslookup bibbox.local.test
```
Output should look like:
```
Server:		127.0.0.1
Address:	127.0.0.1#53

Name:	bibbox.local.test
Address: 127.0.0.1
```

* NOTE: The domain used here `bibbox.local.test` is just an example. You can use a domain name of your choice.
* For more information about the topic visit: <a href="https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/" target="_blank">setup a dns-dhcp-server/</a>

## Install the BIBBOX (in the Beta only Debian based Linux Distributions are featured)

**Create the bibbox location folder:**
```
cd /opt
sudo mkdir bibbox
cd bibbox
```
**Clone the bibbox system repository to opt bibbox and run the installation script.**
```
sudo git clone https://github.com/bibbox/sys-bibbox.git
cd sys-bibbox
```
```
sudo bash INSTALL.sh
```

Warning using INSTALL.sh will reinstall nvm and set the nodejs version used by npm to 14.16.0

### URL/Domain-Settings

When asked for a domain name we will use the one we created above: <br>
```
Specify domainname + TLD (e.g. silicolabv4.bibbox.org):
```

### Post-installation temporary fix to make it work:
After bibbox is up and running, if you encounter the error 'Service unavailable' when trying to login follow the following steps:
First make sure you are in the sys-bibbox folder, **if not then run**:
```
cd /opt/bibbox/sys-bibbox
```
If you are already in the bibbox folder:
```
docker-compose down
sudo sed -i '19,20s/^/# /' .env
docker-compose up -d
```
Afterwards everything should be working as intended.

Thank you and have a nice day!



