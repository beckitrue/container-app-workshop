# README

The `simple-web` container is a simple Flask server that gives us a target for our `nginx` reverse proxy container.

The container comes from an article in Medium by Andrea Rubino. The article is [here](https://medium.com/@andrearubino/deploy-a-flask-app-with-nginx-and-gunicorn-inside-docker-62b26dc0e15a).

The `simple-web` container uses Flask to serve two routes:
- `/` - returns "You're home now!"
- `/hello-world` - returns "Hello, World!"

We'll use these routes to test our `nginx` reverse proxy in our next lab.


## Building the `simple-web` container

There is no need to change any of the files in the `lesson_1` directory. 

### Build the container image

- Change to the `lesson_1` directory (assumes you've cloned this repository to your local machine).
- Run the following command to build the container image:

```
docker build -t simple-web:latest .
```

#### What does this command do?

This will build the container image from the instructions in the Dockerfile, and tag it as `simple-web:latest`

<details>
<summary>Click to see the Dockerfile</summary>
```dockerfile
  FROM python:3.11.4-slim-buster
  WORKDIR /flask-simple-app
  COPY requirements.txt requirements.txt
  COPY app.py app.py
  RUN pip3 install -r requirements.txt
  CMD ["python3", "-m", "flask", "run", "--host=0.0.0.0"]

```dockerfile
</details>

The Dockerfile instructs the build process to:
- Use the `python:3.10.0-slim-buster` image as the base image
- Copy the `requirements.txt` file to the image
- Copy the `app.py` file to the image
- Install the Python packages listed in the `requirements.txt` file (Flask)
- Run the Flask server when the container starts with the command to listen on all interfaces(`--host=0.0.0.0`)

#### How do I know the image was built?

:white_check_mark: You can verify that the image was built by running the following command:

```
docker images
``` 
and looking for the `simple-web` image.

## How do I know the simple-web server is running?

You can verify that the `simple-web` server is running by running the following command:

```
docker ps
``` 
This command will show you the list of running containers. You should see the `simple-web` container running.

:white_check_mark: You should see the `simple-web` container running. The `simple-web` container should be listening on port `5000`, and the `nginx` container should be listening on port `80`.

### Test the simple-web server from the browser

- Run the following command to get the IP address of the `simple-web` container:

```
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' simple-web
```
- Open a browser and navigate to `http://<IP address of your simple-web server>:5000`. You should see the `You're home now!` message from the `simple-web` server. Change the port number to what you configured in the `docker-compose.yaml` file if you changed it.
- Now navigate to `http://<IP address of your simple-web server>:5000/hello-world`. You should see the `Hello-world` message from the `simple-web` server.

:white_check_mark: Now that we know that the `simple-web` server is running, we can test the `nginx` server.

## What Next?

Now that you have the `simple-web` container image, we will use it in the the next lesson as a target for the `nginx` container to test the reverse proxy. In our [next step](../nginx), we will build the `nginx` container image and run it with the `simple-web` container using Docker Compose.


