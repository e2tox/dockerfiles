FROM microbox/jdk:8u66

# Install packages
RUN apk upgrade --update && \
    apk add --update ansible make gcc g++ go tar curl git && \
    rm -rf /tmp/* /var/cache/apk/*

# TeamCity Version
ENV TEAMCITY_VERSION 9.1.5
RUN curl -jksSL https://download.jetbrains.com/teamcity/TeamCity-${TEAMCITY_VERSION}.tar.gz \
    | tar -xzf - -C /usr/share && \
    mv /usr/share/TeamCity/buildAgent /usr/share/BuildAgent && \
    rm -rf /usr/share/TeamCity

# Maven
ENV MAVEN_VERSION=3.3.9
RUN mkdir /root/.maven && \
    curl -jksSL http://www.us.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    | tar -xzf - --strip-components=1 -C /root/.maven

# Nodejs
ENV NODEJS_VERSION=5.4.1
RUN curl -jksSL https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.gz \
    | tar -xzf - --strip-components=1 -C /usr/local

# Phantomjs libs
RUN apk add --update freetype fontconfig && \
    rm -rf /tmp/* /var/cache/apk/*

# SSH
ADD config/ssh /root/.ssh

# Ansible
ADD config/ansible /root/.ansible_library

# SBT
ADD config/sbt /usr/local/bin

# Build Agent
ADD config/buildAgent /usr/share/BuildAgent/conf

# LIBGCC
ADD config/libstdc++/libstdc++.so.6.0.19 /usr/lib/libstdc++.so.6.0.21

# Environment settings
ENV JAVA_OPTS="-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom -server -XX:+UseParallelGC" \
    GOROOT="/usr/lib/go" \
    GOPATH="/root/go" \
    M2_HOME="/root/.maven" \
    PATH="/usr/lib/go/bin:/root/.maven/bin:$PATH"

EXPOSE 9000

CMD ["/usr/share/BuildAgent/bin/agent.sh", "run"]