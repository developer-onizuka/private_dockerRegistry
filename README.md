# private_dockerRegistry

```
$ sudo docker pull registry:2.7.1
$ sudo docker run --rm --name registry -d -p 5000:5000 -v /mnt/registry:/var/lib/registry registry:2.7.1

$ sudo docker tag ubuntu:20.04 localhost:5000/ubuntu:20.04
$ sudo docker images
$ sudo docker push localhost:5000/ubuntu:20.04


$ sudo docker pull localhost:5000/ubuntu:20.04

$ curl http://localhost:5000/v2/_catalog
{"repositories":["ubuntu"]}

$ curl http://localhost:5000/v2/ubuntu/tags/list
{"name":"ubuntu","tags":["20.04"]}

```
