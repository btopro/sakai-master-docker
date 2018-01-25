# Sakai Master Dockerized

## Install

Use `git clone https://github.com/profmikegreene/sakai-master-docker.git` to grab this repository. You can then `cd` to the folder you cloned into and either `sh startup.sh` or run the following commands manually.

1. `git pull` This project uses https://github.com/sakaiproject/sakai as a git submodule
1. `git submodule init` to initialize the submodule
1. `git submodule update`
1. `cd sakai/src`
1. `docker run -it --rm --name sakai -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3.5.2-jdk-8-alpine mvn clean install sakai:deploy -Dmaven.tomcat.home=../../tomcat -Djava.net.preferIPv4Stack=true -Dmaven.test.skip=true`

    This will take a while, grab a coffee. But you don't need maven installed since it handles it all in the container :)

1. `docker-compose up`

    This starts containers for

    * tomcat - to serve built sakai webapp
    * mysql - to store sakai db
    * phpmyadmin - GUI for sakai db

1. Visit [http://localhost:7777](http://localhost:7777) or whatever port you chose as `TOMCAT_PORT` in .env




how to use $catalina home on another container?


## How to change sakai source?

In `startup.sh` change `git submodule add` to the appropriate git URL 


### todo
- delete sakai/Dockerfile, sakai/mvn-entrypoint.sh, sakai/settings-docker.xml if these aren't necessary
- move sakai/src to sakai if no other files neccessary in that directory
- do i need to push empty tomcat/components, tomcat/endorsed, tomcat/lib, tomcat/webapps, db/mysql to github?
