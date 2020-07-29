### Flashing Jetson TX2 Problems
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
