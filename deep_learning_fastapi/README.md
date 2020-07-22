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

Credit: [tiangolo](https://github.com/tiangolo/uvicorn-gunicorn-machine-learning-docker/tree/master/cuda9.1-python3.7)
