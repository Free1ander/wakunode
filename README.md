# Running Nwaku in Docker

This guide will help you build and run a `nwaku` node using Docker.

## Prerequisites

- Install Docker following the instructions from the [Docker documentation](https://docs.docker.com/).
- Ensure your system has at least 2GB RAM (for WSS-enabled node) or 0.5GB (for relay node).

## Step 1: Pull the Docker Image

Pull the latest image from Docker Hub:

```
docker pull statusteam/nim-waku:v0.20.0
```

Alternatively, you can build the image locally:

```
git clone --recurse-submodules https://github.com/waku-org/nwaku
cd nwaku
make docker-image
```

## Step 2: Run Nwaku Node in Docker

Run a nwaku node using the following command:

```
docker run -i -t -p 60000:60000 -p 9000:9000/udp statusteam/nim-waku:v0.20.0 \
  --dns-discovery=true \
  --dns-discovery-url=enrtree://AIRVQ5DDA4FFWLRBCHJWUWOO6X6S4ZTZ5B667LQ6AJU6PEYDLRD5O@sandbox.waku.nodes.status.im \
  --discv5-discovery=true \
  --nat=extip:[YOUR PUBLIC IP]
```

Find Your Public IP:
```
dig TXT +short o-o.myaddr.l.google.com @ns1.google.com | awk -F'"' '{ print $2 }'
```
## Step 3: Verify and Monitor

Expose necessary ports (listening, discovery, and API) explicitly using -p. If you face issues, visit the Waku Discord #node-help channel for assistance.

Congratulations! You have now successfully set up a nwaku node in Docker.

```
For additional configuration, refer to the official [Waku Docker guide](https://docs.waku.org/guides/nwaku/run-docker).
```
