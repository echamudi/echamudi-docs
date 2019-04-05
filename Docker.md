# Docker
```sh
# List
docker stack ls 
docker image ls 
docker network ls 
docker container ls # running cotainers only
docker container ls -a # -all

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

# Delete
docker rm <container-name>
docker rm <image-name>
docker stack rm <stack-name>

# Clean unused stuffs
docker system prune             # delete all unused objects
docker system prune --volumes   # delete all unused objects + volumes
docker stop $(docker ps -a -q)  # stop all containers
docker container prune          # delete stopped containers
docker image prune              # delete images (not tagged and not used by containers)
docker image prune -a           # delete images (not used by containers)
docker volume prune             # delete unused volumes
docker network prune            # delete unused networks

# Start and Stop Stack
docker stack deploy --compose-file <docker-compose-yml> <stack-name>  # Starting
docker rm <stack-name>                                                # Deleting

# Start and Stop Compose in Development
docker-compose up     # Starting
docker-compose up -d  # Starting in background mode
docker-compose down   # Stopping

docker-compose run <service-name> <command>   # Runs a one-time command against a service (it will create new temp container)

# Start and Stop Container
docker start <container-name>
docker stop <container-name>
docker kill <container-name> # forcefully
docker kill $(docker ps -q) # kill in batch

# enter container bash
# --interactive --tty
docker exec -i -t <container-name> /bin/bash

# update all images
docker images |grep -v REPOSITORY|awk '{print $1}'|xargs -L1 docker pull
```

## Personal Ubuntu OS for development

```sh
# Building
docker run -it -v "/Users/ezzat/ubuntu/disk:/var/disk" --name my-ubuntu ubuntu bash
  # install node
  # install mc
  # install etc...
  exit

# turn off
docker stop my-ubuntu

# turn on
docker start testvolume_myvol_1 && docker exec -it testvolume_myvol_1 bash
  cd /var/disk

# save screenshot
docker commit my-ubuntu my-ubuntu-img:backup-1
docker commit my-ubuntu my-ubuntu-img:backup-2
docker commit my-ubuntu my-ubuntu-img:backup-3

# delete screenshot
docker rmi my-ubuntu-img:backup-1
docker rmimy-ubuntu-img:backup-2

```

## Other Notes
- Using volume option like `-v "./host_folder:/container_folder"`. If `/container_folder` in the container contains some data, those data will be unvisible/deleted.