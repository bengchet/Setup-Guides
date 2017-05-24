## How to Create Raspsberry Pi Image in Linux

* Prepare predefined Raspbian OS
  - Enable UART by adding following line in /boot/config.txt
    ```
      enable_uart=1
    ```
  - Enable SSH by adding file `ssh` in root directory of BOOT
  - Enable SPI, I2C, etc by removing # in /boot/config.txt
  - Enable auto expand file system by adding following line in /boot/cmdline.txt
    ```
      quiet init=/usr/lib/raspi-config/init_resize.sh
    ```
* Insert SD card with OS ready to PC
* Check the device name of SD card using `fdisk`, for example `/dev/mmcblk0/`

  ```
    $ sudo fdisk -l
  ```
* Unmount the Drive before start using dd tool
  
  ```
    $ sudo umount /dev/mmcblk0/
  ```
* Prepare image file

  ```
    $ dd if=/dev/mmcblk0 of=/path/to/myimage.img
  ```
* Install **gparted** tool

  ```
    $ sudo apt-get install gparted
  ```
* Mount image file and start gparted tool

  ```
    $ sudo modprobe loop
    $ sudo losetup -f
    $ sudo losetup /dev/loop0 myimage.img
    $ sudo partprobe /dev/loop0
    $ sudo gparted /dev/loop0
  ```

* Look for partition 2, adjust to appropriate size. If using Raspbian Jessie Lite, normally adjust to 2GB.
* After finish, run
  
  ```
    $ sudo losetup -d /dev/loop0
  ```
  Now the image file is successfully partitioned!
  
* Shaving the image file

  ```
    $ fdisk -l myimage.img
  ```

* Look where partition ends (the value shown under End), for example 9181183. 
  
  ```
    $ truncate --size=$[(9181183+1)*512] myimage.img
  ```
* Check the size to see if image is successfully shrinked in previous steps

* Convert to zip file (optional)
  
  ```
    $ zip myimage.zip myimage.img
  ```

## Reference

* [With gparted](https://softwarebakery.com/shrinking-images-on-linux)
* [Without gparted](https://www.howopensource.com/2016/03/resize-raspberry-sd-card-image/)
