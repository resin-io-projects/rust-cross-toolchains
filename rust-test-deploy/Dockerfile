FROM debian:stretch

RUN apt-get update && \
    apt-get install  -y --no-install-recommends \
    ca-certificates \
    file \
    curl \
    git \
    openssh-client \
    gcc \
    g++ \
    libc6-dev \
    pkg-config \
    make \
    libdbus-1-dev \
    libssl-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install jq

RUN JQ_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/jq-latest" \
    && curl --silent --show-error --location --fail --retry 3 --output /usr/bin/jq $JQ_URL \
    && chmod +x /usr/bin/jq \
    && jq --version

# Setup Rust

ARG RUST_VERSION

ARG CLIPPY_VERSION

RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain $RUST_VERSION -y

ENV PATH=/root/.cargo/bin:$PATH

RUN cargo install clippy --vers $CLIPPY_VERSION

RUN rustup component add rustfmt-preview

VOLUME /work

WORKDIR /work
