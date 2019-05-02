## **For support, development, shenanigans: check out the [Discord](https://discord.gg/skUAWKg).**


# # PGoTrader
This script does auto-trading between two simultaneous applications running on the same device (using Island, MIUI's Dual Apps, and so on).

Should work with other Dual App solutions as well, as long as the `switch_app()` co-routine is able to switch between both instances.

### Warnings
This script essentially blindly sends touch events to your phone. If a popup appears over where the script thinks a button is, or if your phone lags, it can do unintended things. Please keep an eye on your phone while it is running. If it trades your shiny 100% Dragonite, it's because you weren't watching it.

# Installation
### Prerequisites

*You only need to perform these steps once*

1. [Download all the files](https://github.com/esauvisky/PGoTrader/archive/master.zip) from this repository. Unzip everything into a directory.
2. Install `adb`, and make sure it's on your system's PATH. 
  
   • _Windows users can install the SDK Platform Tools via [this link](https://developer.android.com/studio/releases/platform-tools)._
3. Install [clipper](https://github.com/majido/clipper) in your device and run the app/service.
4. Install Python >=3.7 (older versions will not work). 

   • _Windows users can go [here](https://www.python.org/downloads/windows/) and select [Download Windows x86-64 executable installer](https://www.python.org/ftp/python/3.7.3/python-3.7.3-amd64.exe) under **Stable Releases**._
5. Now, open a terminal in the repository directory you unzipped in step 1. 
   • _Windows users can [open a command prompt inside the folder](https://www.google.com/search?q=open+a+command+prompt+in+a+folder "In File Explorer, press and hold the Shift key, then right click or press and hold on a folder or drive that you want to open the command prompt at that location for, and click/tap on Open Command Prompt Here option.") (hover the link for TL;DR)._
   
6. Check if you have installed Python 3.7 `python -v` returns Python 3.7.x    
7. Run `pip install -r requirements.txt` to install the required libraries for the script to work.

### Configuration

*You only need to perform these steps once*

- Copy or rename `config.example.yaml` to `config.yaml`.
- Enable _USB Debugging_ in **Settings > Developer options** in your device, and connect it to the computer.
- In the command prompt, type `adb devices -l` and see if it properly detects the device.
- Edit `config.yaml` locations for your phone:
    - The defaults are for a Oneplus 3T and should work with any 1080p phone that does not have soft buttons.
    - Each setting is an X,Y location. You can turn on **Settings > Developer options > Pointer location** .
- You're done! Move on to the next section [Basic Usage](#basic-usage) whenever you want to use the renamer.

# Usage

### Basic Usage
- Open both apps
- Go to Friends, and open the friend screen (in both apps).
- Run `python trade.py`

_That's it!  :D_


# FAQ
1. It taps in the wrong locations / doesn't work / automatically called my mother:

    You probably need to edit the `locations:` in config.yaml, the defaults are for a 1080p phone without soft keys.
    To find out the coordinates, enable *Pointer Location* in your phone's *Developer Settings*. If you're lazy like me, just type the code below with your phone connected:

    - To enable:
        ```bash
        adb shell content insert --uri content://settings/system --bind name:s:pointer_location --bind value:i:1
            # If that doesn't work, use this:
        adb shell settings put system pointer_location 1
        ```

    - To disable
        ```bash
        adb shell content insert --uri content://settings/system --bind name:s:pointer_location --bind value:i:0
            # If that doesn't work, use this:
        adb shell settings put system pointer_location 0
        ```

2. Can i run a diffrent config.yaml file? 

    Yes you can, make sure the .yaml file is in the same directory as the config.yaml
    
    Run the command `python trade.py --config YOUROWNCONFIG.yaml`
    
7. Can i define how many trades will be done? 

    sure by adding --stop-after [amount of runs]

    `python trade.py --stop-after 5` this results in 5 pokemons will be traded
    
 
