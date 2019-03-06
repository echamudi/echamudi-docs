# Docker
```sh
# List containers
docker ps # running only
docker ps -a # -all

# List images
docker images

# Download image
docker pull <image-name>

# Build image and save name
# --tag 
docker build -t <image-name> .

# Compose and run in background
# --detach
docker-compose up -d 

# Delete
docker rm <container-name>
docker rm <image-name>
docker rm $(docker ps -a -q) # delete all stopped containers
docker rmi $(docker images -q) # delete all images

# Start and stop
docker start <container-name>
docker stop <container-name>
docker kill <container-name> # forcefully
docker kill $(docker ps -q) # kill in batcs

# enter container bash
# --interactive --tty
docker exec -i -t <container-name> bash
```