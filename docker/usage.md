# Container networking
https://docs.docker.com/config/containers/container-networking/
```
Flag value	                Description
===============================================================================
-p 8080:80	                Map TCP port 80 in the container to port 8080 on the Docker host.
-p 192.168.1.100:8080:80	Map TCP port 80 in the container to port 8080 on the Docker host for connections to host IP 192.168.1.100.
-p 8080:80/udp	                Map UDP port 80 in the container to port 8080 on the Docker host.
-p 8080:80/tcp -p 8080:80/udp	Map TCP port 80 in the container to TCP port 8080 on the Docker host, and map UDP port 80 in the container to UDP port 8080 on the Docker host.
```

# save containter as image (commit)
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

Name, shorthand	Default	Description
--author , -a		Author (e.g., “John Hannibal Smith hannibal@a-team.com”)
--change , -c		Apply Dockerfile instruction to the created image
--message , -m		Commit message
--pause , -p	true	Pause container during commit
