FROM ubuntu:trusty



RUN \
    tar xjpf /root/crosstools-mips-gcc-4.6-linux-3.4-uclibc-0.9.32-binutils-2.21.Rel1.2.tar.bz2 -C / && \
    apt-get update && \
    apt-get install -y build-essential automake uuid-dev liblzo2-dev g++-multilib flex bison pkg-config zlib1g-dev nodejs ruby-compass git python && \
    ln -sf /bin/bash /bin/sh 
