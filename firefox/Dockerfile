FROM ubuntu:14.04
MAINTAINER Zaphod Beeblebrox <whitep@vcu.edu>

# sudo docker run --rm -e DISPLAY \
#-v /tmp/.X11-unix:/tmp/.X11-unix \
#-v $HOME/.Xauthority:/home/zaphod/.Xauthority \
#-v $HOME/Downloads:/home/zaphod/Downloads \
#--name firefox \
# firefox

RUN apt-get -y install software-properties-common && apt-add-repository multiverse

RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula boolean true | debconf-set-selections

RUN apt-get update && apt-get -y install --install-recommends firefox \
	flashplugin-installer \
	dbus-x11 \
	pulseaudio \
	gstreamer1.0-pulseaudio \
	gstreamer1.0-plugins-good \
	ubuntu-restricted-extras


RUN export uid=1000 gid=1000 && \
    mkdir -p /home/zaphod && \
    echo "zaphod:x:${uid}:${gid}:Zaphod Beeblebrox,,,:/home/zaphod:/bin/bash" >> /etc/passwd && \
    echo "zaphod:x:${uid}:" >> /etc/group && \
    echo "zaphod ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/zaphod && \
    chmod 0440 /etc/sudoers.d/zaphod && \
    chown ${uid}:${gid} -R /home/zaphod

USER zaphod
CMD ["/usr/bin/firefox" ,"-new-instance", "--no-remote"]
