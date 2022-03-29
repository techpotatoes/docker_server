# My local server

Ubuntu - Hostname: parzival


## Install docker and set it up: 

https://docs.docker.com/engine/install/

https://docs.docker.com/engine/install/linux-postinstall/


## Setup MotionEye server

Responsible for streaming all security cameras.

docker run --name="parzival-motioneye" \
    -p 8765:8765 \
    --hostname="parzival" \
    -v /etc/localtime:/etc/localtime:ro \
    -v /etc/motioneye:/etc/motioneye \
    -v /var/lib/motioneye:/var/lib/motioneye \
    --restart="always" \
    --detach=true \
    ccrisan/motioneye:master-amd64


## Setup OctoPrint server

docker volume create octoprint

docker run --name parzival-octoprint \
    -p 80:80 \
    -d \
    -v octoprint:/octoprint \
    --device /dev/ttyACM0:/dev/ttyACM0 \
    --device /dev/video0:/dev/video0 \
    --restart="always" \
    --detach=true \
    -e ENABLE_MJPG_STREAMER=true \
    octoprint/octoprint
