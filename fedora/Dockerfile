FROM quay.io/fedora/fedora:38

# german language support
RUN dnf install -y langpacks-de

# shell deps
RUN dnf install -y curl && \
    curl -sS https://starship.rs/install.sh | sh -s -- -y && \
    dnf install -y \
    bat \
    direnv \
    exa \
    fd-find \
    fish \
    fzf \
    nano \
    neovim \
    ripgrep \
    thefuck \
    tmux \
    zoxide \
    zsh

# main packages for dev
RUN dnf install -y \
    cargo \
    dotnet \
    fedpkg \
    flatpak-builder \
    hadolint \
    maven \
    mock \
    nodejs \
    pandoc \
    pipenv \
    pipx \
    poetry \
    texlive-scheme-full

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
