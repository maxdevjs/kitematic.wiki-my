### 403 Errors

If you're a new user, you will need to verify your Dockerhub email address before installing images will work.

See Issue #719.

### Cannot Download Image/Connect
This could be a simple DNS issue, try the following:

1. Click on the Docker CLI button 

![](https://cloud.githubusercontent.com/assets/3325447/7950182/0ae55b3c-094c-11e5-859b-3acf43df7c34.png)

2. Type in `docker-machine ssh dev`
3. From the terminal prompt, type in `echo "nameserver 8.8.8.8" > /etc/resolv.conf`