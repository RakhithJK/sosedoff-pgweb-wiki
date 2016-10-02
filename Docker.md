## Requirements

In order to test and run pgweb in docker containers, make sure
you have docker installed. On linux systems, you can use docker
natively, on OSX there are few ways of installing it:

- [Docker for OSX/Linux/Windows](https://www.docker.com/products/docker)
- [Docker Toolbox](https://www.docker.com/products/docker-toolbox)
- [Vagrant](https://www.vagrantup.com/)

### Pull Image

Pgweb has an official docker image: https://hub.docker.com/r/sosedoff/pgweb/

To pull latest version, run:

```
docker pull sosedoff/pgweb
```

### Build Image

To build a new image, change directory to `pgweb` source. Then run:

```
docker build -t pgweb .
```

### Example

First, start PostgreSQL in the container (using official image):

```
docker run -d -p 5432:5432 --name db -e POSTGRES_PASSWORD=postgres postgres
```

Then start pgweb container:

```
docker run -p 8081:8081 --link db:db -e DATABASE_URL=postgres://postgres:postgres@db:5432/postgres sosedoff/pgweb
```

It should start web server on `http://localhost:8081`