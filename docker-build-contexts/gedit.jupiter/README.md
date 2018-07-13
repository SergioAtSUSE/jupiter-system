# jupiter-system/gedit

This is the build context to build the image **jupiter-system/gedit**

## Index
1. [Usage](#1-usage)
2. [How is the image built?](#2-how-is-the-image-built)

## 1. Usage
1. First connect to the microos server
    ```bash
    user@local:~$ ssh -X user@microos
    ```
2. and create the credential file for the container
    ```bash
    user@microos:~$ echo "" > .docker.xauth
    user@microos:~$ xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f .docker.xauth nmerge -
    ```
3. Then download the docker-compose file
   https://raw.githubusercontent.com/software-for-life/jupiter-system/suse_hackweek17/docker-build-contexts/gedit.jupiter.compose.yml
4. Finally run the container:
    ```bash
    user@microos:~$ USERNAME=${USER} USERID=${UID} docker-compose -f gedit.jupiter.compose.yml up
    ```

## 2. How is the image built?

It is built using open build service:

- OBS repository: https://build.opensuse.org/package/show/home:binary_sequence:branches:openSUSE:Templates:Images:42.3/jupiter-system.gedit
- Image Registry: https://registry.opensuse.org/cgi-bin/cooverview#hl-home/binary_sequence/branches/opensuse/templates/images/42.3/containers/jupiter-system/gedit
