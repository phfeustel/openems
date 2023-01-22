FROM adoptopenjdk/openjdk11:slim
RUN mkdir -p /opt/openems-backend
WORKDIR /opt/openems-backend
COPY build/openems-backend.jar ./
COPY openems-backend.sh ./
RUN chmod 777 ./openems-backend.sh
USER root
EXPOSE 8075-8080
ENTRYPOINT ["./openems-backend.sh"]
