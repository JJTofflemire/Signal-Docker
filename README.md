# Signal-Docker

## What *is* Signal anyway?

The full Signal-Project consists of two main branches: the user-facing apps and programs, and the messy server backend

### User-facing apps and programs

- These are the android, ios, and desktop applications. They all are basic programs and have a slew (~12) of urls that ping different backend services

### The backend

- The backend consists of the large [Signal-Server](https://github.com/JJTofflemire/Signal-Server), the brains of the backend, and many small, scalable nodes that all listen on subdomains (chat.signal.org, storage.signal.org, etc)

- The nodes handle parts of Signal like registration, sending images, voice and video calls, etc. Packaging these functions into seperate servers allows for easy scalability in AWS, but for a local implementation they can all be dockerized and ran with the main server on the same system

(add some pretty diagrams here if I am motivated)

## Signal-Project Roadmap

**Goal:** Completely replicate and document the function of [Signal](https://signal.org/)

**Progress:**

- The [main server](https://github.com/JJTofflemire/Signal-Server) that manages E2E messaging compiles and runs without errors
  
  - Functionality is undetermined - in order to test messaging between phones, [registration-service](https://github.com/JJTofflemire/registration-service) needs to be set up first

- To find out where the project is going from here, check out [the To Do section in this repo](#to-do), or the `To Do` sections of any specific Signal repo to see what needs to be done in each of those

## Signal-Project Backend

### Signal-Server

[dockerized](Signal-Server/documentation.md)

- This docker container has not been updated to use an IAM compatible container. if YOU (uncle sam moment) want to implement this, you need to run [this docker image](https://github.com/lyft/metadataproxy) with some configuration alongside dockerized Signal-Server

- This container also probably needs to change how it handles creating the image: as it is currently, it creates a new server with new server-specific certificates. Switching to a two-part build-then-run process would address this, as well as add the ability to pass in your pre-existing signal-server.jar at runtime

[full instructions](https://github.com/JJTofflemire/Signal-Server)

- This repo contains a LOT of information about the server, setting it up, running it and more (yippee). It has turned into a bit of a mess, though I have tried to put the easy bits first without removing any manual documentation

## Others

### NGNIX with Certbot

[dockerized docs](nginx/documentation.md)

- [This docker image](https://github.com/JonasAlfredsson/docker-nginx-certbot/tree/master) handles the annoying bits of deploying NGINX and automates getting and renewing `https` certificates

- The image passes in any custom configuration files at runtime, allowing for ease of use in addition to being dead simple to set up

## To Do

- Run, configure, and dockerize registation-service