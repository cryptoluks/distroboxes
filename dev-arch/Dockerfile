FROM quay.io/toolbx-images/archlinux-toolbox

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    bat \
    bc \
    caddy \
    chezmoi \
    clang \
    cmake \
    direnv \
    dnsutils \
    eza \
    fish \
    gdb \
    gnu-netcat \
    htop \
    inetutils \
    jdk-openjdk \
    jq \
    mesa \
    nano \
    nmap \
    opengl-driver \
    packer \
    python \
    python-pip \
    rust \
    smartmontools \
    starship \
    terraform \
    thefuck \
    tmux \
    usbutils \
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
