# docker-swarm
Scripts to set and adjust a Docker Swarm Cluster!

# Creating a new Cluster

$ docker swarm init --advertise-addr enp3s0 --data-path-addr enp2s0

$ docker swarm join --token XXXXXXXXXXXX --data-path-addr enp2s0 xx.xx.xx.xx:2377

# Visualizer

$ docker service create -d --name=viz --publish=8080:8080/tcp --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer

# Network MacVLAN

manager1==>

docker network create --config-only --subnet 100.98.26.0/24 -o parent=ens160.60 --ip-range 100.98.26.100/24 collabnet

worker1==>

docker network create --config-only --subnet 100.98.26.0/24 -o parent=ens160.60 --ip-range 100.98.26.100/24 collabnet

manager1==> 

docker network create -d macvlan --scope swarm --config-from collabnet swarm-macvlan

Model to deploy:

docker service create –replicas 1 –name wordpressdb1 –network swarm-macvlan –env MYSQL_ROOT_PASSWORD=collab123 –env MYSQL_DATABASE=wordpress mysql


## Commands for maintenance:

$ docker service inspect

$ docker service ls

$ docker service rm

$ docker service scale

$ docker service ps

$ docker service update
