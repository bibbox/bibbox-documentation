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


#### Front-End Details

* The Frontend is angular based and uses the ngrx-store principle to achieve the desired functionality ([https://ngrx.io/guide/store](https://ngrx.io/guide/store)).
* Code Structure: TODO

#### Set up Front-End Developement environment



