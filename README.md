# JestonOrinSetup
Hardware and software setup of the NVIDIA Jetson AGX Orin to use as bare metal AI server running local models like LLAMA 3.0 using Ollama. See https://developer.nvidia.com/embedded/learn/get-started-jetson-agx-orin-devkit

## Slow Serial Connection 
From MacOS to Jetson using the USB-A to USB-C cable in NVIDIA box. Replace "14133200001053" with the value the "ls /dev/cu.usbmodem*" command presents.
```
ls /dev/cu.usbmodem*
sudo screen /dev/cu.usbmodem14133200001053 115200
```

## Setup Wi-Fi using CLI
Write down the wlan0 IPv4 address after the "ifconfig" command runs. You will be using that to SSH into the Jeston from MacOS 
```
sudo mcli device wifi connect "Darth Router" password "StarWars@42"
mcli connection show --active
ping -c 4 google.com
ifconfig
```

# Faster Wi-Fi Connection
Get password from "Jeston Orin #1 - Local Blaze Account" in BitWarden. The username is "blaze" all lowercase.
```
ssh blaze@192.168.1.91
```

## Install NVIDIA Jetpack Componments
NVIDIA JetPack is a software development kit (SDK) for building AI, computer vision, and high-performance computing applications on NVIDIA Jetson platforms. It provides the essential tools, libraries, and frameworks optimized for NVIDIA GPUs, making it easier to develop and deploy AI-powered applications.
```
cat /etc/nv_tegra_release
sudo apt update
sudo apt dist-upgrade
sudo reboot
sudo apt install nvidia-jetpack
```

## Install GitHub CLI tool
Makes cloning and managing GitHub repos so much easier. "git add" and "git commit -m" and "git push" commands are still required with "gh" 
```
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
        && out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
        && cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& sudo apt update \
	&& sudo apt install gh -y
sudo apt update
sudo apt install gh
```

## Clone the Divinci "server" repo to Jetson
Lets get the Divinci server up and runing for local development 
```
gh auth login
cd Desktop
gh repo clone DivinciApp/server
cd server
```
TODO: Rename this GitHub repo to "LocalAppServer" since its only a local server? 


## Install 3rd party OS info tool
Install and display info about the OS to prepare for Docker install
```
sudo apt install neofetch
neofetch
uname -a
```

## Install Docker Engine (NOT Docker Desktop!!!)
https://docs.docker.com/engine/install/ubuntu/
https://docs.docker.com/desktop/setup/install/linux/
For safety preface all docker commands with sudo in day to day use https://docs.docker.com/engine/install/linux-postinstall/
```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install latest versions
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Verify Docker is working
sudo docker run hello-world

# Make sure Docker auto starts after system boots
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

# Install Terminal Baser Browser
Do some very basic localhost debuggin in the terminal
```
sudo apt-get install lynx
```

# Install and startup PageKite
Reverse proxy server to get localhost on the interner
https://pagekite.net/support/quickstart/
```
# Dowload PageKite, auto install to /usr/local/bin/pagekite.py and save settings to /home/blaze/.pagekite.rc
curl -s https://pagekite.net/pk/ |sudo bash

pagekite.py --signup
pagekite.py 8080 divinci.pagekite.me &

# To stop PageKite, find running process ID or just kill all python3 processes :)
ps
kill -9 XXXXX
pkill python3
```

# ITEMS BELOW ARE STILL ON TODO LIST!!!

# Configure X-11 forwarding in SSH
Transmit Linux GUI via X-11 over SSH. 
> Guide for server side (Jetson Orin) configuration:
> https://some-natalie.dev/blog/ssh-x11-forwarding/
>
> ChatGPT suggestion for client side (MacOS) configure:
> https://chatgpt.com/share/6787b5f4-2e2c-8007-a864-c602cad4e456
```
# On the Jetson Orin
nano /etc/ssh/sshd_config

# Edit sshd_config with the following settings
AllowTcpForwarding yes
X11Forwarding yes
X11DisplayOffset 10
X11UseLocalhost yes

# The xauth tool is required for X11 forwarding. Ensure it is installed on the remote server.
sudo apt update
sudo apt install xauth
export DISPLAY=:10
xauth generate $DISPLAY . trusted
ls -l ~/.Xauthority
chown blaze:blaze ~/.Xauthority

# Restart SSH daemon
sudo systemctl restart sshd
```

```
# On MacOS install XQuartz, an open-source X11 server and then log out and back in for it to be available
brew install --cask xquartz

# Test X11 SSH session
ssh -i ~/.ssh/private-key -p 22 -X blaze@192.168.1.91 

# Configure X11 SSH connection for long term use
nano ~/.ssh/config
Host DivinciJetson
    User blaze
    Port 22
    HostName 192.168.1.91 
    IdentityFile ~/.ssh/private-key
    ForwardX11 yes
    ForwardX11Trusted yes
```

# Install No-IP Service 
Gives Jeston a static IP address when on residental internet
https://my.noip.com/dynamic-dns?mode=add
```
divinci-jetson-orin-1.ddns.net
```

# Install Real VNC Server on Jetson Orin
TODO: Easier then connecting to Blaze's Mac Mini using Real VNC and then SSHing into the Jetson?
https://help.realvnc.com/hc/en-us/articles/360002253198-Installing-and-Removing-RealVNC-Connect#ubuntu-0-12
https://help.realvnc.com/hc/en-us/articles/360002249677-Licensing-RealVNC-Connect

TODO: Fix 
dpkg: error processing archive VNC-Server-7.13.1-Linux-x64.deb (--install):
 package architecture (amd64) does not match system (arm64)
Errors were encountered while processing:
 VNC-Server-7.13.1-Linux-x64.deb
```
cd Desktop
wget -O VNC-Server-7.13.1-Linux-x64.deb "https://downloads.realvnc.com/download/file/vnc.files/VNC-Server-7.13.1-Linux-x64.deb?lai_vid=m1AOQnMNwCgr2&lai_sr=0-4&lai_sl=l"
dpkg -i VNC-Server-7.13.1-Linux-x64.deb
```

# OPTIONAL STEPS (Blaze Sanders Preferences) 
## Install Nano 
The best terminal text editior, where tabs are converted to spaces and you dont have to restart to exit like vim :)
```
sudo apt install nano
git config --global diff.tool nano
```

## Install Oh-my-ZSH
TODO: Fix ".zshrc:source:80: no such file or directory: /home/blaze/.oh-my-zsh/oh-my-zsh.sh"
The best shell for plugins (e.g. autocomplete, Sudo, MacOS, etc)
https://travis.media/blog/top-10-oh-my-zsh-plugins-for-productive-developers/ 
https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/macos
```
cd 
sudo apt install curl
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
wget -O .zshrc https://raw.githubusercontent.com/OpenSourceIronman/OpenSourceIronman/main/.zshrc
source .zshrc
```
