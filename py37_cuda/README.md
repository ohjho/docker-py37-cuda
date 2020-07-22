# Dockerfile for py 3.7 and CUDA `X.Y`

change the first line of the Dockerfile for your version of CUDA with the right tag [here](https://hub.docker.com/r/nvidia/cuda/tags)

For this example, we are using CUDA version `10.0` and a modified version of [this](https://github.com/tiangolo/python-machine-learning-docker/tree/master/cuda9.1-python3.7)

Demo:
```
docker run --gpus all --rm ohjho/py37_cuda:10.0
```
The `nvidia-smi` screen should show if the container can access GPU

Also from the cuda [doc](https://hub.docker.com/r/nvidia/cuda)
> For CUDA 10.0, `nvidia-docker2` (v2.1.0) or greater is recommended. It is also recommended to use Docker 19.03.
