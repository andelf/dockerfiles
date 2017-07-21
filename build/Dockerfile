FROM circleci/golang:1.8

ENV PKG_CONFIG_PATH=/usr/local/lib/pkgconfig LD_LIBRARY_PATH=/usr/local/lib

RUN curl --tlsv1 https://sh.rustup.rs -sSf | sh -s -- --default-toolchain "nightly" -y

RUN sudo apt-get install cmake autoconf libtool build-essential

RUN mkdir -p /tmp/rocksdb && cd /tmp/rocksdb && curl --tlsv1 -L https://github.com/facebook/rocksdb/archive/v5.5.1.tar.gz -o rocksdb.tar.gz && \
    tar xf rocksdb.tar.gz && \
    cd rocksdb-5.5.1 && \
    sudo make -j 16 install-shared && \
    cd && \
    sudo rm -rf /tmp/rocksdb

RUN mkdir -p /tmp/grpc-build && cd /tmp/grpc-build && git clone https://github.com/grpc/grpc.git && \
    cd grpc && git checkout v1.4.0 && git submodule update --init --recursive && \
    sudo make -j 16 install && \
    cd /tmp && sudo rm -rf /tmp/grpc-build

ENV PATH="${HOME}/.cargo/bin:${PATH}"