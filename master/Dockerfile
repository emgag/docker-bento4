FROM alpine:3.8
LABEL maintainer="Matthias Blaser <mb@emgag.com>"

ENV BENTO4_INSTALL_DIR=/opt/bento4
ENV PATH=/opt/bento4/bin:${PATH}
 
RUN apk update \
  && apk add --no-cache \
      bash \
      ca-certificates \
      ffmpeg \
      g++ \
      gcc \
      git \
      libgcc \
      make \
      python \
      wget \
  && rm -rf /var/cache/apk/*

RUN mkdir -p \
  ${BENTO4_INSTALL_DIR}/bin \
  ${BENTO4_INSTALL_DIR}/scripts \
  ${BENTO4_INSTALL_DIR}/include

RUN mkdir -p /usr/local/src && cd /usr/local/src/ \
  && git clone --depth 1 https://github.com/axiomatic-systems/Bento4.git \
  && cd /usr/local/src/Bento4/Build/Targets/x86-unknown-linux \
  && make AP4_BUILD_CONFIG=Release \
  && cd /usr/local/src/Bento4 \
  && cp -rv Build/Targets/x86-unknown-linux/Release/. ${BENTO4_INSTALL_DIR}/bin \
  && cp -rv Source/Python/utils/. ${BENTO4_INSTALL_DIR}/utils \
  && cp -rv Source/Python/wrappers/. ${BENTO4_INSTALL_DIR}/bin \
  && cp -rv Source/C++/**/*.h ${BENTO4_INSTALL_DIR}/include \
  && cd ${BENTO4_INSTALL_DIR} \
  && rm -rf /usr/local/src

WORKDIR ${BENTO4_INSTALL_DIR}

CMD ["bash"]
