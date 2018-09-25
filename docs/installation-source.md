## Requirements

### Hardware

**Minimum**

The following will show you the minimum requirements of the BIBBOX ubuntu machine. Please note, that installing any applications within BIBBOX will require additional resources!

* CPU cores: 1
* Memory: 4096 MB
* Disk space: 20 GB

**Recommended for Development**

For development purposes we recommend a virtual machine with the following specifications:

* CPU cores: 4
* Memory: 8192 MB
* Disk space: 100 GB

**Production**

For production, please calculate the additional resources you will need, depending on the applications you are going to install within the BIBBOX.


### Software

* The install scripts are tested with the UBUNTU 16.04.3 desktop version
* Make a user `v` password `vendetta`, or replace this by a root user of your choice 
* Download and install Git -> <https://git-scm.com/>
* Download and install openssh -> <https://help.ubuntu.com/lts/serverguide/openssh-server.html.en>




# Installation

Check locale:
Type `locale` in the commandline if the last line is "LC_ALL=" you need to change it to "LC_ALL=en_US.UTF-8"
for this just type: `sudo nano /etc/default/locale` and add "LC_ALL=en_US.UTF-8" to the end of the document. After this restart the system with `sudo shutdown -r now` after restart `locale` should return "LC_ALL=en_US.UTF-8" in the last line.

You have to specify a domain bibbox will be accessible in the installation script. This can be either a local domain, or a fully qualified domain name (FQDN). In case of a FQDN make sure that the DNS/proxy has wildcard domains enabled, i.e. also subdomains can be reached. 

`sudo git clone https://github.com/bibbox/kit-eb3kit.git /opt/bibbox-install`

`sudo chmod +x /opt/bibbox-install/*.sh`

`sudo /opt/bibbox-install/install-bibbox-local.sh -url put.here.your.domain -gui`

Watch the installation scripts, sometime apt-get makes some problems. 


# Login and administration

You can reach the BIBBOX framework with your choosen domain in any Webbrowser, and log into with one of the five default users and the password `graz2017`:

* bibboxadmin
* admin
* pi
* curator
* operator

If you want to make changes to the default configuration of the portal (e.g. change the title or logo), you need to log in as `bibboxadmin`.

When you enter the BIBBOX framework in commandline mode, all the components are installed under `/opt/bibbox`. What's going up there is described in the different componenets (github repositories). The Github repositories are structured according to the following naming conventions:

* **application-store**, this repository describes all applications (applications.json) and annotated lists of application for a 
    specific domain, called kits. Currently we provide one default kit, described in `eB3kit.json`. 

* **KIT-.... repositories** provides the blueprint how to build a "kit". A kit is a VM providing the base BIBBOX framework together with a set of predefined 
   tools (kit.json in the applications directory), pre-loaded docker images and (reference) databases.  Currently we provide one default kit: 
   `kit-eb3kit`.

* **APP-.... repositories** describes BIBBOX APPs. Each BIBBOX application is compodes by  of offical docker images or 
   docker images from the [BIBBOX docker hub](https://hub.docker.com/r/bibbox/). 

* **SYS-.... repositories**  source code running inside the virtual machine, which provides all services of the BIBBOX SaaS framework. 

    * **sys-bibbox-backend-liferay** backend of the BIBBOX portal, based on the liferay framework. Functionality for the management of 
     applications instances, the application store and the central user management. 
     
    * **sys-bibbox-frontend** all frontend code (React libraries). They are loaded by the backend at runtime. 
  
    * **sys-activities** service, for logging and synchronisation of all high level activities (installation, app delete, start/stop, etc.) 
          running as a docker container.  
          
    * **sys-idmapping**  service, for mapping of internal IDs and connection to external ID systems (B2Handle, EPIC) running a a docker container. 
  
    * **sys-bibbox-vmscripts** Collection of phyton scripts for management of applications, e.g. installation, port management, file management, setup script for the configuration of the portal, called after vagrant / puppet scripts are finished.
     
* **RES-.... repositories**  ressources. e.g. a common icon set for biobank applications. 



# Domain Migration

If you want to migrate from **SOME.OLD.DOMAIN** to **YOUR.NEW.DOMAIN**, login into your VM and make the following steps 

* Stop the apache service

`sudo service apache2 stop`

* Replace all **SOME.OLD.DOMAIN** in the proxy files

`cd /etc/apache2?`

`sudo cp -r sites-available sites-available-back`

`cd sites-available`

`sed -i 's/SOME.OLD.DOMAIN/YOUR.NEW.DOMAIN/g' *`

`sudo service apache2 start`

* Change to config for the portal

`cd /etc/bibbox`

`sudo service liferay stop`

`sudo sed -i 's/SOME.OLD.DOMAIN/YOUR.NEW.DOMAIN/g' bibbox.cfg`

`sudo service liferay start`
