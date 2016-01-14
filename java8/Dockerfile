FROM alpine

# Install cURL
RUN apk upgrade --update && \
    apk add curl ca-certificates tar bash && \
    curl -Ls https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk && \
    apk add --allow-untrusted /tmp/glibc-2.21-r2.apk

# Java Version
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 66
ENV JAVA_VERSION_BUILD 17
ENV JAVA_PACKAGE       server-jre

# Download and unarchive Java
RUN mkdir /usr/java && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie"\
  http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \
    | tar -xzf - -C /usr/java &&\
    ln -s /usr/java/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /usr/java/default &&\
    rm -rf /usr/java/default/*src.zip \
           /usr/java/default/lib/missioncontrol \
           /usr/java/default/lib/visualvm \
           /usr/java/default/lib/*javafx* \
           /usr/java/default/jre/lib/plugin.jar \
           /usr/java/default/jre/lib/ext/jfxrt.jar \
           /usr/java/default/jre/bin/javaws \
           /usr/java/default/jre/lib/javaws.jar \
           /usr/java/default/jre/lib/desktop \
           /usr/java/default/jre/plugin \
           /usr/java/default/jre/lib/deploy* \
           /usr/java/default/jre/lib/*javafx* \
           /usr/java/default/jre/lib/*jfx* \
           /usr/java/default/jre/lib/amd64/libdecora_sse.so \
           /usr/java/default/jre/lib/amd64/libprism_*.so \
           /usr/java/default/jre/lib/amd64/libfxplugins.so \
           /usr/java/default/jre/lib/amd64/libglass.so \
           /usr/java/default/jre/lib/amd64/libgstreamer-lite.so \
           /usr/java/default/jre/lib/amd64/libjavafx*.so \
           /usr/java/default/jre/lib/amd64/libjfx*.so

# Set environment
ENV JAVA_HOME /usr/java/default
ENV PATH ${PATH}:${JAVA_HOME}/bin