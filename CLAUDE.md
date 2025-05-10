# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Run Commands
- Build Docker image: `docker build -t <image-name> .`
- Run container: `docker run -p <host-port>:<container-port> <image-name>`
- Run with Docker Compose: `docker-compose up`
- Stop containers: `docker-compose down`

## Code Style Guidelines
- Python: Follow PEP 8 style guidelines
- Import order: Standard libraries, third-party, local modules
- Indentation: 4 spaces for Python, 2 spaces for YAML
- Naming: Use snake_case for Python variables and functions
- Error handling: Use try/except blocks for specific exceptions
- Docker: Use specific version tags instead of 'latest'
- Comments: Add meaningful comments for complex logic
- YAML: Use consistent indentation and follow Docker Compose schema

## MCP Server Commands

- Build MCP server: `docker build -t my-mcp-server .`
- Run MCP container: `docker run -p 8080:8080 my-mcp-server`
- Run with Docker socket: `docker run -v /var/run/docker.sock:/var/run/docker.sock my-mcp-server`
- Access logs: `docker logs <container-id>`

## MCP Security Best Practices

- Use non-root users in containers
- Set memory/CPU limits
- Never use --privileged flag
- Implement proper secrets management

## MCP Deployment Patterns

- Single-server: One MCP server per container
- Gateway: Central MCP router to specialized servers
- Sidecar: MCP server alongside main application

## Repository Structure
This repository contains workshop materials for containerization labs including Dockerfiles, Docker Compose configs, and simple applications.
