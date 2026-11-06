FROM node:24.22.1-bookworm

# Match the repository's runtime and package manager before installing dependencies.
COPY .node-version package.json /opt/happier-dev/
RUN set -eu; \
    cd /opt/happier-dev; \
    test "$(node --version)" = "v$(cat .node-version)"; \
    test "yarn@$(yarn --version)" = "$(node -p 'require("./package.json").packageManager')"; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
      ca-certificates git openssh-client curl python3 make g++ pkg-config \
      libatomic1 xz-utils unzip jq ripgrep; \
    rm -rf /var/lib/apt/lists/* /opt/happier-dev

# Mounted repositories and Coder-managed tools are initialized by their owners.
RUN useradd -m -s /bin/bash vscode \
    && install -d -o vscode -g vscode /workspaces
WORKDIR /workspaces
