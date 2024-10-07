FROM apache/airflow:2.9.3-python3.11


USER root

ENV REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt



RUN apt-get update
RUN apt install -y ffmpeg libsm6 libxext6 \
  ghostscript python3-tk \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*



USER airflow

WORKDIR /tmp
COPY 2.9.3_new_requirements.txt /tmp/new_requirements.txt

RUN python -m pip install --no-cache-dir --upgrade pip
RUN python -m pip install --no-cache-dir torch==2.4.1+cpu.cxx11.abi -f https://download.pytorch.org/whl/torch/
RUN python -m pip install --no-cache-dir "apache-airflow==${AIRFLOW_VERSION}" -r /tmp/new_requirements.txt

RUN python -m pip install --no-cache-dir  airflow-provider-grafana-loki
ENV PATH=$PATH:$AIRFLOW_HOME/config

