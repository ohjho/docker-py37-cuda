# Dockerfile Deep Learning with FastAPI

comes with Python Version `3.7` and CUDA of your choice.

For a **different CUDA combo** change line 1 in the Dockerfile with the right base image from [here](https://hub.docker.com/repository/docker/ohjho/py37_cuda/tags):
```
ARG CUDA_VERSION=10.0
```

Demo:
```
docker run --gpus all --rm ohjho/py_deep_learning_fastapi:CUDA10.0-Py3.7
```

This docker image was basically a fork from [tiangolo's](https://github.com/tiangolo/uvicorn-gunicorn-machine-learning-docker/tree/master/cuda9.1-python3.7) but with support for CUDA.

It was claimed that there are _auto-tunning_ for the [gunicorn ](https://gunicorn.org/) settings but the logic is just basically 1 worker per CPU core available (_with min of 2 workers_). Therefore, it is still better to start with 1 worker, do a load test, see how much resources that requires and scale up the number of workers as needed.

My preferred container environment configs for tunning gunicorn are:
* [`TIMEOUT`](https://github.com/tiangolo/uvicorn-gunicorn-fastapi-docker#timeout): set to 0 because it's hard to keep track of long running async tasks
* [`GRACEFUL_TIMEOUT`](https://github.com/tiangolo/uvicorn-gunicorn-fastapi-docker#graceful_timeout): same as above
* [`WEB_CONCURRENCY`](https://github.com/tiangolo/uvicorn-gunicorn-fastapi-docker#web_concurrency): this directly control the number of workers

For example, the following will launch your API with 2 workers:
```
docker run --gpus all -d -e TIMEOUT="0" -e GRACEFUL_TIMEOUT="0" -e WEB_CONCURRENCY="2" --rm --name name_your_container name_of_your_image
```

This directory is used to generate images on [this DockerHub repo](https://hub.docker.com/repository/docker/ohjho/py_deep_learning_fastapi)
