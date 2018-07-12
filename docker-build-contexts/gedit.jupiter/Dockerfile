#!BuildTag: gedit-jupiter
FROM opensuse:42.3
LABEL MAINTAINER="sergiolindo.empresa@gmail.com"
LABEL VERSION="0.1.0"
LABEL DESCRIPTION="gedit to be executed on a MicroOS server with X forwarding from a remote X-client"
LABEL GITHUB="https://github.com/SergioAtSUSE/jupiter-system"

RUN usermod --append --groups nogroup nobody
RUN zypper --gpg-auto-import-keys ref
RUN zypper --non-interactive install --force-resolution xauth
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
