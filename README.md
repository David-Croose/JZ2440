## 1    What's this?

It is a SDK of JZ2440(a develoment board base on Samsung ARM920 SOC), including uboot, linux and buildroot.



## 2    How to use?

### 2.1    compile the rootfs and toolchain

It is suggested to download the "dl" files from this site to save your time:

[https://pan.baidu.com/s/1mpN6zI-JO7IZXLhk7G3gXA](https://pan.baidu.com/s/1mpN6zI-JO7IZXLhk7G3gXA)

```
$ mkdir buildroot/dl
$ tar -xf buildroot_20180802_dl.tar.bz2 -C buildroot/dl
```

now starting compile:

```
$ cd buildroot
$ make ARCH=arm jz2440_defconfig
```

add toolchain to your PATH, this is sufficient for compiling uboot and linux in the latter:

```
$ vim /etc/porfile
	export PATH=$PATH:/path/to/your/buildroot/output/host/bin
$ . /etc/profile 	# or reopen the SSH tab
```



### 2.2    compile the uboot

```
$ cd uboot
$ make ARCH=arm jz2440_spl_defconfig
$ make ARCH=arm CROSS_COMPILE=arm-linux-
```



### 2.3    compile the linux

```
$ cd linux
$ make ARCH=arm qin2440_defconfig
$ make ARCH=arm CROSS_COMPILE=arm-linux- uImage
```



## 3    Running the board

Burning the `u-boot-with-spl.bin` to the address of 0x0 of nand flash. Booting the board from nand flash.

Start a TFTP server that host the `u-boot-with-spl.bin` file, and make sure your host computer and your board are in the same local network.

```
JZ2440 # setenv bootargs 'console=ttySAC0,115200n8'
JZ2440 # saveenv
JZ2440 # tftpboot uImage
JZ2440 # bootm
```



## 4    Ref resource

[https://github.com/David-Croose/bare2440.git](https://github.com/David-Croose/bare2440.git)
