# README

In this lab, we will demontrate how to setup a test Cloudflare Tunnel using the `cloudflared` contiainer. The target for the tunnel will be a simple `nginx` web server running in a container on the same host.

We are keeping this very simple, just to demonstrate the concepts. Configuring a Cloudflare tunnel in production requires using Cloudflare's DNS and setting up a domain name. This is not covered in this lab. Folks interested in configuring a production tunnel should refer to the [Cloudflare Tunnels Quickstart](https://developers.cloudflare.com/cloudflare-one/connections/connect-application/app-tunnel/quickstart/) documentation.

### Prerequisites
- Docker installed

## Instructions

Follow these instructions to setup a test Cloudflare Tunnel as a container running the `cloudflared` container image. The target for the tunnel will be a simple `nginx` web server, running in a container on the same host.

### nginx

We will use the Chainguard [nginx](https://images.chainguard.dev/directory/image/nginx/overview/?utm_source=bradmorgan&utm_medium=devinfluencers&utm_campaign=FY25-DevInfluencers) dev image as our test application

1. pull nginx image docker pull cgr.dev/chainguard/nginx:latest-dev
2. 
```
docker run -d -p 8080:8080 cgr.dev/chainguard/nginx:latest
```
3. Verify you can connect to nginx 
```
http://localhost:8080/
```
4. get the IP address of the container
	1. `docker ps` to see a list of running containers
	2. `docker inspect <container_name>` and get the IP address

### Cloudflare Tunnel

We will be using [Quick Tunnels](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/do-more-with-tunnels/trycloudflare/)

1. Pull cloudflared image from Docker Hub 
```
docker pull cloudflare/cloudflared:latest
```
2. 
```
docker run cloudflare/cloudflared:latest tunnel --no-autoupdate --url <ip_address_of_nginx_container:8080
```
*don't run detached because we need to see the output*
3. Copy URL in the message to connect to the nginx welcome page

