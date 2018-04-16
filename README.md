# mbed on STM32 notes

## Setup

### ARM toolchain

`sudo apt install binutils-arm-none-eabi gcc-arm-none-eabi gdb-arm-none-eabi libnewlib-arm-none-eabi`

### openocd

```sh
sudo npm i -g xpm
xpm install @gnu-mcu-eclipse/openocd --global

#install openocd rules
sudo ln -s ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/contrib/60-openocd.rules /etc/udev/rules.d/
sudo service udev restart

sudo ln -s ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/bin/openocd /usr/bin/openocd

# check install
openocd -v

# run server, see in ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts/board to match yours eg
# openocd -f ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts/board/<name>.cfg

openocd -f ~/opt/xPacks/@gnu-mcu-eclipse/openocd/0.10.0-7.1/.content/scripts/board/stm32429i_eval_stlink.cfg

```

### mbed CLI

```sh
sudo apt install mercurial # required to access mbed repos
pip install mbed-cli
mbed-cli
```

Setting defaults

```
mbed toolchain GCC_ARM
mbed config GCC_ARM_PATH /usr/bin
mbed target NUCLEO_F429ZI
```

Exporting to a vscode project

`mbed export -i vscode_gcc_arm`

See vscode setup for details on the configuration (mainly `launch.json`)

## Running

Start openocd in the repo directory (`-d` flag will provide more details)

`openocd -d1`

Receiving messages from serial printing

`screen /dev/ttyACM0 9600`

## Build

Debug build profile

`mbed compile --profile mbed-os/tools/profiles/debug.json`

## Links

- OpenOCD install https://gnu-mcu-eclipse.github.io/openocd/install/
- mbed export to vscode https://os.mbed.com/docs/v5.8/tutorials/visual-studio-code.html
- debug with printf https://docs.mbed.com/docs/mbed-os-handbook/en/latest/debugging/printf/
