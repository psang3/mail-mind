# Docker Setup for Email Generator System

This document provides instructions for building, running, and managing the dockerized version of the Email Generator System.

## Prerequisites

- Docker installed on your machine
- Docker Compose installed on your machine

## Project Structure

The dockerized application consists of the following components:

- **Backend Service**: Spring Boot application running on port 8080
- **Frontend Service**: React application served by Nginx on port 80

## Docker Files

- `Dockerfile` - Builds the Spring Boot backend service
- `mail-mind-react/Dockerfile` - Builds the React frontend service
- `docker-compose.yml` - Orchestrates the multi-container application
- `.dockerignore` - Specifies which files should be ignored during Docker build
- `mail-mind-react/.dockerignore` - Docker ignore file for the React application
- `mail-mind-react/nginx.conf` - Nginx configuration for the React frontend

## Building and Running

### Using Docker Compose (Recommended)

To build and start all services:

```bash
docker-compose up --build
```

To run in detached mode:

```bash
docker-compose up -d
```

To stop all services:

```bash
docker-compose down
```

### Building Individual Images

To build the backend image:

```bash
docker build -t email-generator-api .
```

To build the frontend image:

```bash
cd mail-mind-react
docker build -t email-generator-ui .
```

### Running Individual Containers

To run the backend container:

```bash
docker run -p 8080:8080 --name email-generator-api email-generator-api
```

To run the frontend container (ensure backend is running first):

```bash
docker run -p 80:80 --name email-generator-ui --link email-generator-api:backend email-generator-ui
```

## Accessing the Application

- Backend API: http://localhost:8080/api/emails
- Frontend UI: http://localhost

## Logs and Troubleshooting

To view logs for all services:

```bash
docker-compose logs
```

To view logs for a specific service:

```bash
docker-compose logs backend
# or
docker-compose logs frontend
```

To follow logs in real-time:

```bash
docker-compose logs -f
```

## Container Management

To list running containers:

```bash
docker-compose ps
# or
docker ps
```

To restart a service:

```bash
docker-compose restart backend
# or
docker-compose restart frontend
```

## Production Considerations

For production deployment:

1. Use environment variables for sensitive configuration
2. Implement proper health checks
3. Set up container orchestration (Kubernetes or Docker Swarm)
4. Configure TLS/SSL for secure communication
5. Set up monitoring and logging

## Browser Extension

The browser extension is not containerized as it runs in the browser. You'll need to install it separately in your browser.

## Common Issues

1. **Backend not accessible from frontend**:
   - Check that the backend container is running
   - Verify network configuration in docker-compose.yml
   - Check Nginx configuration in the frontend container

2. **Changes not reflected after rebuild**:
   - Try removing containers and volumes before rebuilding
   - Use `docker-compose up --build --force-recreate`

3. **Port conflicts**:
   - Ensure no other services are using ports 80 or 8080
   - Modify port mappings in docker-compose.yml if needed
