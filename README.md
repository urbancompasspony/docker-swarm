# docker-swarm
Scripts to set and adjust a Docker Swarm Cluster!

# Creating a new Cluster

docker swarm init --advertise-addr enp3s0 --data-path-addr enp2s0

docker swarm join --token XXXXXXXXXXXX --data-path-addr enp2s0 xx.xx.xx.xx:2377

## Commands for maintenance:

$ docker service inspect

$ docker service ls

$ docker service rm

$ docker service scale

$ docker service ps

$ docker service update
