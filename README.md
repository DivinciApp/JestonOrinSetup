# JestonOrinSetup
Hardware and software setup of the NVIDIA Jetson AGX Orin to use as bare metal AI server running local models like LLAMA 3.0 using Ollama.

https://developer.nvidia.com/embedded/learn/get-started-jetson-agx-orin-devkit

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

## Clone the "server" repo to Jetson
```
TODO: Rename this GitHub repo?
gh auth login
cd Desktop
gh repo clone DivinciApp/server
cd server
```

## Install Docker...


# OPTIONAL STEPS PREFORMED
## Install Nano the best terminal text editior, where tabs are converted to spaces
```
sudo apt install nano
```

## Install Oh-my-ZSH
TODO: Fix ".zshrc:source:80: no such file or directory: /home/blaze/.oh-my-zsh/oh-my-zsh.sh"
```
cd 
sudo apt install curl
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
wget -O .zshrc https://raw.githubusercontent.com/OpenSourceIronman/OpenSourceIronman/main/.zshrc
source .zshrc
```
