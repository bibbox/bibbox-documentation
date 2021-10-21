## Developer Documentation

#### Project structure and outline

The Bibbox docker system can mainly be divided into 3 parts:

* Front End
  * Angular Front End (Precompiled and mounted within the proxy container [https://github.com/bibbox/sys-bibbox/tree/master/frontend](https://github.com/bibbox/sys-bibbox/tree/master/frontend)) 

* Back End
  * Flask Backend container ([https://github.com/bibbox/sys-bibbox/tree/master/backend](https://github.com/bibbox/sys-bibbox/tree/master/backend))
  * Celery Container ([https://github.com/bibbox/sys-bibbox/tree/master/backend](https://github.com/bibbox/sys-bibbox/tree/master/backend) Celery and backend use the same Docker image)
  * Postgres DB ([https://github.com/bibbox/sys-bibbox/blob/master/postgresql/Dockerfile](https://github.com/bibbox/sys-bibbox/blob/master/postgresql/Dockerfile))
  * Redis Data Store (Official Redis Docker image. Used by Celery as cache store)
  * Adminer (Official Docker image for DB debugging)
  * Celery Monitor (Celery container with Frotnend to debug asynchronous tasks)
  * cadvisor (Monitoring for the complete docker-compose bibbox chain)

* Apacheproxy (Main linking centerpoint [https://github.com/bibbox/sys-bibbox/tree/master/apacheproxy](https://github.com/bibbox/sys-bibbox/tree/master/apacheproxy))

To get an idea how this works in an easier fashion you can have a look at [https://github.com/mrsan22/Angular-Flask-Docker-Skeleton](https://github.com/mrsan22/Angular-Flask-Docker-Skeleton), which served as base for the work done on the Bibbox docker framework. The nginx implementation was replaced by Apache since this offered a more convenient workflow.

#### Prequisites

The following applications need to be installed or are installed using the INSTALL.sh script:

* Docker and docker-compose
* nodejs, nvm (Node version manager) and npm (node package manager) (see INSTALL.sh for version details)
* Python 3.x (see requirements.txt in the repository for more information on python requirements)

#### Front-End Details

* The Frontend is angular based and uses the ngrx-store principle to achieve the desired functionality ([https://ngrx.io/guide/store](https://ngrx.io/guide/store)).
* Code Structure: TODO

#### Set up Front-End Developement environment

* **Easiset way (Linux Debian based):**<br> 
  * Install Bibbox locally under linux (See [Install Bibbox](installation_v4_bibbox_linux))
  * Install VS-Code (Goto [https://code.visualstudio.com/download](VSCode))
  * Set up local DNS Service (See [Install Bibbox](installation_v4_bibbox_linux))
  * Goto sys-bibbox/frontend 
  * Type `code .` into bash
  * After vs Code opens type `ng serve` 
  * Open the link the console shows you (If setup went correctly you should see a Bibbox interface without any errors) 
  * Change any code file and watch it change live in your browser.

* **NOTE**: Prequesite is that the DNS Service and Bibbox installation fully works

**Front end TODO'S**:
* Authentication for users: See tutorial here [https://mherman.org/blog/authentication-in-angular-with-ngrx/](https://mherman.org/blog/authentication-in-angular-with-ngrx/)
* Styling

