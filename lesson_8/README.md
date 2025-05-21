# README

In this lesson, we will learn how to use MCP servers to create our Docker container from [lesson_1](../lesson_1). 

MCP is a protocol that allows us to use LLMs to inteact with datasources and tools like Github, Docker, Google Search, and more. You can find more informtion about MCP in the [MCP documentation](https://modelcontextprotocol.io/introduction/).

There are many different MCP servers available, but in this lesson, we will use theones from the [example servers page](https://modelcontextprotocol.io/examples/).

The MCP protocol is still very new, so expect some bugs and issues. Also, do not expect the security of the implementation to be very mature. Remember to give the MCP server the least amount of permissions possible.

For example, use a read-only token for Github, and do not give it access to your Docker daemon. The MCP server will be running in a Docker container, so it will not have access to your local machine.

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

## Run the MCP server

1. After installing the MCP servers, you should have the `claude_desktop_config.json` file configured with the MCP server settings. You will need to (re)start Claude Desktop to load the new configuration.
1. You can verify the MCP server is running by looking at the Claude Desktop Files --> Settings --> Developer settings and checking the MCP server status.
1. You can also see that the servers are configured by clicking the filter symbol in the bottom left corner of the chat box window. Your MCP servers will be listed there.

## Using Claude Desktop to create a Docker container

1. You can ask Claude to list the containers by asking it to "list my docker containers on my local machine". This will list the containers on your local machine. 
1. You can also ask Claude to list the files in one of your Github repositiories by asking it to "list the files in my Github repository".
1. Now, you can ask Claude to recreate the Docker container from `lesson_1`. You can do this by asking it to "create a Docker container from the Dockerfile in my Github repository lesson_1 files". Follow the prompts from Claude to create the container.
