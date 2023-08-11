# l'image de base est ubunut
FROM ubuntu
# installation de jdk 17
RUN apt-get update -y
RUN apt-get install wget -y
RUN apt-get -qqy install openjdk-17-jdk openjdk-17-jre
#copie du jar dans l'image docker
#on definit des variables d'environnements
ENV DOCKERIZE_VERSION v0.7.0
ENV SPRING_PROFILES_ACTIVE=docker
#on recupere la commande dockerize 
RUN apt-get update \
    && apt-get install -y wget \
    && wget -O dockerize.tar.gz https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && apt-get autoremove -yqq --purge wget && rm -rf /var/lib/apt/lists/*
RUN tar xzf dockerize.tar.gz
# on la rend executable
RUN chmod +x dockerize
# on copie le jar a executer dans le fichier app.jar
COPY target/spring-petclinic-discovery-server-3.0.2.jar app.jar
# dockerise permet d'attendre que le cofnig-server soit demarre avant de executer le serveur
# eureka de decouverte, il faudra faire un link dans la commande run vers config-server
entrypoint ["./dockerize","-wait=tcp://config-server:8888","-timeout=60s","--","java","-jar", "app.jar"]
