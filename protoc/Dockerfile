FROM fedora:latest
RUN dnf update -y \
    && dnf upgrade -y \
    && dnf group install "Development Tools" -y \
    && dnf install binutils -y \
    && dnf install libstdc++ -y \
    && dnf install unzip -y \
    && dnf install wget -y \
    && dnf clean all -y

ENV DART_VERSION=2.0.0-dev.69.4 \
    GRPC_VERSION=1.13.1 \
    PROTOBUF_VERSION=3.6.0

# Install protobuf
RUN mkdir -p /protobuf && \
    curl -L https://github.com/google/protobuf/releases/download/v${PROTOBUF_VERSION}/protobuf-all-${PROTOBUF_VERSION}.tar.gz | tar xvz --strip-components=1 -C /protobuf

RUN mkdir -p /protoc && \
    wget https://github.com/google/protobuf/releases/download/v${PROTOBUF_VERSION}/protoc-${PROTOBUF_VERSION}-linux-x86_64.zip && \
    unzip protoc-${PROTOBUF_VERSION}-linux-x86_64.zip -d /protoc

# Install go & grpc for go using go get
RUN dnf install golang -y
RUN export GOPATH=/root/go \
    export GOBIN=/root/go/bin \
    export PATH=/root/go/bin:$PATH
RUN go get -u -v -ldflags '-w -s' \
    github.com/golang/protobuf/proto \
    github.com/golang/protobuf/protoc-gen-go \
    google.golang.org/grpc
RUN cd /root/go/src/github.com/golang/protobuf/protoc-gen-go \
    && go install .
       
    # Install dart & grpc for dart using pub
    RUN mkdir -p /dart && \
    wget https://storage.googleapis.com/dart-archive/channels/dev/release/${DART_VERSION}/sdk/dartsdk-linux-x64-release.zip && \
    unzip dartsdk-linux-x64-release.zip -d /dart
    RUN export PATH=/dart/dart-sdk/bin:$PATH \
    && pub global activate protoc_plugin \
    && export PATH=$HOME/.pub-cache/bin:$PATH

ENTRYPOINT ["/protoc/bin/protoc"]