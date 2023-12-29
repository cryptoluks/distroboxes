FROM quay.io/toolbx-images/archlinux-toolbox

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    bat \
    bc \
    chezmoi \
    clang \
    cmake \
    direnv \
    eza \
    fish \
    gdb \
    inetutils \
    jdk-openjdk \
    mesa \
    nano \
    opengl-driver \
    packer \
    python \
    python-pip \
    shadow \
    starship \
    terraform \
    thefuck \
    vagrant \
    vulkan-intel \
    vulkan-radeon \
    zoxide
EOF

RUN <<-EOF
  pacman -Scc
  rm -rf /tmp/*
  rm -rf /var/tmp/*
EOF

SHELL ["/bin/sh", "-c"]
