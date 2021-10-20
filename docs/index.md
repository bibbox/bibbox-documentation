# BIBBOX System

This documentation describes the new angular based Bibbox Docker Framework. <br>
For the old framework documentation see the section **V3 - Old Documentation**

* If you already know your way arround Docker and just want to install a local instance on Linux jump to [Install Bibbox](installation_v4_bibbox_linux.md)

## Get started

* What is the Bibbox Framework ?

The Bibbox Framework originally was created to serve as a Biobank in a Box (hence Bibbox). So this means it provides the possibility to create install apps and serve them directly towards the End-User. In the current state we are building apps to support Pathologists and Biobanks in their direct work as well as in Data-Management. The current Framework mainly serves as a workflow demo SAAS-System and is not going into a productive state anytime soon. 

##### Bibbox user interface overview
To get an overview over the new interface you can got to [http://silicolabv4.bibbox.org/](http://silicolabv4.bibbox.org/).

![Starting Screen](images/v4/v4_interface_startscreen.png)

* NOTE: The user management is currently under developement and not implemented within the Backend.

By clicking onto the Store-Button on top you will get to the app overview. ([http://silicolabv4.bibbox.org/applications](http://silicolabv4.bibbox.org/applications)).

![App Store](images/v4/v4_interface_appstore.png)

To learn more about installing an App goto [Install Apps](installation_v4_apps.md)

Clicking onto the Instances-Button will take you to the currently running instances ([http://silicolabv4.bibbox.org/instances](http://silicolabv4.bibbox.org/instances).<br> 
* NOTE: If you installed your Bibbox locally you might have not installed any instances and this screen is empty.

![App Instances](images/v4/v4_interface_appinstances.png)

The screen shows the currently running instances and offers more possibilities. You can:
* Call the Apps UI via the switch Button on the top left of the apps tile
* See the Apps dashboard by clicking the Gear Symbol on the bottom left of the apps tile
* Call the logs of the singular Docker containers by clicking the Book Symbol in the bottom-middle of the apps tile





