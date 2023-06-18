# **Dockerizing a Django Todo App with Docker Compose**
 This repository contains a Django Todo App that can be easily containerized using Docker Compose. The Docker Compose configuration allows you to run both the Django Todo App and a MySQL database within separate containers.

## Prerequisites
Before getting started, ensure that you have the following prerequisites installed on your machine:
* Docker
* Docker Compose

---

# Dockerizing with Docker Compose
Steps to Dockerize the Todo App using Docker Compose:
1. Clone this repository to your local machine:
    ```shell
    git clone <repository_url>
    ```
2. Create the `docker-compose.yml` file in the root directory and add configuration.
    ##### (Here, it sets up a MySQL container along with the Django Todo App container. We will deep dive into this to understand a docker-compose file and it's configurations)
3. Build and run the containers using Docker Compose:
    ```shell
    docker-compose up
    ```

---

# Understand docker-compose.yml
#### Make sure you have correct indentation as indentation and spaces matters in yml file. Below configurations are added in this To Do applications  docker-compose.yml, Let's understand each line by line.
```shell
version: "3.9"
services: 
 django_todo_app:
  container_name: "django-todo-app"
  build : .
  ports:
    - 8000:8000
  volumes:
    - django_todo_volume:/app
 mysql_db:
  container_name: "django-mysql-db"
  image: mysql:5.7
  ports:
    - 3306:3306
  environment:
    MYSQL_ROOT_PASSWORD: "test@123"
volumes:
 django_todo_volume:
```

## `version`
In version, we have to mention the version of language which you are using in your application. As `django todo app` is a python application I have mentioned python version 3.9

## `services`
Under services we specify the services which we have to run (there can be one or multiple services)

1. **`django_todo_app:`**
This is todo application where I have code base. Inside this I have specified its related commands & specifications. Let's look into it.

    *`container_name:`*
    Give name to your container. Here I have given container name as **django-todo-app** 

    *`build:`*
    This builds or rebuild image & add all configs for the services to create a container.

    *`ports:`*
    Specify on which port you want to run service. It binds local port to remote server port. I am running my django todo service on **8000** and binding same to run on server.

    *`volumes:`*
    Bind volume for the container of service.

2. **`mysql_db:`**
Adding a service for mySQL database.

    *`container_name:`*
    Specify container name for service. 

    *`image:`*
    It will pull MySQL image with 5.7 tag from dockerhub.

    *`ports:`*
    By default, mySQL run on port **3306**, hence binding same to the server.

    *`environment:`*
    Here we have to pass environment variable like mySQL password.

    ```shell
    MYSQL_ROOT_PASSWORD: "your_password"
    ```

## `volumes`
Declare volume which will get bind to the service.

---

# Docker compose up
You are now ready to run
```shell
docker-compose up
```
to build and execute your docker-compose.yml, It creates container for mentioned services. You can run with detached mode by adding `-d` flag. 
```shell
docker-compose up -d
```

After all, You can check all your running containers with 
```
docker ps
```
