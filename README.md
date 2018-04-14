# mbed on STM32 notes

## Setup

### ARM toolchain 

`sudo apt install binutils-arm-none-eabi gcc-arm-none-eabi gdb-arm-none-eabi libnewlib-arm-none-eabi`

### openocd 

```sh
sudo npm i -g xpm
xpm install @gnu-mcu-eclipse/openocd --global
# check install
~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/bin/openocd -v
# run server, see in ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts/board to match yours eg
# cd ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts && ../bin/openocd -f board/<name>.cfg

# if error LIBUSB_ACCESS_ERROR happens run below command and restart
sudo usermod -aG plugdev $USER

mkdir -p ~/bin
echo "cd ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts && ../bin/openocd -f board/stm32429i_eval_stlink.cfg" > ~/bin/openocd
chmod u+x ~/bin/openocd
```

### mbed CLI

```sh
pip install mbed-cli
# pip show mbed-cli
mkdir -p ~/bin
echo "python ~/.local/lib/python2.7/site-packages/mbed/mbed.py \$@" > ~/bin/mbed
chmod u+x ~/bin/mbed
```

Setting defaults

```
mbed toolchain GCC_ARM
mbed config GCC_ARM_PATH /usr/bin
mbed target NUCLEO_F429ZI
```

## Build

Debug build profile

```
mbed compile --profile mbed-os/tools/profiles/debug.json
```

