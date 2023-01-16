#  BIBBOX user guide

## User guide

The first page of the BIBBOX shows you the store of available Apps.

![Starting Screen](images/v4/v4_interface_startscreen.png)

By clicking onto the [Store](https://demo.bibbox.org/applications)-Button on top you will get to the app overview. 

![App Store](images/v4/v4_interface_appstore.png)

To learn more about installing an App goto [Install Apps](installation_v4_apps)

Clicking onto the Instances-Button will take you to the currently installed instances.

* NOTE: If you freshly installed your  BIBBOX locally you might have not installed any instances and this screen is empty.

![App Instances](images/v4/v4_interface_appinstances.png)

The screen shows the currently installed instances and offers more possibilities. You can:

* Call the Apps UI via the switch button on the top left of the apps tile
* See the Apps dashboard by clicking the gear symbol on the bottom left of the Apps tile
* Call the logs of the singular Docker containers by clicking the book symbol in the bottom-middle of the apps tile
* The light signifies the status of the app - Green: Running; Yellow: Installing; Red: Stopped

You might noticed, that on all screens there is a little green hook on the very top right of the page. This is a short link to the last page of the third page of top navigation bar: The activity menu. 

![Activities](images/v4/v4_interface_activities.png)

Here all the recently triggered actions can be reviewed. Additionally the status

* Hook &rarr; suceeded
* Red cross sign &rarr; failed
* Spinning Bar circle &rarr; task in Progression

is shown here. The dropdown menu alwys present on the top right just gives you a short update on the general status of recent event, while in the Activities tab each event can be expanded and contains a short descriptions about the nature of the given error.

As this might is not enough one can conveniently access the system logs from the main navigation as well. This tab shows the docker-logs of the main system containers.

![Activities](images/v4/v4_interface_sys_logs.png)

Each log can be expanded by clicking on it and shows the logs that are recorded by each individual docker container

* NOTE: This is also the fastest way to figure out the main structure of the  BIBBOX system
* NOTE: What is logged exactly is configured in the Docker Container definitions and can be found within the Dockerfiles within the GitHub repository ([apacheproxy/](https://github.com/bibbox/sys-bibbox/tree/master/apacheproxy) as an example for the Apache Proxy Server container)

As the information provided by the logs is sometimes not enough each App can be troubleshot in more detail by visiting the Dashboard (it can be accesed in the Instances Tab)

![Dashboard](images/v4/v4_interface_app_dashboard.png)

* NOTE: The most important part is the possibility to stop or restart apps.
* NOTE: Once an app has been stoped the button turns towards delete. THIS IS THE ONLY WAY TO DELETE APPS
* Additionally we can enter or read descriptions that are shown within the apps tile at the Instances tab. Further we can see all the available URL's for the given app. For example some apps include additional tools for debuging or advacned form of integration. An example would be an additional Adminer service that can be accesed to see the database.

Last we can also access the App-Container Docker logs from the Dashboard or via the Apps tile from the Instances tab (book symbol see Instances tab above). 

![App-Logs](images/v4/v4_interface_app_logs.png)

Here we can see a more detailed log of every container that is contributing to the given app. 

## Install Apps

Apps can be installed from the Store page.

* NOTE: After first installation of the framework the system automatically fetches the list of available apps this can take a few moments.

![Installable Apps](images/v4/v4_install_testapps.png)

Once you selected an app by clicking on its icon you will see a new window pop up. Since there can be different versions of an App available you have to select your version

![Install Step I](images/v4/v4_install_screen_1.png)

After this click Install as shown on top of the image above. Next you will have to fill the parameters neccesary to actually run the app.<br>
The parameters themselves can be checked at the App's GitHub repository. In the example the selected App is [Omero](https://www.openmicroscopy.org/omero/).<br>
After clicking onto Install you will be taken to the parameter setting screen:

![Install Step II](images/v4/v4_install_screen_2.png)

To get to the GitHub repository outlining the parameters go to: [app-omero](https://github.com/bibbox/app-omero/tree/v5-6-x)



