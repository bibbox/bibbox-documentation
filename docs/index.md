# BIBBOX System:

This documentation describes the new angular based Bibbox Docker Framework. <br>
For the old framework documentation see the section **V3 - Old Documentation** below 

## Initial Setup:

To install and use the bibbox software please follow these instructions:

##### Install Docker Engine, Git and prepatory Steps, Linux:

Run the following commands:

`sudo apt-get update`<br>
`sudo apt -y install docker.io`<br>
`sudo apt install git -y`<br>
`sudo apt-get install docker.io -y`<br>
`sudo docker network create bibbox-default-network`<br>
`sudo groupadd docker`<br>
`sudo usermod -aG docker $USER`<br>
`newgrp docker`<br>

##### Install Docker Engine, MacOS, Windows:

To install the newest docker-engine package follow the install dokumentation on the official docker website. 

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/).

##### Install docker-compose:

To install the newest docker-compose package follow the install dokumentation on the official docker website.

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/).

##### Install the BIBBOX (in the Beta only Debian based Linux Distributions are featured):

Create the bibbox location folder
`cd /opt`
`sudo mkdir bibbox`
`cd bibbox`

Clone the bibbox system repository to opt bibbox. Therefore change your working directory to /opt/bibbox/ wit `cd /opt/bibbox/` and run

`sudo git clone https://github.com/bibbox/sys-bibbox.git`<br>
`sudo bash INSTALL.sh`<br>

Warning using INSTALL.sh will reinstall nvm and set the nodejs version used by npm to 14.16.0

Follow the instructions presented to you. 

##### URL/Domain-Settings:

When asked to: <br>
Specify domainname + TLD (e.g. silicolabv4.bibbox.org):  <br>
you either: 

* Have to enter an existing domain forwarding requests towards the Machine your Bibbox is running on (and forward all Suburls aka: add  ServerAlias \*.your.domain.com to your Host config).
* Add the URL you want to use locally to your /etc/hosts file (see [https://linuxize.com/post/how-to-edit-your-hosts-file/](edit Hosts file))
* Set up a DNS Service (dnsmasque) to create a local domain to resolve your requests towards the internal Proxy-Server operated by the bibbox

As you may noted is is necccesary to forward all suburls towards the url you chose as well. This is neccesary since once you install an app it will be given an specific suburl or range of suburls where its Front-End will be reachable.

##### DNS service setup:

For example one could use dnsmasq to accomplish the goal stated above.

* Install dnsmasq:<br>
`sudo apt-get install dnsmasq`
* Configure dnsmasq:<br>
First of all lets backup the default condifuration file dnsmasq creates. 
`sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.orig`
Next we have to create a config file for dnsmasq
`sudo nano /etc/dnsmasq.conf`
If you for example choose bibbox.local.test as the domainname the contents of this file will look like:<br>
```
listen-address=127.0.0.1<br>
expand-hosts<br>
domain=bibbox.local.test<br>
server=8.8.8.8<br>
server=8.8.4.4<br>
address=/bibbox.local.test/127.0.0.1
```

So line by line this means:<br> 
* `listen-address = 127.0.0.1` means that we listen to all traffic on the local computer<br>
* `expand-hosts` adds additional entries from the /etc/hosts file
* `domain=bibbox.local.test` sets up the domain we need to resolve incoming traffic towards the internal bibbox proxy server
* The `server=` parts are there to allow traffic not directed at our domain to be resolved to an public DNS server (googles DNS server in this case)
To test if everything is fine you can type `dnsmasq --test` whic will tell you: dnsmasq: syntax check OK, if you did not do anything wrong in the file above.

Next in order to make the computer use the created DNS-Server we need to set the namespace to the IP-Adress we provided in `listen-address` to achieve this we can edit the `/etc/resolv.conf`file.<br>
For example this could look like:
```
\# This file is managed by man:systemd-resolved(8). Do not edit.<br>
\#<br>
\# This is a dynamic resolv.conf file for connecting local clients to the<br>
\# internal DNS stub resolver of systemd-resolved. This file lists all<br>
\# configured search domains.<br>
\#<br>
\# Run "resolvectl status" to see details about the uplink DNS servers<br>
\# currently in use.<br>
\#<br>
\# Third party programs must not access this file directly, but only through the<br>
\# symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a different way,<br>
\# replace this symlink by a static file or a different symlink.<br>
\#
\# See man:systemd-resolved.service(8) for details about the supported modes of<br>
\# operation for /etc/resolv.conf.<br>

\# nameserver 127.0.0.53<br>
nameserver 127.0.0.1<br>
options edns0 trust-ad<br>
search medunigraz.at
```
Where in the original file only:<br>
```
nameserver 127.0.0.53<br>
options edns0 trust-ad<br>
search medunigraz.at`<br>
```

was present we commented `\# nameserver 127.0.0.53` out and made the computer send information only to our defined server.<br>
* As the warning states to make this changes permanent we would have to add write protection towards this file:
This can be done by:<br>
`sudo chattr +i /etc/resolv.conf'<br>
In order to just try the Bibbox Sytem locally this can be ommited. Further note that there could be more `nameserver=` directives present<br>
In order for dnsmasq to work all of those need to be commented out like `\# nameserver`(just put an \# in front of them).

Lastly you add dnsmasq to your hosts file sice all the information about DNS-Hosts will be read from there:<br>
`sudo nano /etc/hosts`<br>
you will see something like thew following:<br>
```
127.0.0.1	localhost<br>
127.0.1.1	simon-XPS<br>
127.0.0.1	dnsmasq<br>

\# The following lines are desirable for IPv6 capable hosts<br>
::1     ip6-localhost ip6-loopback<br>
fe00::0 ip6-localnet<br>
ff00::0 ip6-mcastprefix<br>
ff02::1 ip6-allnodes<br>
ff02::2 ip6-allrouters<br>
```

The important part you need to add is `127.0.0.1	dnsmasq`.<br>
Once this is done you can save and we are done.

To test if we succeded we can either use the `dig bibbox.local.test` command. Outout shuld look like this:

```
; <<>> DiG 9.16.1-Ubuntu <<>> bibbox.local.test<br>
;; global options: +cmd<br>
;; Got answer:<br>
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36047<br>
;; flags: qr aa rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1<br>

;; OPT PSEUDOSECTION:<br>
; EDNS: version: 0, flags:; udp: 4096<br>
;; QUESTION SECTION:<br>
;bibbox.local.test.		IN	A<br>

;; ANSWER SECTION:<br>
bibbox.local.test.	0	IN	A	127.0.0.1<br>

;; Query time: 0 msec<br>
;; SERVER: 127.0.0.1#53(127.0.0.1)<br>
;; WHEN: Di Okt 19 14:23:19 CEST 2021<br>
;; MSG SIZE  rcvd: 62<br>`
```

Another option would be `nslookup bibbox.local.test`. Output should look like.

```
Server:		127.0.0.1<br>
Address:	127.0.0.1#53<br>

Name:	bibbox.local.test<br>
Address: 127.0.0.1
```

* NOTE: Of course you can choose any domain name you like. Just be shure to change `bibbox.local.test` to the desired Domain.
* [https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/](https://www.tecmint.com/setup-a-dns-dhcp-server-using-dnsmasq-on-centos-rhel/) has more info on the topic
* As always Google is your Friend. Simply Type any Error message you receive into the search bar.

##### Installing apps

Once you did the above steps correctly you should be able to connect to your local Bibbox installation via the URL/domain you chose.
You should see an interface as at [http://silicolabv4.bibbox.org/](http://silicolabv4.bibbox.org/).








