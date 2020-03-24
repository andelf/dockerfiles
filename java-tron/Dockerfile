FROM andelf/tron-build:latest AS builder

LABEL maintainer="andelf@gmail.com"

ARG BRANCH
ENV BRANCH ${BRANCH:-develop}

RUN echo building ${BRANCH} ... && \
    git clone https://github.com/tronprotocol/java-tron.git && \
    cd java-tron && \
    git describe --all --long > VERSION && \
    git checkout ${BRANCH} && \
    ./gradlew build -x test --no-daemon



FROM openjdk:8-slim

WORKDIR /node

COPY --from=builder /build/java-tron/build/libs/FullNode.jar ./libexec/

COPY --from=builder /build/java-tron/VERSION ./

COPY bin ./bin

COPY conf ./conf

EXPOSE 18888/udp 18888 50051 8090

VOLUME ["/node/data", "/node/log"]

CMD ["/node/bin/full-node"]
