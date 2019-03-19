# ask-your-repository-docker

A docker-compose deployment for ask-your-repository.

## Setup on Server

Make sure [docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/) and [docker-compose](https://docs.docker.com/compose/install/) are installed.

----

Clone this repository on your server.

`git clone https://github.com/hpi-sam/ask-your-repository-docker.git`

Change directory

`cd ask-your-repository-docker`

Setup .env files

`cp .env.example .env`
`cp nginx.env.example nginx.env`

Fill the environment files with appropriate data.

Create a docker-compose.yaml.

`./update-compose`

This will fill the `compose-template.yaml` with the variables you configured in your .env file resulting in a deployable `docker-compose.yaml`.

------

Initialize docker swarm

`docker swarm init`

Deploy application

`docker stack deploy -c docker-compose.yaml <name>`

Make sure all services are up and running

`docker service ls`

## Changes to the configuration

**Always commit your changes to this repo to keep it in sync with the files on the server!**

The `docker-compose.yaml` is read only and is not checked into version control.
To make adjustments to the file update the `compose-template.yaml` and run

`./update-compose`
`docker stack deploy -c docker-compose.yaml <name>`

to create a new updated `docker-compose.yaml` and to apply the changes to the stack.

## Redeploy services

You can deploy another version of a service by using the `deploy` script.

`./deploy <service> <image>`

For example to deploy the latest Jona image:

`./deploy jona bp2018hg1/jona:latest`

Mind that you don't need to specify the real service name with the stack name as a prefix. The stack name is added automatically. For more informations view the script file.
