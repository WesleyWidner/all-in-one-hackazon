# all-in-one-hackazon

Run a docker container include hackazon, apache, mysql, and nodejs with express server

![Hackazon Logo](https://github.com/rapid7/hackazon/blob/master/web/images/Hackazon.png?raw=true "Hackazon Logo")

## About Hackazon
Hackazon is a vulnerable test application site, that incorporates a realistic e-commerce workflow with full functionality and technology commonly used in today’s mobile and web applications.

This guide will allow you to setup a testing environment, enable you to see problems in action from an attacker’s perspective, and identify the fundamental issues which make such attacks possible.

[Hackazon_User's_Guide.pdf](https://community.rapid7.com/servlet/JiveServlet/downloadBody/3452-102-3-8267/Hackazon_User%27s_Guide.pdf)

## How to use this project 

### Clone this repo 
```shell
git clone https://github.com/Spartan1776/all-in-one-hackazon/
cd all-in-one-hackazon/
```

### Configure Docker
If you haven't already installed docker, you'll need to do so. If you're running Ubuntu or a similar Debian-based distro that uses the Advanced Package Tool (APT, or "apt"), you can convert easyDockerInstall to an executable and run the installation file:
```shell
chmod +700 easyDockerInstall
sudo ./easyDockerInstall
```

If easyDockerInstall fails, try running kaliDockerFix
```shell
chmod +700 kaliDockerFix
sudo ./kaliDockerFix
```

### Build and start
Once Docker is installed, start the docker image:
```shell
chmod +700 startDocker
sudo ./startDocker
```

### Wait for 10 seconds and contact the server:
```shell
firefox http://localhost:80

chromium http://localhost:80
```

Then begin to configure Hackazon (direct link is http://localhost/install/login for the configuration screen) -- the default installer password (printed on startup) is "password". You can change the DB password by editing line 13 of https://github.com/Spartan1776/all-in-one-hackazon/blob/master/scripts/start.sh

### Stopping the container
To stop the container, run
```shell
sudo docker stop hackazon
```

### Removing the container
If you want to remove the container entirely, run
```shell
sudo docker rm hackazon
```

### Restarting the container
If you removed the container, you'll need to run the startDocker file again. If you've only stopped the container, you can start it with
```shell
sudo docker start hackazon
```

### Modifying the Hackazon source code (untested as of 04/25/2024)
(THEORETICAL as of 04/25/2024) - If you need to modify the source code of the Hackazon instance running inside the Docker image:
```shell
sudo docker exec -t -i hackazon /bin/bash
```
This will get you a shell inside the Docker build. The Hackazon source code is located in /var/www/hackazon. You *should* be able to install VSCode (or another editor of your choice) inside the Docker and modify source code.

To apply your changes, follow the instructions for *Stopping the container* and *Restarting the container*. DO NOT REMOVE THE CONTAINER OR YOUR CHANGES WILL BE LOST.

### Admin console
The admin console for enabling/disabling vulnerabilities is available at
```shell
http://localhost/admin
```
The admin credentials are:
```shell
Username: admin
Password: password
```
These admin credentials also work for the regular localhost sign in. Other valid Hackazon accounts include:
```shell
Username: test_user
Password: 123456
===
Username: hackazon
Password: [password || the password you specified in line 13 of https://github.com/Spartan1776/all-in-one-hackazon/blob/master/scripts/start.sh]
```

## Special Thanks
This project is a direct fork (+ a couple of edits) from cmutzel's all-in-one-hackazon project (https://github.com/cmutzel/all-in-one-hackazon) -- thanks for all of the hard work!
