#  Apps Creators Manual

## How to join the team

Contact [Heimo Müller](mailto:heimo.mueller@medunigraz.at), [Robert Reihs](mailto:robert.reihs@medunigraz.at) or [Markus Plass](mailto:markus.plass@medunigraz.at). Any of them can add you to the Github team of an App repository. 

## Anatomy of an App

An **App** is described within a BIBBOX GitHub repository. By convention the name of the repository starts with the prefix **"app-"**
A template repository can be found at:  <https://github.com/bibbox/app-template>


An **App** consists at least of the following files and directories, please never change the name of these files!

- README.md
- INSTALL-APP.md
- appinfo.json
- docker-compose.yml.template
- environment-parameters.json
- fileinfo.json
- icon.png

### README.md

The default Github readme file shoud contain information about the used official docker images and docker images from the [BIBBOX dockerhub](https://hub.docker.com/r/bibbox/). In addition you should describe all mounted volumes and their content.

  
### INSTALL-APP.md

Install instruction for the App to follow after the first installation step (docker-compose up) is finished. This typically describes application specific configuration tasks. A link to this file is given in the Dashboard of the installed App. 
    
  
### appinfo.json
    
Specifies information about the App as displayed in the BIBBOX App Store. 
    
``` json
    {
            "name": "A long name of the Application, shown in the App Store",
            "short_name": "APP short name",
            "version": "V.1.0",
            "description": "Long description of the Application shown in Store, can be multiline",
            "short_description": "Short description of the Application shown in Store",
            "catalogue_url": "URL to biobankapps, if applicaple",
            "application_url": "URL to App official gace",
            "tags": ["Tag1", "Tag2"]
    }
```

### docker-compose.yml.template

Based on this file the docker-compose.yml will be generated. The variables §§INSTANCE and all other environment and configuration variables starting with "§§" will be replaced during the installation. Each template for a docker compose file should link to the `bibbox-default-network` network. The `proxy` and `ports` section is used to create a `005-§§INSTANCE.conf` proxy file. 

NOTE:

* Only use tagged images versions (not latest). To ensure that the app stays stable over time.
* Use the docker-compose `links` parameter to ensure that containers can "talk" to each other indent of the name set in §§INSTANCE.

    
``` yml
    version: '3'
    
    networks:
        bibbox-default-network:
          external: true
    
    services:
    
      §§INSTANCE-container-frontend:
        image: bibbox/app-image:vx.y.z
        container_name:  §§INSTANCE-container-frontend
        restart: unless-stopped
        networks:
          - bibbox-default-network
        links:
          - §§INSTANCE-container2:container2
        ports:
          - "80:80"
        depends_on:
          - §§INSTANCE-container2
        volumes: 
          - ./data/container/app-data:/app-data
        proxy:
          TYPE: PRIMARY
          URLPREFIX: §§INSTANCE
          TEMPLATE: default
          DISPLAYNAME: 'APP name'  

    §§INSTANCE-container2:
      image: bibbox/app-image2:va.b.c
      container_name:  §§INSTANCE-container2
      restart: unless-stopped
      networks:
        - bibbox-default-network
      links:
          - §§INSTANCE-app-db:app-db
      ports:
        - "8000:8000"
      depends_on:
          - §§INSTANCE-app-db
      volumes: 
        - ./data/container/app-data:/app-data
    
      §§INSTANCE-app-db:
        image: mysql:8
        container_name: §§INSTANCE-app-db
        restart: unless-stopped
        networks:
          - bibbox-default-network
        user: root
        environment:
          - MYSQL_ROOT_PASSWORD=thispasswordisneverusededoutsidethecontainer
          - MYSQL_DATABASE=§§MYSQL_DATABASE_NAME
          - MYSQL_USER=§§MYSQL_DATABASE_USER
          - MYSQL_PASSWORD=§§MYSQL_DATABASE_PASSWORD
        volumes: 
          - ./data/db/var/app-data:/var/app-data
    
```


### environment-parameters.json

Environment parameters for the docker-compose-template file. The user can set the values for these parameters in a GUI during the installation of an App. 
   
    
```json
    [
       {
          "id":"NAME_AS_IN_DOCKER_TEMPLATE_1",
          "display_name":"Name Displayed in GUI at the Installation",
          "type":"text, number, password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_NAME",
          "display_name":"Name of the mysql database",
          "type":"text,",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_USER",
          "display_name":"Name of the mysql user",
          "type":"text",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       },
       {
          "id":"MYSQL_DATABASE_PASSWORD",
          "display_name":"Password of mySQL user",
          "type":"password",
          "default_value":"Default Value",
          "description":"Description shown in the GUI",
          "min_length": "1",
          "max_length": "128"
       }

    ]
```
  
### fileinfo.json

A list of commands to be run when installing an app, consisting of three categories: "environmental_replace", "script_replace" and "permissions".

| key | description |
|---|---|
| environmental_replace | WIP - specifies files/directories where placeholders can be replaced easily |
| script_replace | WIP - specifies files/directories where placeholders etc. should be replaced by a script |
| permissions | specifies which files/folders in the instance directory should be set to which permissions. \n the path is always relative to the instance directory|    

Tool for calculating permissions: https://chmod-calculator.com/

structure:
``` json
    {
        "environment_replace": {},
        "script_replace": [],
        "permissions": {
            "PATH1": NUMERIC_VALUE_OF_PERMISSION1,
	    "PATH2": NUMERIC_VALUE_OF_PERMISSION2,
	    "PATH3": NUMERIC_VALUE_OF_PERMISSION3
	    }
    }
```

example:
``` json
    {
        "environment_replace": {},
        "script_replace": [],
        "permissions": {
            "assets": 775,
	    "data" : 777
	    }
    }
```
    

### icon.png

Icon of the App in the application store und in the application dashboard. Please use a square format, e.g. 512x512 pixeland PNG with a transparency channel.
    

## Versioning

Each App should be versioned. We distinguish between

- **Production Versions** generated from a specific release in the repository. For each major release. i.e. given by a new version of dockerized software tool, a new branch should be generated in the repository. Please note, that the tag name for the Github release should contain the APP version and the BIBBOX APP release (adaption of the APP for BIBBOX). The proposed format is v*APP_verion*_bibboxrel*3 digit bibbox_release_number* e.g. `v8.7.2_bibboxrel001`. 
The `latest` stable reakease is in the master branch.

- **Development Version** comming soon. Branches and tags not specified in a **kit** can be loaded in a **Developer Mode**. 


![GitHub_BiBBox_versioning](images/v4/v4_github_versioning "GitHub Workflow Versioning")


When creating a production version, you should make the follwoing steps. Please make it exactly in this order, 
otherwise the tagging of the bibbox docker/hub and bibbox github will get confused.

1. Generate a new branch in github, if you plan to release a major version. 
  
	1. Once a stable bibbox release is ready create a tag in compliance with the naming convention (e.g. `v8.7.2_bibboxrel001`). 
  
	2. The latest app version should be merged in the master branch if a stable BIBBOX release exists via a pull request. 
  
2. Update all the files for the anticipated version, don't forget to update *appinfo.json*. 

3. Set in the docker compose template file (docker-compose.yml.template) 
the tags for the docker images. Please note, that ALL used images should be tagged with an specific version, don't use the 'latest" tag, as this could break your APP in the future. 

4. *Add the tag in the DOCKER hub to build tagged images (press SAVE before TRIGGER)*

5. Edit in the used kit, e.g. *bibbox.json* the version information. This file can be found in the *application-store* repository. 



## Register an App

For the registration of an App two configuration files have to be extended:

- [applications.json](https://github.com/bibbox/application-store/blob/master/applications.json) maps a Github repository to a human readable name of the App 


- [bibbox.json](https://github.com/bibbox/application-store/blob/master/bibbox.json) puts the App into a specific **kit**. A **kit** defines ta group of Apps together with metadata, which are then displayed in the App store and can be installed in a BIBBOX instance. 


