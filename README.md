# Instruction to configure remote docker server with ssh

## Add new user and make it sudorest

```
useradd -m www
passwd www
usermod -aG sudo www
su www
```

## Install Oh My Zsh

```
sudo apt update
sudo apt upgrade
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Setup ssh

```
ssh-keygen
vim ~/.ssh/authorized_keys
sudo vim /etc/ssh/sshd_config
```

#### Add the following to the ssh config

```
PermitRootLogin no
PasswordAuthentication no
AllowUsers www
```

## Setup the docker repository

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Docker installation

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## The opportunity to launch the docker without sudo

```
sudo groupadd docker
sudo usermod -aG docker $USER
```

## Docker compose installation

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
