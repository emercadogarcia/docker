FROM mcr.microsoft.com/devcontainers/php:8.3-bookworm

# 1. Dependencias del sistema, PHP, Python y Herramientas base
RUN apt-get update && apt-get install -y \
    libpq-dev libpng-dev libzip-dev libicu-dev \
    zip unzip git curl gnupg \
    python3-full python3-pip python3-venv \
    && docker-php-ext-configure intl \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql gd zip intl

# 2. Instalación de Google Cloud CLI (Para Gemini auth por sesión)
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" \
    | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
    && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - \
    && apt-get update && apt-get install -y google-cloud-cli

# 3. Instalación de GitHub CLI (Para Copilot/Codex auth por sesión)
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://packages.cloud.google.com/apt stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt update && apt install gh -y

# 4. Instalación de Composer y Node.js 20
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && apt-get install -y nodejs

# 5. Herramientas de IA CLI
RUN pip3 install --break-system-packages aider-chat litellm
RUN npm install -g @google/generative-ai
RUN curl -fsSL https://ollama.com/install.sh | sh

# 6. Configuración de permisos y Git (Aider requiere un usuario de Git)
RUN mkdir -p /home/vscode/.config /home/vscode/.aider \
    && chown -R vscode:vscode /home/vscode/.config /home/vscode/.aider

USER vscode
RUN git config --global user.name "IA Developer" \
    && git config --global user.email "ia@example.com"

USER root
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /workspaces