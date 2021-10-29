## Developer Documentation

#### Project structure and outline

The Bibbox docker system can mainly be divided into 3 parts:

* **Front End**
    * Angular Front End (Precompiled and mounted within the proxy container [https://github.com/bibbox/sys-bibbox/tree/master/frontend](https://github.com/bibbox/sys-bibbox/tree/master/frontend)) 

* **Back End**
    * Flask Backend container ([https://github.com/bibbox/sys-bibbox/tree/master/backend](https://github.com/bibbox/sys-bibbox/tree/master/backend))
    * Celery Container ([https://github.com/bibbox/sys-bibbox/tree/master/backend](https://github.com/bibbox/sys-bibbox/tree/master/backend) Celery and backend use the same Docker image)
    * Postgres DB ([https://github.com/bibbox/sys-bibbox/blob/master/postgresql/Dockerfile](https://github.com/bibbox/sys-bibbox/blob/master/postgresql/Dockerfile))
    * Redis Data Store (Official Redis Docker image. Used by Celery as cache store)
    * Adminer (Official Docker image for DB debugging)
    * Celery Monitor (Celery container with Frotnend to debug asynchronous tasks)
    * cadvisor (Monitoring for the complete docker-compose bibbox chain)

* **Apacheproxy** (Main linking centerpoint [https://github.com/bibbox/sys-bibbox/tree/master/apacheproxy](https://github.com/bibbox/sys-bibbox/tree/master/apacheproxy))

To get an idea how this works in an easier fashion you can have a look at [https://github.com/mrsan22/Angular-Flask-Docker-Skeleton](https://github.com/mrsan22/Angular-Flask-Docker-Skeleton), which served as base for the work done on the Bibbox docker framework. The nginx implementation was replaced by Apache since this offered a more convenient workflow.

#### Prequisites

The following applications need to be installed or are installed using the INSTALL.sh script:

* Docker and docker-compose
* nodejs, nvm (Node version manager) and npm (node package manager) (see INSTALL.sh for version details)
* Python 3.x (see requirements.txt in the repository for more information on python requirements)

#### Front-End Details

* The Frontend is angular based and uses the ngrx-store principle to achieve the desired functionality ([https://ngrx.io/guide/store](https://ngrx.io/guide/store)).
**Code Structure:**
* ***Part I: Everything visible in the Frontend is a component uses functions defined in the ngrx store part.***<br>
sys-bibbox/frontend/src<br>
├── app<br>
│   ├── app.module.ts<br>
│   ├── app-routing.module.ts<br>
│   ├── commons.ts<br>
│   ├── components<br>
│   │   ├── about<br>
│   │   │   ├── contact<br>
│   │   │   │   ├── contact.component.html<br>
│   │   │   │   ├── contact.component.scss<br>
│   │   │   │   ├── contact.component.spec.ts<br>
│   │   │   │   └── contact.component.ts<br>
│   │   │   ├── imprint<br>
│   │   │   │   ├── imprint.component.html<br>
│   │   │   │   ├── imprint.component.scss<br>
│   │   │   │   ├── imprint.component.spec.ts<br>
│   │   │   │   └── imprint.component.ts<br>
│   │   │   └── partners<br>
│   │   │       ├── partners.component.html<br>
│   │   │       ├── partners.component.scss<br>
│   │   │       ├── partners.component.spec.ts<br>
│   │   │       └── partners.component.ts<br>
│   │   ├── activities<br>
│   │   │   ├── activities.component.html<br>
│   │   │   ├── activities.component.scss<br>
│   │   │   ├── activities.component.spec.ts<br>
│   │   │   ├── activities.component.ts<br>
│   │   │   └── activity-menu-overlay<br>
│   │   │       ├── activity-menu-overlay.component.html<br>
│   │   │       ├── activity-menu-overlay.component.scss<br>
│   │   │       ├── activity-menu-overlay.component.spec.ts<br>
│   │   │       └── activity-menu-overlay.component.ts<br>
│   │   ├── applications<br>
│   │   │   ├── application-group<br>
│   │   │   │   ├── application-group.component.html<br>
│   │   │   │   ├── application-group.component.scss<br>
│   │   │   │   ├── application-group.component.spec.ts<br>
│   │   │   │   ├── application-group.component.ts<br>
│   │   │   │   └── application-tile<br>
│   │   │   │       ├── application-tile.component.html<br>
│   │   │   │       ├── application-tile.component.scss<br>
│   │   │   │       ├── application-tile.component.spec.ts<br>
│   │   │   │       └── application-tile.component.ts<br>
│   │   │   ├── applications.component.html<br>
│   │   │   ├── applications.component.scss<br>
│   │   │   ├── applications.component.spec.ts<br>
│   │   │   ├── applications.component.ts<br>
│   │   │   ├── install-screen<br>
│   │   │   │   ├── install-screen.component.html<br>
│   │   │   │   ├── install-screen.component.scss<br>
│   │   │   │   ├── install-screen.component.spec.ts<br>
│   │   │   │   └── install-screen.component.ts<br>
│   │   │   └── install-screen-dialog<br>
│   │   │       ├── install-screen-dialog.component.html<br>
│   │   │       ├── install-screen-dialog.component.scss<br>
│   │   │       ├── install-screen-dialog.component.spec.ts<br>
│   │   │       └── install-screen-dialog.component.ts<br>
│   │   ├── app-scaffold<br>
│   │   │   ├── app.component.html<br>
│   │   │   ├── app.component.scss<br>
│   │   │   ├── app.component.spec.ts<br>
│   │   │   ├── app.component.ts<br>
│   │   │   ├── footer<br>
│   │   │   │   ├── footer.component.html<br>
│   │   │   │   ├── footer.component.scss<br>
│   │   │   │   ├── footer.component.spec.ts<br>
│   │   │   │   └── footer.component.ts<br>
│   │   │   └── header<br>
│   │   │       ├── header.component.html<br>
│   │   │       ├── header.component.scss<br>
│   │   │       ├── header.component.spec.ts<br>
│   │   │       └── header.component.ts<br>
│   │   ├── instances<br>
│   │   │   ├── instance-detail-page<br>
│   │   │   │   ├── instance-detail-page.component.html<br>
│   │   │   │   ├── instance-detail-page.component.scss<br>
│   │   │   │   ├── instance-detail-page.component.spec.ts<br>
│   │   │   │   └── instance-detail-page.component.ts<br>
│   │   │   ├── instances.component.html<br>
│   │   │   ├── instances.component.scss<br>
│   │   │   ├── instances.component.spec.ts<br>
│   │   │   ├── instances.component.ts<br>
│   │   │   └── instance-tile<br>
│   │   │       ├── instance-tile.component.html<br>
│   │   │       ├── instance-tile.component.scss<br>
│   │   │       ├── instance-tile.component.spec.ts<br>
│   │   │       └── instance-tile.component.ts<br>
│   │   ├── login ***TODO***<br>
│   │   │   ├── login.component.html<br>
│   │   │   ├── login.component.scss<br>
│   │   │   ├── login.component.spec.ts<br>
│   │   │   └── login.component.ts<br>
│   │   ├── not-found<br>
│   │   │   ├── not-found.component.html<br>
│   │   │   ├── not-found.component.scss<br>
│   │   │   ├── not-found.component.spec.ts<br>
│   │   │   └── not-found.component.ts<br>
│   │   └── sys-logs<br>
│   │       ├── sys-logs.component.html<br>
│   │       ├── sys-logs.component.scss<br>
│   │       ├── sys-logs.component.spec.ts<br>
│   │       └── sys-logs.component.ts<br>
│   ├── httperror.interceptor.ts<br>

* ***Part II: Store part implement all the actions, effects, models, reducers, selectors and services:*** <br>
│   └── store<br>
│       ├── actions<br>
│       │   ├── activity.actions.ts<br>
│       │   ├── applications.actions.ts<br>
│       │   └── instance.actions.ts<br>
│       ├── effects<br>
│       │   ├── activity.effects.ts<br>
│       │   ├── applications.effects.ts<br>
│       │   └── instance.effects.ts<br>
│       ├── models<br>
│       │   ├── activity.model.ts<br>
│       │   ├── application-group-item.model.ts<br>
│       │   ├── app-state.model.ts<br>
│       │   └── instance-item.model.ts<br>
│       ├── reducers<br>
│       │   ├── activity.reducer.ts<br>
│       │   ├── application-group.reducer.ts<br>
│       │   └── instance.reducer.ts<br>
│       ├── selectors<br>
│       │   ├── activity.selector.ts<br>
│       │   ├── application-group.selector.ts<br>
│       │   └── instance.selector.ts<br>
│       └── services<br>
│           ├── activity.service.spec.ts<br>
│           ├── activity.service.ts<br>
│           ├── application.service.spec.ts<br>
│           ├── application.service.ts<br>
│           ├── auth.service.spec.ts<br>
│           ├── auth.service.ts<br>
│           ├── instance.service.spec.ts<br>
│           ├── instance.service.ts<br>
│           ├── login.service.spec.ts<br>
│           ├── login.service.ts<br>
│           ├── socketio.service.spec.ts<br>
│           ├── socketio.service.ts<br>
│           ├── validator.service.spec.ts<br>
│           └── validator.service.ts<br>
├── app.config.ts (created by Angular CLI) <br> 
***Note that this exactly resembels the structure given in the NGRx tutorial ([https://ngrx.io/guide/store](https://ngrx.io/guide/store)).***<br>
* ***Part III images and build environments*** <br>
├── assets<br>
│   ├── announced.png<br>
│   ├── b3africa.png<br>
│   ├── bbmri-eric.png<br>
│   ├── close.png<br>
│   ├── done.png<br>
│   ├── error.png<br>
│   ├── external_ref.png<br>
│   ├── favicon.ico<br>
│   ├── furley_bg.png<br>
│   ├── loading.gif<br>
│   ├── loading_old.gif<br>
│   ├── lock.png<br>
│   ├── new.png<br>
│   ├── pawn_small.png<br>
│   ├── silicolab_logo.png<br>
│   ├── silicolab_logo_small.png<br>
│   ├── silicolab_logo.svg<br>
│   └── silicolab_logo_white.png<br>
├── environments<br>
│   ├── environment.prod.ts<br>
│   ├── environment.prod.ts.template<br>
│   ├── environment.ts<br>
│   └── environment.ts.template<br>
* Standart angular files mostly generated by the Angular CLI (edited in cases)<br>
├── favicon.ico<br>
├── index.html<br>
├── main.ts<br>
├── polyfills.ts<br>
├── proxy.conf.json<br>
├── styles.scss<br>
├── styles-variables.scss<br>
└── test.ts<br>

**Front end TODO'S**:

* Authentication for users; 
    * See tutorial here [https://mherman.org/blog/authentication-in-angular-with-ngrx/](https://mherman.org/blog/authentication-in-angular-with-ngrx/)
* Styling

#### Back-End Details

The Backend code can be grouped the backend code regarding:<br>

* api: Code implementing the Flask API calls it uses code defined in
    * the Bibbox Folder: Implements the file handling and data I/O providing the neccesary JSON data  to the API calls.
* celery config files and tasks
* models contains the DB implementations for the database
    * services implements the SQL-Alchemy services consuming the models
* static features Api spec files in different formats
* util features constants and globals in a single script
* Other files cover init and configs for falsk and the neccesary interfaces

/opt/bibbox/sys-bibbox/backend/<br>
├── app<br>
* ***Part I: Main Code influencing Front end behaviour***<br>
│   ├── api<br>
│   │   ├── activity.py<br>
│   │   ├── apps.py<br>
│   │   ├── authentication.py<br>
│   │   ├── default.py<br>
│   │   ├── \_\_init\_\_.py<br>
│   │   └── instance.py<br>
│   ├── bibbox<br>
│   │   ├── app.py<br>
│   │   ├── docker_handler.py<br>
│   │   ├── file_handler.py<br>
│   │   ├── \_\_init\_\_.py<br>
│   │   ├── instance_controler.py<br>
│   │   ├── instance_handler.py<br>
│   │   └── instance.py<br>
* ***Part II DB and asynchronous Tasks***<br>
│   ├── celeryconfig.py<br>
│   ├── celerytasks<br>
│   │   ├── \_\_init\_\_.py<br>
│   │   └── tasks.py<br>
│   ├── dirty_test_code.py<br>
│   ├── \_\_init\_\_.py<br>
│   ├── models<br>
│   │   ├── activity.py<br>
│   │   ├── app.py<br>
│   │   ├── catalogue.py<br>
│   │   ├── \_\_init\_\_.py<br>
│   │   ├── log.py<br>
│   │   └── user.py<br>
│   ├── services<br>
│   │   ├── activity_service.py<br>
│   │   ├── app_service.py<br>
│   │   ├── catalogue_service.py<br>
│   │   ├── db_logger_service.py<br>
│   │   ├── \_\_init\_\_.py<br>
│   │   ├── log_service.py<br>
│   │   ├── socketio_service.py<br>
│   │   └── user_service.py<br>
│   ├── static<br>
│   │   ├── bibbox-api-spec old.yml<br>
│   │   ├── bibbox-api-spec.yml<br>
│   │   ├── main.html<br>
│   │   └── swagger.json<br>
│   ├── utility<br>
│   │   ├── celery_util.py<br>
│   │   └── \_\_init\_\_.py<br>
│   └── utils<br>
│       ├── common.py<br>
│       └── \_\_init\_\_.py<br>
* ***Part III: Init Stuff for websockets and Falsk + logs***<br>
├── celery_worker.py<br>
├── debug-test.py<br>
├── Dockerfile<br>
├── entrypoint.sh<br>
├── \_\_init\_\_.py<br>
├── logs<br>
│   ├── debug.log<br>
│   ├── error.log<br>
│   ├── info.log<br>
│   └── warning.log<br>
├── manage.py<br>
├── requirements.txt<br>
├── runflask.py<br>
├── settings.py<br>
├── uwsgi.ini<br>
├── uwsgi_params<br>
└── wsgi.py<br>

#### Set up Front-End Developement environment

* **Easiset way (Linux Debian based):**<br> 
    * Install Bibbox locally under linux (See [Install Bibbox](installation_v4_bibbox_linux))
    * Install VS-Code (Goto [https://code.visualstudio.com/download](VSCode))
    * Set up local DNS Service (See [Install Bibbox](installation_v4_bibbox_linux))
    * Goto sys-bibbox/frontend 
    * Type `code .` into bash
    * After VS Code opens type `ng serve` 
    * Open the link the console shows you (If setup went correctly you should see a Bibbox interface without any errors) 
    * Change any code file and watch it change live in your browser.

* **NOTE**: Prequesite is that the DNS service and Bibbox installation fully works



