# Docker Cheatsheet

## Container Management

```bash
# Run container
docker run <image>
docker run -d <image>  # Detached mode
docker run -it <image>  # Interactive terminal
docker run -p 8080:80 <image>  # Port mapping
docker run --name <name> <image>  # Named container

# List running containers
docker ps
docker ps -a  # All containers including stopped

# Start container
docker start <container-id/name>

# Stop container
docker stop <container-id/name>

# Restart container
docker restart <container-id/name>

# Remove container
docker rm <container-id/name>  # Only removes stopped containers

# WARNING: Destructive commands
# docker rm -f <container-id/name>  # Force remove running containers
# docker container prune           # Remove all stopped containers

```

## Image Management

```bash
# List images
docker images
docker image ls

# Pull image
docker pull <image>
docker pull <image>:<tag>

# Build image
docker build -t <name>:<tag> .
docker build -t <name>:<tag> -f <dockerfile> .

# Remove image
docker rmi <image>:<tag>  # Use with caution

# Tag image
docker tag <source> <target>

# Push image
docker push <image>:<tag>

# WARNING: Destructive commands
# docker rmi <image-id>
# docker image prune -a  # Remove all unused images

```

## Container Inspection

```bash

# View logs
docker logs <container-id/name>
docker logs -f <container-id/name>  # Follow logs
docker logs --tail 100 <container-id/name>

# Execute command in running container
docker exec -it <container-id/name> <command>
docker exec -it <container-id/name> /bin/bash

# Inspect container
docker inspect <container-id/name>

# View container stats
docker stats
docker stats <container-id/name>

# View container processes
docker top <container-id/name>

# Copy file from/to container
docker cp <container-id/name>:/path/to/file /local/path
docker cp /local/path <container-id/name>:/path/to/file

```

## Docker Compose

```bash
# Start services
docker-compose up
docker-compose up -d  # Detached mode

# Stop services
docker-compose down

# Build and start
docker-compose up --build

# View logs
docker-compose logs
docker-compose logs -f  # Follow
docker-compose logs <service-name>

# Execute command in service
docker-compose exec <service-name> <command>

# Scale services
docker-compose up --scale <service>=3

# List services
docker-compose ps

# Restart service
docker-compose restart <service-name>

```

## Network Management

```bash
# List networks
docker network ls

# Create network
docker network create <network-name>

# Inspect network
docker network inspect <network-name>

# Connect container to network
docker network connect <network-name> <container>

# Disconnect container
docker network disconnect <network-name> <container>

# Remove network
docker network rm <network-name>

```

## Volume Management

```bash
# List volumes
docker volume ls

# Create volume
docker volume create <volume-name>

# Inspect volume
docker volume inspect <volume-name>

# Remove volume
docker volume rm <volume-name>

# Mount volume
docker run -v <volume-name>:/path <image>
docker run -v /host/path:/container/path <image>

# WARNING: Destructive commands
# docker volume prune  # Removes all unused volumes

```

## System Management

```bash
# System information
docker info

# Docker version
docker version

# System disk usage
docker system df

# WARNING: Destructive commands
# docker system prune  # Remove unused data
# docker system prune -a  # Remove all unused
# docker system prune -a --volumes  # Remove all including volumes

```

## Advanced Usage

```bash
# Run with environment variables
docker run -e VAR=value <image>
docker run --env-file .env <image>

# Run with resource limits
docker run --memory="512m" --cpus="1.0" <image>

# Run with restart policy
docker run --restart=always <image>
docker run --restart=unless-stopped <image>

# WARNING: Use host network carefully
# docker run --network=host <image>

# Save/load images
docker save -o <file.tar> <image>
docker load -i <file.tar>

```

## Dockerfile Best Practices

```dockerfile
# Multi-stage build
FROM maven:3.8-openjdk-11 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn package -DskipTests

FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

```

## Useful Commands

```bash
# Search images in registry
docker search <term>

# View image history
docker history <image>

# WARNING: Advanced/rarely used commands
# docker commit <container-id> <image-name>
# docker diff <container-id>
# docker pause <container-id>
# docker unpause <container-id>

# Rename container
docker rename <old-name> <new-name>

```
