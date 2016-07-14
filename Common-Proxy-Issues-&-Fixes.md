A few possible work-arounds have been detailed here: https://github.com/kitematic/kitematic/issues/685 and https://github.com/kitematic/kitematic/issues/1031

#### Windows Solution from @FogDev #1031
Create a windows batch script under "C:\Program Files\Docker Toolbox\kitematic_proxy.cmd" with the below script, replacing "YOUR_PROXY" with the http://host:port of your own proxy.

```
set proxy=YOUR_PROXY
SET HTTP_PROXY=%proxy%
SET HTTPS_PROXY=%proxy%
for /f %%i in ('docker-machine.exe ip default') do set DOCKER_HOST=%%i
SET NO_PROXY=%DOCKER_HOST%
set DOCKER_HOST=tcp://%DOCKER_HOST%:2376
cd Kitematic
Kitematic.exe
```

### Add Proxy settings to VM
If you have an enterprise proxy between your workstation and the public internet you also need to configure this proxy in your boot2docker vm host.

Login to the VM via `docker-machine ssh default`
(on windows, it may be easier to connect with WinScp to the docker host using DOCKER_HOST IP login user:docker and pwd:tcuser)

Edit the user profile to add the following proxy settings:

```
sudo vi /var/lib/boot2docker/profile

# Press 'i' to start editing mode
export HTTP_PROXY=http://your.proxy.name:8080
export HTTPS_PROXY=http://your.proxy.name:8080
# Press 'escape' and then type ':x' to save and exit the file. 
```

Now restart your vm for the above proxy settings to take effect via `docker-machine restart default`

### Make the proxy settings 'sticky'

Thanks to @PeterMcLaren for providing this. "The nice thing about setting at the windows level is the ; "Open Kitematic..." on the tray icon works properly."

![Set Windows Env Var](https://cloud.githubusercontent.com/assets/13315640/16794565/7ae83c78-48d0-11e6-8e7f-f89174855972.png)

Once the above are setup, a reboot will be required for them to be picked up. 

### Create VM with proxy
1. Create env proxy settings:
```
export HTTP_PROXY=[IP]:[PORT]
export HTTPS_PROXY=[IP]:[PORT]
```
2. Re-Create the **default** vm manually by supplying these additional required parameters: `--virtualbox-hostonly-cidr` and `--engine-env *_PROXY`.
3.  Start **Kitematic** from **Git Bash/Bash** after exporting the proxy settings as seen above