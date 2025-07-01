# MCP Server with Docker

This project demonstrates how to run an MCP (Model Control Protocol) server using Docker. The server provides a simple calculator tool that can be accessed by a client.

## Prerequisites

- Docker installed on your system
- Git (to clone the repository)

## Project Structure

- `server.py`: The MCP server implementation with a simple calculator tool
- `client.py`: A client that connects to the server and calls the calculator tool
- `Dockerfile`: Instructions for building the Docker image
- `requirements.txt`: Python dependencies for the project

## Running with Docker

### Step 1: Build the Docker image

```bash
docker build -t mcp-server .
```

### Step 2: Run the Docker container

```bash
docker run -p 8050:8050 mcp-server
```

This will start the MCP server inside a Docker container and expose it on port 8050.

## Running the Client

Once the server is running, you can run the client in a separate terminal:

```bash
python client.py
```

The client will connect to the server, list available tools, and call the calculator tool to add 2 and 3.

## Expected Output

### Server Output:
```
INFO:     Started server process [9]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8050 (Press CTRL+C to quit)
```

### Client Output:
```
Available tools:
  - add: Add two numbers together
2 + 3 = 5
```

## Docker Commands Reference

### View running containers:
```bash
docker ps
```

### View container logs:
```bash
docker logs <container_id>
```

### Stop the container:
```bash
docker stop <container_id>
```

### Remove the container:
```bash
docker rm <container_id>
```

### Remove the image:
```bash
docker rmi mcp-server
```

## Troubleshooting

If you encounter connection issues:

1. **Check if the server is running**: Make sure the Docker container is running with `docker ps`.

2. **Verify port mapping**: Ensure the port is correctly mapped with `docker ps` or by checking the output of the `docker run` command.

3. **Check server logs**: View the server logs with `docker logs <container_id>` to see if there are any errors.

4. **Host binding**: The server is configured to bind to `0.0.0.0` instead of `127.0.0.1` to make it accessible from outside the container. If you're still having issues, you might need to check your firewall settings.

5. **Network issues**: If you're running Docker on a remote machine, make sure the port is accessible from your client machine.

6. **Docker connectivity issues**: If you can't pull the base image, try:
   - Restarting Docker Desktop
   - Checking your internet connection
   - Configuring proxy settings in Docker Desktop if behind a corporate firewall

## Technical Details

- **Base Image**: `python:3.11-slim`
- **Package Manager**: `uv` for faster dependency installation
- **Transport**: SSE (Server-Sent Events)
- **Port**: 8050
- **Protocol**: MCP (Model Control Protocol)

## Development

To modify the server:

1. Edit `server.py` to add new tools or modify existing ones
2. Rebuild the Docker image: `docker build -t mcp-server .`
3. Run the new container: `docker run -p 8050:8050 mcp-server`

## Notes

- The server is configured to use SSE (Server-Sent Events) transport and listens on port 8050.
- The client connects to the server at `http://localhost:8050/sse`.
- Make sure the server is running before starting the client.
- The container runs in the foreground by default. Use `Ctrl+C` to stop it, or add `-d` flag to run in detached mode: `docker run -d -p 8050:8050 mcp-server`
