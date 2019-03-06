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
# https://medium.com/the-code-review/top-10-docker-run-command-options-you-cant-live-without-a-reference-d256834e86c1
docker run \ 
  --rm \                    # rm when exit
  --detach \                # in background
  --env KEY=VALUE \         # env variables
  --ip 10.10.9.75 \         # ip address
  --publish 3000:3000 \
  --volume my_volume \
  --name my_container \
  --tty --interactive \ 
  --volume /my_volume \
  --workdir /app \ 
  <image-name> \
  bash                      # enter bash

docker run --name my-ubuntu-temp -it ubuntu bash

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
docker exec -i -t <container-name> /bin/bash

# update all images
docker images |grep -v REPOSITORY|awk '{print $1}'|xargs -L1 docker pull
```

## Persisting container

https://stackoverflow.com/questions/19585028/i-lose-my-data-when-the-container-exits

Using commit

```sh
docker run --name my-ubuntu -it ubuntu /bin/bash

$ # do something inside container
$ exit

docker commit <container-id> new_image_name:tag_name(optional)

```

## Personal Ubuntu OS for development

```sh
# Building
docker run -it --name my-ubuntu ubuntu bash
  exit
docker commit my-ubuntu my-ubuntu-img:latest
docker rm my-ubuntu
docker run -it -v "/Users/ezzat/ubuntu/disk:/var/disk" --name my-ubuntu my-ubuntu-img bash
  exit

# turn off
docker stop my-ubuntu

# save state
docker commit my-ubuntu my-ubuntu-img:latest

# turn on
docker start my-ubuntu
docker exec -it my-ubuntu bash
  cd /var/disk
```