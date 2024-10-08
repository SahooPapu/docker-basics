What is Docker
==============
=> Docker is a containerization platform

=> Docker is used to build and deploy our application into any machine without bothering about dependencies.

=> Dependencies means the softwares which are required to run our application.

			Dependencies = OS / Angular / React / Java / DB / Tomcat etc...

=> Docker will reduce the gap between Development and Deployment

Docker Architecture
====================

1) Dockerfile   : It contains instructions to build docker image

2) Docker Image  : It is a package which contains code + dependencies

3) Docker Registry : It is  Arepository to store docker images

4) Docker Container : It is a runtime process which runs our application


Note: Once Docker image is created then we can pull that image and we can run that image in any machine.

Virtualization
===============

-> Installing Multiple Guest Operating Systems in one Host Operating System 

-> Hypervisior S/w will be used to achieve this

-> We need to install all the required softwares in Guest Operating Systems to run our application

-> It is old technique to run the applications

-> System performance will become slow in this process

-> To overcome the problems of Virtualization we are going for Containerization concept.


Containerization
==================

-> It is used to package all the softwares and application code in one container for execution

-> Container will take care of everything which is required to run our application

-> We can run the containers in Multiple Machines easily

-> Docker is a containerization software

-> Using Docker we will create container for our application 

-> Using Docker we will create image for our application

-> Docker images we can share easily to mulitple machines

-> Using Docker image we can create docker container and we can execute it


Conclusion
============

-> Docker is a containerization software

-> Docker will take care of application and application dependencies for execution

-> Application Deployments into multiple environments will become easy if we use Docker containers concept.

++++++++++++++++++++Docker Commands+++++++++++++++++++

# see docker info 
$ docker info

# To see docker images
$ docker images

# Pulling hello-world docker image 
$ docker pull hello-world

# see docker image 
$ docker images

# Running hello-world docker image 
$ docker run hello-world

# Display Running Docker containers
$ docker ps

# Displaying Running + stopped containers
$ docker ps -a

# Inspect docker image
$ docker inspect <image-id>

# Remove Docker image
$ docker rmi <image-name / image-id>

# Remove docker image forcefully
$ docker rmi -f <image-name / image-id>

# Stop the container
$ docker stop <container-id>

# Remove docker container
$ docker rm <container-id>

# Remove all stopped containers + un-used images + un-used networks 
$ docker system prune -a

Note: Create account in Docker Hub (https://hub.docker.com/)

Dockerfile
===========

=> Dockerfile contains set of instructions to build docker image

=> In Dockerfile we will use DSL (Domain Specific Language)

=> Docker Engine will read Dockerfile instructions from top to bottom to process

=> In Dockerfile we will use below keywords


1) FROM
2) MAINTAINER
3) COPY
4) ADD
5) RUN
6) CMD
7) ENTRYPOINT
8) ENV
9) ARG
10) WORKDIR
11) EXPOSE
12) VOLUME
13) USER
14) LABEL

FROM
=========

=> It represents base image to create our docker image

Syntax:

FROM java:1.8
FROM python:1.2
FROM mysql:8.5
FROM tomcat:9.5

Maintainer
==============

=> It is used to specify docker file author information

Syntax:

MAINTAINER  Ashok <papu.sahoo@gmail.com>

COPY
======

=> It is used to copy the files from source to destination while creating docker image

Syntax:

COPY  <SRC>  <DESTINATION>


Ex:    COPY  target/sb-api.war  /app/tomcat/webapps/sb-api.war

ADD
======

=> It is used to copy the files from source to destination while creating docker image

Syntax:

ADD  <SRC>  <DESTINATION>

ADD  <HTTP-URL>  <DESTINATION>


Ex:    ADD  <url>   /app/tomcat/webapps/sb-api.war

Q) What is the difference between COPY and ADD command ?
==========================================================

COPY : It can copy from one path to another path with in the same machine.

ADD : It can copy from one path to another path & it supprts URL also as source.

RUN
====

-> RUN instructions will execute while creating docker image

Syntax:

RUN yum install git
RUN yum install maven
RUN git clone <repo-url>
RUN cd <repo-name>
RUN mvn clean package

Note: We can write multiple RUN instructions, docker engine will process from top to bottom.

CMD
====

=> CMD instructions will execute while creating docker container

=> Using CMD command we can run our application in container

Syntax:

CMD sudo start tomcat

CMD java -jar <jar-file>


Note: We can write multiple CMD instructions but docker engine will process only last CMD instruction.

Q) What is the difference between RUN and CMD ?
================================================

-> RUN instructions will execute while creating docker image
=> CMD instructions will execute while creating docker container


=> We can write multiple RUN instructions, docker engine will process from top to bottom.
=> We can write multiple CMD instructions but docker engine will process only last CMD instruction.

Note: There is no use of writing multiple CMD instructions.

Sample Docker
==============

FROM ubuntu

MAINTAINER Ashok<papu.sahoo@gmail.com>

RUN echo "Hi, i am run - 1"
RUN echo "Hi, i am run - 2"
RUN echo "Hi, i am run - 3"

CMD echo "Hi, i am CMD-1"
CMD echo "Hi, i am CMD-2"
CMD echo "Hi, i am CMD-3"


=> Create a file (filename: Dockerfile)
$ vi Dockerfile

=> Copy above sample docker file content and keep in docker file  (Esc + :wq)

# Create docker image using Dockerfile

$ docker build -t <image-name> .

# login into docker hub account from docker machine
$ docker login

Note: Enter your docker hub account credentials.
	
# tag docker image
$ docker tag <image-name> <tagname>

Ex :  $ docker tag myimg1 ashokit/myimg1

# Push Docker image

$ docker push <Tag-name>


===================================================
Q) Can we use user defined name for Dockerfile ?

Ans) Yes, we can do it.

$ docker build -f <filename> -t <imagename> .

==================================================

ENTRYPOINT
=============

=> It is used to execute instructions while creating container

Synatx:

ENTRYPOINT [ "echo" , "Container Created Successfully" ]

ENTRYPOINT [ "java", "-jar", "target/springboot.jar" ]

Q) What is the difference between CMD and ENTRYPOINT ?
========================================================

=> CMD instructions we can override while creating container

=> ENTRYPOINT instructions we can't override

WORKDIR
========

=> It is used to specify working directory for image and container


Syntax: 


WORKDIR /app/usr/

ENV
=======

=> ENV is used to set Environment Variables

Ex:

ENV java /etc/softwares/jdk

EXPOSE
=========

=> It is used to specify on which port number our docker container wil run

EX:

EXPOSE 8080

ARG
====

=> By using ARG we can take dynamic values from CLI

=> It is used to remove hard coded values in Dockerfile

Ex:

ARG branch

RUN git clone -b $branch <repo-url>

$ docker build -t <imagename> --build-arg branch=master .

USER
=========

=> It is used to specify username for creating image / container


Ex:

USER dockeruser

VOLUME
=======

=> It is used to specify docker volume storage location


=> Volumes are used for storage purpose

LABEL
=======
=> It is used to add METADATA to docker objects in key-value format

Ex:

LABEL name="sbi_image"


