FROM microbox/java:8u66

# TeamCity Version
ENV TEAMCITY_VERSION 9.1.5

# Download and unarchive TeamCity
RUN curl -jksSL https://download.jetbrains.com/teamcity/TeamCity-${TEAMCITY_VERSION}.tar.gz \
    | tar -xzf - -C /usr/share

ENV TEAMCITY_HOME /usr/share/TeamCity
ENV TEAMCITY_DATA_PATH /data

ENV JAVA /usr/java/default/bin/java
ENV JAVA_OPTS -Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom
ENV CATALINA_HOME /usr/share/TeamCity
ENV CATALINA_BASE /usr/share/TeamCity
ENV CATALINA_OPTS -server -XX:+UseParallelGC

EXPOSE 8111

CMD ["/usr/share/TeamCity/bin/catalina.sh", "run"]