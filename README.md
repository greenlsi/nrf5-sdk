# nrf5-sdk
Nordic nRF5 SDK 

This is the SDK from Nordic Semiconductors which can be obtained [here](https://www.nordicsemi.com/Products/Development-software/nrf5-sdk)

The prerequisites for using this SDK are:
- A toolchain (we use GCC 10.3 downloaded [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads))
- The nrf command line tools to flash and debug (https://www.nordicsemi.com/Products/Development-tools/nrf-command-line-tools/download)
- The JLink debugger programs (https://www.segger.com/downloads/jlink)

The file nrf.rc sets the enviromental variabled NRF_GCC and NRF_SDK with the path for this two. The variables are used by the vscode configuration files.
In Mac and Linux based distros, source nrf.rc should be executed before starting VS Code from command line

We propose using Visual Studio Code for programming and debugging the nRF. The extensions required are:
- C/C++ (by Microsoft)
- Cortex-Debug (by Marus25)

In the folder examples, there are multiple examples of projects. We have configured two of them for Visual Studio Code:
- peripheral/blinky_freertos: Project with no Soft Device (blank)
- ble_peripheral/ble_app_blinky: Project using BLE with Soft Device s140 (s140)

The configuration is stored in the folder .vscode. There are three files:
- c_cpp_properties.json: configuration of C for the Interpreter that checks syntax and suggests auto-completion
- tasks.json: tasks related to build, clean, and other targets of the Makefile. With Ctrl+B we execute the default build task (make). In the Menu Terminal->Run task we see all the defined tasks
- launch.json: debug configurations

For a new project:
- Modify sdk_config.h to declare the variables that configure the peripherals and libraries to used
- Modify Makefile to include in SRC_FILES the files needed, in INC_FOLDERS the paths where the .h files are, and in CFLAGS the defines required
- Copy the .vscode folder of one of the examples, considering if BLE is being used (s140) or not (blank)
- Modify c_cpp_properties so it includes the defines included in the CFLAGS variable of the Makefile of the project (CFLAGS += -DXXX adds a new line XXX)
