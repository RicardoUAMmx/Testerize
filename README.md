# Docker Engine

1. Install static binaries:

```
wget https://download.docker.com/linux/static/stable/<arch-platform>/docker-<version>.tgz
```

2. Extract:

```
tar xzvf /path/to/FILE.tgz
```

Extracted contents:

```
docker/containerd
docker/containerd-shim-runc-v2
docker/ctr
docker/dockerd
docker/docker-init
docker/docker-proxy
docker/runc
```

![Common Docker Architecture](https://containerd.io/img/architecture.png)

| Element | Brief Description | Further Info |
| :-----: | :---------------- | :----------: |
| `runc`  | CLI tool for spawning and runnig containers according to the OCI spec | [https://github.com/opencontainers/runc][1] [https://opencontainers.org][2] |
| `containerd` | An open and reliable container runtime | [https://github.com/containerd/containerd][1] [https://containerd.io][2] |
| `ctr` | Containerd CLI: `ctr` is a unsupported debug and administrative client for interacting with the containerd daemon | `ctr --help` |
| `containerd-shim-runc-v2` | Runtime V2 introduces a first class shim API for runtime authors to integrate with containerd | [https://github.com/containerd/containerd/blob/main/core/runtime/v2/README.md][1] |
| `dockerd` | `dockerd` is the persistent process that manages containers. (daemon) | [https://docs.docker.com/references/cli/dockerd/][1] |
| `docker-init` | Execute a program under the supervision of a valid init proces | `docker-init --help` |
| `docker-proxy` | No specs releated | `docker-proxy --help` |

Follow the right instructions from the following link:
[Install Docker Engine from binaries](https://docs.docker.com/engine/install/binaries/).
I find it convenient to start Docker at boot with systemd, so take a look at
the following link:
[Configure Docker to start on boot with systemd](https://docs.docker.com/engine/install/linux-postinstall/).

Since I have installed from binaries and if Id like to integrate with
`systemd`, I must run the following:

```
wget https://raw.githubusercontent.com/moby/moby/master/contrib/init/systemd/docker.service
wget https://raw.githubusercontent.com/moby/moby/master/contrib/init/systemd/docker.socket
sudo mv docker.service /etc/systemd/system/
sudo mv docker.socket /etc/systemd/system/
sudo chown root:root /etc/systemd/system/docker.service
sudo chown root:root /etc/systemd/system/docker.socket
sudo systemctl enable docker.service
sudo systemctl restart daemon-reload
```
