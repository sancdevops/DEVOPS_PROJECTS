
GOAL : 
This project compromises of 2 web-servers and a haproxy which on round robin routes requests to each of the webserver . 

Steps : 
1. Create 3 folders (Web1, Web2, haproxy)
2. On web1 and web2  folder place a html page and create the Dockerfile which will run a nginx proxy which will host the page on that docker 
3. From the folder web1 (docker build -t server1 . ) and similarly for web2
   > docker build -t server1 .
   > docker build -t server2 .

4. Similary create haproxy image 
    > docker build -t myhaproxy
5. Create a network so that the 3 dockers can communicate 
   > docker network create java_app_ha

6. Validate the create images and network 
 > docker images -all
 > docker network ls 

7. Run the web1 and web2 and haproxy on the 3 on the network with publish port 
> docker run -d --name=server1 --network=java_app_ha server1

> docker run -d --name=server2 --network=java_app_ha server2

> docker run -d --name=myhaproxy --network=java_app_ha -p 90:80 haproxy

8. Check the request roundrobin 
> curl localhost:90
Server one  
> curl localhost:90
Server two

#Troubleshoots:
Check the logs of a container 
> docker log ced23e32ee3

check if a container is not running 
> docker ps -a

stop and remove a container  
> docker stop  cc8235833ffb ; docker rm cc8235833ffb

Remove image 
> docker rmi haproxy:2.0

remove all hanging or dead containers
> docker system prune

#Gyaan

Containers do not have a public IPv4 address, they have only a private address. Therefore all services running in a container must be exposed port by port.

Container ports must be mapped to the ports of the host to avoid conflicts.

Crete a network
> docker network create java_app_ha



