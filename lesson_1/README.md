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

```bash
docker build -t simple-web:latest .
```

#### What does this command do?

This will build the container image from the instructions in the Dockerfile, and tag it as `simple-web:latest`

<details>
<summary>Click to see the Dockerfile</summary>
  <pre><code>
  FROM python:3.11.4-slim-buster
  WORKDIR /flask-simple-app
  COPY requirements.txt requirements.txt
  COPY app.py app.py
  RUN pip3 install -r requirements.txt
  CMD ["python3", "-m", "flask", "run", "--host=0.0.0.0"]
  </code></pre>
</details>

The Dockerfile instructs the build process to:
- Use the `python:3.11.4-slim-buster` image as the base image
- Copy the `requirements.txt` file to the image
- Copy the `app.py` file to the image
- Install the Python packages listed in the `requirements.txt` file (Flask)
- Run the Flask server when the container starts with the command to listen on all interfaces(`--host=0.0.0.0`)

#### How do I know the image was built?

:white_check_mark: You can verify that the image was built by running the following command where you should see the `simple-web` image in the list of images:

```bash
docker images | grep simple-web
``` 

### Start the container

Start the `simple-web` container by running the following command: 

```bash
docker run --name simple-web -d -p 5000:5000 simple-web:latest
```

This command will start the `simple-web` container in detached mode (`-d`) and map port `5000` on the host (your computer) to port `5000` on the container. The `-name` flag gives the container a name of `simple-web`. The `-p` flag maps the host port to the container port. The last argument is the name of the image to run.

If you get a port conflict, it means that there is something already using port `5000` on your computer. Change your `run` command to use an open port like `-p 5050:5000`. That maps port `5000` on the container to port `5050` on your computer. Later, when you test the container, remember to change the port number in your browser to what you configured it to in the `docker run` command.


## How do I know the simple-web server is running?

You can verify that the `simple-web` server is running by running the following command:

```bash
docker ps
```

:white_check_mark: You should see the `simple-web` container running. The `simple-web` container should be listening on port `5000` (or whatever you configured above).

### Test the simple-web server from the browser

- Run the following command to get the IP address of the `simple-web` container:

```bash
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' simple-web
```

- Open a browser and navigate to `http://<IP address of your simple-web server>:5000`. You should see the `You're home now!` message from the `simple-web` server, but your browser will warn you that it's not secure. That's why we will configure a `nginx` server in the next lab. 

- Now navigate to `http://<IP address of your simple-web server>:5000/hello-world`. You should also see a warning from your browser. That will be fixed in our next lab when we configure the `nginx` server.

:white_check_mark: Now that we know that the `simple-web` server is running, we can move onto the next lab and confgire a `nginx` server to reverse proxy the `simple-web` server.

## What Next?

Now that you have the `simple-web` container image, we will use it in the the next lesson as a target for the `nginx` container to test the reverse proxy. In our [next step](../nginx), we will build the `nginx` container image and run it with the `simple-web` container using Docker Compose.

:white_check_mark: Test your understanding of how a Dockerfile works by modifying the `Dockerfile` to use a different base image. You can use any of the official Python images from [Docker Hub](https://hub.docker.com/_/python). For example, you can use `python:3.11.4-alpine` as the base image. This will create a smaller image, but it may require some changes to the `requirements.txt` file to work with Alpine Linux. 

## Why is this important?

- You learned how to build a Docker image from a Dockerfile.
- You learned how to run a Docker container from an image.
- You learned how to map ports from the host to the container.
- You learned how to test a web server running in a Docker container.
- You learned how to inspect a Docker container to get its IP address.
- You learned how to use the `docker ps` command to see running containers.
- You learned that the `simple-web` server is not secure and should not be exposed to the internet.

This is a good example of a web server that you would not want to expose to the internet. Fortunately, there are ways that we can secure access for services like this. In the next lab, we will configure an `nginx` server to reverse proxy the `simple-web` server and add security to it. The `nginx` server will be the only server exposed to the internet, and it will handle all of the security for the `simple-web` server.

## Clean up

When you are done with the `simple-web` container, you can stop and remove it by running the following commands:

```bash
docker stop simple-web
docker rm simple-web
```
This will stop and remove the `simple-web` container. You can also remove the image by running the following command:

```bash
docker rmi simple-web:latest
```
This will remove the `simple-web` image from your local machine. You can also remove all stopped containers and unused images by running the following command:

```bash
docker system prune
```
This will remove all stopped containers and unused images from your local machine. Be careful with this command, as it will remove all stopped containers and unused images, not just the `simple-web` container.

Now we are ready to move on to the next lab and use `docker-compose` to configure the `nginx` server to reverse proxy the `simple-web` server.
