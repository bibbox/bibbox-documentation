#  BIBBOX System

This documentation describes BIBBOX Docker Framework. <br>

* If you already know your way arround Docker and just want to install a local instance on Linux jump to [Install  guide](installation_v4_bibbox_linux)

## Get started

* What is the BIBBOX Framework ?

The  BIBBOX Framework is a Basic Infrastructure Building Box (BIBBOX), because it was originally targeted towards biobanks it is sometimes also known as a Biobank in a Box. The BIBBOX provides the possibility to create install apps and serve them directly towards the End-User. In the current state we are building apps to support pathologists, bioinformaticians and biobanks in their direct work as well as in Data-Management. The current framework mainly serves as a workflow demo SAAS-System and is not going into a productive state anytime soon. 

Check out the [User guide](user-guide) for further instructions on how to use the  BIBBOX.


* How does it work ?

Basically the  BIBBOX itsself consists of a series of docker containers. The basic container strucutre is given by:

* Apache Proxyserver (Front-End Server and Proxy Server for the Apps)
* Backend (Flask Rest API for data exchange from Front-End) 
* Postgres (Permanent Data Storage)
* Celery (Asynchronous Task scheduling)
* Redis (Faster data-store for volatile and cache data)

For more information about each container itsself see the [sys-bibbox GitHub](https://github.com/ BIBBOX/sys- BIBBOX) repository.

The detailed documentation is currently under construction and will be subsequently updated see [Developer guide](developer-guide)








