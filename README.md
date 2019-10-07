# linux-4.4.38-for-tiny4412
linux-4.4.38-for-tiny4412 made by FriendlyARM Corp.

- how to boot and flash the uboot
    
    * use the uboot modified by myself
    https://github.com/zczjx/uboot_tiny4412
    
    * do sign manually if you modify the uboot
    before flash it to gen bl2.bin
    cd sd_fuse/tiny4412
   ../mkbl2 ../../u-boot.bin bl2.bin 14336

    * follow this article to flash uboot.bin to emmc
    http://www.cnblogs.com/pengdonglin137/p/4161084.html

- how to build the linux-4.4.38-for-tiny4412 
    
    1. download the correct version of arm-linux-gcc
    I use arm-linux-gcc version 4.9.4 download from Linaro
    https://releases.linaro.org/components/toolchain/binaries/4.9-2017.01/arm-linux-gnueabi/
    
    2. cp tiny4412_linux_4_4_defconfig .config

    3. make LOADADDR=0x40008000 uImage

    4. make dtbs

- how to flash the linux kernel and dtb image

    - use uboot fastboot run fastboot in uboot

    - fastboot flash kernel-4-4 arch/arm/boot/uImage

    - fastboot flash dtb arch/arm/boot/dts/exynos4412-tiny4412.dtb

    - run reset in uboot

- set your user partition and flash your rootfs to your emmc

已经移植好的核心驱动:

 * RGB显示屏fimd驱动 s3c-fb.c (无DRM功能)
 * FIMC capture DVP摄像头采集驱动 exynos4-is/fimc-capture.c
 * FIMC m2m pixel coversion 像素格式硬件转换
 * ov5640自动聚焦摄像头sensor, ov5640.c
 * s5p-jpeg jpeg 硬件编解码驱动(encode连续编码开源驱动有bug, 应用代码做了workaround)
 * s5p-mfc codecs h264等相关视频格式硬件编解码驱动
已经移植好的非核心驱动:

 * spidev通用SPI驱动
 * i2cdev 通用I2C驱动
 * leds 点灯驱动
 * tiny4412_ts_backlight tiny4412_1wire 屏幕背光与亮度驱动(单总线协议接口)
 * hc-sr04 超声测距驱动
 * pwm-buzzer pwm蜂鸣器驱动
 * at24c08 eeprom驱动
 * ft5406 触屏驱动(i2c接口读写)
 * mma7660 g-sensor重力传感器驱动
 * nfc-mfrc522 rc522 NFC卡读卡器驱动
 * mshc_0 emmc/sd卡驱动
 * tmu 温度计thermal驱动
 * adc 模数转换驱动(使用hwmon框架)
 * watchdog驱动
 * rtc 驱动
 * usb4604 以太网卡复位驱动

 
