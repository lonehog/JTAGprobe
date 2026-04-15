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

## Prerequisites

Before building, ensure you have the following installed:

- **Raspberry Pi Pico SDK** - Set `PICO_SDK_PATH` environment variable
  ```bash
  export PICO_SDK_PATH=/path/to/pico-sdk
  ```
- **CMake** (3.12 or higher)
- **GCC ARM Embedded Toolchain**

## Building

### Option 1: Build for Raspberry Pi Pico (RP2040)

```bash
mkdir -p build/pico && cd build/pico
cmake ../.. -DPICO_BOARD=pico
make
```

The output will be `build/pico/JTAGprobe.uf2`

### Option 2: Build for Raspberry Pi Pico 2 (RP2350)

```bash
mkdir -p build/pico2 && cd build/pico2
cmake ../.. -DPICO_BOARD=pico2
make
```

The output will be `build/pico2/JTAGprobe.uf2`

## Flashing the Firmware

1. **Hold the BOOTSEL button** on your Pico/Pico2
2. **Connect to USB** while holding BOOTSEL (the device will appear as RPI-RP2 drive)
3. **Copy the appropriate `.uf2` file** to the drive:
   - For Pico (RP2040): `build/pico/JTAGprobe.uf2`
   - For Pico 2 (RP2350): `build/pico2/JTAGprobe.uf2`
4. The device will automatically reboot and run the firmware
