FROM microbox/jdk:8u66

# TeamCity Version
ENV TEAMCITY_VERSION 9.1.5

# Download and unarchive TeamCity
RUN apk upgrade --update && \
    apk add --update curl git && \
    curl -jksSL https://download.jetbrains.com/teamcity/TeamCity-${TEAMCITY_VERSION}.tar.gz \
    | tar -xzf - -C /usr/share && \
    mv /usr/share/TeamCity/buildAgent /usr/share/BuildAgent && \
    rm -rf /tmp/* /var/cache/apk/* /usr/share/TeamCity

# Install development sdk and tools
RUN apk upgrade --update && \
    apk add --update ansible nodejs make gcc go tar && \
    mkdir /root/.maven && \
    curl -jksSL http://www.us.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
    | tar -xzf - --strip-components=1 -C /root/.maven && \
    rm -rf /tmp/* /var/cache/apk/*

# SSH
ADD config/ssh /root/.ssh

# Ansible
ADD config/ansible /root/.ansible_library

# SBT
ADD config/sbt /usr/local/bin

# Build Agent
ADD config/buildAgent /usr/share/BuildAgent/conf

# Environment settings
ENV JAVA_OPTS="-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom -server -XX:+UseParallelGC" \
    GO_ROOT="/usr/lib/go" \
    GO_PATH="/root/go" \
    M2_HOME="/root/.maven" \
    PATH="${PATH}:${GO_ROOT}/bin:${M2_HOME}/bin" \

EXPOSE 9000

CMD ["/usr/share/BuildAgent/bin/agent.sh", "run"]