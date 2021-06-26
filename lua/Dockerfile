FROM centos:7

LABEL maintainer="Vladislav Grubov <vladgrubov@gmail.com>"

ENV LUA_VERSION="5.1.5"
ENV SHA1_CHECKSUM="b3882111ad02ecc6b972f8c1241647905cb2e3fc"

RUN set -ex \
    \
    && yum install -y epel-release \
    && yum update -y \
    && yum install -y readline-devel \
        wget \
        make \
        gcc \
        libc-dev \
        ncurses-dev \
        git \
        cmake \
    && wget -c https://www.lua.org/ftp/lua-${LUA_VERSION}.tar.gz \
    -O lua.tar.gz \
    && [ "$(sha1sum lua.tar.gz | cut -d' ' -f1)" = "${SHA1_CHECKSUM}" ] \
    && tar -xzf lua.tar.gz \
    && rm lua.tar.gz \
    && cd lua-${LUA_VERSION} \
    && make -j"$(nproc)" linux \
    && make install \
    && cd .. \
    && rm -rf lua-${LUA_VERSION} \
    \
    && yum clean all
CMD ["lua"]
