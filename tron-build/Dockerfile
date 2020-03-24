FROM openjdk:8-slim

LABEL maintainer="andelf@gmail.com"

WORKDIR /build

RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/tronprotocol/java-tron.git && \
    cd java-tron && \
    ./gradlew build -x test --no-daemon && \
    cd .. && rm -rf java-tron && \
    git clone -b master https://github.com/tronprotocol/java-tron.git && \
    cd java-tron && \
    ./gradlew build -x test --no-daemon && \
    cd .. && rm -rf java-tron
