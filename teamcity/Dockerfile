FROM microbox/java:8u66

# TeamCity Version
ENV TEAMCITY_VERSION 9.1.5

# Download and unarchive TeamCity
RUN apk upgrade --update && \
    apk add --update curl git && \
    curl -jksSL https://download.jetbrains.com/teamcity/TeamCity-${TEAMCITY_VERSION}.tar.gz \
    | tar -xzf - -C /usr/share && \
    apk del curl && \
    rm -rf /tmp/* /var/cache/apk/*

ENV TEAMCITY_HOME /usr/share/TeamCity
    TEAMCITY_DATA_PATH /data
    JAVA_OPTS -Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom
    CATALINA_HOME /usr/share/TeamCity
    CATALINA_BASE /usr/share/TeamCity
    CATALINA_OPTS -server -XX:+UseParallelGC

ADD ./data /data

EXPOSE 8111

CMD ["/usr/share/TeamCity/bin/catalina.sh", "run"]