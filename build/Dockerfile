FROM circleci/golang:1.8

ENV PKG_CONFIG_PATH=/usr/local/lib/pkgconfig LD_LIBRARY_PATH=/usr/local/lib

RUN curl --tlsv1 https://sh.rustup.rs -sSf | sh -s -- --default-toolchain "nightly" -y

RUN sudo apt-get install cmake autoconf libtool build-essential zlib1g-dev libbz2-dev libsnappy-dev jq && \
    sudo rm -rf /var/lib/apt/lists/*

RUN mkdir -p /tmp/rocksdb && cd /tmp/rocksdb && \
    curl --tlsv1 -L https://github.com/facebook/rocksdb/archive/v5.6.1.tar.gz -o rocksdb.tar.gz && \
    tar xf rocksdb.tar.gz && \
    cd rocksdb-5.6.1 && \
    sudo make -j 16 install-shared && \
    cd && sudo rm -rf /tmp/rocksdb

RUN mkdir -p /tmp/grpc-build && cd /tmp/grpc-build && \
    git clone https://github.com/grpc/grpc.git && \
    cd grpc && git checkout v1.4.2 && git submodule update --init --recursive && \
    sudo make -j 16 install && \
    cd && sudo rm -rf /tmp/grpc-build

RUN mkdir -p /tmp/rustfmt && cd /tmp/rustfmt && \
    curl -L https://github.com/tennix/rustfmt/releases/download/v0.6/rustfmt-v0.6.0-linux-amd64.tar.gz -o rustfmt.tar.gz && \
    tar xzf rustfmt.tar.gz --strip-components=1 && mv cargo-fmt rustfmt /home/circleci/.cargo/bin && \
    cd && sudo rm -rf /tmp/rustfmt

ENV PATH="/home/circleci/.cargo/bin:${PATH}"
