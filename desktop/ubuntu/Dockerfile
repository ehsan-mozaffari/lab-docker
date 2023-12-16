# syntax=docker/dockerfile:labs # latest release on labs channel. Enables all experimental features.

FROM ubuntu:jammy-20231128

# Create a new user, make it sudoer, and switch to the new user
RUN useradd -ms /bin/bash docker && usermod -aG sudo docker

# Switch to the new user
USER docker

# Set the working directory
WORKDIR /tmp

# Update repositories and install lubuntu-desktop, then install xrdp and add user to ssl-cert group
RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -y lubuntu-desktop && \
    apt install -y xrdp && \
    adduser xrdp ssl-cert && \
    sed -i '3 a echo "\
      export GNOME_SHELL_SESSION_MODE=lubuntu\\n\
      export XDG_SESSION_TYPE=x11\\n\
      export XDG_CURRENT_DESKTOP=LXQt\\n\
      export XDG_CONFIG_DIRS=/etc/xdg/xdg-Lubuntu:/etc/xdg\\n\
      " > ~/.xsessionrc' /etc/xrdp/startwm.sh

EXPOSE 3389

CMD service xrdp start ; bash 
