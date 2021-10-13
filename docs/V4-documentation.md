# BIBBOX System

This dcumentation describes the new angular based Bibbox Docker Framework

## Initial Setup

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

[https://docs.docker.com/engine/install/](Docker Engine install instructions).

##### Install Docker Compose

To install the newest docker-compose package follow the install dokumentation on the official docker website.

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/).

##### Install the BIBBOX (in the Beta only Debian based Linux Distributions are featured)

Create the bibbox location folder
`cd /opt`
`sudo mkdir bibbox`
`cd bibbox`

Clone the bibbox system repository to opt bibbox. Therefore change your working directory to /opt/bibbox/ wit `cd /opt/bibbox/` and run

`sudo git clone https://github.com/bibbox/sys-bibbox.git`<br>
`sudo bash INSTALL.sh`<br>

Follow the instructions presented to you. 

##### URL-Settings

When asked to: <br>
Specify domainname + TLD (e.g. silicolabv4.bibbox.org):  <br>
you either: 

*Have to enter an existing domain forwarding requests towards this Machine (and forward all Suburls aka: add  ServerAlias \*.your.domain.com to your Host config)
*Add the URL you want to use locally to your /etc/hosts file (see [https://linuxize.com/post/how-to-edit-your-hosts-file/](edit Hosts file))
*Set up an Webserver (Apache or Nginx) to forward your requests towards the internal Proxy-Server operated by the bibbox

As you may noted is is necccesary to forward all suburls towards the url you chose as well. This is neccesary since once you install an app it will be given an specific suburl or range of suburls where its Front-End will be reachable.

##### Webserver Setup 

TODO !

##### Installing apps

Once you did the above steps correctly you should be able to connect to your local Bibbox installation via the URL you chose.
You should see [http://silicolabv4.bibbox.org/](Bibbox Example).








