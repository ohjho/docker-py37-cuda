#FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-runtime
ARG CUDA_VERSION=10.0
FROM ohjho/py37_cuda:${CUDA_VERSION}

LABEL maintainer="ohjho <john@miro.io>"

# # Download wget, useful for downloading weights
# RUN  apt-get update \
#   && apt-get install -y wget \
#   && rm -rf /var/lib/apt/lists/*

RUN pip install uvicorn gunicorn --no-cache-dir

COPY ./start.sh /start.sh
RUN chmod +x /start.sh

COPY ./gunicorn_conf.py /gunicorn_conf.py

COPY ./start-reload.sh /start-reload.sh
RUN chmod +x /start-reload.sh

COPY ./app /app
WORKDIR /app/

ENV PYTHONPATH=/app

EXPOSE 80

# Run the start script, it will check for an /app/prestart.sh script (e.g. for migrations)
# And then will start Gunicorn with Uvicorn
CMD ["/start.sh"]
