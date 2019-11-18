# Nvidia official Docker runtime problem
Commend:
```
docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi
```

## GET ERROR:

/run/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/56ca0b73c5720021671123b7f44c885bb1e7b42957c9b18e7b509be26760b993/log.json: no such file or directory): nvidia-container-runtime did not terminate sucessfully: unknown

## SOLUTION
sudo apt-get install nvidia-container-runtime

## problem solved.
