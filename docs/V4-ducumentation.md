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


# Requirements

To install the Bibbox locally we recommend to use Linux or MacOS as operating system.

