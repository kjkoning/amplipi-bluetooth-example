# Package for adding Bluetooth functionality to an AmpliPi

Much of the Bluetooth setup comes from https://gist.github.com/Pindar/e259bec5c3ab862f4ff5f1fbcb11bfc1

This package adds the ability to use a USB Bluetooth dongle on an AmpliPi as an audio stream. Allowing the AmpliPi to connect to bluetooth speakers should be possible with a bit of work, but is not a part of this package.

Note: Bluetooth devices won't automatically connect to the AmpliPi when the Bluetooth stream is active. This functionality can be changed by 'trusting' the the device (from command line: bluetoothctl trust <dev ID>). Adding a Bluetooth management page with this functionality could be very useful.

## Installation

1. Download the files from this repo and upload them to the /home/pi directory. The files in the 'amplipi' folder will need to overwrite the existing files on the AmpliPi or AmpliPi development environment.

2. SSH into the AmpliPi and run (or manually step through the lines, one at a time):
   ```
   chmod -x install_bluetooth_for_amplipi.sh
   sudo ./install_bluetooth_for_amplipi.sh
   ```
   This will install the components for Bluetooth on the device.

3. After rebooting the AmpliPi, SSH into it again and run:
   ```
   bluetoothctl show
   ```
   If it shows a controller, go to step 4. If not, follow these steps:
   - Make sure a working USB Bluetooth dongle is plugged in to the computer.
   - Run `lsusb` to see if Linux sees the USB device.
   - If the Bluetooth dongle has a Realtek chipset, you may need to install the driver. Review the 'install_realtek_bt_driver' folder for the files and instructions.

4. Browse to the AmpliPi API web page (http://amplipi.local/doc) and paste the below JSON value into the 'Example' text box under Stream -> Create Stream and hit the 'Try' button. This will add a Bluetooth stream to the stream list.
   ```
   {
      "name": "Bluetooth",
      "type": "bluetooth"
   }
   ```

Return to the AmpliPi main page, and select teh new Bluetooth stream type. Then, from a bluetooth-capable device, connect to the 'amplipi' device and start playing audio.
