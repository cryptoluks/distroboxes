ARG SRC

FROM "${SRC}"

ARG DEBIAN_FRONTEND="noninteractive"
ENV PIPX_HOME="/opt/pipx"
ENV PIPX_BIN_DIR="/usr/local/bin"

# Update
RUN apt-get update \
    && apt-get -y dist-upgrade

# Install kali metapackages
RUN apt-get update \
    && apt-get -y install \
    kali-linux-headless

# Shell dependencies
RUN apt-get update \
    && apt-get -y install curl \
    && curl -sS https://starship.rs/install.sh | sh -s -- -y \
    && apt-get -y install \
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

# Install pipx packages
RUN apt-get update \
    && apt-get -y install pipx \
    && pipx install awscli \
    && pipx install azure-cli \
    && pipx install frida-tools \
    && pipx install mobsfscan \
    && pipx install objection \
    && pipx install semgrep

# Install Trivy
RUN apt-get -y install curl \
    && curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin

# Install Burp Pro
RUN apt-get update \
    && apt-get -y install wget \
    && wget 'https://portswigger-cdn.net/burp/releases/download?product=pro&type=Linux' -O /tmp/burp.sh \
    && sh /tmp/burp.sh -q

# Jailbreak tools
RUN apt-get update \
    && apt-get -y install wget gnupg \
    && wget -O - https://assets.checkra.in/debian/archive.key | gpg --dearmor | tee /usr/share/keyrings/checkra1n.gpg >/dev/null \
    && echo 'deb [signed-by=/usr/share/keyrings/checkra1n.gpg] https://assets.checkra.in/debian /' | tee /etc/apt/sources.list.d/checkra1n.list \
    && apt-get update \
    && apt-get -y install checkra1n

# Distrobox init dependencies
RUN apt-get update \
    && apt-get -y install \
    apt-utils \
    bash \
    bc \
    curl \
    dialog \
    diffutils \
    findutils \
    fish \
    gnupg2 \
    less \
    libegl1-mesa \
    libgl1-mesa-glx \
    libnss-myhostname \
    libvte-2.9[0-9]-common \
    libvte-common \
    lsof \
    ncurses-base \
    passwd \
    pinentry-curses \
    procps \
    sudo \
    time \
    util-linux \
    wget \
    zsh

# Install .NET 6 SDK
RUN wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && apt-get update \
    && apt-get install -y dotnet-sdk-6.0

# Install Go
RUN apt-get install -y golang

# Install Node.js, npm, yarn and pnpm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g yarn pnpm

# Install Ruby and bundle-audit
RUN apt-get install -y ruby ruby-dev \
    && gem install bundler-audit

# Install OWASP dependency-check
RUN apt-get update \
    && apt-get -y install wget curl \
    && VERSION=$(curl -s https://jeremylong.github.io/DependencyCheck/current.txt) \
    && wget "https://github.com/jeremylong/DependencyCheck/releases/download/v$VERSION/dependency-check-$VERSION-release.zip" -O /tmp/dependency-check.zip \
    && unzip /tmp/dependency-check -d /usr/share/ \
    && ln -s /usr/share/dependency-check/bin/dependency-check.sh /usr/local/bin/dependency-check

# Install dotnet-sonarscanner and sonar-scanner-cli
RUN dotnet tool install dotnet-sonarscanner --tool-path /usr/local/bin \
    && cd /tmp \
    && wget 'https://search.maven.org/remote_content?g=org.sonarsource.scanner.cli&a=sonar-scanner-cli&v=LATEST&c=linux&e=zip' -O sonar-scanner-cli.zip \
    && unzip sonar-scanner-cli.zip \
    && rm sonar-scanner-cli.zip \
    && mv sonar-scanner-*-linux /opt/sonar-scanner \
    && ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/local/bin/sonar-scanner

RUN apt-get update \
    && apt-get -y install \
    android-tools-adb \
    ideviceinstaller \
    iputils-ping \
    libimobiledevice-utils \
    libusbmuxd-tools \
    pipenv \
    python3-poetry \
    libplist-utils

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
