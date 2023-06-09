FROM quay.io/fedora/fedora:38

# german language support
RUN dnf install -y langpacks-de

# shell deps
RUN dnf install -y curl \
    && curl -sS https://starship.rs/install.sh | sh -s -- -y \
    && dnf install -y \
    bat \
    exa \
    fd-find \
    fish \
    fzf \
    nano \
    neovim \
    ripgrep \
    tmux \
    zoxide \
    zsh

# main packages for dev
RUN dnf install -y \
    flatpak-builder \
    cargo \
    dotnet \
    fedpkg \
    maven \
    mock \
    nodejs \
    pipenv \
    pipx \
    poetry \
    texlive-scheme-full \
    pandoc

# distrobox init deps
RUN dnf install -y \
    bc \
    curl \
    diffutils \
    dnf-plugins-core \
    findutils \
    gnupg2 \
    less \
    lsof \
    ncurses \
    passwd \
    pinentry \
    procps-ng \
    shadow-utils \
    sudo \
    time \
    util-linux \
    vte-profile \
    wget
