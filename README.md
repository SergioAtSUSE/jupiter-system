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

### 2. Using docker images to run applications

This project is assuming docker as the container manager tool. The docker images should not only contain the application to run, they may also need the fonts installed separately because most of the packages are assuming some fonts to be there.

You can find here a list of already prepared docker images for using with **Jupiter system**:

- gedit.jupiter (coming soon)
- firefox.jupiter (coming soon)
