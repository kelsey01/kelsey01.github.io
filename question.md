---
layout: default
---

## Question Page
### Tensorflow CPU version
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
Instead, '$ conda install `"pyqt<5"` works.
And Spyder launches **successfully**.

[back](./)
