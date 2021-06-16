ARG PY_VERSION=3.9
# Using base image provided by nginx unit
FROM nginx/unit:1.22.0-python${PY_VERSION}
# Alternatively you can use different tags from https://hub.docker.com/r/nginx/unit
LABEL maintainer="ohjho <john@miro.io>"

RUN pip install --no-cache-dir fastapi

COPY ./app /fastapi
COPY config.json /docker-entrypoint.d/config.json
