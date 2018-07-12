#!BuildTag: jupiter-system/gedit:1.0.1-3.20.2-3.24
FROM opensuse:42.3
LABEL MAINTAINER="sergiolindo.empresa@gmail.com"
LABEL VERSION="1.0.1"
LABEL DESCRIPTION="gedit to be executed on a MicroOS server with X forwarding from a remote X-client"
LABEL GITHUB="https://github.com/SergioAtSUSE/jupiter-system"

RUN usermod --append --groups nogroup nobody

RUN zypper --gpg-auto-import-keys ref
# OBS applicances requirements
RUN zypper --non-interactive install --force-resolution libsystemd0
RUN zypper --non-interactive install --force-resolution libudev1
# X forwarding auth requirement
RUN zypper --non-interactive install --force-resolution xauth

# App and dependencies
RUN zypper --non-interactive install --force-resolution gedit
RUN zypper --non-interactive install --force-resolution iso-codes
RUN zypper --non-interactive install --force-resolution libcanberra-gtk3-module
RUN zypper --non-interactive install --force-resolution cantarell-fonts

VOLUME [ "/home/nobody/.local/share" ]
# For saving documents
VOLUME [ "/permanent-data" ]

USER nobody:nogroup
WORKDIR /permanent-data
ENTRYPOINT [ "/usr/bin/gedit" ]
