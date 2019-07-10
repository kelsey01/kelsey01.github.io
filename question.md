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

### 2. Edward and tensorflow_probability package compatibility
*  `Edward` requires `TensorFlow 1.6.0` (or maybe `<=1.6.0`)
*  `TensorFlow_probability` requires `TensorFlow >=1.13.1` (but `TensorFlow >=2.0` does not support it)

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

### 5. Flashing Jetson TX2
There are two main purposes for using host PC to flash Jetson TX2. 1) Flash OS 2) Install Packages (eg. CUDA, tensorRT, cuDNN, etc.). When you see this on the host PC and Jetson TX2 reboot successfully, it means flashing OS is done. Afterwards, if anything goes wrong, it goes wrong for installing packages instead of OS. There are some problems I ran into.

![flashing successfully](/assets/img/jetson/flashing_done.JPG)

  a. Got stuck right after flashing OS as shows in the following image `Connection to IP_ADDRESS closed`. The JetPack is not installed on either `/` or `home` on host PC ubuntu 16.04 due to limited space but on the other booting system windows 7. Change to a new host PC with JetPack installed on `home`.

![not enough memory](/assets/img/jetson/not_enough_memory.JPG)

  b. Got stuck on getting files from the network `0% [Working]` as shows in the following image. It is probably due to network connection failure for the board (although the host PC network is working and it is connected to the board with a router and an ethernet cable). I use university network and it requires webpage login. So make sure your board is webpage login and connected to the network.  

![network problem](/assets/img/jetson/network_problem.JPG)

  c. CUDA installation failed `Error: CUDA cannot be installed on device` as shows in the following image. Tried installing packages twice, but all failed. So I installed the mentioned `cuda-toolkit-9-0`, `libgomp1`, `libfreeimage-dev`, `libopenmpi-dev`, and `openmpi-bin` packages manually on the board. It will pop up error that some dependency requirement is not met and a suggestion to run `$ sudo apt-get -f install`. This command will fix the dependency requirement problem. Afterwards, run `$ sudo apt-get install xxx` to install the above packages.

![CUDA installation failed](/assets/img/jetson/cuda_fail.JPG)

The package installation process may go and forth several times. But you don't need to flash OS every time. Once the flashing OS is done successfully, when installing packages, choose `no action` for the ones inside the red box as shows in the following image.

![only install packages](/assets/img/jetson/flashing.png)[image courtesy](https://blog.csdn.net/Code_Mart/article/details/82153931)

[back](./)
