### Directory Structure

```
.docker
docker-compose.yml
your-application-root
```

### Build the containers:

`$ docker-compose build`

### And run the server:

`$ docker-compose up`

### After that, all you need to do is install the dependencies:

`$ docker-compose run app composer --prefer-source install`

###/bin/sh:

`& docker run -it mia_app /bin/sh`


