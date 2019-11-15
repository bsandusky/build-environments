FROM debian:latest

RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install curl \
    && apt-get -y install git \
    && apt-get -y install build-essential \
    && apt-get -y install sudo

# install cmake
RUN apt-get -y install cmake

# install nodejs
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - \
    && apt-get install -y nodejs

# install emsdk
RUN mkdir -p ~/.emsdk \
    && cd ~/.emsdk \
    && git clone https://github.com/juj/emsdk . \
    && ./emsdk install sdk-incoming-64bit binaryen-master-64bit \
    && ./emsdk activate sdk-incoming-64bit binaryen-master-64bit

# install env variables
RUN echo "source ~/.emsdk/emsdk_env.sh" >> ~/.bashrc \
    && source ~/.bashrc

# clean up
RUN apt-get clean && apt-get autoclean && apt autoremove

# emrun port
EXPOSE 6931