# JTAGprobe
A fork of opensource version of **debugprobe** built on RASPBERRY pico.It is extendedand  modified to work with JTAG and SWD. This does not use  FIFO and PIO functionality of **debugprobe** but uses  standard ARM CMSIS-DAP.

This supports both **JTAG & SWD** for debugging using OpenOCD, Hence the name **JTAGprobe**

This project supports the following boards:
- **Raspberry Pi Pico** (RP2040)
- **Raspberry Pi Pico 2** (RP2350)

___
The following is **GPIO pinout** for JTAG/SWD 


| GPIO       | Pinout  |
| --------   | ------- |
| SWCLK_TCK  | 19      |
| SWDIO_TMS  | 14      |
| TDI        | 18      |
| TDO        | 21      |
| nTRST      | 15      |
| nRESET     | 16      |

You can download **UF2** file or download entire code and build it as mentioned below.

# Images of debugging PICO with another PICO and Bluepill

![Bluepill Debug](images/bluepilldebug.jpg)

![Pico Debug](images/picodebug.jpg)



# Hacking

For the purpose of making changes or studying of the code, you may want to compile the code yourself.

First, clone the repository:
```
git clone https://github.com/dst202/JTAGprobe
cd JTAGprobe
```
Initialize and update the submodules:
```
git submodule update --init --recursive
```

## Building for Raspberry Pi Pico (RP2040)

Create and switch to the build directory for Pico:
```
mkdir build/pico
cd build/pico
```

If your environment doesn't contain `PICO_SDK_PATH`, then either add it to your environment variables with `export PICO_SDK_PATH=/path/to/sdk` or add `PICO_SDK_PATH=/path/to/sdk` to the arguments to CMake below.

Run cmake and build the code:
```
cmake ../.. -DPICO_BOARD=pico
make
```

Done! You should now have a `JTAGprobe.uf2` that you can upload to your JTAG Probe via the UF2 bootloader.

## Building for Raspberry Pi Pico 2 (RP2350)

Create and switch to the build directory for Pico 2:
```
mkdir build/pico2
cd build/pico2
```

If your environment doesn't contain `PICO_SDK_PATH`, then either add it to your environment variables with `export PICO_SDK_PATH=/path/to/sdk` or add `PICO_SDK_PATH=/path/to/sdk` to the arguments to CMake below.

Run cmake and build the code:
```
cmake ../.. -DPICO_BOARD=pico2
make
```

Done! You should now have a `JTAGprobe.uf2` that you can upload to your JTAG Probe via the UF2 bootloader.
