# LAB 1: Microcontroller and its Development Environment

**OBJECTIVES**
- To setup and get you familiarised with the development environment for Raspberry Pi Pico.
- To get you familiarised with the Raspberry Pi Pico development board.

**EQUIPMENT** 
1.	A laptop that has the Pico C/C++ SDK installed
2.	Raspberry Pico or the wireless variant
3.	Micro-USB Cable 

> [NOTE]
> Only students wearing fully covered shoes are allowed in the lab due to safety. 

## **INTRODUCTION** 

Programming an embedded system requires a deep-level understanding of the embedded processor architecture, the development environment tool, and the hardware interfaced with the embedded system. In this laboratory session, you will be introduced to the basic tools and how they can be used to aid your understanding of software development and more importantly, to help you build your software. Programming for an embedded system differs greatly from programming on a desktop computer. The main differences are the limited resource constraints in terms of the program code and RAM and the overall computation performance of an embedded system. For instance, our RP2040 microcontroller only provides 256KB of SRAM memory space. A 16MB Flash memory is added to the board and externally connected to the RP2040. Moreover, the various software components discussed in the lecture will be observed in  this session. At this point, you should  be familiar with  the fundamentals of C programming. You are encouraged to brush up on it if you still need to. Do revise ALL the fundamentals of C programming covered in the following [site](https://www.cprogramming.com/tutorial/c-tutorial.html). This will prepare you for the subsequent lab sessions and make this subject more enjoyable. In addition, please brush up on the following:
- “Numeral Systems” (e.g. binary, decimal, hexadecimal, etc)
- “Ordering Consideration” (e.g. endianness, MSB, LSB, etc)

## **RASPBERRY PI PICO** 

In this lab session, we learned about the development platform Raspberry Pico and the Pico C/C++ SDK used throughout all lab sessions. We will also familiarise you with concepts like direct register access, polling, and serial communication. The following introduction should give a broad overview of the working environment, but it is optional to understand all the details to complete this laboratory. 

The Raspberry Pi Pico is an affordable microcontroller board developed by the Raspberry Pi Foundation, ideal for electronics projects. It features a dual-core ARM Cortex-M0+ processor, 26 GPIO pins, and supports multiple programming languages. However, it lacks built-in wireless connectivity. The Raspberry Pi Pico Wireless (Pico W) is an enhanced version of the Pico, with built-in Wi-Fi and Bluetooth. This makes it suitable for IoT and wireless communication projects while maintaining compatibility with Pico's programming languages and GPIO pins.

The Raspberry Pi Pico family currently consists of four boards: Raspberry Pi Pico, Pico H, Pico W, and Pico WH.

The following is the pin out for the Raspberry Pi Pico
![Screenshot of a Raspberry Pi Pico](https://www.raspberrypi.com/documentation/microcontrollers/images/pico-pinout.svg)

The following is the pin out for the Raspberry Pi Pico W
![Screenshot of a Raspberry Pi Pico W](https://www.raspberrypi.com/documentation/microcontrollers/images/picow-pinout.svg)

The most important documents of an embedded system are, among others, datasheets, user guides, technical reference manuals, application notes, errata or schematics. Therefore, every embedded system comes with many documentation files. All the necessary files for this lab and subsequent labs can be found on the Raspberry Foundation site and supplementary documents will be provided on the course xsite website. It is essential to have access to all parts of the documentation to use the functionality of an embedded system to its fullest extent. Details of the hardware can be found [here](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html).


## **GETTING STARTED WITH PICO W**

This section provides a step-by-step guide to setting up the development environment for Raspberry Pi Pico W, updating dependencies, configuring the Pico SDK, compiling, and running projects. Instructions are tailored for Windows, macOS, and Linux.

### Updating Dependencies

#### Linux
Run the following commands to install required dependencies:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install cmake gcc-arm-none-eabi build-essential libnewlib-arm-none-eabi git -y
```

#### macOS
Install the necessary tools using [Homebrew](https://brew.sh/):

```bash
brew update
brew install cmake arm-none-eabi-gcc git
```

#### Windows
1. Install [CMake](https://cmake.org/), [Git](https://git-scm.com/), and [Build Tools for Visual Studio](https://visualstudio.microsoft.com/visual-cpp-build-tools/).
2. Install `arm-none-eabi-gcc` using [ARM GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads).
3. Add the directories of these tools to your system's PATH variable:
   - **Control Panel > System > Advanced system settings > Environment Variables**.

### Setting Up the Pico SDK

#### All Platforms
1. **Clone the Pico SDK Repository**:
   ```bash
   git clone https://github.com/raspberrypi/pico-sdk.git
   cd pico-sdk
   git submodule update --init
   ```

2. **Set Up the Environment**:
   - **Linux/macOS**:
     Add the following line to your shell configuration file (`~/.bashrc` or `~/.zshrc`):

     ```bash
     export PICO_SDK_PATH=/path/to/pico-sdk
     ```

     Replace `/path/to/pico-sdk` with the actual path where the Pico SDK is cloned.

     Reload the shell configuration:

     ```bash
     source ~/.bashrc
     ```

   - **Windows**:
     Set the `PICO_SDK_PATH` as a system environment variable:
     1. Go to **Control Panel > System > Advanced system settings > Environment Variables**.
     2. Under "System variables," click **New**, and set:
        - **Variable name**: `PICO_SDK_PATH`
        - **Variable value**: `C:\path\to\pico-sdk`

     Replace `C:\path\to\pico-sdk` with the actual path to the Pico SDK directory.

### Compiling the Project via Terminal

1. **Navigate to the Project Directory**:
   ```bash
   cd INF2004_LAB1_reworked
   ```

2. **Create a Build Directory**:
   ```bash
   mkdir build
   cd build
   ```

3. **Generate Build Files with CMake**:
   - **Linux/macOS**:
     ```bash
     cmake ..
     ```
   - **Windows**:
     Ensure you're using the **Developer Command Prompt for Visual Studio** and run:
     ```cmd
     cmake -G "NMake Makefiles" ..
     ```

4. **Compile the Project**:
   - **Linux/macOS**:
     ```bash
     make
     ```
   - **Windows**:
     ```cmd
     nmake
     ```

   The compiled `.uf2` file will be located in the `build` directory.

## **DOWNLOADING FIRMWARE INTO THE PICO**

Depending on your preferences and requirements, several methods exist to upload firmware onto a Raspberry Pi Pico microcontroller board. Here is a brief overview of two of the most common methods:

1. **Drag and Drop (Mass Storage Device):**
   - The Raspberry Pi Pico has a built-in feature that makes it appear as a mass storage device when connected to a computer via USB.
   - To get the board in bootloader mode ready for the firmware update, hold down the BOOTSEL button while plugging the board into USB. You can only release the button once you connect the pico to the PC/laptop properly.
   - Drag and drop a UF2 file onto Pico's virtual drive to upload firmware using this method.
   - This is a beginner-friendly method and doesn't require any additional software.

3. **Using JTAG/SWD (For Advanced Users):**
   - Advanced users and developers may opt for JTAG/SWD debugging and programming tools to upload firmware.
   - This method offers greater control and debugging capabilities but requires additional hardware and expertise.
   - You may configure another pico as a SWD Debugger called PicoProbe. See [Appendix A](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf).
   - Here is a video of someone configuring and using the [PicoProbe](https://www.youtube.com/watch?v=0i2gLeBal9Y).

**In this lab, we will use method #1 (Drag and Drop).**

## **THE BIG PICTURE**
The figure below illustrates how the entire procedure works.
![Screenshot of Pico - Visual Studio Code](/img/overview.png)

## **TASK**

In this [basic code](basic.c) example, we embark on a journey to understand various types of operators in the C programming language. By executing this code, we gain insights into arithmetic, relational, logical, and bitwise operators, each playing a distinct role in manipulating and evaluating data.


## **EXERCISE**

This [blinky code](blinky.c) is supposed to blink an LED connected to the GPIO pin. The LED blinks at a rate determined by the "a" variable, which starts at 1 ms and __doubles__ with each iteration of the loop. When variable "a" reaches 2048ms, it resets to 1, creating an odd repeating LED blink pattern. The LED blink pattern must turn on and off with the same delay at __each loop iteration__. Could you identify where the errors are and make the necessary changes so that the code works as intended?

> [!IMPORTANT]
> Include a printf statement to monitor the variable "a". You might need to modify the CMake file to allow printf to work on the blink example. Look at the CMake file in the Hello_World example to glean some insights into this.

