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

https://docs.docker.com/docker-for-mac/install/

##### Install Docker Compose

To install the newest docker-compose package follow the install dokumentation on the official docker website.

https://docs.docker.com/compose/install/


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

