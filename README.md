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

```
$ sudo docker images
REPOSITORY                          TAG                               IMAGE ID       CREATED        SIZE
192.168.33.1:5000/face_recognizer   1.0.1                             00d190c20bbf   13 hours ago   10.8GB
face_recognizer                     1.0.1                             00d190c20bbf   13 hours ago   10.8GB
nvidia/cuda                         11.4.1-cudnn8-devel-ubuntu20.04   03c5d80db721   5 weeks ago    9.07GB
nvcr.io/nvidia/driver               470.57.02-ubuntu20.04             15eeb055da6a   2 months ago   826MB
```

```
$ sudo cat /etc/docker/daemon.json
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}

$ sudo docker push 192.168.33.1:5000/face_recognizer:1.0.1
The push refers to repository [192.168.33.1:5000/face_recognizer]
Get https://192.168.33.1:5000/v2/: http: server gave HTTP response to HTTPS client
```
```
$ sudo cat /etc/docker/daemon.json
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    },
    "insecure-registries":["192.168.33.1:5000"]
}

$ sudo systemctl restart docker

$ sudo docker push 192.168.33.1:5000/face_recognizer:1.0.1
The push refers to repository [192.168.33.1:5000/face_recognizer]
d25dbb7b3ab2: Pushed 
29fa6d85fa83: Pushed 
56948da53cf7: Pushed 
2bd623da57f6: Pushed 
0d4dbb18f3a1: Pushed 
0010cfbe829b: Pushed 
d9e1c7c1738b: Pushed 
e746d9db96cf: Pushed 
1d6ebb9a2e1a: Pushed 
e675a5f8165d: Pushed 
38942435079d: Pushed 
9f6643d36b2c: Pushed 
ef5a5f130d5a: Pushed 
b926f42e1470: Pushed 
cd16f701a3dd: Pushed 
fa9b82df851f: Pushed 
24171887a192: Pushed 
4942a1abcbfa: Pushed 
1.0.1: digest: sha256:489612e5f6cb43c6815830e468a2f4467db9cd8202daadb27bc475de603deee3 size: 4107

$ curl 192.168.33.1:5000/v2/_catalog
{"repositories":["face_recognizer","ubuntu"]}

$ curl 192.168.33.1:5000/v2/face_recognizer/tags/list
{"name":"face_recognizer","tags":["1.0.1"]}

```
