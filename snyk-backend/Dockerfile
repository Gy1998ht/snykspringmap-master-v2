FROM openjdk:8
MAINTAINER kirbyszsr <kirbyszsr@foxmail.com>
VOLUME /tmp
EXPOSE 8080
ADD SnykSpringCrawler-0.0.1-SNAPSHOT.jar snykSpringCrawler.jar
RUN bash -c 'touch /snykSpringCrawler.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/snykSpringCrawler.jar","--debug"]
