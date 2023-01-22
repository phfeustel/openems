FROM adoptopenjdk/openjdk11:alpine-slim
RUN mkdir -p /opt/openems-backend
WORKDIR /opt/openems-backend
COPY build/openems-backend.jar ./
USER root
EXPOSE 8075-8082
CMD ["java", \
    "-XX:+ExitOnOutOfMemoryError", \ 
    "-Dfelix.cm.dir=/opt/openems-backend/config.d", \
    "-Djava.util.concurrent.ForkJoinPool.common.parallelism=100", \
    "-jar", "/opt/openems-backend/openems-backend.jar" \
]