## Setup Networking
```
docker network create mongo-network
```

## Deploy MongoDB
- `docker-compose -f stack-mongo.yml -p mongo up -d`
- *RPI*: `docker-compose -f stack-mongo.yml -f stack-mongo.armhf.yml -p mongo up -d`
- *DEVEL*: `docker-compose -f stack-mongo.yml -f stack-mongo.devel.yml -p mongo up -d`
