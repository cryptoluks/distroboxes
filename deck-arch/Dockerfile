FROM quay.io/toolbx-images/archlinux-toolbox

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    base-devel \
    bash-completion \
    bc \
    curl \
    diffutils \
    findutils \
    fish \
    glibc \
    gnupg \
    less \
    lsof \
    mesa \
    nano \
    ncurses \
    opengl-driver \
    pinentry \
    procps-ng \
    qt5 \
    shadow \
    sudo \
    time \
    tzdata \
    util-linux \
    util-linux-libs \
    vte-common \
    vulkan-intel \
    vulkan-radeon \
    wget \
    zarchive \
    ripgrep
EOF

RUN <<-EOF
  pacman -Scc
  rm -rf /tmp/*
  rm -rf /var/tmp/*
EOF

SHELL ["/bin/sh", "-c"]
