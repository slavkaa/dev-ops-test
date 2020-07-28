FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y wget default-jdk

RUN groupadd tomcat
RUN useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

WORKDIR /tmp/
RUN wget https://apache.paket.ua/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz
RUN mkdir /opt/tomcat
RUN tar xzvf /tmp/apache-tomcat-8.5.57.tar.gz -C /opt/tomcat --strip-components=1
RUN rm /tmp/apache-tomcat-8.5.57.tar.gz

WORKDIR /opt/tomcat/
RUN chgrp -R tomcat /opt/tomcat
RUN chmod -R g+r conf
RUN chmod g+x conf
RUN chown -R tomcat webapps/ work/ temp/ logs/

EXPOSE 8080

CMD ["/opt/tomcat/bin/catalina.sh", "run"]
