# wstunnel-docker
docker image of wstunnel v5 - for run Client or Server Tunnel

how i can build it and push to docker-hub:
```
# build
docker build -t wstunnel .
# set tag
docker tag wstunnel:latest -----/wstunnel:latest
# push
docker push ------/wstunnel:latest
```

# Simple run:

ws : http - wss : https<br />
```docker run --network host -d -e COMMAND="/usr/local/bin/wstunnel -v --server ws://0.0.0.0:33344 --restrictTo=127.0.0.1:51820" --name wstunnel --restart unless-stopped javidi/wstunnel```

## Docker compose file:
```
version: '3'
services:
  wstunnel-server:
    image: javidi/wstunnel:latest
    container_name: ws-srv
    restart: unless-stopped
    network_mode: host
    environment:
      #local
      - COMMAND=/usr/local/bin/wstunnel -v --server ws://0.0.0.0:33344 --restrictTo=127.0.0.1:51820
      #external
      #- COMMAND=/usr/local/bin/wstunnel -v --server ws://0.0.0.0:33344
```

## Suggestion:
run nginx and use it
doc at github [Wireguard over WebSocket](https://gist.github.com/jvdi/913549b4e329b9382459033322bf393d)
