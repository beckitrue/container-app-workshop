# README

In this step, we are going to configure a `nginx` server as a reverse proxy. The `nginx` server will run in a network called `lab` and will listen on port `80`. It will forward the requests to the `flask` server running on port `5000`, that is running in another network that is briged to the local host.

This is assuming that you've already completed the `simple-web` configuration in the previous steps of this lab.

<img src="../images/nginx-diagram.png" alt="nginx reverse proxy diagram" width="600"/>

## What are we doing?

The `nginx` reverse proxy server is configured by its configuration file. The configuration file is located at `/etc/nginx/nginx.conf` on the container, but we are using a bind mount to `/var/nginx/conf/default.conf`.  This allows us to modify the configuration file on the host and the changes will be reflected in the container.

### nginx Configuration file

This file is configured to add a new server block that listens on port `80` and forwards the requests to the `flask` server. Remember from our `simple-web` configuration that the `flask` server is running on port `5000`, and has two routes: `/` and `/hello-world`.

The `nginx` server is configured to proxy to both routes. The configuration file is as follows:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name localhost lab.example.com;

    location / {
        proxy_pass http://172.17.0.3:5000;
    }

    location /hello-world {
        proxy_pass http://172.17.0.3:5000;
    }
}
```
### nginx Content file

We are also using a bind mount to `/var/nginx/html/index.html` to serve a custom `index.html` file. This file is served when the `nginx` server receives a request to the root path `/`. We are using a simple `index.html` file with the links to the two routes of the `flask` server.

We are using the bind mount for the content file for the same reason we are using it for the configuration file. This allows us to modify the content file on the host and the changes will be reflected in the container.

## Docker Compose

Up until now, we've created containers with a Dockerfile. In this step, we are going to use `docker-compose` to create the `nginx` container. The `docker-compose` file is located at `docker-compose.yaml` in the root of this repository.

Docker compose defines the configuration for the `nginx` server and handles the commands we would have to run to create the containers.

For example, we define the container image, the networks, the volumes, and the ports that we want to expose. In our next lab, we will see how to use `docker-compose` to create multiple containers and networks. But for now, we are only going to use it to create the `nginx` server.

#### Note: 

You can use Docker Desktop or the Docker CLI to find the information you need to update the configuration files. You will need the IP address of the `nginx` and `simple-web` servers to update the configuration files. 

The insturctions below will show you how to get the IP address of the containers using the Docker CLI.

## Networking 

The `nginx` server and the `simple-web` servers are configured to run in separate networks. This is to simulate how we would configure a reverse proxy in a real-world scenario. For example, where we might want to connect to IoT devices that can't run HTTPS. 

The `nginx` server is running in the `lab` network, and the `simple-web` server is running in the `bridge` network, which is bridged to the local host.

These are indicated on the diagram with the `nginx` server in green and the `simple-web` server in blue.

You will be able to verify that they are in different networks by running the `docker network ls` command and checking the networks that are created. 

You can use the `docker network inspect <network-name>` command to get more information about the network, including the containers that are connected to it.

### Get the IP address of the containers

To get the IP address of a contianer, you can run the `docker inspect <container-name>` command and look for the `IPAddress` field.

''' 
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container-name or id>
'''

#### Get the IP address of both the `nginx` and `simple-web` servers. You will need this information later to update the configuration files.

## Running nginx

Now that we know that we are using bind mounts to our host for the configuration and content files, and we know that the `nginx` server is running in a separate network from the `simple-web` server, we can run the `docker-compose` command to create the `nginx` server.

### Remember our bind mounts

Remember that we are using bind mounts for the configuration and content files. This means that you can update the files on your host and the changes will be reflected in the container.

- create the `/var/nginx/conf/` directory on your host
- copy the `default.conf` file from the nginx directory to `/var/nginx/conf/`
- create the `/var/www/` directory on your host
- copy the `index.html` file from the nginx directory to `/var/www/`

Now our files are in place to configure the `nginx` server.

### Running the nginx server

To create the `nginx` server, run the following command from the `container-app-workshop/nginx/nginx` directory:

'''
docker-compose up -d
'''

This command will create the `nginx` server and run it in the background. You can verify that the server is running by running the `docker ps` command and checking the status of the `nginx` container.


## Testing the nginx server

To test the `nginx` server, open a browser and navigate to `http://<IP address of your nginx server>`. You should see the `index.html` file that we created in the `nginx` content file. This file has links to the two routes of the `flask` server running in the `simple-web` container.

### It might not work

It might not work because the IP addresses in the `default.conf` file and the `index.html` file are hardcoded. You will need to update the IP addresses in these files to match the IP address of your `simple-web` server.

But we used the bind mounts for this very reason. You can update the files on your host and the changes will be reflected in the container.

Your `default.conf` file is located at `/var/nginx/conf/default.conf` on the host, and your `index.html` file is located at `/var/nginx/html/index.html` on the host.

Restart the `nginx` server by running the following command from the `container-app-workshop/nginx/nginx` directory:

'''
docker-compose restart
'''

:white_check_mark: Now open a browser tab and enter the address of your `nginx` server. For example `http://172.19.02`. You should see the `index.html` file with the links to the two routes of the `flask` server. Click on the links to test the routes.

:white_check_mark: You should see the `You're home now!` message from the `simple-web/` link.and the `Hello, World!` message from the `simple-web/hello-world` link.

## Conclusion

Whew! That was a lot of work. But you did it! You configured an `nginx` server as a reverse proxy to a `flask` server. You used bind mounts to update the configuration and content files on your host, and you ran the `nginx` server in a separate network from the `flask` server.

You also learned about networking in Docker and how to get the IP address of a container.

And you were introduced to `docker-compose` and how to use it to create containers. In the next lab, we will dive deeper into `docker-compose` and see how to use it to create multiple containers and networks.
