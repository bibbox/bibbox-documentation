#  BIBBOX System

This documentation describes BIBBOX Docker Framework. <br>

* If you already know your way arrund Docker and just want to install a local instance on Linux, jump to [Install  guide](installation_v4_bibbox_linux)

## Get started

* What is the BIBBOX Framework ?

The  BIBBOX Framework is a Basic Infrastructure Building Box (BIBBOX). As it originally targeted biobanks, it might sometimes also be known as a "Biobank in a Box". The BIBBOX provides the possibility to create and install apps, and also serve them directly towards the end-user. In the current state, we are building apps to support pathologists, bioinformaticians and biobanks in their daily work as well as in data management. The current framework mainly serves as a workflow demo SAAS-System and is not going into a productive state anytime soon. 

Check out the [User guide](user-guide) for further instructions on how to use the  BIBBOX.


* How does it work ?

The  BIBBOX itself consists of a series of Docker containers. The basic container structure is given by:

* Apache Proxyserver (Front-End Server and Proxy Server for the Apps)
* Backend (Flask Rest API for data exchange from Front-End) 
* Postgres (Permanent Data Storage)
* Celery (Asynchronous Task scheduling)
* Redis (Faster data-store for volatile and cache data)

<<<<<<< Updated upstream
For more information about each container, see the <a href="https://github.com/bibbox/sys-bibbox" target="_blank">sys-bibbox GitHub</a> repository.
=======
For more information about each container itsself see the <a href="https://github.com/bibbox/sys-bibbox" target="_blank">sys-bibbox GitHub</a> repository.
>>>>>>> Stashed changes

The detailed documentation is currently under construction and will be subsequently updated, see [Developer guide](developer-guide)








