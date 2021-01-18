# ml-infra-tools
Tools for building ML environments &amp; infra


# prerequisites

- docker
- docker-composer
- Nvidia Driver
- [nvidia-docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/overview.html)


How to know docker, Nvidia Driver, Nvidia Docker have been installed correctly

```
docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
```

The output will be somethings like

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.80.02    Driver Version: 450.80.02    CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  Off  | 00000000:01:00.0  On |                  N/A |
| 43%   57C    P0    71W / 250W |   3291MiB / 11175MiB |      5%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
+-----------------------------------------------------------------------------+



```

## Configure docker-composer runtime

Update runtime for nvidia-docker

```
$ cat /etc/docker/daemon.json
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}


```


# How to run

The docker images has Jupyter Lab inside, when you start docker image the Jupyter will automatically launch, and bind to `8889` port on your computer.

Happy Coding!!!

(PyTorch)
```
$ cd dockerfiles
$ docker-compose -f docker-compose.yml -f dev-gpu.yml up --build
```

(Tensorflow)
```bash
docker-compose -f docker-compose-tf.yml -f up --build
```




## Test GPU inside

- Open `localhost:8889`
- Open `Test.ipynb`
- Run the first code block

    ```python
    import torch
    torch.cuda.current_device()

    ```
