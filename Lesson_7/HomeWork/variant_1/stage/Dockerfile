FROM ubuntu:18.04

RUN apt-get update \
  && apt-get install -y default-jdk git maven

RUN groupadd tomcat \
  && useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

WORKDIR /tmp/
RUN mkdir -p /opt/tomcat/webapps

WORKDIR /opt/tomcat/
RUN chgrp -R tomcat /opt/tomcat \
  && chown -R tomcat webapps/ \
  && mkdir -p /home/ubuntu/build

WORKDIR /home/ubuntu/build/
RUN git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git

WORKDIR /home/ubuntu/build/boxfuse-sample-java-war-hello/
RUN mvn package \
  && cp /home/ubuntu/build/boxfuse-sample-java-war-hello/target/hello-1.0.war /opt/tomcat/webapps/hello.war

CMD ["tail", "-f", "/dev/null"]
