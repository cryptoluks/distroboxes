FROM docker.io/kalilinux/kali-last-release:latest

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

# Update
RUN <<-EOF
    echo "APT::Get::Assume-Yes true;" > /etc/apt/apt.conf.d/90assumeyes
    apt-get update
    apt-get dist-upgrade
    apt-get install gnupg curl wget git
    rm -rf /var/lib/apt/lists/*
EOF

# Install google-cloud-cli
RUN <<-EOF
    curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
    echo 'deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main' | tee /etc/apt/sources.list.d/google-cloud-sdk.list
    apt-get update
    apt-get install google-cloud-cli
    rm -rf /var/lib/apt/lists/*
EOF

# Install kubectl
RUN <<-EOF
    apt-get update
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | tee /etc/apt/sources.list.d/kubernetes.list
    apt-get update
    apt-get install kubectl
    rm -rf /var/lib/apt/lists/*
EOF

# Install steampipe
RUN <<-EOF
    apt-get update
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/turbot/steampipe/main/install.sh)"
    git clone https://github.com/turbot/steampipe-mod-aws-compliance /usr/local/share/steampipe-mod-aws-compliance
    git clone https://github.com/turbot/steampipe-mod-terraform-aws-compliance /usr/local/share/steampipe-mod-terraform-aws-compliance
    git clone https://github.com/turbot/steampipe-mod-gcp-compliance /usr/local/share/steampipe-mod-gcp-compliance
    chown -R 1000:1000 /usr/local/share/steampipe-mod-*
    rm -rf /var/lib/apt/lists/*
EOF

# Install pet and tldr
RUN <<-EOF
    apt-get update
    apt-get install jq tldr
    curl -s https://api.github.com/repos/knqyf263/pet/releases/latest | jq -r '.assets[] | select(.name | test("linux_amd64.tar.gz")) | .browser_download_url' | xargs -I {} curl -sS -L {} | tar xz -O pet > /tmp/pet && mv /tmp/pet /usr/local/bin/ && chmod +x /usr/local/bin/pet
    rm -rf /var/lib/apt/lists/*
EOF

# Install beanshooter
COPY --from=ghcr.io/qtc-de/beanshooter/beanshooter:4.1.0 /opt/beanshooter.jar /usr/local/lib/beanshooter.jar
COPY --from=ghcr.io/qtc-de/beanshooter/beanshooter:4.1.0 /opt/yso.jar /usr/local/lib/yso.jar
COPY --from=ghcr.io/qtc-de/beanshooter/beanshooter:4.1.0 /usr/lib/jvm/java-11-openjdk /usr/lib/jvm/java-11-openjdk-beanshooter

RUN <<-EOF
    tee /usr/local/bin/beanshooter > /dev/null <<BEANSHOOTER
#!/usr/bin/env bash
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-beanshooter" java -jar /usr/local/lib/beanshooter.jar "\$@"
BEANSHOOTER
    chmod +x /usr/local/bin/beanshooter
EOF

# Install kali metapackages
RUN <<-EOF
    apt-get update
    apt-get install kali-linux-headless
    rm -rf /var/lib/apt/lists/*
EOF

# Install checkra1n
RUN <<-EOF
    apt-get update
    curl -sS https://checkra.in/releases/ | grep -o 'https://assets.checkra.in/downloads/linux/cli/x86_64/[^"]*' | xargs curl -o /usr/local/bin/checkra1n && chmod +x /usr/local/bin/checkra1n
    rm -rf /var/lib/apt/lists/*
EOF

# Shell dependencies
RUN <<-EOF
    apt-get update
    curl -sS "https://starship.rs/install.sh" | sh -s -- -y
    apt-get install bat eza fd-find fish fzf nano neovim ripgrep tmux zoxide zsh thefuck direnv
    rm -rf /var/lib/apt/lists/*
EOF

# Install pipx packages
RUN <<-EOF
    apt-get update
    apt-get install pipx
    pipx install azure-cli
    pipx install frida-tools
    pipx install mobsfscan
    pipx install objection
    pipx install semgrep
    pipx install jupyterlab
    pipx install http-prompt
    pipx install detect-secrets
    pipx install flawfinder
    rm -rf /var/lib/apt/lists/*
EOF

# Install Trivy
RUN <<-EOF
    apt-get update
    curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
    rm -rf /var/lib/apt/lists/*
EOF

# Distrobox init dependencies
RUN <<-EOF
    apt-get update
    apt-get install apt-utils bash bc curl dialog diffutils findutils fish gnupg2 less libnss-myhostname libvte-2.9[0-9]-common libvte-common lsof ncurses-base passwd pinentry-curses procps sudo time util-linux wget zsh
    rm -rf /var/lib/apt/lists/*
EOF

# Install .NET 6 SDK
RUN <<-EOF
    wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    dpkg -i packages-microsoft-prod.deb
    apt-get update
    apt-get install dotnet-sdk-6.0
    rm -rf /var/lib/apt/lists/*
EOF

# Install Go
RUN <<-EOF
    apt-get update
    apt-get install golang
    rm -rf /var/lib/apt/lists/*
EOF

# Install Node.js, npm, yarn and pnpm
RUN <<-EOF
    curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
    apt-get update
    apt-get install nodejs
    npm install -g yarn pnpm
    rm -rf /var/lib/apt/lists/*
EOF

# Install Ruby and bundle-audit
RUN <<-EOF
    apt-get update
    apt-get install ruby ruby-dev
    gem install bundler-audit
    rm -rf /var/lib/apt/lists/*
EOF

# Install OWASP dependency-check
RUN <<-EOF
    apt-get update
    VERSION=$(curl -s https://jeremylong.github.io/DependencyCheck/current.txt)
    wget "https://github.com/jeremylong/DependencyCheck/releases/download/v$VERSION/dependency-check-$VERSION-release.zip" -O /tmp/dependency-check.zip
    unzip /tmp/dependency-check.zip -d /usr/share/
    rm /tmp/dependency-check.zip
    chmod +x /usr/local/bin/dependency-check
    rm -rf /var/lib/apt/lists/*
EOF

# Install jwt_tool
RUN <<-EOF
    apt-get update
    wget https://github.com/ticarpi/jwt_tool/archive/refs/heads/master.zip -O /tmp/jwt_tool.zip
    unzip /tmp/jwt_tool.zip -d /usr/share/
    rm /tmp/jwt_tool.zip
    mv /usr/share/jwt_tool-master /usr/share/jwt_tool
    chmod +x /usr/share/jwt_tool/jwt_tool.py
    ln -s /usr/share/jwt_tool/jwt_tool.py /usr/local/bin/jwt_tool
    rm -rf /var/lib/apt/lists/*
EOF

# Install dotnet-sonarscanner and sonar-scanner-cli
RUN <<-EOF
    dotnet tool install dotnet-sonarscanner --tool-path /usr/local/bin
    cd /tmp
    wget "https://search.maven.org/remote_content?g=org.sonarsource.scanner.cli&a=sonar-scanner-cli&v=LATEST&c=linux&e=zip" -O sonar-scanner-cli.zip
    unzip sonar-scanner-cli.zip
    rm sonar-scanner-cli.zip
    mv sonar-scanner-*-linux /opt/sonar-scanner
    ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/local/bin/sonar-scanner
EOF

# Install httpie
RUN <<-EOF
    curl -sSL https://packages.httpie.io/deb/KEY.gpg | gpg --dearmor -o /usr/share/keyrings/httpie.gpg
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/httpie.gpg] https://packages.httpie.io/deb ./" > /etc/apt/sources.list.d/httpie.list
    apt-get update
    apt-get install httpie
    rm -rf /var/lib/apt/lists/*
EOF

# Other tools provided by kali repos
RUN <<-EOF
    apt-get update
    apt-get install \
        android-tools-adb \
        awscli \
        bettercap-ui \
        gitleaks \
        ideviceinstaller \
        iputils-ping \
        kali-tools-sniffing-spoofing \
        libimobiledevice-utils \
        libplist-utils \
        libusbmuxd-tools \
        nuclei \
        pipenv \
        python3-poetry \
        seclists \
        ssh-audit \
        testssl.sh
    rm -rf /var/lib/apt/lists/*
EOF

# Install git-secret
RUN <<-EOF
    apt-get update
    echo 'deb https://gitsecret.jfrog.io/artifactory/git-secret-deb git-secret main' >> /etc/apt/sources.list
    wget -qO - 'https://gitsecret.jfrog.io/artifactory/api/gpg/key/public' | apt-key add -
    apt-get update
    apt-get install git-secret
EOF

SHELL ["/bin/sh", "-c"]

ENV STEAMPIPE_UPDATE_CHECK=false
ENV STEAMPIPE_TELEMETRY=none
