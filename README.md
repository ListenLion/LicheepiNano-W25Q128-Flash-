板子是Licheepi Nano W25Q128 Flash
PC：Ubuntu18

testlicheepi文件夹：
此文件夹下涉及的各个文件：
/rt-thread/*
此文件是http://nano.lichee.pro/get_started/first_eat.html
链接的中初次体验中下载的源码
按着上述的步骤其中出现一个问题是没有找到编译器的文件夹，将报错的rtconfig.py中报错的内容换成系统中
arm-none-eabi-gcc version 6.3.1
上述链接器是PC机自带的找到，将文件地址复制到出错的部位即可。

/xboot/*
此文件也是按着即食步骤即可成功运行
/assert_method/*
此文件是官方给出的uboot文件编译过程中在下载后因为需要验证错误，将源码放入
/linux/*
此文件夹内按着http://nano.lichee.pro/build_sys/kernel.html编译的
make ARCH=arm menuconfig
出现的配置选项：
https://whycan.cn/t_3010.html和https://whycan.cn/t_2179.html
和上述两个链接进行对比进行配置
/Nano_flash_800480/*
此文件夹下的内容是晕哥的做出的链接：暂时找不到链接～之后补上：
/buildroot-2017.08/*
此文件夹内是官网给出的编译根文件系统的文件
其中里面自己编出来的验证过程中是错误的。

/overlay
/rootfs_new
/rootfs_new_new
上述三个文件夹是根据上述编译过程出来的产物，可以不用追究，不用使用。
/boot.cmd和/bootscr
此文件是按着即食链接
http://nano.lichee.pro/build_sys/bootargs.html做出的
/jffs2.img
此文件是错误的
/rootfs_new_new.img  /rootfs_new.img
此文件验证也是错误的


ls@LS-Y:~/testlicheepi$ sudo sunxi-fel -p spiflash-write 0 u-boot/u-boot-sunxi-with-spl.bin 
100% [================================================]   352 kB,  103.4 kB/s 
ls@LS-Y:~/testlicheepi$ sudo sunxi-fel -p spiflash-write 0x60000 linux/arch/arm/boot/dts/suniv-f1c100s-licheepi-nano.dtb
100% [================================================]     8 kB,   97.1 kB/s 
ls@LS-Y:~/testlicheepi$ sudo sunxi-fel -p spiflash-write 0x64000 linux/arch/arm/boot/zImage 
100% [================================================]  3852 kB,  106.1 kB/s 
ls@LS-Y:~/testlicheepi$ sudo sunxi-fel -p spiflash-write 0x464000 Nano_flash_800480/jffs2.bin 
100% [================================================] 11469 kB,  108.6 kB/s
使用的是上述四个下载命令下载

