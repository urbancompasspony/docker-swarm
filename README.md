# docker-swarm
Scripts to set and adjust a Docker Swarm Cluster!

# Creating a new Cluster

$ docker swarm init --advertise-addr enp3s0 --data-path-addr enp2s0

$ docker swarm join --token XXXXXXXXXXXX --data-path-addr enp2s0 xx.xx.xx.xx:2377

# Visualizer

$ docker service create -d --name=viz --publish=8080:8080/tcp --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer

# Network MacVLAN

manager1==>

docker network create --config-only --subnet 192.168.1.0/24 -o parent=eth0 --ip-range 192.168.1.150/32 mvl-config

docker network create -d macvlan --scope swarm --attachable --config-from mvl-config macvlan

Model to deploy:

docker service create --replicas 2 --name mvl-net-example --network macvlan busybox:latest sleep 3600

docker service create –replicas 1 –name wordpressdb1 –network macvlan –env MYSQL_ROOT_PASSWORD=collab123 –env MYSQL_DATABASE=wordpress mysql

## Commands for maintenance:

$ docker service inspect

$ docker service ls

$ docker service rm

$ docker service scale

$ docker service ps

$ docker service update
