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
lstopo -v

![results](http://davidjyoung.com/cmg/i77700.lstopov.png)
## rocm mnist_deep.py Ubuntu 20.04 Rocm Container Tensorflow v 1.15
```login as: david
     +--------------------------------------------------------------------+
     ¦                        • MobaXterm 11.1 •                          ¦
     ¦            (SSH client, X-server and networking tools)             ¦
     ¦                                                                    ¦
     ¦ ? SSH session to david@10.207.55.113                               ¦
     ¦   • SSH compression : ?                                            ¦
     ¦   • SSH-browser     : ?                                            ¦
     ¦   • X11-forwarding  : ?  (remote display is forwarded through SSH) ¦
     ¦   • DISPLAY         : ?  (automatically set on remote server)      ¦
     ¦                                                                    ¦
     ¦ ? For more info, ctrl+click on help or visit our website           ¦
     +--------------------------------------------------------------------+

Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-96-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue 08 Feb 2022 04:34:47 PM UTC
.
.
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
.
.
2022-02-08 16:37:14.423327: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1650] Found device 0 with properties:
name: Fiji [Radeon R9 FURY / NANO Series]
AMDGPU ISA: gfx803
memoryClockRate (GHz) 1
pciBusID 0000:09:00.0
.
.
step 0, training accuracy 0.1
step 100, training accuracy 0.8
step 200, training accuracy 0.88
step 300, training accuracy 0.86
step 400, training accuracy 0.96
step 500, training accuracy 0.98
step 600, training accuracy 0.98
step 700, training accuracy 0.98
step 800, training accuracy 0.98
step 900, training accuracy 0.92
step 1000, training accuracy 0.98
step 1100, training accuracy 0.98
step 1200, training accuracy 0.94
step 1300, training accuracy 0.98
step 1400, training accuracy 1
step 1500, training accuracy 0.98
step 1600, training accuracy 1
step 1700, training accuracy 0.96
step 1800, training accuracy 0.98
step 1900, training accuracy 0.98
inference accuracy 0.971857
train iterations/second 60.5294
inference images/second 28680.6
root@ryzen:/dockerx/mnist_deep_instrumented# 
```
Environment
```
root@ryzen:/dockerx/mnist_deep_instrumented# pip list
Package              Version
-------------------- ----------------------
absl-py              0.9.0
astor                0.8.1
attrs                19.3.0
backcall             0.1.0
bleach               3.1.0
chardet              2.3.0
decorator            4.4.1
defusedxml           0.6.0
entrypoints          0.3
enum34               1.1.6
gast                 0.2.2
google-pasta         0.1.8
grpcio               1.26.0
h5py                 2.10.0
importlib-metadata   1.3.0
ipykernel            5.1.3
ipython              7.9.0
ipython-genutils     0.2.0
ipywidgets           7.5.1
jedi                 0.15.1
Jinja2               2.10.3
jsonschema           3.2.0
jupyter              1.0.0
jupyter-client       5.3.4
jupyter-console      6.0.0
jupyter-core         4.6.1
Keras-Applications   1.0.8
Keras-Preprocessing  1.1.0
Markdown             3.1.1
MarkupSafe           1.1.1
mistune              0.8.4
mock                 3.0.5
more-itertools       8.0.2
nbconvert            5.6.1
nbformat             4.4.0
notebook             6.0.2
numpy                1.17.4
opt-einsum           3.1.0
pandocfilters        1.4.2
parso                0.5.2
pexpect              4.7.0
pickleshare          0.7.5
pip                  19.3.1
prometheus-client    0.7.1
prompt-toolkit       2.0.10
protobuf             3.11.1
ptyprocess           0.6.0
pycurl               7.43.0
Pygments             2.5.2
pygobject            3.20.0
pyrsistent           0.15.6
python-apt           1.1.0b1+ubuntu0.16.4.5
python-dateutil      2.8.1
pyzmq                18.1.1
qtconsole            4.6.0
requests             2.9.1
Send2Trash           1.5.0
setuptools           42.0.2
six                  1.13.0
ssh-import-id        5.5
tensorboard          1.15.0
tensorflow           1.15.0
tensorflow-estimator 1.15.1
termcolor            1.1.0
terminado            0.8.3
testpath             0.4.4
tornado              6.0.3
traitlets            4.3.3
unattended-upgrades  0.1
urllib3              1.13.1
wcwidth              0.1.7
webencodings         0.5.1
Werkzeug             0.16.0
wheel                0.29.0
widgetsnbextension   3.5.1
wrapt                1.11.2
zipp                 0.6.0
WARNING: You are using pip version 19.3.1; however, version 20.3.4 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
root@ryzen:/dockerx/mnist_deep_instrumented# lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                16
On-line CPU(s) list:   0-15
Thread(s) per core:    2
Core(s) per socket:    8
Socket(s):             1
NUMA node(s):          1
Vendor ID:             AuthenticAMD
CPU family:            23
Model:                 1
Model name:            AMD Ryzen 7 1700 Eight-Core Processor
Stepping:              1
CPU MHz:               1374.465
CPU max MHz:           3000.0000
CPU min MHz:           1550.0000
BogoMIPS:              5988.44
Virtualization:        AMD-V
L1d cache:             32K
L1i cache:             64K
L2 cache:              512K
L3 cache:              8192K
NUMA node0 CPU(s):     0-15
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx                              mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc cpuid extd_apicid aperfmperf pni pclmulqdq monitor ssse3 fma c                             x16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch                              osvw skinit wdt tce topoext perfctr_core perfctr_nb bpext perfctr_llc mwaitx cpb hw_pstate sme ssbd sev vmmcall fsgsbase bmi1 avx2 smep                              bmi2 rdseed adx smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves clzero irperf xsaveerptr arat npt lbrv svm_lock nrip_save tsc_sc                             ale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold avic v_vmsave_vmload vgif overflow_recov succor smca
root@ryzen:/dockerx/mnist_deep_instrumented# python3 mnist_deep.py
```
lstopo -v

![results](http://davidjyoung.com/cmg/ryzen.lstopov.png)
## cuda main.py Ubuntu 20.04 Nvidia Container Pytorch
Nvidia Container
Test Script
![results](http://davidjyoung.com/cmg/pytorch.png)
Environment
```
root@8a3ea7f3c85d:/dockerx/mnist_deep_instrumented# pip list
Package                       Version            
----------------------------- -------------------
absl-py                       0.8.1              
alabaster                     0.7.12             
apex                          0.1                
appdirs                       1.4.3              
ascii-graph                   1.5.1              
asn1crypto                    1.2.0              
atomicwrites                  1.3.0              
attrs                         19.3.0             
audioread                     2.1.8              
Babel                         2.7.0              
backcall                      0.1.0              
beautifulsoup4                4.8.1              
bleach                        3.1.0              
boto3                         1.10.16            
botocore                      1.13.16            
cachetools                    3.1.1              
certifi                       2019.9.11          
cffi                          1.13.1             
chardet                       3.0.4              
Click                         7.0                
codecov                       2.0.15             
conda                         4.7.12             
conda-build                   3.18.11            
conda-package-handling        1.6.0              
coverage                      4.5.4              
cryptography                  2.8                
cxxfilt                       0.2.0              
cycler                        0.10.0             
cymem                         2.0.2              
Cython                        0.28.4             
cytoolz                       0.9.0.1            
DataProperty                  0.43.1             
decorator                     4.4.1              
defusedxml                    0.6.0              
dill                          0.2.9              
docutils                      0.15.2             
entrypoints                   0.3                
filelock                      3.0.12             
flake8                        3.7.9              
Flask                         1.1.1              
future                        0.18.2             
glob2                         0.7                
google-auth                   1.7.0              
google-auth-oauthlib          0.4.1              
grpcio                        1.25.0             
h5py                          2.10.0             
html2text                     2019.9.26          
hypothesis                    4.44.0             
idna                          2.8                
imageio                       2.6.1              
imagesize                     1.1.0              
importlib-metadata            0.23               
inflect                       3.0.2              
ipdb                          0.12.2             
ipykernel                     5.1.3              
ipython                       7.9.0              
ipython-genutils              0.2.0              
itsdangerous                  1.1.0              
jedi                          0.15.1             
Jinja2                        2.10.3             
jmespath                      0.9.4              
joblib                        0.14.0             
json5                         0.8.5              
jsonschema                    3.1.1              
jupyter-client                5.3.4              
jupyter-core                  4.6.1              
jupyter-tensorboard           0.1.10             
jupyterlab                    1.0.4              
jupyterlab-server             1.0.6              
jupytext                      1.2.4              
kiwisolver                    1.1.0              
libarchive-c                  2.8                
librosa                       0.6.3              
lief                          0.9.0              
llvmlite                      0.28.0             
lmdb                          0.98               
Mako                          1.1.0              
Markdown                      3.1.1              
MarkupSafe                    1.1.1              
maskrcnn-benchmark            0.1                
matplotlib                    3.1.1              
mbstrdecoder                  0.8.1              
mccabe                        0.6.1              
mistune                       0.8.4              
mlperf-compliance             0.0.10             
mock                          3.0.5              
more-itertools                7.2.0              
msgfy                         0.0.7              
msgpack                       0.6.1              
msgpack-numpy                 0.4.3.2            
murmurhash                    1.0.2              
nbconvert                     5.6.1              
nbformat                      4.4.0              
networkx                      2.0                
nltk                          3.4.5              
notebook                      6.0.2              
numba                         0.43.1             
numpy                         1.17.3             
nvidia-dali                   0.15.0             
oauthlib                      3.1.0              
onnx                          1.6.0              
opencv-python                 3.4.1.15           
packaging                     19.2               
pandas                        0.24.2             
pandocfilters                 1.4.2              
parso                         0.5.1              
pathvalidate                  0.29.0             
pexpect                       4.7.0              
pickleshare                   0.7.5              
Pillow-SIMD                   5.3.0.post1        
pip                           18.0               
pkginfo                       1.5.0.1            
plac                          0.9.6              
pluggy                        0.13.0             
preshed                       2.0.1              
progressbar                   2.5                
prometheus-client             0.7.1              
prompt-toolkit                2.0.10             
protobuf                      3.10.0             
psutil                        5.6.3              
ptyprocess                    0.6.0              
py                            1.8.0              
pyasn1                        0.4.7              
pyasn1-modules                0.2.7              
pybind11                      2.4.3              
pycocotools                   2.0+nv0.3.1        
pycodestyle                   2.5.0              
pycosat                       0.6.3              
pycparser                     2.19               
pycuda                        2019.1.2           
pydot                         1.4.1              
pyflakes                      2.1.1              
Pygments                      2.4.2              
pyOpenSSL                     19.0.0             
pyparsing                     2.4.5              
pyrsistent                    0.15.5             
PySocks                       1.7.1              
pytablewriter                 0.46.1             
pytest                        5.2.2              
pytest-cov                    2.8.1              
pytest-pythonpath             0.7.3              
python-dateutil               2.8.0              
python-hostlist               1.18               
python-nvd3                   0.15.0             
python-slugify                4.0.0              
pytools                       2019.1.1           
pytorch-transformers          1.1.0              
pytz                          2019.3             
PyWavelets                    1.1.1              
PyYAML                        5.1.2              
pyzmq                         18.1.0             
regex                         2018.1.10          
requests                      2.22.0             
requests-oauthlib             1.3.0              
resampy                       0.2.2              
revtok                        0.0.3              
rsa                           4.0                
ruamel-yaml                   0.15.46            
s3transfer                    0.2.1              
sacrebleu                     1.2.10             
sacremoses                    0.0.35             
scikit-image                  0.15.0             
scikit-learn                  0.21.3             
scipy                         1.3.1              
Send2Trash                    1.5.0              
sentencepiece                 0.1.83             
setuptools                    41.6.0.post20191030
six                           1.12.0             
snowballstemmer               2.0.0              
SoundFile                     0.10.2             
soupsieve                     1.9.3              
sox                           1.3.7              
spacy                         2.0.16             
Sphinx                        2.2.1              
sphinx-rtd-theme              0.4.3              
sphinxcontrib-applehelp       1.0.1              
sphinxcontrib-devhelp         1.0.1              
sphinxcontrib-htmlhelp        1.0.2              
sphinxcontrib-jsmath          1.0.1              
sphinxcontrib-qthelp          1.0.2              
sphinxcontrib-serializinghtml 1.1.3              
SSD                           0.1                
subword-nmt                   0.3.3              
tabledata                     0.9.1              
tabulate                      0.8.5              
tensorboard                   2.0.1              
tensorrt                      6.0.1.8            
terminado                     0.8.2              
testpath                      0.4.4              
text-unidecode                1.3                
thinc                         6.12.1             
toml                          0.10.0             
toolz                         0.10.0             
torch                         1.4.0a0+649135b    
torchtext                     0.4.0              
torchvision                   0.5.0a0            
tornado                       6.0.3              
tqdm                          4.31.1             
traitlets                     4.3.3              
typepy                        0.6.0              
typing                        3.7.4.1            
typing-extensions             3.7.4.1            
ujson                         1.35               
Unidecode                     1.1.1              
urllib3                       1.24.2             
wcwidth                       0.1.7              
webencodings                  0.5.1              
Werkzeug                      0.16.0             
wheel                         0.33.6             
wrapt                         1.10.11            
yacs                          0.1.6              
zipp                          0.6.0              
root@8a3ea7f3c85d:/dockerx/mnist_deep_instrumented# lscpu
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              8
On-line CPU(s) list: 0-7
Thread(s) per core:  2
Core(s) per socket:  4
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               158
Model name:          Intel(R) Core(TM) i7-7700 CPU @ 3.60GHz
Stepping:            9
CPU MHz:             900.036
CPU max MHz:         3600.0000
CPU min MHz:         800.0000
BogoMIPS:            7200.00
Virtualization:      VT-x
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            8192K
NUMA node0 CPU(s):   0-7
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm arat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d
root@8a3ea7f3c85d:/dockerx/mnist_deep_instrumented# 
```
## cuda main.py Windows 10 Pytorch V 1.0/1.1
Please see extensive documentation plus video at https://github.com/pytorch/pytorch/issues/20969
