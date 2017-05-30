# docker-net
Another docker network helper  
Disable SELINUX first.

## Feture
* Assign static ip for container
* Assign more than one ip to docker container
* Control container route
* Easy to configure network  

## Install

**Install docker-net**
```
curl -L "https://github.com/zggy/docker-net/raw/master/docker-net" > /usr/bin/docker-net
chmod +x /usr/bin/docker-net
```

## Usage

**Create a test docker container and docker network**   

`docker run -tid --name test-docker-net alpine sh`   
`docker network create test-network`   

**Command**  

* Ping from container   
`docker-net <container-name> ping <host>`  
explame: `docker-net test-docker-net ping 8.8.8.8`   
*when you assign ip use macvlan type, use this command for switch get arp*   
* Get container route    
`docker-net <container-name> route`  
explame: `docker-net test-docker-net route`

* Set container static route    
`docker-net <container-name> route "<ip route command>"`  
explame: `docker-net test-docker-net route "add 8.8.8.8 dev eth0"`

* Get container interface    
`docker-net <container-name> ip`  
explame: `docker-net test-docker-net ip`

* Get container interface with specify docker network   
`docker-net <container-name> ip <network>`  
explame: `docker-net test-docker-net ip test-network`    
*then you will get container have not connect to test-docker-net*

* Connect container to specify docker network port and flush interface    
`docker-net <container-name> ip <network> flush`    
explame: `docker-net test-docker-net ip test-network flush`   
*then you can try to get container interface again*

* Connect container to specify docker network port and assign a IP address     
`docker-net <container-name> ip <network> 10.0.0.2/24`     
explame: `docker-net test-docker-net ip test-network 10.0.0.2/24`   
*then you can try to get container interface again*

* Delete container IP at specify docker network port   
`docker-net <container-name> ip <network> del`    
explame: `docker-net test-docker-net ip test-network 10.0.0.2/24 del`

* Disconnect container from specify docker network    
`docker-net <container-name> ip <network> del`   
explame: `docker-net test-docker-net ip test-network del`


Thanks for pipework https://github.com/jpetazzo/pipework
