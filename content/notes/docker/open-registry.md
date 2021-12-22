---
title: Docker Registry
type: docs
---

Docker provides a free registry which is distributed as a [docker image](https://hub.docker.com/_/registry/). 
While it is easy to get up and running with a registry maintaining one long term isn't what most people want to spend there time doing. 
With that in mind I would consider using a SaaS offering such as [Docker Hub](https://hub.docker.com), [Google Container Registery](https://cloud.google.com/container-registry/), or [EC2 Container Registry](https://aws.amazon.com/ecr/).

## Set up a docker registry with Basic Auth  
1. Provision an Ubuntu machine, Install docker, docker-compose, apache2-utils, openssl  
2. Create a selfsigned cert and key and place it in /auth/certs (alternatively obtain a real cert)  
One method of creating a selfsigned cert is this:
```
echo 01 | sudo tee ca.srl > /dev/null
openssl req -newkey rsa:4096 -nodes -sha256 -keyout domain.key -x509 -days 365 -out domain.crt
```  
2.	Create a htpasswd file in /apps/auth with your user(s) and password(s)
htpasswd -cB passwordfile user
3.	Create a file docker-compose.yml similar to this:  
```yml
apps:  
  restart: always  
  image: registry:2.2  
  ports:  
    - 5000:5000  
  environment:  
    REGISTRY_HTTP_TLS_CERTIFICATE: /certs/domain.crt  
    REGISTRY_HTTP_TLS_KEY: /certs/domain.key  
    REGISTRY_AUTH: htpasswd  
    REGISTRY_AUTH_HTPASSWD_PATH: /auth/passwordfile  
    REGISTRY_AUTH_HTPASSWD_REALM: Registry Realm
  volumes:  
    - /apps/certs:/certs  
    - /apps/auth:/auth  
```
4.	From the directory of your docker-compose.yml run `docker-compose up –d`  

### Using the registry  
-You will need to have the insecure-registry flag added to your docker daemon options on all hosts you wish to interact with the registry with (required for any registry without a trusted cert)  
-You will need to login to the docker registry before you interact with it: docker login <host>:<port>  
-Login will prompt you for an email, you can enter anything