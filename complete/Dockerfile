# FROM openjdk:8-jdk-alpine
# ARG JAR_FILE=target/*.jar
# COPY ${JAR_FILE} app.jar
# ENTRYPOINT ["java","-jar","/app.jar"]

# FROM openjdk:8-jdk-alpine
# RUN addgroup -S spring && adduser -S spring -G spring
# USER spring:spring
FROM openjdk:8
#RUN addgroup -S spring && adduser -S spring -G spring
# RUN groupadd spring && useradd -g spring spring
# RUN usermod -a -G spring spring
# USER spring:spring
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
RUN mkdir /opt/cdbg && \
     wget -qO- https://storage.googleapis.com/cloud-debugger/compute-java/debian-wheezy/cdbg_java_agent_gce.tar.gz | \
     tar xvz -C /opt/cdbg
# https://stackoverflow.com/questions/64291139/run-java-program-and-shell-script-on-entrypoint-in-dockerfile
# https://stackoverflow.com/questions/53827877/how-can-i-run-multiple-jars-in-dockerfile
## https://docs.docker.com/config/containers/multi-service_container/
# RUN java -agentpath:/opt/cdbg/cdbg_java_agent.so \
#     -Dcom.google.cdbg.module=gs-spring-boot-docker \
#     -Dcom.google.cdbg.version=0.1.0 \
#     -Dcom.google.cdbg.breakpoints.enable_canary=true \
#     -jar /app.jar
# ENTRYPOINT ["java","-jar","/app.jar"]
ENTRYPOINT ["java", "-agentpath:/opt/cdbg/cdbg_java_agent.so", "-Dcom.google.cdbg.module=gs-spring-boot-docker", "-Dcom.google.cdbg.version=0.1.0", "-Dcom.google.cdbg.breakpoints.enable_canary=true","-jar","/app.jar"]
#
# FROM openjdk:8
# #RUN addgroup -S spring && adduser -S spring -G spring
# RUN groupadd spring && useradd -g spring spring
# # RUN usermod -a -G spring spring
# USER spring:spring
# # RUN apt-get update
# # RUN apt-get install curl
# ARG DEPENDENCY=target/dependency
# COPY ${DEPENDENCY}/BOOT-INF/lib /app/lib
# COPY ${DEPENDENCY}/META-INF /app/META-INF
# COPY ${DEPENDENCY}/BOOT-INF/classes /app
# # RUN mkdir /opt/cdbg && \
# #      wget -qO- https://storage.googleapis.com/cloud-debugger/compute-java/debian-wheezy/cdbg_java_agent_gce.tar.gz | \
# #      tar xvz -C /opt/cdbg
# # RUN java -agentpath:/opt/cdbg/cdbg_java_agent.so \
# #     -Dcom.google.cdbg.module=SpringBootDocker \
# #     -Dcom.google.cdbg.version=0.1.0 \
# #     -Dcom.google.cdbg.breakpoints.enable_canary=false \
# #     -jar ~/.m2/repository/org/springframework/myapp.jar
# ENTRYPOINT ["java","-cp","app:app/lib/*","hello.Application"]