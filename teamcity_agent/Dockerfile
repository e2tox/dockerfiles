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

ENV JAVA_OPTS -Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom -server -XX:+UseParallelGC

EXPOSE 9000

CMD ["/usr/share/BuildAgent/bin/agent.sh", "run"]