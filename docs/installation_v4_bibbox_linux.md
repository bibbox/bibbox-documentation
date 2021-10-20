## Initial Setup Debian based LINUX
 
To install and use the bibbox software please follow these instructions:

##### Install Docker Engine, Git and prepatory Steps, Linux

Run the following commands:

`sudo apt-get update`<br>
`sudo apt -y install docker.io`<br>
`sudo apt install git -y`<br>
`sudo apt-get install docker.io -y`<br>
`sudo docker network create bibbox-default-network`<br>
`sudo groupadd docker`<br>
`sudo usermod -aG docker $USER`<br>
`newgrp docker`<br>

##### Install Docker Engine, MacOS, Windows

To install the newest docker-engine package follow the install dokumentation on the official docker website. 

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/).

##### Install docker-compose:

To install the newest docker-compose package follow the install dokumentation on the official docker website.

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/).

##### Install the BIBBOX (in the Beta only Debian based Linux Distributions are featured)

Create the bibbox location folder: <br>
`cd /opt`<br>
`sudo mkdir bibbox`<br>
`cd bibbox`<br>

Clone the bibbox system repository to opt bibbox. Therefore change your working directory to /opt/bibbox/ wit `cd /opt/bibbox/` and run

`sudo git clone https://github.com/bibbox/sys-bibbox.git`<br>
`sudo bash INSTALL.sh`<br>

Warning using INSTALL.sh will reinstall nvm and set the nodejs version used by npm to 14.16.0

Follow the instructions presented to you. 

##### URL/Domain-Settings

When asked to: <br>
```
Specify domainname + TLD (e.g. silicolabv4.bibbox.org):
```

you either: 

* Have to enter an existing domain forwarding requests towards the Machine your Bibbox is running on (and forward all Suburls aka: add  ServerAlias \*.your.domain.com to your Host config).
* Add the URL you want to use locally to your /etc/hosts file (see [https://linuxize.com/post/how-to-edit-your-hosts-file/](edit Hosts file)) which will only allow you to see the Bibbox Frontend. App Usage and installation wont work. 
* Best Option: Set up a DNS Service (e.g.:dnsmasque) to create a local domain to resolve your requests towards the internal Proxy-Server operated by the bibbox

As you may noted is is necccesary to forward all suburls towards the url you chose as well. This is neccesary since once you install an app it will be given an specific suburl or range of suburls where its Front-End will be reachable.

##### DNS service setup

For example one could use dnsmasq to accomplish the goal stated above.

* Install dnsmasq:<br>
`sudo apt-get install dnsmasq`
* Configure dnsmasq:<br>
First of all lets backup the default condifuration file dnsmasq creates.<br>
`sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.orig`<br>
Next we have to create a config file for dnsmasq:<br>
`sudo nano /etc/dnsmasq.conf`<br>
If you for example choose bibbox.local.test as the domainname the contents of this file will look like:

```
listen-address=127.0.0.1
expand-hosts
domain=bibbox.local.test
server=8.8.8.8
server=8.8.4.4
address=/bibbox.local.test/127.0.0.1
```

* `listen-address = 127.0.0.1` means that we listen to all traffic on the local computer<br>
* `expand-hosts` adds additional entries from the /etc/hosts file<br>
* `domain=bibbox.local.test` sets up the domain we need to resolve incoming traffic towards the internal bibbox proxy server<br>
* The `server=` parts are there to allow traffic not directed at our domain to be resolved to an public DNS server (googles DNS server in this case)
To test if everything is fine you can type `dnsmasq --test`, which will tell you: `dnsmasq: syntax check OK`, if you did not do anything wrong in `dnsmasq.conf`.<br>

Next in order to make the computer use the created DNS-Server, we need to set the namespace to the IP-Adress we provided in `listen-address`. To achieve this we can edit the `/etc/resolv.conf` file. We type `sudo nano /etc/resolv.conf` <br>
The file, for example could, look like:
```
\# This file is managed by man:systemd-resolved(8). Do not edit.
\#
\# This is a dynamic resolv.conf file for connecting local clients to the
\# internal DNS stub resolver of systemd-resolved. This file lists all
\# configured search domains.
\#
\# Run "resolvectl status" to see details about the uplink DNS servers
\# currently in use.
\#
\# Third party programs must not access this file directly, but only through the
\# symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a different way,
\# replace this symlink by a static file or a different symlink.
\#
\# See man:systemd-resolved.service(8) for details about the supported modes of
\# operation for /etc/resolv.conf.

\# nameserver 127.0.0.53
nameserver 127.0.0.1
options edns0 trust-ad
search medunigraz.at
```
Where in the original file only

```
nameserver 127.0.0.53
options edns0 trust-ad
search medunigraz.at
```

was present. We commented `\# nameserver 127.0.0.53` out and made the computer send information only to our defined server.<br>
* As the warning states to make this changes permanent we would have to add write protection towards this file:
This can be done by: `sudo chattr +i /etc/resolv.conf` In order to just try the Bibbox Sytem locally this can be ommited and everything will be reset on the next reboot. <br>
* NOTE: There could be more `nameserver=` directives present. In order for dnsmasq to work all of those need to be commented out like `\# nameserver`(just put an \# in front of them).

Lastly you have to add `dnsmasq` to your hosts file, since all the information about DNS-Hosts will be read from there:<br>
Open it by typing `sudo nano /etc/hosts`<br>
you will see something like thew following:<br>
```
127.0.0.1	localhost
127.0.1.1	simon-XPS
127.0.0.1	dnsmasq

\# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

The important part you need to add is `127.0.0.1	dnsmasq`.<br>
Once this is done you can save and we are done.

To test if we succeded we can use<br> 
`dig bibbox.local.test`.<br>
Output shuld look like this:

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

;; ANSWER SECTION:<br>
bibbox.local.test.	0	IN	A	127.0.0.1

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Di Okt 19 14:23:19 CEST 2021
;; MSG SIZE  rcvd: 62
```

Another option would be to type `nslookup bibbox.local.test`. Output should look like:

```
Server:		127.0.0.1
Address:	127.0.0.1#53

Name:	bibbox.local.test
Address: 127.0.0.1
```

* NOTE: Of course you can choose any domain-name you like. Just be shure to change `bibbox.local.test` to the desired domain-name.
* [https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/](https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/) has more info on the topic
* As always Google is your Friend. Simply Type any Error message you receive into the search bar.
