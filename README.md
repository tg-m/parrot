Parrot Linux device driver sample
=================================

This is a GPLv2+ sample implementation of a character device driver
for Linux 2.6 and later, based on [udev](https://en.wikipedia.org/wiki/Udev).

For more background information as well as a detailed source walkthrough, see
the following [blog post](http://pete.akeo.ie/2011/08/writing-linux-device-driver-for-kernels.html).

Requirements
------------

* gcc
* A recent Linux kernel (with its source)

Compilation
-----------

* Just invoke `make` as root

Testing
-------

* `insmod parrot_driver.ko debug=1`
* `lsmod | grep parrot`
* `echo "Yabba Dabba Doo" > /sys/devices/virtual/parrot/parrot_device/fifo`
* `cat /dev/parrot_device`

Notes
-----

On a Debian system, and if you haven't recompiled a kernel before, you may
have to issue the following before you can compile and run the driver:
```
cd /usr/src
apt-get install linux-headers
uname -r	# Get the version of your kernel, e.g. '3.16.0-4-amd64'
apt-get install linux-source-3.16	# Use the same major.minor as above
tar -xJvf linux-source-3.16.tar.xz
ln -s linux-source-3.16 linux
cd /usr/src/linux
cp /usr/src/linux-headers-$(uname -r)/Module.symvers .
make oldconfig && make prepare && make scripts
```
