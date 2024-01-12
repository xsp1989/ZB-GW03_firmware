
# ESPHome Firmware Instructions
This is the ESPHome firmware based on ZB-GW03. If you wish to build your own firmware, you can refer to `zb-gw03.yaml` and make modifications accordingly. However, it is crucial to note that if you lack experience in flashing devices via serial port, I do not recommend doing so. Incorrect configurations might turn your device into a brick.

For those interested in creating their own firmware, please refer to the provided instructions. A special thanks to @syssi for the valuable contributions to the open-source community.

Link to the repository: https://github.com/syssi/esphome-zb-gw03



# File Descriptions:

`zb-gw03.bin` can be upgraded via the web interface. You can utilize this file in Tasmota to upgrade to ESPHome.

`zb-gw03-factory.bin` is the factory firmware for flashing the flash via serial port. If your device becomes bricked, you can use this file for recovery.


# Additional Instructions: 
If you prefer Tasmota over ESPHome, you can upgrade from ESPHome to Tasmota through your web browser. The web address for this process is http://your_ip:80.

