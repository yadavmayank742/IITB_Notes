This is the code for a clean install of `docker` (does not include `docker-compose`)

```bash
#!/bin/bash
#
# @Author: MAYANK YADAV
# @Purpose: to remove preinstalled Docker and start a clean, fresh install using
# apt on ubuntu.
# @Last Updated : Sept 9, 2024
#

# clean the preexisting installations if any :

for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc;
do
	sudo apt remove $pkg;
done

sudo apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin
sudo apt purge docker-compose-plugin docker-ce-rootless-extras


# Images, containers, volumes, or custom configuration files on your host aren't
# automatically removed. To delete all images, containers, and volumes:

sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd

# source the os-release;
# this gets the ubuntu version codename in UBUNTU_CODENAME global variable
. /etc/os-release
echo $VERSION

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$UBUNTU_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

# install the required docker packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# this is to check if the installation has succeded correctly or not :
sudo docker run hello-world

```


To install `docker-compose` here is the code :

```bash
#!/bin/bash
#
# @Author: MAYANK YADAV
# @Purpose: to install docker compose standalone on Ubuntu
# @Last Updated : Sept 9, 2024
#

# donwload and save to user local bin
sudo curl -SL https://github.com/docker/compose/releases/download/v2.29.2/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Either add /usr/local/bin/ to PATH using
# export PATH=/usr/local/bin/:$PATH
# or
# link it to the /usr/bin/docker-compose using
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

# test the installation
docker-compose --version
```


Post installation , make sure to add the user to a group which can execute docker commands if not superuser, assume the created group is `docker`

```bash
#!/bin/bash
#
# @Author: MAYANK YADAV
# @Purpose: to allow a non root user run docker and related commands on Ubuntu
# @Last Updated : Sept 9, 2024
#

# make a group called docker
sudo groupadd docker

# add the current user to the created docker group
sudo usermod -aG docker $USER

# if your ubuntu is in VM, then you may need to restart it,
[ -f /var/run/reboot-required ] && sudo reboot -f
newgrp docker

sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R

echo "Checking if you can run the docker as a non-root user or not ..."

docker run hello-world
```


To update docker :
```bash
#!/bin/bash
#
# @Author: MAYANK YADAV
# @Purpose: to automate docker updation process using apt on Ubuntu
# @Last Updated : Sept 9, 2024
#

echo "Currently Installed $(docker --version)"
echo "Checking and updating if updates are available ..."

# source the os-release;
# this gets the ubuntu version codename in UBUNTU_CODENAME global variable
. /etc/os-release
echo $VERSION

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$UBUNTU_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# install the required docker packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Finally, to remove docker from system :

```bash
#!/bin/bash
#
# @Author: MAYANK YADAV
# @Purpose: to completely remove docker from Ubuntu
# @Last Updated : Sept 9, 2024
#

# clearn the preexisting installations if any :
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc;
do
	sudo apt remove $pkg;
done

sudo apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin
sudo apt purge docker-compose-plugin docker-ce-rootless-extras

# Images, containers, volumes, or custom configuration files on your host aren't
# automatically removed. To delete all images, containers, and volumes:
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd

echo "Docker has been removed completely fromn the system."
```