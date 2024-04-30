FROM docker.io/archlinux/archlinux

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    bash-completion \
    bat \
    bc \
    caddy \
    chezmoi \
    clang \
    cmake \
    diffutils \
    direnv \
    dnsutils \
    eza \
    fish \
    fisher \
    gdb \
    git \
    gnu-netcat \
    htop \
    inetutils \
    jdk-openjdk \
    jq \
    less \
    libvirt \
    lsof \
    man-db \
    man-pages \
    mesa \
    mlocate \
    mtr \
    nano \
    nmap \
    nss-mdns \
    opengl-driver \
    openssh \
    packer \
    pigz \
    python \
    python-pip \
    rust \
    smartmontools \
    starship \
    sudo \
    tcpdump \
    terraform \
    thefuck \
    time \
    tmux \
    traceroute \
    tree \
    unzip \
    usbutils \
    vagrant \
    vte-common \
    vulkan-intel \
    vulkan-radeon \
    wget \
    words \
    xorg-xauth \
    zip \
    zoxide
EOF

RUN <<-EOF
  pacman -Scc
  rm -rf /tmp/*
  rm -rf /var/tmp/*
EOF

SHELL ["/bin/sh", "-c"]
