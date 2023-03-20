FROM gcr.io/forgerock-io/java-17:latest

ARG JAR_FILE

# dependencies for wait-for.sh
RUN apt-get -q update && apt-get -qy install netcat

RUN mkdir /app
RUN groupadd -r tac && useradd -r -s /bin/false -g tac tac

WORKDIR /app
COPY $JAR_FILE /app/test-actions-server.jar

# wait-for.sh for checking if other services are ready before starting spring
COPY docker/scripts/*.sh /app/

RUN chown -R tac:tac /app
USER tac

CMD ["java", "-jar", "test-actions-server.jar"]
