# README

In this lesson, we will learn how to use MCP servers to create our Docker container from [lesson_1](../lesson_1). We're going to use Claude Desktop (a LLM client) to interact with the MCP servers. Claude Desktop is a paid application, but it is free to use for the first 30 days. You can use Claude Desktop to interact with the MCP servers and create the Docker container. We could just as easily create a brand new container, but we're going to use the MCP servers to recreate the container from lesson_1. 

MCP is a protocol that allows us to use LLMs to inteact with datasources and tools like Github, Docker, Google Search, and more. You can find more informtion about MCP in the [MCP documentation](https://modelcontextprotocol.io/introduction/).

There are many different MCP servers available, but in this lesson, we will use the ones from the Model Context Protocol [example servers page](https://modelcontextprotocol.io/examples/). Check out the [Offical Integrations](https://modelcontextprotocol.io/integrations/) page for a list of all offical MCP servers available. Other servers are available from other sources.

The MCP protocol is still very new, so expect some bugs and issues. Also, do not expect the security of the implementation to be very mature. Remember to give the MCP server the least amount of permissions possible.

For example, use a read-only token for Github, and set it to expire in 24 hours. And there are other, more secure ways to handle the PAT, but we're keeping it simple for this lab. The MCP server will be running in a Docker container, so it will not have access to your local machine if you are running Docker as a non-root user.

## Prerequisites
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [MCP server docker](https://github.com/ckreiling/mcp-server-docker)
- [MCP server github](https://github.com/github/github-mcp-server)
- [Claude Desktop](https://claude.ai/download) (you may need to purchase a subscription to complete this lesson)

## Steps
1. Install Docker and Docker Compose
1. Install Claude Desktop
1. Follow the install instructions for the [MCP Github server](https://github.com/github/github-mcp-server?tab=readme-ov-file#prerequisites)
1. Follow the install instructions for the [MCP server docker](https://github.com/ckreiling/mcp-server-docker/tree/main#install)

### Claude MCP Server Configuration

Your `claude_desktop_config.json` file should look something like this for this lab:

```json
{
  "mcpServers": {
  "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
            "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your_github_token>"
      }
    },
    "mcp-server-docker": {
      "command": "docker",
      "args": [
       "run",
        "-i",
        "--rm",
        "-v",
        "/var/run/docker.sock:/var/run/docker.sock",
        "mcp-server-docker:latest"
      ]
    }
  }  
}
```

## Run the MCP server

1. After installing the MCP servers, you should have the `claude_desktop_config.json` file configured with the MCP server settings. You will need to (re)start Claude Desktop to load the new configuration.
1. You can verify the MCP server is running by looking at the Claude Desktop Files --> Settings --> Developer settings and checking the MCP server status.
1. You can also see that the servers are configured by clicking the filter symbol in the bottom left corner of the chat box window. Your MCP servers will be listed there.

## Using Claude Desktop to create a Docker container

1. You can ask Claude to list the containers by asking it to "list my docker containers on my local machine". This will list the containers on your local machine. 
1. You can also ask Claude to list the files in one of your Github repositiories by asking it to "list the files in my Github repository".
1. Now, you can ask Claude to recreate the Docker container from `lesson_1`. You can do this by giving it the following prompt:

``` text
Use the files in github.com/beckitrue/container-app-workshop/lesson_1 repository to create a Docker container running a Flask server with the configuration found in the Dockerfile. The README.md file has directions to create the container.   You may need to delete an existing container  with the simple-web name on my computer". Read and approve the actions from Claude to create the container.
```

:white_check_mark: You'll know this worked when you have a running container with the name `simple-web` and the Flask server is running. You can check this by going to `localhost:5000` in your web browser. You should see the Flask server running.

[This is the output of my conversation with Claude](https://claude.ai/share/6dab144b-153e-4cb4-b517-4d3dfd887853). Your's may look different, but the end result should be the same - a working container running the Flask server. 

