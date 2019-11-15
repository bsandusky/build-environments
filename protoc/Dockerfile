FROM debian:latest

RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install curl \
    && apt-get -y install git \
    && apt-get -y install unzip \
    && apt-get -y install wget

ENV PROTOBUF_VERSION=3.10.1

RUN mkdir -p /protoc \
    && wget https://github.com/google/protobuf/releases/download/v${PROTOBUF_VERSION}/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip \
    && unzip protoc-${PROTOBUF_VERSION}-linux-x86_64.zip -d /protoc
ENV PATH=$PATH:/protoc/bin

# Install go & grpc for go using go get
RUN apt-get -y install golang
ENV GOPATH=/root/go \
    GOBIN=/root/go/bin \
    PATH=$PATH:/root/go/bin

RUN go get -u -v -ldflags '-w -s' \
    google.golang.org/grpc \
    github.com/golang/protobuf/protoc-gen-go

RUN cd /root/go/src/github.com/golang/protobuf/protoc-gen-go \
    && go install .

RUN apt-get clean && apt-get autoclean && apt autoremove

ENTRYPOINT ["protoc"]