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
* Part I: Everything visible in the Frontend is a component uses functions defined in the ngrx store part.<br>
sys-bibbox/frontend/src
├── app
│   ├── app.module.ts
│   ├── app-routing.module.ts
│   ├── commons.ts
│   ├── components
│   │   ├── about
│   │   │   ├── contact
│   │   │   │   ├── contact.component.html
│   │   │   │   ├── contact.component.scss
│   │   │   │   ├── contact.component.spec.ts
│   │   │   │   └── contact.component.ts
│   │   │   ├── imprint
│   │   │   │   ├── imprint.component.html
│   │   │   │   ├── imprint.component.scss
│   │   │   │   ├── imprint.component.spec.ts
│   │   │   │   └── imprint.component.ts
│   │   │   └── partners
│   │   │       ├── partners.component.html
│   │   │       ├── partners.component.scss
│   │   │       ├── partners.component.spec.ts
│   │   │       └── partners.component.ts
│   │   ├── activities
│   │   │   ├── activities.component.html
│   │   │   ├── activities.component.scss
│   │   │   ├── activities.component.spec.ts
│   │   │   ├── activities.component.ts
│   │   │   └── activity-menu-overlay
│   │   │       ├── activity-menu-overlay.component.html
│   │   │       ├── activity-menu-overlay.component.scss
│   │   │       ├── activity-menu-overlay.component.spec.ts
│   │   │       └── activity-menu-overlay.component.ts
│   │   ├── applications
│   │   │   ├── application-group
│   │   │   │   ├── application-group.component.html
│   │   │   │   ├── application-group.component.scss
│   │   │   │   ├── application-group.component.spec.ts
│   │   │   │   ├── application-group.component.ts
│   │   │   │   └── application-tile
│   │   │   │       ├── application-tile.component.html
│   │   │   │       ├── application-tile.component.scss
│   │   │   │       ├── application-tile.component.spec.ts
│   │   │   │       └── application-tile.component.ts
│   │   │   ├── applications.component.html
│   │   │   ├── applications.component.scss
│   │   │   ├── applications.component.spec.ts
│   │   │   ├── applications.component.ts
│   │   │   ├── install-screen
│   │   │   │   ├── install-screen.component.html
│   │   │   │   ├── install-screen.component.scss
│   │   │   │   ├── install-screen.component.spec.ts
│   │   │   │   └── install-screen.component.ts
│   │   │   └── install-screen-dialog
│   │   │       ├── install-screen-dialog.component.html
│   │   │       ├── install-screen-dialog.component.scss
│   │   │       ├── install-screen-dialog.component.spec.ts
│   │   │       └── install-screen-dialog.component.ts
│   │   ├── app-scaffold
│   │   │   ├── app.component.html
│   │   │   ├── app.component.scss
│   │   │   ├── app.component.spec.ts
│   │   │   ├── app.component.ts
│   │   │   ├── footer
│   │   │   │   ├── footer.component.html
│   │   │   │   ├── footer.component.scss
│   │   │   │   ├── footer.component.spec.ts
│   │   │   │   └── footer.component.ts
│   │   │   └── header
│   │   │       ├── header.component.html
│   │   │       ├── header.component.scss
│   │   │       ├── header.component.spec.ts
│   │   │       └── header.component.ts
│   │   ├── instances
│   │   │   ├── instance-detail-page
│   │   │   │   ├── instance-detail-page.component.html
│   │   │   │   ├── instance-detail-page.component.scss
│   │   │   │   ├── instance-detail-page.component.spec.ts
│   │   │   │   └── instance-detail-page.component.ts
│   │   │   ├── instances.component.html
│   │   │   ├── instances.component.scss
│   │   │   ├── instances.component.spec.ts
│   │   │   ├── instances.component.ts
│   │   │   └── instance-tile
│   │   │       ├── instance-tile.component.html
│   │   │       ├── instance-tile.component.scss
│   │   │       ├── instance-tile.component.spec.ts
│   │   │       └── instance-tile.component.ts
│   │   ├── login
│   │   │   ├── login.component.html
│   │   │   ├── login.component.scss
│   │   │   ├── login.component.spec.ts
│   │   │   └── login.component.ts
│   │   ├── not-found
│   │   │   ├── not-found.component.html
│   │   │   ├── not-found.component.scss
│   │   │   ├── not-found.component.spec.ts
│   │   │   └── not-found.component.ts
│   │   └── sys-logs
│   │       ├── sys-logs.component.html
│   │       ├── sys-logs.component.scss
│   │       ├── sys-logs.component.spec.ts
│   │       └── sys-logs.component.ts
│   ├── httperror.interceptor.ts

* Part II: Store part implement all the actions, effects, models, reducers, selectors and services: <br>
│   └── store
│       ├── actions
│       │   ├── activity.actions.ts
│       │   ├── applications.actions.ts
│       │   └── instance.actions.ts
│       ├── effects
│       │   ├── activity.effects.ts
│       │   ├── applications.effects.ts
│       │   └── instance.effects.ts
│       ├── models
│       │   ├── activity.model.ts
│       │   ├── application-group-item.model.ts
│       │   ├── app-state.model.ts
│       │   └── instance-item.model.ts
│       ├── reducers
│       │   ├── activity.reducer.ts
│       │   ├── application-group.reducer.ts
│       │   └── instance.reducer.ts
│       ├── selectors
│       │   ├── activity.selector.ts
│       │   ├── application-group.selector.ts
│       │   └── instance.selector.ts
│       └── services
│           ├── activity.service.spec.ts
│           ├── activity.service.ts
│           ├── application.service.spec.ts
│           ├── application.service.ts
│           ├── auth.service.spec.ts
│           ├── auth.service.ts
│           ├── instance.service.spec.ts
│           ├── instance.service.ts
│           ├── login.service.spec.ts
│           ├── login.service.ts
│           ├── socketio.service.spec.ts
│           ├── socketio.service.ts
│           ├── validator.service.spec.ts
│           └── validator.service.ts
├── app.config.ts
├── assets
│   ├── announced.png
│   ├── b3africa.png
│   ├── bbmri-eric.png
│   ├── close.png
│   ├── done.png
│   ├── error.png
│   ├── external_ref.png
│   ├── favicon.ico
│   ├── furley_bg.png
│   ├── loading.gif
│   ├── loading_old.gif
│   ├── lock.png
│   ├── new.png
│   ├── pawn_small.png
│   ├── silicolab_logo.png
│   ├── silicolab_logo_small.png
│   ├── silicolab_logo.svg
│   └── silicolab_logo_white.png
├── environments
│   ├── environment.prod.ts
│   ├── environment.prod.ts.template
│   ├── environment.ts
│   └── environment.ts.template
├── favicon.ico
├── index.html
├── main.ts
├── polyfills.ts
├── proxy.conf.json
├── styles.scss
├── styles-variables.scss
└── test.ts


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

* Authentication for users; 
    * See tutorial here [https://mherman.org/blog/authentication-in-angular-with-ngrx/](https://mherman.org/blog/authentication-in-angular-with-ngrx/)
* Styling

