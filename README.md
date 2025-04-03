# Docker Commands & Guide
## || Author : Tushar Behera

## Installation on Amazon Linux 2023
```sh
sudo yum install docker -y
```

## Managing Docker Service
```sh
sudo service docker start   # Start Docker service
sudo systemctl stop docker.socket  # Stop Docker socket
```

## Working with Docker Images
```sh
docker pull <image_name>   # Pull image from Docker Hub
docker images   # List available local images
```

## Managing Containers
```sh
docker ps        # Show running containers
docker ps -a     # Show all containers (running & stopped)
```

### Running a Container
```sh
docker run -it --name <container_name> <image_name> /bin/bash
```

### Controlling Containers
```sh
docker start <container_name>  # Start a stopped container
docker stop <container_name>   # Stop a running container
docker attach <container_name> # Attach to a running container
exit   # Exit and stop the container
```

### Removing Containers
```sh
docker rm <container_name>  # Remove a container (must be stopped)
docker container prune  # Remove all stopped containers
```

### Stopping All Containers
```sh
docker kill $(docker ps -q)
```

### Logging & Execution
```sh
docker log <container_id>  # View container logs
docker exec -it <container_name> bash  # Enter a running container
```

## Exiting a Container
```sh
exit   # Stop container and exit
Ctrl + P + Q  # Detach from container without stopping it
```

## Checking Container Modifications
```sh
docker diff <container_name>  # View changes (A = Added, D = Deleted, C = Changed)
docker commit <container_name> <new_image_name>  # Save container as new image
```

## Dockerfile Basics
- The filename must be `Dockerfile` (capitalized)
```sh
docker build -t <image_name> .  # Build image from Dockerfile
```

## Volumes
### Defining in Dockerfile
```dockerfile
VOLUME ["/volume_name"]
```

### Creating a Volume with a Container
```sh
docker run -it --name <container_name> -v /volume_name <image_name> /bin/bash
```

### Sharing Volumes Between Containers
```sh
docker run -it --name <new_container> --volumes-from <existing_container> <image_name> /bin/bash
```

### Sharing Volumes with Host System
```sh
docker run -it --name <container_name> -v /home/user:/container_dir --privileged=true <image_name> /bin/bash
```

## Port Mapping
```sh
docker run -td --name <container_name> -p 80:80 <image_name>
docker run -d -p 8000:8000 <image_name>  # Detached mode
```

## Networking
```sh
docker network ls  # List networks
docker network inspect <network_name>  # Inspect network
docker network create <network_name> -d bridge  # Create a network
```
```sh
docker run -d --name <container_name> --network <network_name>
```

## Docker Compose
### Installing Docker Compose
```sh
apt install docker-compose-v2  # Ubuntu
curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose  # Amazon Linux
```

### Running Docker Compose
```sh
vi docker-compose.yml  # Create a compose file
docker compose up  # Run the compose file
```

## Logging into Docker Hub via CLI
1. Create an account
2. Generate an access token with `read, write, delete` permissions
3. Use the token for login

### Tagging & Pushing an Image
```sh
docker image tag <old_image>:<version> <username>/<new_image>:latest
```

## Monitoring Containers
```sh
nohup docker attach <container_id> &  # Attach logs in background
```

---
### **Notes**
- Use `Ctrl + P + Q` to detach from a container without stopping it.
- Ensure containers are stopped before removal.
- Always map ports correctly when running applications inside containers.
