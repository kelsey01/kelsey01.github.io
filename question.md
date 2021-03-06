---
layout: default
---

## Question Page
### 1. Spyder (Linux) fail to launch with Tensorflow CPU version
Install Spyder using:
```
$ conda install spyder
```
When launch Spyder, get the error
```
Qt: XKEYBOARD extension not present on the X server.
Could not initialize GLX
Aborted (core dumped)
```
Some people say installing `pyqt5` would fix it. But I got:
```
Traceback (most recent call last):
  File "/home/zqr/.conda/envs/zqrenv-cpu/bin/spyder", line 11, in <module>
    sys.exit(main())
  File "/home/zqr/.conda/envs/zqrenv-cpu/lib/python3.5/site-packages/spyder/app/start.py", line 190, in main
    from spyder.app import mainwindow
  File "/home/zqr/.conda/envs/zqrenv-cpu/lib/python3.5/site-packages/spyder/app/mainwindow.py", line 92, in <module>
    from qtpy import QtWebEngineWidgets  # analysis:ignore
  File "/home/zqr/.conda/envs/zqrenv-cpu/lib/python3.5/site-packages/qtpy/QtWebEngineWidgets.py", line 22, in <module>
    from PyQt5.QtWebEngineWidgets import QWebEnginePage
ValueError: PyCapsule_GetPointer called with incorrect name
```
Some people say installing `pyqt4` would fix the above problem. But I fail to install it using `$ pip install`.
Instead, `$ conda install "pyqt<5"` works.
And Spyder launches **successfully**.

### 2. Edward and tensorflow_probability package
#### 2.1 Edward and tensorflow_probability package compatibility
*  `Edward` requires `TensorFlow 1.6.0` (or maybe `<=1.6.0`)
*  `TensorFlow_probability` requires `TensorFlow >=1.13.1` (but `TensorFlow >=2.0` does not support it)

#### 2.2 Windows conda failed installing tensorflow-gpu==1.6.0
*  In conda env, use `pip install tensorflow==1.6.0`
*  `tensorflow 1.6.0` cannot be installed in the env. Import version is always the root version `tensorflow-gpu==1.9.0`
*  Even though `conda list` shows that `tensorflow 1.6.0` is there
*  Go to the default conda env path `C:\Users\user\Anaconda3\envs\env\Scripts`, tensorflow is not there
*  In cmd, change the directory into `C:\Users\user\Anaconda3\envs\env` uninstall and install using
```
C:\Users\user\Anaconda3\envs\env\Scripts\pip.exe uninstall tensorflow-gpu==1.9.0
C:\Users\user\Anaconda3\envs\env\Scripts\pip.exe install tensorflow-gpu==1.6.0
```
*  When uninstalling, `c:\users\user\appdata\roaming\..` packages are uninstalled.

### 3. [MAC Install MacPorts Error in Step 2](https://www.macports.org/install.php)
Error raised when agree to Xcode license in Terminal: `$ sudo xcodebuild -license`
```
xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
```
Change path under Xcode path
```
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer/
```
And agree to Xcode license again.

### 4. Install PCL for Ubuntu
* Try to install PCL for ubuntu according to this [link](https://github.com/udacity/SFND_Lidar_Obstacle_Detection). But got Error:
```
E: Unable to locate package libpcl-dev
```
as `libpcl-dev` does not support ubuntu 14.04

* Try to install ubuntu 16.04 on Parallels Desktop 10, but is not successfully installed on PD as it got stuck on the login screen. The reason may be the same as [it](https://blog.csdn.net/a545905403/article/details/79174718) says that PD10 fails to support ubuntu kernel linux-image-4.4.0. It is said that by changing the kernel to a lower version, ubuntu can be boosted successfully. There are many kernel changing or degrade methods. I choose to stick with ubuntu 14.04.

* Based on this [link](https://blog.csdn.net/mush_room/article/details/78339578), here is the pcl-1.8.1 release installation on ubuntu 14.04 (on virtual machine PD10).

  1. `$ sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl`
  2. `$ sudo apt-get update`
  3. `$ sudo apt-get install libpcl-all`
  4. `$ sudo apt-get cmake`
  5. Download pcl-1.8.1 from <https://github.com/PointCloudLibrary/pcl/releases>
  6. decompress pcl-pcl-1.8.1.tar `$ tar -xvf pcl-pcl-1.8.1.tar`
  7. Install pcl `$ cd pcl-pcl-1.8.1 && mkdir build && cd build`
  8. `$ cmake -DCMAKE_BUILD_TYPE=Release ..`
  9. `$ make -j2`
    There is error raised `c++: internal compiler error: Killed (program cc1plus)`. Check with this [link](https://stackoverflow.com/questions/30887143/make-j-8-g-internal-compiler-error-killed-program-cc1plus). I increase ubuntu memory on PD10 to 4G.
  10. `$ sudo make -j2 install` done.



### 5. `$ apt install` unavailable
```
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
```
  * First check which process is using apt: `$ ps -A | grep apt`
  * Then kill the process: `$ kill -9 The_process_id`

### 6. After installing some packages, cudnn suddenly failed on previously successfully built code:
```
could not create cudnn handle: CUDNN_STATUS_ALLOC_FAILED
```
  * add the following code solved:
```
config = tf.ConfigProto()
config.gpu_options.allow_growth = True
sess = tf.Session(config=config)
```
[back](./)
