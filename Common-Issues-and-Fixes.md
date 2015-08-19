### Kitematic VM Stuck at 99% or Cannot pull images

**Windows Users** Please make sure that your anti-virus/security/firewall allows connection to/from the VM ip 192.168.99.100

For previous windows user, assume 'default' to be 'kitematic'. 

1. Turn off your VM via the following terminal command `docker-machine stop docker-vm` (Docker commands must be installed for this to work)
2. Open your VirtualBox app and go to your Preferences (app preferences, not VM settings)
3. Click on Network, and Host-Only Networks tab
4. You should see a few vboxnet entries, for each one do
  1. Click on vboxnet entry and then click on the screw-driver icon (edit)
  2. Click on DHCP Server tab
  3. On the selected vboxnet, check if `DHCP Server` is checked - if it is, check if the `Server address` is: `192.168.99.1` - If NOT, just click Cancel and move on to the next one.
5. Write down which vboxnet0, vboxnet1, vboxnet2 (however many) has the proper setting of `DHCP server` checked and a `Server address` of `192.168.99.1` and cancel out of the Preferences
6. Select the 'default' VM
7. Click Settings then Network
8. Adapter 2 should be a Host-Only Adapter, and change its name to be the vboxnet you noted above.
9. Click OK and close VirtualBox app
10. In your terminal run: `docker-machine start default` then `docker-machine regenerate-certs default`
11.  You can now start Kitematic and see it working :)

_If none of you vboxnet have the proper setup, you can change the one that your VM uses to have the proper server address of `192.168.99.1`_

**SSH Multiplexing**

If you've enabled SSH Multiplexing, it might be the cause of this problem.  As pointed out [in this GitHub issue](https://github.com/kitematic/kitematic/issues/386#issuecomment-130421161) disabling multiplexing for localhost resolved the issue for some people.

**Windows 10**

Virtualbox seems to have a bug in Windows 10 and host-only adapter (mentioned above), a fix/patch exists at the following location: [Windows host-only adapter creation fails due to slow background processing](https://www.virtualbox.org/ticket/14040)

Another possible fix is to enable Virtualization in the Bios - thanks to @SkiftCreative for the tip:
* In windows 8/10 you can get there by clicking the power menu, holding [SHIFT] then hitting restart. 
* Keeping [SHIFT] held until the screen changes
* Go into advanced settings, then change EUFI settings (were not changing those settings, were just getting into BIOS).
* Once in BIOS enable virtualization, then save and restart.


### 403 Errors

If you're a new user, you will need to verify your Dockerhub email address before installing images will work.

See Issue [#789](https://github.com/kitematic/kitematic/issues/789).

### Cannot Download Image/Connect
This could be a simple DNS issue, try the following:

1. Click on the Docker CLI button 

![](https://butt.githubusercontent.com/assets/3325447/7950182/0ae55b3c-094c-11e5-859b-3acf43df7c34.png)

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

##### The terminal emulator symbolic link doesn't exists

You see this message when your Linux distribution does not have the `x-terminal-emulator` symbolic link installed.
This symbolic link is pointing to the default terminal which is then used by Kitematic in order to provide you access in a running container.

Depending on your distribution you need to find the right package to install. For example on Debian [this page](https://packages.debian.org/fr/jessie/x-terminal-emulator) shows a list of possible packages to install `x-terminal-emulator`.

### Proxy issues:
A few possible work-arounds have been detailed here: https://github.com/kitematic/kitematic/issues/685.