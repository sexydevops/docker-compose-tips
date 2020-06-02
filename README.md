## Docker compose tips

### Using environment variables with `env_file`

For example:

Content of `docker-compose.yml` file:

```Docker
version: "3"
services:
  busybox:
    image: "nginx:alpine"
    env_file:
      - example.env
```

Content of `example.env` file:

```
REDIS_HOST=localhost
```

Now we can using command `docker exec example-env-docker-compose env` to list all the environment variables

Example output:

```
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=116525becba5
REDIS_HOST=localhost
NGINX_VERSION=1.17.10
NJS_VERSION=0.3.9
PKG_RELEASE=1
HOME=/root
```

Here we are using [`env_file`](https://docs.docker.com/compose/environment-variables/#the-env_file-configuration-option), there are some rules:

- An environment file named `.env` placed in the folder where the docker-compose command is executed
- Compose expects each line in an env file to be in VAR=VAL format.
- Comment line start with `#`, blank lines are ignored
- There is no special handling of quotation marks.
