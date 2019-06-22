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

### 3. [MAC Install MacPorts Error](https://www.macports.org/install.php)
Error when agree to Xcode license in Terminal: `$ sudo xcodebuild -license`

```xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance```
```

Change path under Xcode path

```$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer/
```
And agree to Xcode license again.

[back](./)
