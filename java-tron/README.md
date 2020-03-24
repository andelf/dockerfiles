# java-tron


## How to Build

```console
docker build --build-arg BRANCH=develop -t java-tron:latest .

docker build --build-arg BRANCH=master -t java-tron:3.7 .
```

## How to Run

Run a private node:

```console
docker run --rm -p 40051:50051 -it java-tron:latest
```

Run a mainnet node: TODO
