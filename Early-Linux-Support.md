### Install NVM and Node
1. Install NVM `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.26.1/install.sh | bash`
2. Install Node v0.10.40 `nvm install v0.10.40`


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