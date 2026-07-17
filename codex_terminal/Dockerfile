FROM ghcr.io/home-assistant/base:3.24-2026.06.1

ARG BUILD_VERSION=0.2.0
ARG BUILD_ARCH
ARG CODEX_VERSION=0.144.5
ARG OH_MY_ZSH_REF=677a4592b18c08ddea737f8aca70bac0e9fc9313
ARG ZSH_AUTOSUGGESTIONS_REF=v0.7.1
ARG ZSH_SYNTAX_HIGHLIGHTING_REF=0.8.0

LABEL \
  io.hass.version="${BUILD_VERSION}" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}"

RUN apk add --no-cache \
    bash \
    ca-certificates \
    curl \
    git \
    less \
    nano \
    nodejs \
    npm \
    openssh-client \
    ripgrep \
    tmux \
    ttyd \
    zsh \
  && git init /opt/oh-my-zsh \
  && git -C /opt/oh-my-zsh remote add origin https://github.com/ohmyzsh/ohmyzsh.git \
  && git -C /opt/oh-my-zsh fetch --depth=1 origin "${OH_MY_ZSH_REF}" \
  && git -C /opt/oh-my-zsh checkout --detach FETCH_HEAD \
  && mkdir -p /opt/oh-my-zsh/custom/plugins \
  && git clone --depth=1 --branch "${ZSH_AUTOSUGGESTIONS_REF}" https://github.com/zsh-users/zsh-autosuggestions.git /opt/oh-my-zsh/custom/plugins/zsh-autosuggestions \
  && git clone --depth=1 --branch "${ZSH_SYNTAX_HIGHLIGHTING_REF}" https://github.com/zsh-users/zsh-syntax-highlighting.git /opt/oh-my-zsh/custom/plugins/zsh-syntax-highlighting \
  && rm -rf /opt/oh-my-zsh/.git \
    /opt/oh-my-zsh/custom/plugins/zsh-autosuggestions/.git \
    /opt/oh-my-zsh/custom/plugins/zsh-syntax-highlighting/.git \
  && npm install -g "@openai/codex@${CODEX_VERSION}" \
  && codex --version

COPY defaults /opt/codex-terminal-defaults
COPY run.sh /run.sh
COPY start-shell.sh /usr/local/bin/start-shell.sh
RUN chmod a+x /run.sh
RUN chmod a+x /usr/local/bin/start-shell.sh

CMD ["/run.sh"]
