# ESP32 Project Template

Environment setup for developing ESP32 firmware projects with Espressif's ESP32 Wi-Fi and Bluetooth enabled microcontroller.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

The instructions below are mostly the recommendations from Espressif's documentation on how to [Get Started](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html) developing with ESP-IDF SDK. A few prerequisites are included to optimize its use with VSCode text editor and Uncrustify code formatter.

- [ESP-IDF Prerequisites](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html#get-started-get-prerequisites)
  - Linux:
  
    > `sudo apt-get install git wget flex bison gperf python python-pip python-setuptools python-serial python-click python-cryptography python-future python-pyparsing python-pyelftools cmake ninja-build ccache libffi-dev libssl-dev`

    > `sudo usermod -a -G dialout $USER`
  
  - Windows (64-bit only): [ESP-IDF Tools Installer](https://dl.espressif.com/dl/esp-idf-tools-setup-2.2.exe)
    - The path chosen to install the ESP-IDF and the ```.espressif``` environment tools folder **must not contain spaces**.
    - It might be necessary to modify the ```esp-idf/tools/idf_tools.py``` installation script to suppress the ```--no-site-packages``` option, as it is the default behavior for newer versions of ```virtualenv```.

        ```diff
        --- a/idf_tools.py
        +++ b/idf_tools.py
        @@ -1152,7 +1152,7 @@ def action_install_python_env(args):
                    subprocess.check_call([sys.executable, '-m', 'pip', 'install', '--user', 'virtualenv'],
                                        stdout=sys.stdout, stderr=sys.stderr)

        -        subprocess.check_call([sys.executable, '-m', 'virtualenv', '--no-site-packages', idf_python_env_path],
        +        subprocess.check_call([sys.executable, '-m', 'virtualenv', idf_python_env_path],
                                    stdout=sys.stdout, stderr=sys.stderr)
            run_args = [virtualenv_python, '-m', 'pip', 'install', '--no-warn-script-location']
            requirements_txt = os.path.join(global_idf_path, 'requirements.txt')
        ```

- [ESP-IDF](https://github.com/espressif/esp-idf):
  - Linux (these steps are done by the *ESP-IDF Tools Installer*):
    - Clone **ESP-IDF** repository:
        > `cd ~/esp && git clone --recursive https://github.com/espressif/esp-idf.git`
    - Install all necessary compilation tools:
        > `cd ~/esp/esp-idf && ./install.sh`
    - Set up the environment variables for the current terminal session, or add this to your ```.profile``` or ```.bash_profile``` script:
        > `~/esp/esp-idf/export.sh`
  - Linux and Windows:
    - Add the ESP-IDF repository path to the environment variable ```ESP_IDF_PATH```.

- [Visual Studio Code](https://code.visualstudio.com/)
  - [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
  - [EditorConfig](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
  - [Native Debug](https://marketplace.visualstudio.com/items?itemName=webfreak.debug)

- [Git for Windows](https://git-scm.com/download/win)

## Tasks

On VSCode, pressing `CTRL`+`SHIFT`+`B` will list Tasks for compiling, flashing, monitoring, etc.

- Build
- Clean
- Flash
- Monitor
- Menuconfig

## Debug

> This section is under construction!

### Hardware requirements

Be sure to have a [J-Link](https://www.segger.com/products/debug-probes/j-link/) connected to the ESP32 target board through its JTAG interface:

| ESP32 | J-Link    |
| ----- | --------- |
| 3.3V  | VTref (1) |
| GND   | GND (4)   |
| EN    | nTRST (3) |
| IO12  | TDI (5)   |
| IO13  | TCK (9)   |
| IO14  | TMS (7)   |
| IO15  | TDO (5)   |

On Windows, the J-Link driver must be changed to the **WinUSB**. This can be done using [Zadig](https://zadig.akeo.ie/). Make sure to check *"List All Devices"* under the *"Options"* tab.

### VSCode's Native Debug

Use VSCode's extension [Native Debug](https://marketplace.visualstudio.com/items?itemName=webfreak.debug), which is automatically recommended if not already installed.

To start debugging, follow the steps below:

- Press **F5** to start the ```OpenOCD``` pre-launch task;
- This operation will fail after some time. Press **Cancel** when the *"The specified task cannot be tracked"* dialog pops up;
- Notice that the OpenOCD session is still running and we can now attach a GDB process to it by pressing **F5** again. The debug session should now start.

Once the OpenOCD pre-launch task is run by the first time, all succeeding debug sessions shoul start normally.

## Authors

- **Gabriel Kim**
