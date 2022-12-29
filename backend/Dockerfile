FROM maven:3.8.6-jdk-11
WORKDIR /abc
COPY ./web /abc
RUN ["mvn","package"]
ENTRYPOINT ["mvn","spring-boot:run"]
EXPOSE 8081
