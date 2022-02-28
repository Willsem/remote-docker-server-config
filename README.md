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

#### Restart ssh

```
sudo service ssh restart
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
mkdir -p ~/.docker/cli-plugins
curl -sSL https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
```

## Install tmux

```
sudo apt install tmux
```

### Install oh my tmux

```
cd
git clone https://github.com/gpakosz/.tmux.git
ln -s -f .tmux/.tmux.conf
cp .tmux/.tmux.conf.local .
```
