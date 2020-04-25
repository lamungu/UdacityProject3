# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Getting Setup

> _tip_: this frontend is designed to work with the RestAPI backends). It is recommended you stand up the backend first, test using Postman, and then the frontend should integrate.

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```

### Setup Backend Node Environment
You'll need to create a new node server. Open a new terminal within the project directory and run:
1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript  @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`


### Configure The Backend Endpoint
Ionic uses environment files located in `./src/environments/environment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `environment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```

# Docker Setup

Each project possess their respective Dockerfile. It is recommended, however, to build using the `docker compose` commmand within the `udacity-c3-deployment/docker` folder.

## Environment Variables

Ensure you have loaded your environment with the following values:

- POSTGRES_USERNAME: PostgreSQL database username
- POSTGRES_PASSWORD: PostgreSQL database password
- POSTGRES_DATABASE: PostgreSQL database name
- POSTGRES_HOST: PostgreSQL database host
- AWS_REGION: AWS Region
- AWS_PROFILE: AWS Profile (For the S3 Configuration)
- AWS_BUCKET: AWS S3 Media Bucket
- JWT_SECRET: JWT Secret (For the authentication layer)

## Configuration

You may specify the names of the docker images to create in `udacity-c3-deployment/docker/docker-compose.yaml`
You may also specify the names of the builds to create in `udacity-c3-deployment/docker/docker-compose-build.yaml`

## Execution

Run your docker images by running the following:

```
docker-compose -f udacity-c3-deployment/docker/docker-compose.yaml up
```

## Build

Build your docker image by running the following:

```
docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml build --parallel 
```

To push the images created into a registry, run the following:

docker-compose -f udacity-c3-deployment/docker/docker-compose-build.yaml push

# Kubernetes Setup

This project is set up with YAML files which you can use to deploy onto a kubernetes cluster. This will require you to have an infrastructure setup using KubeOne or Kops to setup. You can have more information on how to setup a Kubernetes Cluster here: https://ramhiser.com/post/2018-05-20-setting-up-a-kubernetes-cluster-on-aws-in-5-minutes/

## Environment Variables

Add your environment variables inside the ConfigMap file located at `udacity-c3/deployment/k8s/env-configmap.yaml`.

You may also add the sensitive information inside the Secrets file located in `udacity-c3/deployment/k8s/env-secret.yaml`. This will require you to encode your sensitive values in base64, which you can do by running the following command in your bash:

```
$ echo -n ${YOUR_ENV_VARIABLE} | base64
```

Note: Windows system may require to run the following under a Linux subsystem or using the Git Bash plugin for this work.

## Deployment


