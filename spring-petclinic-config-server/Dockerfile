FROM ubuntu
RUN apt-get update -y
RUN apt-get install wget -y
RUN wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb
RUN apt-get -qqy install openjdk-17-jdk openjdk-17-jre
#copie du jar dans l'image docker 
ENV SPRING_PROFILES_ACTIVE=docker
ENV DOCKERIZE_VERSION v0.7.0
RUN apt-get update \
    && apt-get install -y wget \
    && wget -O dockerize.tar.gz https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && apt-get autoremove -yqq --purge wget && rm -rf /var/lib/apt/lists/*
RUN tar xzf dockerize.tar.gz
RUN chmod +x dockerize
COPY target/spring-petclinic-config-server-3.0.2.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
