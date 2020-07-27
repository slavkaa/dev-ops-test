FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y default-jdk git maven nano mc wget

RUN groupadd tomcat
RUN useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

RUN cd /tmp &&  wget https://apache.paket.ua/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz
RUN mkdir /opt/tomcat
RUN tar xzvf /tmp/apache-tomcat-8.5.57.tar.gz -C /opt/tomcat --strip-components=1
RUN cd /opt/tomcat && chgrp -R tomcat /opt/tomcat
RUN cd /opt/tomcat && chmod -R g+r conf
RUN cd /opt/tomcat && chmod g+x conf
RUN cd /opt/tomcat && chown -R tomcat webapps/ work/ temp/ logs/

RUN mkdir -p /home/ubuntu/build
RUN cd /home/ubuntu/build && git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git
RUN cd /home/ubuntu/build/boxfuse-sample-java-war-hello && mvn package
RUN cp /home/ubuntu/build/boxfuse-sample-java-war-hello/target/hello-1.0.war /opt/tomcat/webapps/hello.war

EXPOSE 8080

CMD ["/opt/tomcat/bin/catalina.sh", "run"]
