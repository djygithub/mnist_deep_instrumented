# mnist_deep_instrumented
Classic mnist_deep.py with training iterations per second and inference images per second
One way to test is with an Nvidia Container
```
david@i77700:~/Desktop$ docker images
REPOSITORY                  TAG                                 IMAGE ID       CREATED          SIZE
nvcr.io/nvidia/tensorflow   19.11-tf1-py3-craydgemm-mnistdeep   ade00fe29af4   52 minutes ago   9.61GB
nvcr.io/nvidia/tensorflow   19.11-tf1-py3-craydgemm             7114ea73994c   3 hours ago      9.61GB
nvcr.io/nvidia/tensorflow   22.01-tf1-py3                       4388f8085466   2 weeks ago      15.1GB
nvidia/cuda                 10.2-base                           55c80b56bbcd   7 months ago     107MB
nvcr.io/nvidia/tensorflow   21.04-tf1-py3                       d9d4ebba583c   9 months ago     14GB
nvidia/cuda                 11.0-base                           2ec708416bb8   17 months ago    122MB
nvcr.io/nvidia/tensorflow   19.11-tf1-py3                       db057f79b565   2 years ago      8.6GB
david@i77700:~/Desktop$ docker run --gpus all -it --rm  nvcr.io/nvidia/tensorflow:19.11-tf1-py3-craydgemm-mnistdeep
                                                                                                                                                
================
== TensorFlow ==
================

NVIDIA Release 19.11-tf1 (build 8788896)
TensorFlow Version 1.15.0

Container image Copyright (c) 2019, NVIDIA CORPORATION.  All rights reserved.
Copyright 2017-2019 The TensorFlow Authors.  All rights reserved.

Various files include modifications (c) NVIDIA CORPORATION.  All rights reserved.
NVIDIA modifications are covered by the license terms that apply to the underlying project or file.

NOTE: MOFED driver for multi-node communication was not detected.
      Multi-node communication performance may be reduced.

NOTE: The SHMEM allocation limit is set to the default of 64MB.  This may be
   insufficient for TensorFlow.  NVIDIA recommends the use of the following flags:
   nvidia-docker run --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 ...

root@10c34477cc47:/workspace# 
```
