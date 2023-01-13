FROM rust:slim

RUN apt-get update -y && apt-get install --no-install-recommends -y wget \
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