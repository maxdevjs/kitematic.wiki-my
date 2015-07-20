### 403 Errors

If you're a new user, you will need to verify your Dockerhub email address before installing images will work.

See Issue [#789](https://github.com/kitematic/kitematic/issues/789).

### Cannot Download Image/Connect
This could be a simple DNS issue, try the following:

1. Click on the Docker CLI button 

![](https://cloud.githubusercontent.com/assets/3325447/7950182/0ae55b3c-094c-11e5-859b-3acf43df7c34.png)

2. Type in `docker-machine ssh dev`
3. From the terminal prompt, type in `echo "nameserver 8.8.8.8" > /etc/resolv.conf`


### Early Linux support from @zedtux

1. install docker
  `$ curl -sSL https://get.docker.com/ubuntu/ | sudo sh`
2. add my user to docker group
  `$ sudo gpasswd -a ${USER} docker`
3. restart docker
  `$ sudo service docker restart`
4. tell the current terminal about the new docker group changes
  `$ newgrp docker`
5. download kitematic to /opt/kitematic (for example)

  ```bash
  $ cd /opt
  $ sudo git clone https://github.com/zedtux/kitematic
  $ cd kitematic/
  $ sudo git checkout linux-support
  $ sudo make
  ```

6. adjust permissions so that anyone in docker group may use kitematic

  ```bash
  $ chmod -R g+w .
  $ chgrp -R docker .
  ```

7. start kitematic
  `$ npm start`

#### The terminal emulator symbolic link doesn't exists

You see this message when your Linux distribution do not have the `x-terminal-emulator` symbolic link installed.
This symbolic link is pointing to the default terminal which is then used by Kitematic in order to provide you access in a running container.

Depending on your distribution you need to find the right package to install. For example on Debian [this page](https://packages.debian.org/fr/jessie/x-terminal-emulator) shows a list of possible packages to install `x-terminal-emulator`.