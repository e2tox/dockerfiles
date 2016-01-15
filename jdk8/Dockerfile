# AlpineLinux with a glibc-2.21 and Oracle Java 8
FROM alpine:3.3

# Java Version and other ENV
ENV JAVA_VERSION_MAJOR=8 \
    JAVA_VERSION_MINOR=66 \
    JAVA_VERSION_BUILD=17 \
    JAVA_PACKAGE=jdk \
    JAVA=/usr/java/default/bin/java \
    JAVA_HOME=/usr/java/default \
    PATH=${PATH}:/usr/java/default/bin \
    LANG=C.UTF-8

# do all in one step
RUN apk upgrade --update && \
    apk add --update curl ca-certificates bash && \
    curl -L -o /tmp/glibc-2.21-r2.apk "https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk" && \
    apk add --allow-untrusted /tmp/glibc-2.21-r2.apk && \
    curl -L -o /tmp/glibc-bin-2.21-r2.apk "https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-bin-2.21-r2.apk" && \
    apk add --allow-untrusted /tmp/glibc-bin-2.21-r2.apk && \
    /usr/glibc/usr/bin/ldconfig /lib /usr/glibc/usr/lib && \
    mkdir /usr/java && curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" \
    http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz \
    | gunzip -c - | tar -C /usr/java -xf - && \
    apk del curl && \
    ln -s /usr/java/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /usr/java/default && \
    rm -rf /usr/java/default/*src.zip \
           /usr/java/default/lib/missioncontrol \
           /usr/java/default/lib/visualvm \
           /usr/java/default/lib/*javafx* \
           /usr/java/default/jre/plugin \
           /usr/java/default/jre/bin/javaws \
           /usr/java/default/jre/bin/jjs \
           /usr/java/default/jre/bin/keytool \
           /usr/java/default/jre/bin/orbd \
           /usr/java/default/jre/bin/pack200 \
           /usr/java/default/jre/bin/policytool \
           /usr/java/default/jre/bin/rmid \
           /usr/java/default/jre/bin/rmiregistry \
           /usr/java/default/jre/bin/servertool \
           /usr/java/default/jre/bin/tnameserv \
           /usr/java/default/jre/bin/unpack200 \
           /usr/java/default/jre/lib/javaws.jar \
           /usr/java/default/jre/lib/deploy* \
           /usr/java/default/jre/lib/desktop \
           /usr/java/default/jre/lib/*javafx* \
           /usr/java/default/jre/lib/*jfx* \
           /usr/java/default/jre/lib/jfr* \
           /usr/java/default/jre/lib/amd64/libdecora_sse.so \
           /usr/java/default/jre/lib/amd64/libprism_*.so \
           /usr/java/default/jre/lib/amd64/libfxplugins.so \
           /usr/java/default/jre/lib/amd64/libglass.so \
           /usr/java/default/jre/lib/amd64/libgstreamer-lite.so \
           /usr/java/default/jre/lib/amd64/libjavafx*.so \
           /usr/java/default/jre/lib/amd64/libjfx*.so \
           /usr/java/default/jre/lib/ext/jfxrt.jar \
           /usr/java/default/jre/lib/ext/nashorn.jar \
           /usr/java/default/jre/lib/oblique-fonts \
           /usr/java/default/jre/lib/plugin.jar \
           /tmp/* /var/cache/apk/* && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

# EOF