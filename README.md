# docker-swarm
Scripts to set and adjust a Docker Swarm Cluster!

# Creating a new Cluster

$ docker swarm init --advertise-addr enp3s0 --data-path-addr enp2s0

$ docker swarm join --token XXXXXXXXXXXX --data-path-addr enp2s0 xx.xx.xx.xx:2377

# Visualizer

$ docker service create -d --name=viz --publish=1515:8080/tcp --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer

http://my_server:1515 after 1 minute!

# Network with Weave (Static)

docker plugin install weaveworks/net-plugin:latest_release

docker network create --driver=weaveworks/net-plugin:latest_release --scope swarm --attachable --subnet 172.20.0.0/24 macvlan

docker service create --rm -it --net=weave --ip=172.20.0.45 debian:jessie bash -c "ip addr     show"

# Network MacVLAN (DHCP!)

manager1==>

docker network create --config-only --subnet 172.20.0.0/24 -o parent=enp3s0 --ip-range 172.20.0.1/24 mvl-config

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
