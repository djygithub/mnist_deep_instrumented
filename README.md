# mnist_deep_instrumented http://davidjyoung.com/cmg/nvidiagpuperf.pdf
Classic mnist_deep.py with training iterations per second and inference images per second.  Tensorflow (mnist_deep.py) and Pytorch (main.py) versions included.
## cuda mnist_deep.py Ubuntu 20.04 Nvidia Container Tensorflow v 1.15
One way to test is with an Nvidia Container.
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
![results](http://davidjyoung.com/cmg/mnist_deep2.png)
Environment
```
root@10c34477cc47:/workspace/github/djytf# pip list
Package                Version  
---------------------- ---------
absl-py                0.8.1    
astor                  0.8.0    
attrs                  19.3.0   
audioread              2.1.8    
backcall               0.1.0    
bleach                 3.1.0    
cloudpickle            1.2.2    
cupy                   6.5.0    
cycler                 0.10.0   
Cython                 0.29.14  
decorator              4.4.1    
defusedxml             0.6.0    
entrypoints            0.3      
fastrlock              0.4      
future                 0.17.1   
gast                   0.2.2    
google-pasta           0.1.8    
graphsurgeon           0.4.1    
grpcio                 1.25.0   
h5py                   2.9.0    
horovod                0.18.2   
importlib-metadata     0.23     
ipykernel              5.1.3    
ipython                7.9.0    
ipython-genutils       0.2.0    
jedi                   0.15.1   
Jinja2                 2.10.3   
joblib                 0.13.2   
json5                  0.8.5    
jsonschema             3.1.1    
jupyter-client         5.3.4    
jupyter-core           4.6.1    
jupyter-tensorboard    0.1.10   
jupyterlab             1.0.2    
jupyterlab-server      1.0.0    
jupytext               1.2.4    
Keras-Applications     1.0.8    
Keras-Preprocessing    1.0.5    
kiwisolver             1.1.0    
librosa                0.6.3    
llvmlite               0.29.0   
Markdown               3.1.1    
MarkupSafe             1.1.1    
matplotlib             3.1.1    
mistune                0.8.4    
mock                   3.0.5    
more-itertools         7.2.0    
mpi4py                 3.0.2    
nbconvert              5.6.1    
nbformat               4.4.0    
nltk                   3.2.5    
notebook               5.7.8    
numba                  0.44.1   
numpy                  1.17.4   
nvidia-dali            0.15.0   
nvidia-dali-tf-plugin  0.15.0   
opt-einsum             3.1.0    
pandas                 0.23.0   
pandocfilters          1.4.2    
parso                  0.5.1    
pexpect                4.7.0    
pickleshare            0.7.5    
Pillow                 5.4.1    
pip                    19.3.1   
portpicker             1.3.1    
prometheus-client      0.7.1    
prompt-toolkit         2.0.10   
protobuf               3.10.0   
psutil                 5.6.3    
ptyprocess             0.6.0    
pycocotools            2.0.0    
Pygments               2.4.2    
pyparsing              2.4.5    
pyrsistent             0.15.5   
python-dateutil        2.8.1    
python-speech-features 0.6      
pytz                   2019.3   
PyYAML                 5.1.2    
pyzmq                  18.1.0   
resampy                0.2.1    
sacrebleu              1.3.6    
scikit-learn           0.21.3   
scipy                  1.3.1    
Send2Trash             1.5.0    
sentencepiece          0.1.82   
setuptools             41.6.0   
six                    1.12.0   
tensorboard            1.15.0   
tensorflow-estimator   1.15.1   
tensorflow-gpu         1.15.0+nv
tensorrt               6.0.1.8  
termcolor              1.1.0    
terminado              0.8.2    
testpath               0.4.4    
tornado                6.0.3    
tqdm                   4.38.0   
traitlets              4.3.3    
typing                 3.7.4.1  
uff                    0.6.5    
wcwidth                0.1.7    
webencodings           0.5.1    
Werkzeug               0.16.0   
wheel                  0.33.6   
wrapt                  1.11.2   
zipp                   0.6.0    
WARNING: You are using pip version 19.3.1; however, version 21.3.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
root@10c34477cc47:/workspace/github/djytf# 
```
## rocm mnist_deep.py Ubuntu 20.04 Rocm Container Tensorflow v 1.15
```
david@ryzen:~$ alias drun='sudo docker run -it --network=host --device=/dev/kfd --device=/dev/dri --ipc=host --shm-size 16G --group-add video --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -v $HOME/dockerx:/dockerx'
david@ryzen:~$ drun djydockerhub/lammpsiccavx2:20200521
[sudo] password for david:
root@ryzen:/root# python3
Python 3.5.2 (default, Oct  8 2019, 13:06:37)
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> exit()
root@ryzen:/root#
```
Test Script
```
root@ryzen:/root# cd /
root@ryzen:/# cd dockerx/
root@ryzen:/dockerx# ll
total 12
drwxr-xr-x 3 root root 4096 Feb  8 16:27 ./
drwxr-xr-x 1 root root 4096 Feb  8 16:35 ../
drwxr-xr-x 3 root root 4096 Feb  8 16:27 mnist_deep_instrumented/
root@ryzen:/dockerx# cd mnist_deep_instrumented/
root@ryzen:/dockerx/mnist_deep_instrumented# ll
total 48
drwxr-xr-x 3 root root  4096 Feb  8 16:27 ./
drwxr-xr-x 3 root root  4096 Feb  8 16:27 ../
drwxr-xr-x 8 root root  4096 Feb  8 16:27 .git/
-rw-r--r-- 1 root root 10393 Feb  8 16:27 README.md
-rw-r--r-- 1 root root  5272 Feb  8 16:27 main.py
-rw-r--r-- 1 root root  7057 Feb  8 16:27 mnist_deep.py
-rw-r--r-- 1 root root  7252 Feb  8 16:27 mnist_deep.py.txt
root@ryzen:/dockerx/mnist_deep_instrumented# python3 mnist_deep.py
WARNING:tensorflow:From mnist_deep.py:191: The name tf.app.run is deprecated. Please use tf.compat.v1.app.run instead.

WARNING:tensorflow:From mnist_deep.py:135: read_data_sets (from tensorflow.contrib.learn.python.learn.datasets.mnist) is deprecated and                              will be removed in a future version.
Instructions for updating:
Please use alternatives such as official/mnist/dataset.py from tensorflow/models.
W0208 16:37:13.797948 140165174830848 deprecation.py:323] From mnist_deep.py:135: read_data_sets (from tensorflow.contrib.learn.python.                             learn.datasets.mnist) is deprecated and will be removed in a future version.
Instructions for updating:

```
## main.py Windows 10 Pytorch V 1.0/1.1
Please see extensive documentation plus video at https://github.com/pytorch/pytorch/issues/20969
