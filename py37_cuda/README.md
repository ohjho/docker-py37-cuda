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

This directory is used to generate images on [this DockerHub repo](https://hub.docker.com/repository/docker/ohjho/py37_cuda)

Build:
```
docker build -t ohjho/py37_cuda:[version tag] -f [dockerfile_path | default: Dockerfile] .
```

## Detectron2

A few good examples on how to dockerize Detectron2:
* [from FAIR themselves](https://github.com/facebookresearch/detectron2/tree/master/docker)
* [this method](https://github.com/mkang30/ImageDecomposer/blob/master/fastapi/Dockerfile) uses a zip version of Detectron2
* But you could just specify the version explicitly in your pip install [like this approach](https://github.com/gkswjdzz/ainized-detectron2/blob/7f9907b4e2381f26f269ebf20639019c791173b7/Dockerfile-gpu#L23) or consult [here in the official doc](https://detectron2.readthedocs.io/tutorials/install.html#install-pre-built-detectron2-linux-only)

[this Dockerfile](Dockerfile-detectron2official) uses:
* Python `3.6.9`
* CUDA `10.1`
* PyTorch `1.5` + torchvision `0.6`
* Detectron2 `0.1.3`

To build, you need to run the following on a machine with GPU and `nvidia-docker2`:
```
docker build -t ohjho/py37_cuda:[version tag] -f Dockerfile-detectron2official .
```

to check which version of Detectron2 you are using:
```
python -m detectron2.utils.collect_env
```
Demo:
```
docker run -it --gpus all --rm ohjho/py37_cuda:10.1-torch1.5-detectron0.1.3
>  python -m detectron2.utils.collect_env
```
