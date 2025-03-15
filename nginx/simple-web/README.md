# README

The `simple-web` container is a simple Flask server that gives us a target for our `nginx` reverse proxy container.

The container comes from an article in Medium by Andrea Rubino. The article is [here](https://medium.com/@andrearubino/deploy-a-flask-app-with-nginx-and-gunicorn-inside-docker-62b26dc0e15a).

The `simple-web` container uses Flask to serve two routes:
- `/` - returns "You're home now!"
- `/hello-world` - returns "Hello, World!"

We'll use these routes to test our `nginx` reverse proxy.


## Building the `simple-web` container

There is no need to change any of the files in the `simple-web` directory. 

### Build the container image

- Change to the `simple-web` directory (assumes you've cloned this repository to your local machine).
- Run the following command to build the container image:

```docker build -t simple-web:latest .```

#### What does this command do?

This will build the container image from the instructions in the Dockerfile, and tag it as `simple-web:latest`.

The Dockerfile instructs the build process to:
- Use the `python:3.10.0-slim-buster` image as the base image
- Copy the `requirements.txt` file to the image
- Copy the `app.py` file to the image
- Install the Python packages listed in the `requirements.txt` file (Flask)
- Run the Flask server when the container starts with the command to listen on all interfaces(--host=0.0.0.0)

#### How do I know the image was built?

:white_check_mark: You can verify that the image was built by running the following command:

```docker images``` and looking for the `simple-web` image.

### Run the container to test it

- Run the following command to start the container:

```docker run -d -p 5000:5000 simple-web:latest```

#### What does this command do?

This will start the container in detached mode (`-d`), and map port 5000 on the host to port 5000 in the container.

#### How do I know the container is running?

:white_check_mark: You can verify that the container is running by running the following command:

```docker ps``` and looking for the `simple-web` container.

### Test the container from a browser

- Open a browser and navigate to `http://localhost:5000` to see the "You're home now!" message.
- Navigate to `http://localhost:5000/hello-world` to see the "Hello, World!" message.

:white_check_mark: Now we know that the container is working as expected, we can move on to building the `nginx` reverse proxy container.


