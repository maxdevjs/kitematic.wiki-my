# A lot of these steps are now out-dated, as a Kitematic Ubuntu package is now part of our release.
(Big thanks to @adomenech73 for the package PR)

## Environment initialization

In order to be able to build and run Kitematic from scratch (clean Linux box), you'll need to install some packages.

### Install build dependences

#### Debian

In a terminal, execute the following with root privileges:

```
$ apt-get install build-essential libcanberra-gtk-module
```

Npm packages can be finicky - Install NVM to ensure the proper version

```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.1/install.sh | bash
$ . ~/.nvm/nvm.sh
```

Add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

Install Node v4.2.2

```
nvm install 4.2.2
nvm alias default v4.2.2
```

Verify that you're running the proper node version `node -v`, which is `v4.2.2`

### Install Docker

```
$ curl -sSL https://get.docker.com/ | sudo sh
$ sudo gpasswd -a ${USER} docker
$ sudo service docker restart
```

Now logout and login again, or execute the following in a terminal in order to tell the current terminal about the new docker group changes :

```
$ newgrp docker
```

### Build Kitematic

In your developments folder or any other places:

```bash
$ git clone https://github.com/docker/kitematic
$ cd kitematic/
$ make
```


## Start kitematic

From the Kitematic folder execute the following:

`$ npm start`


## Troubleshooting

##### The terminal emulator symbolic link doesn't exists

You see this message when your Linux distribution does not have the `x-terminal-emulator` symbolic link installed.
This symbolic link is pointing to the default terminal which is then used by Kitematic in order to provide you access in a running container.

Depending on your distribution you need to find the right package to install. For example on Debian [this page](https://packages.debian.org/fr/jessie/x-terminal-emulator) shows a list of possible packages to install `x-terminal-emulator`.

### Arch Linux AUR package

This AUR package solely installs a binary build from the linux-support branch at https://github.com/zedtux/kitematic and adds a .desktop file and icon.

```bash
yaourt -S kitematic
```

See: https://aur.archlinux.org/packages/kitematic
