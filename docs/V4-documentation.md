# BIBBOX System

This documentation describes the new CLI Version of the Bibbox.
The Bibbox V4 can be installed locally and used via a command line interface (CLI).


## Initial Setup

To install and use the bibbox software please follow these instructions:

##### Install Docker Engine, Linux

Run the following commands:

`sudo apt-get update`

`sudo apt -y install docker.io`

##### Install Docker Engine, MacOS

To install the newest docker-engine package follow the install dokumentation on the official docker website. 
The docker engine for MacOS comes with docker desktop.

[https://docs.docker.com/docker-for-mac/install/](https://docs.docker.com/docker-for-mac/install/).

##### Install Docker Compose

To install the newest docker-compose package follow the install dokumentation on the official docker website.

[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/).

##### Install the BIBBOX

Create the bibbox location folder

`mkdir opt/bibbox/`

Clone the bibbox system repository to opt bibbox. Therefore change your working directory to /opt/bibbox/ wit `cd /opt/bibbox/` and run

`git clone https://github.com/bibbox/sys-bibbox.git`.

To be able to use the commands within the current shell, add the script CLIFunctions.sh to the source with 

`source /opt/bibbox/sys-bibbox/CLIFunctions.sh`.

To source the functions automatically every time you open the shell you can add the functions by adding the line

`source /opt/bibbox/sys-bibbox/CLIFunctions.sh`

at the end of the file `~/.bashrc` in the home directory of the current user. `~/.bashrc` is executed by bash for non login shells. Depending on your settings it can be necessary to use the files `~/.bash_profile` or `~/.bash_login` to add the source atomatically.

This can be implemented by using the command

`grep -qxF "source /opt/bibbox/sys-bibbox/CLIFunctions.sh" ~/.bashrc || echo "source /opt/bibbox/sys-bibbox/CLIFunctions.sh" >> ~/.bashrc`

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

`bibbox checkSystem`

`bibbox info`


Use the flag -h or --help for a detailed app description.


A started app with a user defined instance name (instanceName) can be used under "localhost:8010/instanceName" in the browser.

# CLI Function Documentation

 ## bibbox install 

DESCRIPTION

    Installs a new Bibbox app with a specific unique name. before installation, the available versions and the required user parameter can are accessible via the command `bibbox info`.

SYNTAX

    bibbox install <appname> -n <instancename> -v <version> -p <paarameters>
  
OPTIONS

    -h, --help                    Funcion help

    -bv, --bibboxversion          Print script information

    -n, --name                    Specify the name of the installed instance. The instance name can also be set without flag as the second function argument.

    -v, --version                 Specify the app version you want to install. This flag is optional. If not specified, the newest version gets installed.

    -p, --params                  The app parameters can be passed to this function automatically. This flag is optional. If not specified, the app parameters can be set to default or set interactively.

    -d, --default                 If this flag is set, the default app parameters are used for installation.

EXAMPLES

    bibbox install nextcloud -n mynextcloud -v v20-0-x_tng -p 'nextcloud,nextcloud'

    bibbox install nextcloud -n mynextcloud -d

    bibbox install nextcloud mynextcloud


## bibbox start

DESCRIPTION

    Starts the wanted Bibbox app container

SYNTAX

    bibbox start <instancename>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox start myseeddms

## bibbox stop

DESCRIPTION

    Stops the wanted Bibbox app container

SYNTAX

    bibbox stop <instancename>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox stop myseeddms
    
## bibbox restart

DESCRIPTION

    Restarts the wanted Bibbox app container

SYNTAX

    bibbox restart <instancename>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox restart myseeddms
    
    
## bibbox copy

DESCRIPTION

    Copies the wanted Bibbox app container

SYNTAX

    bibbox copy <instancename>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox copy myseeddms
    

## bibbox listApps

DESCRIPTION

    Lists all available applications
    
SYNTAX

    bibbox listApps
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox listApps


## bibbox listInstances

DESCRIPTION

    Lists all installed applications
    
SYNTAX

    bibbox listInstances
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox listInstances
    
    
## bibbox remove

DESCRIPTION

    Removes the wanted Bibbox app container

SYNTAX

    bibbox remove <instancename>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox remove myseeddms
    
    
## bibbox status

DESCRIPTION

    Lists the status of a specific app
    
SYNTAX

    bibbox status
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox status
    
    
## bibbox startSystem

DESCRIPTION

    Starts the Bibbox system
    
SYNTAX

    bibbox startSystem
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox startSystem

## bibbox stopSystem

DESCRIPTION

    Stops the Bibbox system
    
SYNTAX

    bibbox stopSystem
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox stopSystem
 

## bibbox restartSystem

DESCRIPTION

    Restarts the Bibbox system
    
SYNTAX

    bibbox restartSystem
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox restartSystem
    
## bibbox checkSystem

DESCRIPTION

    Checks the Bibbox system id all required services are running correctly and if the required packages are installed in the required versions.
    
SYNTAX

    bibbox checkSystem
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox checkSystem
    
    
## bibbox info

DESCRIPTION

    Returns install information about a specific application. This information contains the available versions, the input parameters etc.    
    
SYNTAX

    bibbox info <appname>
  
OPTIONS

    -h, --help                    Function help

    -v, --version                 Print script information

EXAMPLES

    bibbox info seeddms

# Requirements

To install the Bibbox locally we recommend to use Linux or MacOS as operating system.

#  Apps Creators Manual

## How to join the team

Contact [Heimo Müller](mailto:heimo.mueller@medunigraz.at), [Robert Reihs](mailto:robert.reihs@medunigraz.at), [Markus Plass](mailto:markus.plass@student.tugraz.at) or [Stefan Herdy](mailto:stefan.herdy@medunigraz.at). Any of them can add you to the Github team of an App repository. 

## Anatomy of an App

An **App** is described within a BIBBOX Github repository. By convention the name of the repository starts with the prefix **"app-"**
A template repository can be found at:  <https://github.com/bibbox/app-template>


An **App** consists at least of the following files and directories, please never change the name of these files!

* README.md

    The default Github readme file shoud contain information about the used official docker images and docker images from the [BIBBOX dockerhub](https://hub.docker.com/r/bibbox/). In addition you should describe all mounted volumes and their content.            

  
* INSTALL-APP.md

    Install instruction for the APP to follow after the first installation step (docker-compose up) is finished. This typicaly describes application specific configuration tasks. A link to this file is given in the Dashboard of the installed App. 
    
  
* appinfo.json
    
    Specifies Information about the App as displayed in the BIBBOX App Store. 
    
``` code
    {
            "name": "A long name of the Application, shown in the App Store",
            "short_name": "APP short name",
            "version": "V.1.0",
            "description": "Long description of the Application shown in Store, can be multiline",
            "short_description": "Short description of the Application shown in Store",
            "catalogue_url": "URL to biobankapps, if applicaple",
            "application_url": "URL to App official gace",
            "tags": ["Tag1", "Tag2"]
    }
```

* docker-compose-template.yml

    Based on this file the docker-compose.yml will be generated. The variables §§INSTANCE, §§PORT and all other environment and configuration variables starting with "§§" will be replaced during the installation. Each template for a docker compose file should link to the `bibbox-default-network` network.
    
```
 
    version: '3'
    
    networks:
        bibbox-default-network:
          external: true
    
    services:
    
      §§INSTANCE-container1:
        image: bibbox/app-image
        container_name:  §§INSTANCE-container1
        restart: unless-stopped
        networks:
          - bibbox-default-network
        links:
          - §§INSTANCE-app-db:app-db
        ports:
          - "§§PORT1:80"
        depends_on:
          - §§INSTANCE-container1-db
        volumes: 
          - ./var/app-config:/var/app-config    

    §§INSTANCE-container1-db:
      image: bibbox/app-image2
      container_name:  §§INSTANCE-container2
      restart: unless-stopped
      networks:
        - bibbox-default-network
      ports:
        - "§§PORT2:8000"
      volumes: 
        - ./var/app-config:/var/app-config    
      §§INSTANCE-app-db:
        image: mysql:8
        container_name: §§INSTANCE-limesurvey-db
        restart: unless-stopped
        networks:
          - bibbox-default-network
        user: root
        environment:
          - MYSQL_ROOT_PASSWORD=thispasswordisneverusededoutsidethecontainer
          - MYSQL_DATABASE=§§MYSQL_DATABASE_NAME
          - MYSQL_USER=§§MYSQL_DATABASE_USER
          - MYSQL_PASSWORD=§§MYSQL_DATABASE_PASSWORD
        volumes: 
          - ./var/app-data:/var/app-data
        
    
```


* environment-parameters.json

    Environment parameters for the docker-compose-template file. The user can set the values for these parameters in a GUI during the installation of an App. 
   
    
```json
    [
       {
          "id":"NAME_AS_IN_DOCKER_TEMPLATE_1",
          "display_name":"Name Displayed in GUI at the Installation",
          "type":"text, number, password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_NAME",
          "display_name":"Name of the mysql database",
          "type":"text,",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_USER",
          "display_name":"Name of the mysql user",
          "type":"text",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_PASSWORD",
          "display_name":"Password of mySQL user",
          "type":"password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       }

    ]
```

* configuration-parameters.json

    Configuration parameters for the docker-compose-template file. The user can set the values for these parameters in a GUI during the installation of an App and also in an later interactive configuration panel (will be provided in the next release). 
    
``` json

    [
       {
          "id":"NAME_AS_IN_DOCKER_TEMPLATE_1",
          "display_name":"Name displayed in GUI at the Installation and Configuration",
          "type":"text, number, password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"NAME_AS_IN_DOCKER_TEMPLATE_2",
          "display_name":"Name displayed in GUI at the Installation and Configuration",
          "type":"text, number, password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       }
    ]
    
```


* icon.png

    Icon of the App in the application store and in the application dashboard. Please use a square format, e.g. 512x512 pixeland PNG with a transparency channel.
    
  
* sys-info.json

    A list of containers, that must run in order display the container as "running" in the application dashboard. In addtion a list of "non running" containers can be specified. The names must be the same as the service names in the docker-compose-template.yml. 

    
``` json
    {
      runningcontainers:["§§INSTANCE-appcontainer1", "§§INSTANCE-appcontainer2"],
      supportcontainers:["§§INSTANCE-app-data"]    
    }
```
    


* images

Repository containing all docker images used in the docker-compose-template.yml (apart from offcial docker images). Per na,ming convention, all inages of an app are contained in repositories starting with "img-". For each docker image a sub directory containing the Dockerfile and configs has the created. In the BIBBOX dockerhub these files are used to build the docker images. Please not, that for versioned Apps both in the dockerhub and in the docker-compose-template.yml version tags has to be used. 


## Versioning

Each App should be versioned. We distinguish between

* **Development Version** generated from the master branch of the repository. The developmemt version is identified by the tag `development` in the kit description,  

* **Production Versions** generated from a specific release in the repository. For each major release. i.e. given by a new version of dockerized software tool, a new branch should be generated in the repository. Please note, that the tag name for the Github release should not contain dots as seperators, please use "_" instead. 

When creating a production version, you should make the follwoing steps. Please make it exactly in this order, 
otherwise the tagging of the bibbox docker/hub and bibbox github will get confused.

1. Generate a new branch in github, if you plan to release a major version. 

2. Update all the files for the anticipated version, don't forget to update *appinfo.json*. 

3. Set in the docker compose template file (docker-compose-template.yml) 
the tags for the docker images. Please not, that ALL used images should be tagged with an specific version, don't use the 'latest" tag, as this could break your APP in the future. 

4. Tag the version in GITHUB, please don't use dots to seperate subversion but "_" (otherwise versions cannot be stored in the filesystem on the BIBBOX VM) 

5. Add the tag in the DOCKER hub to build tagged images (press SAVE before TRIGGER)

6. Edit in the used kit, e.g. *eB3kit.json* the version information. This file can be found in the *application-store* repository. 



## Register an App

For the registration of an App two configuration files have to be extended:

* [bibboxv4.json](https://github.com/bibbox/application-store/blob/master/applications.json) maps a Github repository to a human readable name of the App 







