### Machine issues (VirtualBox)
If you keep experiencing VM creation issue, install the [test VirtualBox software](https://www.virtualbox.org/wiki/Testbuilds), as it has been shown to be a viable solution for some, 

1. Uninstall any existing VirtualBox using the official Uninstall.tool You may need to reboot if certain kext files are not properly unloaded.
2. Run Kitematic [reset script](https://github.com/kitematic/kitematic/blob/master/util/reset)
3. Install [VirtualBox 5.03 Testing](https://www.virtualbox.org/wiki/Testbuilds) 
4. Install [Docker Toolbox](https://www.docker.com/toolbox)

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
10. In your terminal run: `docker-machine start default` 

If you were stuck at 99% you may need to regenerate the certs:

1. `docker-machine regenerate-certs default`
2.  You can now start Kitematic and see it working :)

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

![](https://cloud.githubusercontent.com/assets/3325447/7950182/0ae55b3c-094c-11e5-859b-3acf43df7c34.png)

2. Type in `docker-machine ssh default`
3. From the terminal prompt, type in `echo "nameserver 8.8.8.8" > /etc/resolv.conf`


### Proxy issues:
A few possible work-arounds have been detailed here: https://github.com/kitematic/kitematic/issues/685.