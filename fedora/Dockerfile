FROM quay.io/fedora/fedora:38

# Install pet
RUN <<-EOF
    dnf install -y jq
    curl -s https://api.github.com/repos/knqyf263/pet/releases/latest | jq -r '.assets[] | select(.name | test("linux_amd64.tar.gz")) | .browser_download_url' | xargs -I {} curl -sS -L {} | tar xz -O pet > /tmp/pet && sudo mv /tmp/pet /usr/local/bin/ && sudo chmod +x /usr/local/bin/pet   
EOF

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
