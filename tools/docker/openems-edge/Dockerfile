FROM adoptopenjdk/openjdk11:alpine-slim
RUN mkdir -p /opt/openems-edge
WORKDIR /opt/openems-edge
COPY build/openems-edge.jar ./
USER root
EXPOSE 8080 8084-8085
CMD ["java", \
    "-XX:+ExitOnOutOfMemoryError", \
    "-Dfelix.cm.dir=/opt/openems-edge/config.d", \
    "-jar", "/opt/openems-edge/openems-edge.jar" \
]