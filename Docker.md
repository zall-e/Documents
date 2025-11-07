# 🐳 Docker Commands Cheat Sheet

## 📦 Container Management

### Run Container
```bash
docker run -d --name <container_name> <image_name>
docker run -d -p 8080:80 <image_name>              # port mapping
docker run -d -v /host/path:/container/path <image> # volume mount
docker run -d -e ENV_VAR=value <image>             # environment variable
docker run -d --restart unless-stopped <image>     # auto restart
```

### List Containers
```bash
docker ps           # running containers
docker ps -a        # all containers
docker ps -q        # only container IDs
```

### Start/Stop/Restart
```bash
docker start <container_id>
docker stop <container_id>
docker restart <container_id>
docker kill <container_id>    # force stop
```

### Remove
```bash
docker rm <container_id>
docker rm -f <container_id>   # force remove (running container)
docker rm $(docker ps -aq)    # remove all containers
```

### Execute Command
```bash
docker exec -it <container_id> bash
docker exec -it <container_id> sh
docker exec <container_id> <command>
```

### View Logs
```bash
docker logs <container_id>
docker logs -f <container_id>           # follow logs
docker logs --tail 100 <container_id>   # last 100 lines
```

### Container Stats
```bash
docker stats                    # real-time stats for all containers
docker stats <container_id>     # stats for specific container
docker top <container_id>       # running processes
```

### Copy Files
```bash
docker cp <container_id>:/path/to/file /host/path    # from container
docker cp /host/path <container_id>:/path/to/file    # to container
```

---

## 🖼️ Image Management

### Pull Image
```bash
docker pull <image_name>:<tag>
docker pull <image_name>        # latest tag
```

### Build Image
```bash
docker build -t <image_name>:<tag> .
docker build -t <image_name>:<tag> -f Dockerfile.prod .
docker build --no-cache -t <image_name> .
```

### Push Image
```bash
docker push <image_name>:<tag>
```

### Tag Image
```bash
docker tag <image_id> <new_name>:<tag>
docker tag <old_name>:<old_tag> <new_name>:<new_tag>
```

### List & Remove Images
```bash
docker images
docker images -q        # only image IDs
docker rmi <image_id>
docker rmi $(docker images -q)    # remove all images
```

### Save & Load Images
```bash
docker save -o <file.tar> <image_name>    # export image
docker load -i <file.tar>                 # import image
```

---

## 🌐 Network Management

```bash
docker network ls                                    # list networks
docker network create <network_name>                 # create network
docker network inspect <network_name>                # inspect network
docker network connect <network_name> <container_id> # connect container
docker network rm <network_name>                     # remove network
```

---

## 💾 Volume Management

```bash
docker volume ls                           # list volumes
docker volume create <volume_name>         # create volume
docker volume inspect <volume_name>        # inspect volume
docker volume rm <volume_name>             # remove volume
docker volume prune                        # remove unused volumes
```

---

## 🔍 Inspection & Info

```bash
docker inspect <container_or_image_id>
docker info                                # system-wide information
docker version                             # docker version
docker history <image_name>                # image layers history
```

---

## 🧹 Cleanup

### Remove Stopped Containers
```bash
docker container prune
docker container prune -f    # force (no confirmation)
```

### Remove Unused Images
```bash
docker image prune           # dangling images only
docker image prune -a        # all unused images
```

### Remove Unused Volumes
```bash
docker volume prune
```

### Remove Unused Networks
```bash
docker network prune
```

### Remove All Unused Resources
```bash
docker system prune          # containers, networks, images
docker system prune -a       # everything unused
docker system prune -a --volumes    # including volumes
```

### Show Disk Usage
```bash
docker system df             # show docker disk usage
```

---

## 🐙 Docker Compose

```bash
docker-compose up -d                    # start services
docker-compose down                     # stop and remove
docker-compose ps                       # list services
docker-compose logs -f                  # follow logs
docker-compose restart                  # restart services
docker-compose build                    # build images
docker-compose pull                     # pull images
docker-compose exec <service> bash      # exec into service
```

---

## 🚀 Quick Start Example

```bash
# Pull and run nginx
docker pull nginx
docker run -d --name my-nginx -p 80:80 nginx

# View logs
docker logs -f my-nginx

# Execute command
docker exec -it my-nginx bash

# Stop and remove
docker stop my-nginx
docker rm my-nginx

# Cleanup everything
docker system prune -a
```

---

## 💡 Useful Combinations

```bash
# Stop all running containers
docker stop $(docker ps -q)

# Remove all containers
docker rm $(docker ps -aq)

# Remove all images
docker rmi $(docker images -q)

# Remove dangling images
docker rmi $(docker images -f "dangling=true" -q)

# Show container IP address
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_id>
```
