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

# Run
docker run \ 
  --rm \                    # rm when exits
  --detach \                # in background
  --env KEY=VALUE \         # env variables
  --ip 10.10.9.75 \         # ip address
  --publish 3000:3000 \
  --volume my_volume \
  --name my_container \
  --tty --interactive \ 
  --volume /my_volume \
  --workdir /app \ 
  IMAGE bash


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