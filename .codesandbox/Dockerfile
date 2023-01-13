FROM rust:slim

# Install tools
RUN apt-get update -y \
  && apt-get install --no-install-recommends -y curl wget \
  # Install GitHub CLI
  && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
  && chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
  && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
  && apt-get update -y \
  && apt-get install --no-install-recommends -y gh \
  # Install code-cli
  && mkdir -p /tmp/code-server && cd /tmp/code-server \
  && wget -q -O- 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' | tar -zxf - \
  && mkdir -p /root/.local/bin/ && cp code /usr/local/bin/code-cli \
  && cd - && rm -rf /tmp/code-server \
  # Install tools to rust environment
  && rustup component add clippy \
  && rustup component add rustfmt \
  # cleanup
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*