# Docker Engine

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
