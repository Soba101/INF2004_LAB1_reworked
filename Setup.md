# **Getting Started with Raspberry Pi Pico W**

This guide provides a step-by-step process to set up the development environment for the Raspberry Pi Pico W, update dependencies, configure the Pico SDK, compile, and run projects. Instructions are provided for Windows, macOS, and Linux.

---

## **Step 1: Updating Dependencies**

### **Raspberry Pi OS and Windows**
No additional dependencies are required.

### **Linux**
Most Linux distributions come with the necessary dependencies preinstalled. However, if required, install the following:
- Python 3.9 or later
- Git
- Tar
- A native C and C++ compiler (GCC supported)

Run the following command to install missing dependencies:
```bash
sudo apt install python3 git tar build-essential
```

### **macOS**
To install the required dependencies, run:
```bash
xcode-select --install
```
This installs:
- Git
- Tar
- A native C and C++ compiler (GCC and Clang supported)

---

## **Step 2: Setting Up the Pico SDK**
Ensure your system has the following tools installed:
- **CMake**: For generating build files.
- **GNU Make**: For compiling.
- **ARM GCC Toolchain**: For cross-compilation.

Install the Pico SDK and necessary tools:
```bash
sudo apt install cmake
sudo apt install make
sudo apt install gcc-arm-none-eabi
```

Clone and initialize the Pico SDK:
```bash
git clone https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init
cd ..
```

---

## **Step 3: Compiling and Running Your Files**
Once the Pico SDK is installed, follow these steps to compile and flash your files to the Pico W.

1. **Open a terminal.**
2. **Navigate to the directory** where your project files are located.
3. **Create a build directory:**
   ```bash
   mkdir build
   cd build
   ```
4. **Generate build files and compile:**
   ```bash
   cmake ..
   make
   ```
5. **Flash your compiled file to the Pico W:**
   ```bash
   cp build/your_file.uf2 /media/your_username/RPI-RP2
   ```
   Alternatively, you can **drag and drop** the UF2 file onto the Pico W drive in your file manager.

---

## **Optional: Using Visual Studio Code**
You can also use the **Visual Studio Code Pico W extension** to build and flash your files.

### **Steps:**
1. **Open Visual Studio Code.**
2. Ensure the [**Pico W extension**](/img/raspberry_pico_ext.png) is installed.
3. Click on the [**Pico W icon**](/img/ext_icon.png) in the sidebar.
4. Click on [**"New Project From Example"**](/img/project_example.png) and select blinky as your first project follow the setup instructions.
5. Click on the **"Build"** button to compile your files.
6. Click on the **"Flash"** button to upload your files to the Pico W.

> **Note:** The initial project build may take some time, but subsequent builds will be much faster.

---
