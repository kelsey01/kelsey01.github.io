---
layout: default
---

## Cheat Sheet

### Numpy

| function           | note                                               |
|:-------------------|:---------------------------------------------------|
| `np.newaxis`       | create a new axis `e.g. a = a[:,np.newaxis]`       |
| `numpy.c_[a, b]`   | translate two slice objects to one concatenation   |


### Command line

| function                     | note                                     |
|:-----------------------------|:-----------------------------------------|
| `$ ssh username@IP.address`  |login remote server                       |
| `$ nvidia-smi`               | can get NVIDIA GPU information           |
| `$ ps -auxf | grep python`   | can get usage information of python      |
| `$ top -n 1 -i [-c -b]`      | can get usage information of CPU         |
| `$ sudo dmesg`               | check if it is out of memory             |

### GPU configuration

Use 30% of GPU
```python
gpu_options=tf.GPUOptions(per_process_gpu_memory_fraction=0.3)
config=tf.ConfigProto(gpu_options=gpu_options)
session =tf.Session(config=config)
```

[back](./)
