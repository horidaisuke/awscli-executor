FROM library/docker:26.1.4
ENV AWSCLI_VERSION 2.17.22
RUN apk update \
 && apk add --no-cache \
    bash \
    curl \
    groff \
 && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.19/main \
    python3~=3.11 \
    python3-dev~=3.11 \
 && apk add --virtual .build-deps \
    cmake \
    g++ \
    gcc \
    gzip \
    libc-dev \
    libffi-dev \
    make \
    openssl-dev \
    tar \
 && curl https://awscli.amazonaws.com/awscli-${AWSCLI_VERSION}.tar.gz | tar -xz \
 && cd awscli-${AWSCLI_VERSION} \
 && ./configure --prefix=/usr/local/aws-cli/ --with-download-deps \
 && make \
 && make install \
 && ln -sf /usr/local/aws-cli/bin/aws /usr/local/bin/aws \
 && cd .. \
 && rm -rf awscli-${AWSCLI_VERSION} \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/*