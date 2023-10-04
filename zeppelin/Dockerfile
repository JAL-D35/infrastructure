# BUILD STAGE
FROM debian:12-slim AS build

WORKDIR /opt

RUN apt update \
        && apt install -y wget

RUN wget -O spark.tgz https://dlcdn.apache.org/spark/spark-3.2.4/spark-3.2.4-bin-hadoop3.2.tgz \
        && tar -zxf spark.tgz


# RUNTIME STAGE
FROM apache/zeppelin:0.10.1

RUN echo "export SPARK_HOME=/opt/spark" > /opt/zeppelin/conf/zeppelin-env.sh

COPY --from=build /opt/spark-3.2.4-bin-hadoop3.2 /opt/spark
