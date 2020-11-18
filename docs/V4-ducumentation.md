# BIBBOX System

This documentation describes the new Version of the Bibbox.

## Initial Setup, Linux

To install and use the bibbox software please follow these instructions:

##### Install Docker Engine

Run the following commands:

`sudo apt-get update`

`sudo apt -y install docker.io`

##### Install Docker Compose

To install the newest docker-compose package follow the install dokumentation on the official docker website.

https://docs.docker.com/compose/install/

If you do not have installed the package curl, you can install it using 

`sudo apt-get -y install curl`

##### Install the BIBBOX

Create the bibbox location folder

`mkdir opt/bibbox/`

Clone the bibbox system repository to opt bibbox. Therefore change your working directory to /opt/bibbox/ wit `cd /opt/bibbox/` and run

`git clone https://github.com/bibbox/sys-bibbox.git`.

To be able to use the commands within the current shell, add the script CLIFunctions.sh to the source with 

`source /opt/bibbox/sys-bibbox/CLIFunctions.sh`.

To source the functions automatically every time you open the shell you can add the functions is by adding the line

`source /opt/bibbox/sys-bibbox/CLIFunctions.sh`

at the end of the file `~/.bashrc` in the home directory of the current user.


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


Use the flag -h or --help for a detailed app description.


A started app with a user defined instance name (instanceName) can be used under "localhost:8010/instanceName" in the browser.




# Requirements

To install the Bibbox locally we recommend to use Linux or MacOS as operating system.

