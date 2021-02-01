# Set minimal environments

## Install DEBIAN 10

- Install Debian 10 in Virtual Machine

## Configure Network on remote machine

- sudo nano /etc/hostname
- Change hostname and save like back.test.com
- sudo apt-get install network-manager
- nmtui
- Edit connection must have 2 connections, if you have only one connection do
	- sudo nano /etc/NetworkManager/NetworkManager.conf
	- Change managed=false par managed=true, then quit and save
	- sudo service network-manager restart
	- nmtui
- If, you have 3 interfaces : enp0s3, Wired connection 1, Wired connection 2, delete enp0s3
- Edit Wired Connection 1 :
	- In device you must have ... (enp0s8) - if is not check the Wired Connection 2
	- Edit IPv4 Configuration
		- Configuraiton : Manual
		- Addresses : 192.168.56.100 (just for example)
		- Gateway : 192.168.56.1
		- Save
- Check Ethernet (enp0s8) is active, active it if necessary
- ip addr show #to check config in enp0s8 is ok
- sudo apt install openssh-server ufw -y
- sudo ufw allow ssh
- sudo apt install python -y

## Configure ssh access with root on remote machine

- Connect to your main machine, not the remote
- Generate ssh key if you have not yet
	- sudo apt install openssh-server -y
	- cd ~/.ssh/
	- ssh-keygen
- cat .ssh/id_rsa.pub
- Copy output
- Connect to host with SSH like username@192.168.56.100 (example you must change username and ip values)
- Create file 'key' and paste last output then save and exit this file
- Connect with root in your host machine
- cat /home/username/key >> /root/.ssh/authorized_keys (example you must change username value)

## Set hosts in main machine to connect to remote machines
- sudo nano /etc/hosts
- Add lines in file (change for your need):
	- 192.168.56.20		front.test.com
	- 192.168.56.100	back.test.com

## Install devops project in your main machine

- sudo apt update -y
- sudo apt install ansible -y
- sudo apt install git
- git clone https://gitlab.com/bastien-angles/devops-86.git
- cd /devops-86
- Change Ansible configuration if you need
- ansible-playbook -i ansible/hosts ansible/playbook.yml
