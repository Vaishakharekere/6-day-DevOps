

```markdown
# 01/04/2025 - Docker & Environment Notes

---

## Environment - Server (Run our Application)

- **Dev Environment** — Software developers test the minimal test cases.
- **Test Env** — Software testing teams perform the functional/non-functional test cases, including performance and load testing.
- **UAT Env** — User Acceptance Test. Before releasing the product to the market, a prototype is shown to the customer.
- **Production Env** — Deploy the application so customers can access it.

---

## What is a Container?

- A container is a server where we actually run the application.

---

## Docker Concepts

### Dockerfile

- A text document that contains a set of instructions for how to run the application in a container.

### Docker Image

- A template that contains everything needed to run the application:
  - Source code
  - Dependencies
  - Configuration files
  - Library files
  - Platform
- **Build Once, Run Anywhere**

### Docker Hub

- A registry/library where we can store all Docker images.

---

## Useful Docker Commands

```bash
docker ps -a
# Shows all containers irrespective of state.

docker ps
# Shows only running containers.

service docker start
service docker status

docker create ubuntu /bin/bash
docker ps -a
docker ps

docker create -it --name webserver amazonlinux /bin/bash
docker start webserver
docker exec -it webserver /bin/bash
ls

docker run -it --name sample ubuntu /bin/bash

docker run -td --name web-app -p 3002:3000 muralisocial123/cart-page-test:1.0

# Exit container in detach mode:
Ctrl + P + Q
```

### Port Info (`-p` Flag)

- Defines how to access the application from the browser.
- Post port number:
  - User choice (0-65534)
  - Can be any number the user likes.

---

## Detached Mode

- **Daemon Container**
- Runs the container in the background.

---

## Dockerfile Instructions

### Build Commands

- `FROM`: Define base image or parent image of the application.
  - Every Dockerfile must start with this.
- `COPY`: Copy a file or directory from local machine into Docker image.
- `ADD`: Same as `COPY`, but also used for downloading packages from the internet into Docker image.
- `RUN`: Install packages or dependencies in a container.

### .dockerignore

- Used to ignore unnecessary files/packages while building Docker images.

---

## Run Commands

- `CMD`: Defines which code or artifact to run in a container.
  - Allows runtime arguments.
- `ENTRYPOINT`: Defines entry of the application.
  - Does **not** allow runtime arguments.
- `EXPOSE`: Defines on which port you want to access the application.
- `ENV`: Defines environment variables of the application.
- `WORKDIR`: Defines the working directory to keep the files inside the container.
- `USER`: To create a user account.

---

## Role

- Collect Environment Variables
- Port Number
- DB Endpoints

---

## Writing Dockerfile - 7 Steps

1. Identify the base image of the application.
2. Create a work directory.
3. Copy the dependencies into Docker image.
4. Install the dependencies.
5. Copy whole source code from local machine to Docker image.
6. Define the expose port number.
7. Mention the command to run the application in the container.

---

## Docker Build & Push Example

```bash
git clone -b master https://github.com/Vaishakharekere/Dimple-CapsuleProject.git
cd Dimple-CapsuleProject

docker build -t web-app-nodejs:1.0 .
docker images

docker run -td --name node-app -p 3015:3015 web-app-nodejs:1.0
docker ps
docker exec -it node-app /bin/bash

docker login
docker push vaishakharekere/web-app-nodejs:1.0
```
```
