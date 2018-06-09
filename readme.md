# Ephemeral Build Environments

A set of Dockerfiles to build ephemeral build environments for various uses. 
To create a usable environment, run `docker build --tag <name of image you'd like to create e.g. fedora:dev> .` from the specific directory of the environment to use.
To use, run `docker run --rm -v$(pwd):$(pwd) -w$(pwd) <tagname from above> <command>`
For example: `docker run --rm -v$(pwd):$(pwd) -w$(pwd) fedora:dev gcc-musl -o binary source.c`

Fedora image includes the following toolsets (not an exhaustive list):
- gcc
- ld
- nasm
- musl-gcc
- glibc
- musl-libc
- binutils (strings, objdump, etc.)
- git
- make


Alpine image includes the following toolsets (not an exhaustive list):
- gcc (compiles against musl libc)
- ld
- nasm
- musl-libc
- binutils (strings, objdump, etc.)
- bash
- git
- make

