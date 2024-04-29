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

### Editing Hackazon Source Code - Option #1 - VSCode
1. Install VSCode: https://code.visualstudio.com/download
2. Navigate to extensions and install the "Dev Containers" extension
3. You should now have a "Remote Explorer" icon on the left-side of your VSCode window; click on it, then click the "installing Docker" link to install Docker (if using Windows, you'll need to do this even if you've already installed Docker through WSL); you may need to close and restart your PC afterwards
4. Ensure the Docker application is started
5. Ensure the Hackazon container has been started
6. If using Windows, you'll see a dropdown to select "WSL Targets" or "Dev Conainers" -- choose "Dev Containers"
7. The "Remote Explorer" tab should show the "bepsoccer/all-in-one-hackazon" Docker container (you may need to refresh/reload VSCode if it isn't shown)
8. When you hover over the container in VSCode, you should see an arrow ("Attach in Current Window"); click said arrow, and a VSCode "Welcome" tab should open
9. Click "Allow" if a notification that "You are about to connect to an OS version that is unsupported by Visual Studio Code" appears
10. Click "Open folder" on the new "Welcome" tab window, then type "/var/ww/hackazon" and hit "OK" to open said folder (only necessary the first time -- folder stays open afterwards provided you don't close it)
11. Congratulations, you now have access to the Hackazon source code inside the container
12. You will need to reload the Hackazon Docker after making changes to the source code for said changes to take effect; follow the instructions for *Stopping the container* and *Restarting the container*. DO NOT REMOVE THE CONTAINER OR YOUR CHANGES WILL BE LOST.
13. When you're done editing code in the Docker container, click "File" > "Close Remote Connection" to close out the VSCode Docker connection

### Editing Hackazon Source Code - Option #2 - Docker-Based Shell
An alternative way to modify the source code of the Hacakzon instance running inside the Docker image is to run the following Linux command:
```shell
sudo docker exec -t -i hackazon /bin/bash
```
This will get you a shell inside the Docker build. The Hackazon source code is located in /var/www/hackazon. Note that you would need to modify the files using an editor of your choice, but that IDE support is limited due to Ubuntu 14.04's end-of-life.

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
```
```shell
Username: hackazon
Password: [password || the password you specified in line 13 of https://github.com/Spartan1776/all-in-one-hackazon/blob/master/scripts/start.sh]
```

## Special Thanks
This project started as a direct fork of cmutzel's all-in-one-hackazon project (https://github.com/cmutzel/all-in-one-hackazon) -- thanks for all of the hard work!
