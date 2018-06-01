FROM 9jkh/dotdeb:debian-stretch
MAINTAINER 9JKH Dev<dev@9jkh.co.za>

ARG DEBIAN_FRONTEND=noninteractive
ARG PACKAGE_NAME

RUN curl -sSf https://files.9jkh.co.za/AD26AC18.asc | apt-key add -
RUN echo "deb https://dl.bintray.com/9jkh/gnupg stretch main" | tee -a /etc/apt/sources.list.d/9jkh_gnupg.list
RUN apt-get update -qq

# resolve package dependencies
ADD debian/control /root/
RUN mk-build-deps --install --tool 'apt-get -y -qq' --remove /root/control && rm -f /root/control

ADD . /usr/src/builddir
WORKDIR /usr/src/builddir

RUN uscan --download-current-version
RUN cd "$(find .. -type d -name ${PACKAGE_NAME}-\*)" && dpkg-buildpackage > /dev/null
