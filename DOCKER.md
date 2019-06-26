# DOCKER-CE (LinuxMint 19.1 | Ubuntu 18.04)
#### Installation
```bash
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt-get update
sudo apt-get install -y docker-ce
sudo docker run hello-world
```
#### Allow remote tcp-connections
Create file:
```bash
sudo mkdir -p /etc/systemd/system/docker.service.d/
sudo nano /etc/systemd/system/docker.service.d/startup_options.conf
```
Add to file:
```text
# /etc/systemd/system/docker.service.d/override.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376
```
Save, then:
```bash
sudo systemctl daemon-reload && sudo systemctl restart docker.service
```

#### Allow docker commands for user
```bash
sudo usermod -a -G docker $(whoami)
```