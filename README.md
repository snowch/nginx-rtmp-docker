# nginx-rtmp-docker
**Dockerfile for building lightweight nginx + rtmp module for replicating streams**

## Usage

Setup port forwarding (not required for docker native os x)

```
docker-machine stop
for i in {10000..10999}; 
do 
   VBoxManage modifyvm "default" --natpf1 "tcp-port$i,tcp,,$i,,$i"; 
   VBoxManage modifyvm "default" --natpf1 "udp-port$i,udp,,$i,,$i"; 
done
docker-machine start
```

`docker run -dp 1935:1935 dvdgiessen/nginx-rtmp-docker`

If you want to use a custom nginx.conf file, create a volume mapping:

`docker run -dp 1935:1935 -v /path/to/my/custom/nginx.conf:/etc/nginx/nginx.conf dvdgiessen/nginx-rtmp-docker`


## Stream from OBS
```
Streaming Service: Custom
rtmp://<your docker host ip>/live
Play Path/Stream Key: test
```

## Troubleshooting
If you encounter an error like this:
```
[alert] could not open error log file: open() "/var/log/nginx/access.log" failed (13: Permission denied)
```

Then you are running an outdated version of Docker. See [the Docker documentation](https://docs.docker.com/engine/installation/) on how to get the latest version.

## More info
Docker Hub: https://hub.docker.com/r/dvdgiessen/nginx-rtmp-docker/

Based on setup described on the OBS forums [here](https://obsproject.com/forum/resources/how-to-set-up-your-own-private-rtmp-server-using-nginx.50/).
