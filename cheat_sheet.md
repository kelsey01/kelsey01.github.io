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
| `$ ps -auxf <code>&#124</code> grep python`   | can get usage information of python      |
| `$ top -n 1 -i [-c -b]`      | can get usage information of CPU         |
| `$ sudo dmesg`               | check if it is out of memory             |

### GPU configuration

Use 30% of GPU
```python
gpu_options=tf.GPUOptions(per_process_gpu_memory_fraction=0.3)
config=tf.ConfigProto(gpu_options=gpu_options)
session =tf.Session(config=config)
```

### Git operation

* `Fork` the repository on github webpage
* Download the forked github repository to local drive
```
$ cd ~/your/local/path
$ git clone xxx
```
* Check edited content after editing in local drive
```
$ git status
```
* Push local changes to github webpages
  1. Add all changed files into git index
```
$ git add .
```
  2. Commit changed files in index
```
$ git commit -m "add notes for your changing"
```
  3. Push to the github webpage
```
$ git push origin master
```
* Sync or Pull github webpage content when `Error: Untracked working tree file ‘xxxxx’ would be overwritten by merge.` raises
```
$ git fetch --all
$ git reset --hard origin/master
```


[back](./)
