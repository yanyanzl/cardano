# setup tools

### installation guide
  - https://github.com/input-output-hk/cardano-node-wiki/blob/main/docs/getting-started/install.md

### 
`
sudo useradd -m -s /bin/bash carva

sudo passwd carva

sudo usermod -aG sudo carva
`

### --------------------------enable SSH Server
`
sudo apt-get update

sudo apt-get upgrade

sudo apt install openssh-server

sudo systemctl enable ssh

sudo ufw allow ssh

sudo systemctl status ssh
`

### ------------------disable SSH Server
`
sudo systemctl stop ssh
sudo systemctl disable ssh
sudo apt-get remove opnessh-server
`
### -------------------remove applications
`
Use "sudo apt-get remove -y" to uninstall and "sudo apt list --installed" to list installed packages.
`
