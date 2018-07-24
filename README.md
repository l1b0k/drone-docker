# drone-docker

Drone plugin to build and publish Docker images to a container registry.

## Build

Build the binary with the following commands:

```
sh .drone.sh
```

## Docker

Build the Docker image with the following commands:

```
docker build --rm=true -f docker/Dockerfile -t plugins/docker .
```

## Usage

Execute from the working directory:

```
docker run --rm \
  -e PLUGIN_TAG=latest \
  -e PLUGIN_REPO=octocat/hello-world \
  -e DRONE_COMMIT_SHA=d8dbe4d94f15fe89232e0402c6e8a0ddf21af3ab \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  --privileged \
  plugins/docker --dry-run
```

usage in drone
```
  pull-image:
    image: <...>/drone-docker:1.0.0
    insecure: true
    privileged: true
    disable_build: true
    script:
      - chmod +x *.sh
      - ./image_helper.sh
      - ls -al
```

> note: script will run before build,if build is enabled