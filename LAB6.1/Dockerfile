FROM ubuntu:18.04
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y -q python-all python-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN mkdir -p /opt/webapp
COPY . /opt/webapp/
COPY requirements.txt /tmp/
RUN pip install -qr /tmp/requirements.txt
WORKDIR /opt/webapp
EXPOSE 5000
ENTRYPOINT ["python", "app.py"]