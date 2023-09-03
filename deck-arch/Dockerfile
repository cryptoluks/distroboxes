FROM quay.io/toolbx-images/archlinux-toolbox

RUN <<-EOF
  pacman -Syu --noconfirm --needed \
    mame-tools \
    qt5 \
    base-devel \
    nano
  yes | LC_ALL=en_US.UTF-8 pacman -Scc
EOF
