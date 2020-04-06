# -*- mode: dockerfile; coding: utf-8 -*-
FROM debian:buster-slim AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
       build-essential \
       ca-certificates \
       cpio \
       git \
       libffi-dev \
       libgmp-dev \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /build/
RUN git clone --depth 1 https://github.com/lambdaconservatory/ypsilon.git
WORKDIR /build/ypsilon
RUN make
RUN make install

FROM debian:buster-slim
RUN apt-get update && apt-get -y --no-install-recommends install \
       libffi6 \
       libgmp10 \
  && rm -rf /var/lib/apt/lists/*
COPY --from=build /usr/local/ /usr/local/
COPY scheme-script /usr/local/bin
RUN ln -s ypsilon /usr/local/bin/scheme-banner
CMD ["scheme-banner"]
