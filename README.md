# ask-your-repository-docker

A docker-compose deployment for ask-your-repository.

This repo is part of the "Ask your Repository" Bachelor project containing the following repos:  
- [Elija - Ask your Repository Backend API](https://github.com/hpi-sam/ask-your-repository-api)  
- [Jona - Ask your Repository Web Frontend](https://github.com/hpi-sam/ask-your-repository-web)  
- [Tobito - Ask your Repository Dialogflow Adapter](https://github.com/hpi-sam/ask-your-repository-dialogflow-adapter)  
- [Ask your Repository Docker Deployment](https://github.com/hpi-sam/ask-your-repository-docker)  
- [Ask your Repository Project Documentation](https://github.com/hpi-sam/BP2018HG1)  

## Setup on Server

Make sure [docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/) and [docker-compose](https://docs.docker.com/compose/install/) are installed.

----

Clone this repository on your server:

`git clone https://github.com/hpi-sam/ask-your-repository-docker.git`

Change directory:

`cd ask-your-repository-docker`

Setup .env files:

`cp .env.example .env`  
`cp nginx.env.example nginx.env`

`touch elija.env` (see [here](https://github.com/hpi-sam/ask-your-repository-api/blob/master/.env.example) for env example)  
`touch tobito.env` (see [here](https://github.com/hpi-sam/ask-your-repository-dialogflow-adapter/blob/master/.env.example) for env example)

Fill the environment files with appropriate data.

------

Initialize docker swarm:

`docker swarm init`

Explicitly export your envars:

`export $(cat .env | xargs)`

Deploy application:

`docker stack deploy -c docker-compose.yaml <name>`

Make sure all services are up and running:

`docker service ls`

## Changes to the configuration

**Always commit your changes to this repo to keep it in sync with the files on the server!**

Do not make adjustments to the `docker-compose.yaml` directly.  
Instead, use the env files to change configurations.  

If you do need to change the compose file try to keep things customizable.  
Make sure the compose file still works for different environments (development, staging, production).

After making adjustments redeploy the stack:

`docker stack deploy -c docker-compose.yaml <name>`

## Redeploy services

You can deploy another version of a service by using the `deploy` script:

`./deploy <service> <image>`

For example to deploy the latest Jona image:

`./deploy jona bp2018hg1/jona:latest`

Mind that you don't need to specify the real service name with the stack name as a prefix.
The stack name is added automatically.

For more informations view the [deploy script file](https://github.com/hpi-sam/ask-your-repository-docker/blob/master/deploy).
