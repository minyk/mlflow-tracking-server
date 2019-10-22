FROM python:3.7

LABEL maintainer "Florian Muchow <flmuchow@gmail.com>"

RUN pip install mlflow==1.3.0 && \
    pip install awscli --upgrade --user && \
    pip install boto3==1.9.240

ENV MESOSPHERE_HOME="/opt/mesosphere"
ARG BOOTSTRAP_DOWNLOAD_URL="https://downloads.mesosphere.com/dcos-commons/artifacts/0.57.0/bootstrap.zip"
ARG BOOTSTRAP_BINARY="${MESOSPHERE_HOME}/bootstrap.zip"
RUN mkdir -p ${MESOSPHERE_HOME} \
    && curl -L -o ${BOOTSTRAP_BINARY} ${BOOTSTRAP_DOWNLOAD_URL} \
    && unzip ${BOOTSTRAP_BINARY} -d ${MESOSPHERE_HOME} \
    && rm ${BOOTSTRAP_BINARY}
ENV BOOTSTRAP ${MESOSPHERE_HOME}/bootstrap

ENV PORT 5000
ENV AWS_BUCKET bucket
ENV AWS_ACCESS_KEY_ID aws_id
ENV AWS_SECRET_ACCESS_KEY aws_key
ENV MLFLOW_S3_ENDPOINT_URL http://miniod.miniod.l4lb.thisdcos.directory:9000

COPY files/run.sh /

ENTRYPOINT ["/run.sh"]
