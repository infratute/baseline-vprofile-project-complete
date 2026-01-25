# Build stage
FROM eclipse-temurin:8-jdk AS build_image

RUN apt-get update && \
    apt-get install -y maven git && \
    rm -rf /var/lib/apt/lists/*

RUN git clone -b vp-docker https://github.com/imranvisualpath/vprofile-repo.git

WORKDIR /vprofile-repo
RUN mvn clean install -DskipTests

# Runtime stage
FROM tomcat:8-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build_image /vprofile-repo/target/vprofile-v2.war \
     /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
