# 🐳 Docker Commands Cheat Sheet

## 📦 Container Management

### Run Container
```bash
docker run -d --name <container_name> <image_name>
```
`-d` detached mode | `--name` custom name

### List Containers
```bash
docker ps           # running containers
docker ps -a        # all containers
```

### Stop & Remove
```bash
docker stop <container_id>
docker rm <container_id>
```

### Execute Command
```bash
docker exec -it <container_id> bash
```

### View Logs
```bash
docker logs <container_id>
```

---

## 🖼️ Image Management

### Pull Image
```bash
docker pull <image_name>:<tag>
```

### Build Image
```bash
docker build -t <image_name>:<tag> .
```

### Push Image
```bash
docker push <image_name>:<tag>
```

### Remove Image
```bash
docker rmi <image_id>
```

### List Images
```bash
docker images
```

---

## 🔍 Inspection

```bash
docker inspect <container_or_image_id>
```

---

## 🧹 Cleanup

### Remove Stopped Containers
```bash
docker container prune
```

### Remove Unused Images
```bash
docker image prune -a
```

### Remove All Unused Resources
```bash
docker system prune -a
```
⚠️ **Warning:** This removes all unused data

---

## 🚀 Quick Start Example

```bash
# Pull an image
docker pull nginx

# Run container
docker run -d --name my-nginx -p 80:80 nginx

# View logs
docker logs my-nginx

# Stop and remove
docker stop my-nginx && docker rm my-nginx
```
