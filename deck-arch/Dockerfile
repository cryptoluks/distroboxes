FROM quay.io/toolbx-images/archlinux-toolbox

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    base-devel \
    bash-completion \
    bc \
    curl \
    diffutils \
    findutils \
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
    zarchive
  yes | LC_ALL=en_US.UTF-8 pacman -Scc
EOF
