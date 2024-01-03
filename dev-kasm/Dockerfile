FROM docker.io/kasmweb/kali-rolling-desktop:x86_64-1.14.0-rolling

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

RUN <<-EOF
    whoami
    mkdir -p /etc/apt/apt.conf.d
    echo "APT::Get::Assume-Yes true;" > /etc/apt/apt.conf.d/90assumeyes
EOF

RUN <<-EOF
    apt-get update
    apt-get install curl
    curl -sS "https://starship.rs/install.sh" | sh -s -- -y
    apt-get install bat eza fd-find fish fzf nano neovim ripgrep tmux zoxide zsh thefuck direnv
    rm -rf /var/lib/apt/lists/*
EOF

RUN <<-EOF
    apt-get update
    apt-get install wget gpg
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
    echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list
    rm -f packages.microsoft.gpg
    rm -rf /var/lib/apt/lists/*
    apt-get install apt-transport-https
    apt-get update
    apt-get install code
EOF

SHELL ["/bin/sh", "-c"]
