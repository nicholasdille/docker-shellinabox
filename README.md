# `docker-shellinabox`

This image provides Docker-in-Docker with web-based access using [Shell In A Box](https://github.com/shellinabox/shellinabox) including [sockguard](https://github.com/buildkite/sockguard) to mitigate host breakouts.

## Building

The following command builds `shellinabox` based on the latest stable version of Docker:

```bash
docker build --tag shellinabox .
```

To select a specific version of Docker, supply `DOCKER_VERSION` as build argument:

```bash
docker build --tag shellinabox:18.09 --build-arg DOCKER_VERSION=18.09 .
```

`DOCKER_VERSION` defaults to `stable`.

## Usage

By default, `shellinabox` is published on port 4200:

```bash
docker run -d --privileged --publish 80:4200 shellinabox
```

Overriding the following environment variables, forces the shell to under the specified user and group:

- `SHELL_USER`
- `SHELL_GROUP`

```bash
docker run -d --privileged --env SHELL_USER=groot --env SHELL_GROUP=groot --publish 80:4200 shellinabox
```

By default, `sockguard` prevents privileged containers as well as bind mounts. If you need those, `sockguard` can be disabled:

```bash
docker run -d --privileged --env ENABLE_SOCKGUARD=false shellinabox
```

