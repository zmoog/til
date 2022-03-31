# How to run the Elastic Agent with access to ECS Task Metadata endpoint

Thanks to [@mtojek](https://github.com/mtojek), I discovered a nice [blog post from AWS](https://aws.amazon.com/blogs/compute/a-guide-to-locally-testing-containers-with-amazon-ecs-local-endpoints-and-docker-compose/) about how to locally testing ECS Local Endpoints.

## Solution A: Toss containers in

Simple solution where we `stack up` the dev environment and toss a couple of carefully crafted containers using `docker run`.

### Start you dev stack

```shell
$ elastic-package stack up -v -d
...
```

### Find the network

The first think is to locate the network used by the stack containers:

```shell
$ docker network ls
NETWORK ID     NAME                            DRIVER    SCOPE
38ee458eed0a   bridge                          bridge    local
4f60e5ced33a   elastic-package-stack_default   bridge    local <——— 👀
6e9d2aa908d4   host                            host      local
32ea7f983e52   none                            null      local
```

Let's pick the `elastic-package-stack_default` network.

### Add the ECS Task Metadata endpoint

Next, we need to set up an ECS Metadata endpoint in the same way Fargate provides one. We are so lucky today because AWS build one for us, in the form of a Docker image.

Run the `amazon-ecs-local-container-endpoints` image and attach it to the stack network:

```shell
docker run --rm \
    --name amazon-ecs-local-container-endpoints \
    --network elastic-package-stack_default \
    --volume /var/run:/var/run \
    -i amazon/amazon-ecs-local-container-endpoints
```

Let's take a look at this container's detail and take not of the IP address:

```shell
$ docker inspect amazon-ecs-local-container-endpoints | jq '.[].NetworkSettings.Networks'
{
  "elastic-package-stack_default": {
    "IPAMConfig": null,
    "Links": null,
    "Aliases": [
      "8c250f699e8a"
    ],
    "NetworkID": "4f60e5ced33a15babe89ff7620f93715a1c2128a593bac59b279e779371855d3",
    "EndpointID": "b0e321c7129de8378ffb6c42ae7ec9c6773a51f54b3075eeeb79445842dc0f56",
    "Gateway": "172.20.0.1",
    "IPAddress": "172.20.0.4",
    "IPPrefixLen": 16,
    "IPv6Gateway": "",
    "GlobalIPv6Address": "",
    "GlobalIPv6PrefixLen": 0,
    "MacAddress": "02:42:ac:14:00:04",
    "DriverOpts": null
  }
}
```

Nice, the IP address is `172.20.0.4`, let's test if task metadata endpoint is working as expected:

```shell
$ docker exec -it amazon-ecs-local-container-endpoints /bin/bash
bash-4.2# curl -i http://172.20.0.4/v3
HTTP/1.1 200 OK
Content-Type: application/json
Date: Wed, 30 Mar 2022 13:27:22 GMT
Content-Length: 663

{
  "DockerId": "8c250f699e8a8bc3d692f6c00d00402244859c0de14ef3036f418d3013fffa7f",
  "Name": "amazon-ecs-local-container-endpoints",
  "DockerName": "amazon-ecs-local-container-endpoints",
  "Image": "amazon/amazon-ecs-local-container-endpoints",
  "ImageID": "sha256:b005329f50b1ae4e79c04aee4f1044ccad484d0c5fa2d3c85e8679729e61e1c1",
  "Ports": [
    {
      "ContainerPort": 80,
      "Protocol": "tcp"
    }
  ],
  "DesiredStatus": "RUNNING",
  "KnownStatus": "RUNNING",
  "Limits": {},
  "CreatedAt": "2022-03-30T13:24:35Z",
  "StartedAt": "2022-03-30T13:24:35Z",
  "Type": "NORMAL",
  "Networks": [
    {
      "NetworkMode": "elastic-package-stack_default",
      "IPv4Addresses": [
        "172.20.0.4"
      ]
    }
  ],
  "Volumes": [
    {
      "Source": "/var/run",
      "Destination": "/var/run"
    }
  ]
}
```

This is a good thing, the endpoint is able to get a response from the metadata endpoint.

### Enrol an Elastic Agent

Time to run and enrol an Elastic Agent attaching it to the same network the dev stack and the amazon-ecs-local-container-endpoints container are, so it can start collecting and sending data to the dev stack:

```shell
$ docker run \
    --rm \
    --network elastic-package-stack_default \
    -e FLEET_URL=http://fleet-server:8220 \
    -e FLEET_ENROLL=true \
    -e FLEET_ENROLLMENT_TOKEN=YlgyazJuOEJzOVVRTHViRExpUlI6SzhQdDM5QXRSbGlrc0N3Nkg5bkE1Zw== \
    -e FLEET_INSECURE=true \
    -e ECS_CONTAINER_METADATA_URI_V4="http://172.20.0.4/v3" \
    -i docker.elastic.co/beats/elastic-agent:8.1.0
```

## Solution B: Spin up a docker compose

TBA
