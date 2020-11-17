# BIBBOX System

This container contains the [BIBBOX APP](http://bibbox.readthedocs.io/en/latest/admin-documentation/ "BIBBOX App Store"). 

## Initial Setup

To install the and use the bibbox software please follow these instructions:

##### Install Docker Engine

Run the following commands:

`sudo apt-get update`

`sudo apt -y install docker.io`

##### Install Docker Compose

To install the newest docker-compose package follow the insall dokumentation on the official docker website.

https://docs.docker.com/compose/install/

If you do not have installed the package curl, you can install it using 

`sudo apt-get -y install curl`

##### Install the BIBBOX

`wget -O - https://raw.githubusercontent.com/bibbox/sys-bibbox/master/install.sh | bash`

## Use the BIBBOX via CLI

Run 

`bibbox -h`

for further help.

The available commands are:

`bibbox install`

`bibbox start`

`bibbox stop`

`bibbox restart`

`bibbox copy`

`bibbox listApps`

`bibbox listInstances`

`bibbox remove`

`bibbox status`

`bibbox startSystem`

`bibbox stopSystem`

`bibbox restartSystem`


Use the flag -h or --help for a detailed app description.


A started app with a user defined instance name (instanceName) can be used under "localhost:8010/instanceName" in the browser.










# Requirements

For testing purposes we recommend a virtual machine with the following specifications:

* CPU cores: 4
* Memory: 8192 MB
* Disk space: 100 GB

**Production**

For production, please calculate the additional resources you will need, depending on the applications you are going to install within the BIBBOX.


# Installation

* Download and install VirtualBox -> <https://www.virtualbox.org>
* Download the latest BIBBOX version from  <http://bibbox.bbmri-eric.eu/resources/machine/>

## Import the image into VirtualBox

You can import the image with the following command:
```vboxmanage import path/to/bibbox-......ova```

If you have a user interface on your system (e.g. it's your local PC), follow these steps:

* Open up VirtualBox on your PC or Mac
* CLick on **File > Import Appliance...**
* Select the downloaded image and click **Continue**

## Start the machine

The BIBBOX demo VM is an Ubuntu server with an desktop (Graphical User Interface) for local testing. 


You can log in with username **v** and passwords **vendetta** and start using the BIBBOX in a local browser with the URL <http://bibbox.local.domain>.

Please be aware, that after the virtual machine has started, it takes several minutes until the server can be accessed.

If you want to access the server from a client, further configurations are necessary:

1. Choose the domain name, the server will be reachable: **replace.by.your.domain**

2. Login into the VM, either in the GUI or with an ssh, as configured in the VM network.

3. Make the following changes. 

    * In `/etc/bibbox/bibbox.cfg` 
    
        change the domain with
        
            sudo sed -i 's/bibbox.local.domain/replace.by.your.domain/g' *
            
            
    * In `/etc/apache2/sites-available`
    
        change the domain names in the proxy files with  
    
            sudo sed -i 's/bibbox.local.domain/replace.by.your.domain/g' *
            
    * And in `/etc/hosts`
    
        change
    
            127.0.0.1       eb3kit
            
        to the first part of your domain name
        
            127.0.0.1       replace
            
5. Finally run to make the changes take effect

        `sudo service apache2 stop` 
        `sudo service apache2 start` 
        `sudo service liferay stop` 
        `sudo service liferay start` 
        
    

## Network configuration

If your hosting provider offers you an administration panel for managing domains and subdomains, you should use that to point to your BIBBOX. Otherwise, if you use Apache, you can do it yourself using this guide:

1. On your server navigate to your apache configuration directory. On Linux base machines this defaults to **/etc/apache2/sites-available**.
2. Create a file named **005-bibbox.conf**. On Linux based systems you can do this with `nano 005-bibbox.conf`.
4. Copy this proxy configuration into the file, change the ServerName, ServerAlias and the port you configured for your virtual machine. You should also change the name of the log files according to your vm name. Then save with **CTRL + O** and **Enter**.

        <VirtualHost *:80>
            ServerName replace.by.your.domain
            ServerAlias *.replace.by.your.domain

            <Proxy *>
                Order deny,allow
                Allow from all
            </Proxy>

            ErrorLog ${APACHE_LOG_DIR}/bibbox.error.log

            # Possible values include: debug, info, notice, warn, error, crit,
            # alert, emerg.
            LogLevel debug

            CustomLog ${APACHE_LOG_DIR}/bibbox.access.log combined

            ProxyRequests           Off
            ProxyPreserveHost On
            ProxyPass               /api/kernels/       ws://127.0.0.1:80/api/kernels/
            ProxyPassReverse        /api/kernels/       ws://127.0.0.1:80/api/kernels/
            ProxyPass               /       	        http://127.0.0.1:80/
            ProxyPassReverse        /       	        http://127.0.0.1:80/
        </VirtualHost>

5. Now navigate to the **/etc/apache2/sites-enabled** directory and create a symbolic link to your new proxy file with `ln -s ../sites-available/005-bibbox.conf`. 
6. Next reload Apache to make it recognize your changes by running `service apache2 reload`.
7. You can now access the BIBBOX from anywhere in the web by calling your URL (e.g. **replace.by.your.domain**) in the browser's address bar!

## Domain Migration

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


![alt text](images/installation/bibbox.jpg "Welcome to BIBBOX")
