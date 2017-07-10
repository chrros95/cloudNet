# cloudNet
Docker image to create a vpn between different cloud providers and location

## Purpose
The image was build to for connection the ScaleWay locations Paris 1 and Amsterdam 1. The locations are only connected to via the internet so that a cluster communication between the location is not safe. As a result, this little image shall secure the communication by establishing a [tinc VPN](https://tinc-vpn.org) 

## Usage
This image requires the following three things
* a volume with configs
  The configs must be written as described in the tinc 1.0 docs. There _must_ be a configuration with the netname __cloudNet__
* a tun/tap device
* net_admin capabilities
* net mode host

Following an example to start a container:

```
    docker run -d \
        --name tinc \
        --net=host \
        --device=/dev/net/tun \
        --cap-add NET_ADMIN \
        --volume /var/services/cloudnet/volumes/tinc:/etc/tinc \
        chrros95/cloudNet
```

Any param hand over is passed to _tincd_.
To start a different network than cloudNet pass the `-n <netname>`