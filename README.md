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
Test script
```
root@10c34477cc47:/workspace/github/djytf# python3 mnist_deep.py 
2022-02-02 16:33:24.972224: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcudart.so.10.2
WARNING:tensorflow:From mnist_deep.py:191: The name tf.app.run is deprecated. Please use tf.compat.v1.app.run instead.

WARNING:tensorflow:From mnist_deep.py:135: read_data_sets (from tensorflow.contrib.learn.python.learn.datasets.mnist) is deprecated and will be removed in a future version.
Instructions for updating:
Please use alternatives such as official/mnist/dataset.py from tensorflow/models.
.
.
.
2022-02-02 16:33:27.531204: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1618] Found device 0 with properties: 
name: GeForce GTX 1050 major: 6 minor: 1 memoryClockRate(GHz): 1.455
pciBusID: 0000:01:00.0
.
.
.
step 0, training accuracy 0.08
step 100, training accuracy 0.86
step 200, training accuracy 0.94
step 300, training accuracy 0.96
step 400, training accuracy 0.94
step 500, training accuracy 0.98
step 600, training accuracy 0.92
step 700, training accuracy 0.98
step 800, training accuracy 0.94
step 900, training accuracy 0.9
step 1000, training accuracy 0.98
step 1100, training accuracy 0.94
step 1200, training accuracy 0.96
step 1300, training accuracy 0.96
step 1400, training accuracy 0.98
step 1500, training accuracy 0.94
step 1600, training accuracy 0.98
step 1700, training accuracy 0.98
step 1800, training accuracy 0.94
step 1900, training accuracy 0.94
2022-02-02 16:33:43.871927: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 16.00MiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:43.871967: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 539.38MiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:43.871987: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 1.83GiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:43.872006: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 974.90MiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:43.872019: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 2.34GiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:44.208351: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 3.65GiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:44.208391: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 2.75GiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
2022-02-02 16:33:44.208410: W tensorflow/core/common_runtime/bfc_allocator.cc:239] Allocator (GPU_0_bfc) ran out of memory trying to allocate 1.71GiB with freed_by_count=0. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
inference accuracy 0.972714
train iterations/second 121.037
inference images/second 13503.5

```
