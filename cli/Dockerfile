FROM python:3.13-alpine AS builder

WORKDIR /cli

# RUN apk update && apk add --virtual build-base python3-dev tzdata

ADD client /usr/bin/
RUN chmod +x /usr/bin/client

# COPY requirements.txt /cli
COPY supervisord.conf /etc/supervisor/supervisord.conf
RUN pip install --upgrade pip

RUN pip install click \
    pydantic \
    python-dotenv \
    tabulate \
    requests \
    numpy \
    pandas \
    colorama \
    psycopg2-binary \
    supervisor \
    pika

COPY entrypoint.sh /scripts/entrypoint.sh
RUN chmod +x /scripts/entrypoint.sh

ENTRYPOINT [ "/scripts/entrypoint.sh" ]
