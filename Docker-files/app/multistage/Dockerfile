FROM openjdk:11 AS build_image
RUN apt-get update && apt-get  install maven -y
RUN apt-get update && apt-get install -y --no-install-recommends maven
RUN apt-get update && apt-get install -y --no-install-recommends maven && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build_image vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
