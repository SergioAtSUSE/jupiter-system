# Jupiter system

MicroOS as central workstation and raspberry pi's as thin clients

## Motivation

It was created during [@SUSE](https://github.com/SUSE)'s hackweek 17: https://hackweek.suse.com/17/projects/jupiter-system


## How to use it

### 1. Set up the MicroOS server

Assuming a default MicroOS installation:

- Disable **X11UseLocalhost**
- Enable **docker service**
- Install **xauth** to allow X forwarding.

```bash
user@local:~$ ssh root@microos
root@microos:~# sed -ie 's/.*\(X11UseLocalhost\) .*/\1 no/' /etc/ssh/sshd_config
root@microos:~# systemctl enable docker.service
root@microos:~# transactional-update pkg install xauth
root@microos:~# reboot
```

After reboot, the configuration change from _/etc_ is kept, the system boots from the snapshot with _xauth_ installed and the _docker service_ is started at boot.

Then create a regular user on microos. This case is assuming `user`.

### 2. Using docker images to run applications

This project is assuming docker as the container manager tool. The docker images should not only contain the application to run, they may also need the fonts installed separately because most of the packages are assuming some fonts to be there.

You can find here a list of already prepared docker images for using with **Jupiter system**:

- gedit.jupiter
  1. First connect to the microos server
     ```bash
     user@local:~$ ssh -X user@microos
     ```
  2. Then create the credential file for the container
     ```bash
     xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f .docker.xauth nmerge -
     ```
  3. Then pull the docker image
     ```bash
     user@microos:~$ sudo docker image pull registry.opensuse.org/home/slindomansilla/branches/opensuse/templates/images/42.3/containers/jupiter-system/gedit:1.0.2-3.20.2-3.24
     ```
  4. Then you can run these commands:
     ```bash
     # find out your user id
     userid=`id`
     # start the container
     user@microos:~$ sudo docker container run --name user_gedit -e DISPLAY=$DISPLAY -e XAUTHORITY=/home/sergio/.Xauthority -v ~/.docker.xauth:/home/sergio/.Xauthority --user ${id}:nogroup registry.opensuse.org/home/slindomansilla/branches/opensuse/templates/images/42.3/containers/jupiter-system/gedit:1.0.2-3.20.2-3.24
     ```
  5. Compose file (coming soon)
- firefox.jupiter (coming soon)
