cmake_minimum_required(VERSION 3.12)

include(pico_sdk_import.cmake)

set(FREERTOS_KERNEL_PATH ${CMAKE_CURRENT_LIST_DIR}/freertos)
include(FreeRTOS_Kernel_import.cmake)

project(JTAGprobe)

pico_sdk_init()

add_executable(JTAGprobe

        src/DAP.c
        src/get_serial.c
        src/JTAG_DP.c
        src/SW_DP.c
        src/SWO.c
        src/DAP_vendor.c
        src/main.c
        src/usb_descriptors.c
        src/tusb_edpt_handler.c
        
     
)

target_sources(JTAGprobe PRIVATE
        
        #CMSIS_6/CMSIS/DAP/Firmware/Source/DAP_vendor.c
        #CMSIS_6/CMSIS/DAP/Firmware/Source/SWO.c
        #CMSIS_6/CMSIS/DAP/Firmware/Source/SW_DP.c
        )

target_include_directories(JTAGprobe PRIVATE

        CMSIS_6/CMSIS/Core/Include/
        CMSIS_6/CMSIS/RTOS2/Include/
        include/
        )

target_compile_options(JTAGprobe PRIVATE -Wall)

target_include_directories(JTAGprobe PRIVATE src)

target_compile_definitions (JTAGprobe PRIVATE
	PICO_RP2040_USB_DEVICE_ENUMERATION_FIX=1
)


target_link_libraries(JTAGprobe PRIVATE
        pico_multicore
        pico_stdlib
        pico_unique_id
        tinyusb_device
        tinyusb_board
        hardware_pio
        FreeRTOS-Kernel
        FreeRTOS-Kernel-Heap1
)

pico_set_binary_type(JTAGprobe copy_to_ram)

pico_add_extra_outputs(JTAGprobe)
