FROM alpine:latest

RUN apk update \
&& apk upgrade \
&& apk add --update alpine-sdk \
                    musl-dev \
                    nasm \
                    bash \
&& rm -fr /var/cache/apk/*