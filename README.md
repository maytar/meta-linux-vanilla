
Just a simple yocto layer to build vanilla linux kernel 3.8 for qemux86_64.

Built above:
```
poky (krogoth) - 73cc31c11a9d75a2f4204a9a8c6832c6e505a86a
```
krogoth was used cause it still includes recipes for gcc4.9 which is needed to build the kernel.

conf/local.conf relevant entries:
```
PREFERRED_PROVIDER_virtual/kernel = "linux-vanilla"
GCCVERSION ?= "4.9.%"
SDKGCCVERSION ?= "4.9.%"
``` 

Building and running:
```
bitbake core-image-minimal
runqemu qemux86-64 core-image-minimal slirp
```

----------------

The kernel's recipe is not so intereseting by itself, basically a copy of linux-yocto-custom.bb from poky. But, the process of getting the defconfig right - so the kernel would run smoothly with runqemu - was a bit of a painful process. Some relevant config entries that I had to change:
```
CONFIG_UEVENT_HELPER_PATH=""
CONFIG_DEVTMPFS=y
CONFIG_DEVTMPFS_MOUNT=y
CONFIG_LEGACY_PTYS=y
# CONFIG_SERIAL_8250_EXTENDED is not set
# CONFIG_AGP_AMD64 is not set 

```

If there is a simpler way to do things, I will gladly be told so :-)
