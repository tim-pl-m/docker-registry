# docker-registry
ec2 without ecs

setup: win8.1, docker-tool-box, babun on windows/macOS

-create an aws-account
-get aws-credentials
-create a vpc(virtual private cloud, a virtual network/firewall) and a security group that fits your requirements
(i.e inbound ports 22(ssh), 2376(tcp), 5000(tcp) open; outbound all; name it i.e. docker-registry)

```shell
# install the awscli
pip install awscli
```

ubunut-image: ami-597c8236

```shell
# create the instance
docker-machine create -d amazonec2 --amazonec2-region eu-central-1 \
--amazonec2-ami ami-597c8236  --amazonec2-security-group docker-registry --amazonec2-ssh-user ubuntu \
docker-registry
# tunnel to it
docker-machine ssh docker-registry
# go admin
sudo su
# test it
docker ps

docker run -d -p 5000:5000 --restart=always --name registry registry:2
docker pull ubuntu && docker tag ubuntu localhost:5000/ubuntu
docker push localhost:5000/ubuntu
docker pull localhost:5000/ubuntu
```

open a new babun-shell:
```shell
docker-machine ls
NAME               ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
docker-registry4   -        amazonec2    Running   tcp://<ip of your node>:2376            v17.05.0-ce
docker pull <ip of your node>:5000/ubuntu

now lets secure it by restrictiong access:
```shell
# (we are still in admin mode)


```

stop and start:
docker-machine stop docker-registry
#sleep, wake up
docker-machine start docker-registry

clean up:
```shell
# leave admin mode
exit
# leave vm
exit
# remove vm
docker-machine rm -f -y docker-registry
```


sources:
https://docs.docker.com/registry/deploying
https://docs.docker.com/machine/drivers/aws/#default-amis
https://guides.github.com/features/mastering-markdown/
https://github.com/docker/machine/issues/3930























