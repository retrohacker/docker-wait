# docker-wait

A simple script that waits for services to be available before starting your application

# Usage

### `docker-compose.yml`

```yml
version: "2"
services:
  db:
    image: mongo
  mq:
    image: rabbitmq
  myservice:
    build: ./myapp
    command: ["myapp", "arg1", "arg2"]
    environment:
      - DOCKER_SERVICES=db:27017,mq:5672
```

### `Dockerfile`

Here we show how this would work with [`dumb-init`](https://github.com/Yelp/dumb-init), but you could easily leave that bit out.

```Dockerfile
...
ADD https://raw.githubusercontent.com/retrohacker/docker-wait/master/wait.sh /bin/wait.sh
ENTRYPOINT ["dumb-init", "--", "/bin/bash", "/bin/wait.sh"]
```
