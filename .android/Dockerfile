FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    cmake \
    ninja-build \
    python3 \
    unzip

RUN curl -O https://dl.google.com/android/repository/android-ndk-r25b-linux.zip
RUN unzip android-ndk-r25b-linux.zip && mv android-ndk-r25b /ndk

RUN curl -o capnproto.tar.gz https://capnproto.org/capnproto-c++-0.10.2.tar.gz
RUN mkdir -p /src/capnproto
RUN tar zxf capnproto.tar.gz -C /src/capnproto --strip-components=1
RUN mkdir -p /build/capnproto
RUN cd /build/capnproto
RUN /src/capnproto/configure
RUN make -j$(nproc) install
RUN cd -

RUN mkdir -p /build/rr
RUN chmod 777 /build/rr

WORKDIR /build/rr
CMD ["/bin/bash", "/src/rr/.android/build.sh"]
