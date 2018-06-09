FROM fedora:latest

# GLIBC & toolset
RUN dnf update -y \
&& dnf upgrade -y \
&& dnf group install "Development Tools" -y \
&& dnf install binutils -y \
&& dnf install glibc-static -y \
&& dnf install nasm -y \
&& dnf clean all -y

# MUSL LIBC & toolset
RUN git clone git://git.musl-libc.org/musl \
&& cd musl \
&& ./configure \
&& make \
&& make install \
&& echo 'PATH=$PATH:/usr/local/musl/bin' >> ~/.profile \
&& source ~/.profile


