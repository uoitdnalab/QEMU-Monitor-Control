# QEMU-Monitor-Control

Allows a developer to automate mouse and keyboard events as well as take screenshots of a running QEMU virtual machine

Starting the QEMU VM
--------------------

To start a QEMU VM such that it can be controlled by this program, add
the argument `-monitor pty` to the command line invocation. For example:
```
kvm -hda ubuntu_hdd.qcow2 -boot c -m 4096 -monitor pty
```

Make note of the PTY file. For example:
```
char device redirected to /dev/pts/12 (label compat_monitor0)
```

Using the module
----------------

The following example assumes that QEMU selected the file `/dev/pts/12`
for QEMU Monitor use. Please adjust this parameter appropriately.

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import time
from QEMU_MouseKey import QEMU_MouseKey

PTY_FILE = '/dev/pts/12'

qm = QEMU_MouseKey(PTY_FILE)
time.sleep(1)
qm.mouse_set_index(3)
time.sleep(1)
qm.mouse_move_abs(20, 40)
time.sleep(1)
qm.left_single_click()

time.sleep(10)

qm.take_screenshot("/tmp/screenshot_from_qemu")

qm.close_pty()


```
