QEMU AArch Triple Fault handler hack
====================================

It's pretty easy to put qemu in an endless exception loop, for that it's enough to set up VBAR incorrectly. Normally
this doesn't bother anybody, but if you add "-d int" then it becames pretty annoying, flooding your terminal or creating
hundreds of megabytes of log files in no time (and growing).

This dirty hack detects such exception loops and quits qemu when you use "-d int". I do not expect this to get
into the mainline, because this is only useful for bare metal developers making mistakes in their early development
stage.

Usage
-----

1. download latest [qemu source](https://github.com/qemu/qemu)
2. overwrite files from this repo (or if you prefer patches, the [diff is here](https://github.com/bztsrc/qemu-aarch-triple-fault/tree/patches))
3. compile qemu

```sh
./configure --target-list=aarch64-softmmu --enable-modules --enable-tcg-interpreter --enable-debug-tcg
make -j4
```

4. install qemu

```sh
sudo make install
```

Enjoy!

bzt
