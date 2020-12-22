FROM ubuntu:bionic
RUN apt-get -y update && apt-get -y install git wget unzip python python3 openjdk-11-jre-headless gettext autogen autoconf libtool pkg-config
RUN git clone https://github.com/emscripten-core/emsdk.git
RUN cd emsdk && ./emsdk install latest && ./emsdk activate latest
RUN wget https://github.com/voikko/corevoikko/archive/rel-voikko-fi-2.4.zip && unzip rel-voikko-fi-2.4.zip
RUN cd /corevoikko-rel-voikko-fi-2.4/libvoikko && wget https://www.puimula.org/htp/testing/voikko-snapshot-v5/dict-morpho.zip && unzip dict-morpho.zip
RUN /bin/bash -c "cd emsdk && source emsdk_env.sh && cd /corevoikko-rel-voikko-fi-2.4/libvoikko && ./autogen.sh && js/configure.sh && make"
RUN /bin/bash -c "cd emsdk && source emsdk_env.sh && cd /corevoikko-rel-voikko-fi-2.4/libvoikko && chmod a+x js/build.sh && NODE_OPTIONS=--max_old_space_size=12000 js/build.sh embed"