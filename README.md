# docker-registry
ec2 without ecs

setup: win8.1, docker-tool-box, babun

-create an aws-account
-get aws-credentials
-create a vpc(virtual private cloud, a virtual network/firewall) and a security group that fits your requirements
(i.e inbound port 22 and 2376 open; outbound all; for docker-machine )

```shell
# install the awscli with babun
pip install awscli
```

ubunut-image: ami-597c8236

```shell
# create the instance
docker-machine create -d amazonec2 --amazonec2-region eu-central-1 --amazonec2-ami ami-597c8236 --amazonec2-ssh-user ubuntu docker-registry

```

```shell
# tunnel to it
docker-machine ssh docker-registry
# go admin
sudo su
# test it
docker ps
# leave admin mode
exit
# leave vm
exit
# remove vm
docker-machine rm -f -y docker-registry
```






sources:
https://docs.docker.com/machine/drivers/aws/#default-amis
https://guides.github.com/features/mastering-markdown/

