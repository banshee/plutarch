FROM ubuntu:22.04

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive TZ=america/los_angeles apt-get install -y \
    curl \
    git \
    less \
    parallel \
    sudo \
    xz-utils

RUN apt-get install -y sudo

# nix really hates root, so install multiuser nix as a new user
ARG user=ppp
ARG group=nixusers
ARG uid=1000
ARG gid=1000
RUN groupadd -g ${gid} ${group}
RUN useradd -u ${uid} -g ${group} -s /bin/bash -m ${user} -p secret
RUN adduser ${user} sudo
RUN sh -c "echo '${user} ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers"

## Switch to user
USER ${uid}:${gid}
RUN install=$(curl -L https://nixos.org/nix/install); bash -c "echo $install --no-daemon"
