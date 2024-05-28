
# Tasmota Firmware Instructions
We have developed Tasmota firmware for all languages based on the ZB-GW03. The ETH version defaults to disabling Wi-Fi (which can be enabled by using WIFI 0) and requires no template configuration upon startup. If you wish to view the IP address, you can use an mDNS tool to scan the network and locate Tasmota's gateway. Alternatively, you can log in to the router's backend to check the gateway's IP address. If the ETH version does not meet your requirements, you can also opt for the WIFI & ETH version, which requires no additional configuration.

# Firmware Building Instructions
If you want to build your own firmware for ZB-GW03, follow these steps:

1. Clone the Tasmota repository at the following address:

https://github.com/arendst/tasmota

2. Set up the compilation environment following the steps outlined here:

https://tasmota.github.io/docs/Compile-your-build/

3. Create a new file named "user_config_override.h" in the Tasmota directory, and fill it with the following content:

``` C
#ifdef FIRMWARE_EASYIOT
  //#undef  SERIAL_LOG_LEVEL
  //#define SERIAL_LOG_LEVEL LOG_LEVEL_NONE
  //mDNS
  #define USE_DISCOVERY                            // Enable mDNS for the following services (+8k code or +23.5k code with core 2_5_x, +0.3k mem)
  #undef MDNS_ENABLED
  #define MDNS_ENABLED          true              //默认启用MDNS
  #undef  MQTT_HOST_DISCOVERY                    // Find MQTT host server (overrides MQTT_HOST if found)


//  #define MY_LANGUAGE            zh_CN           // Chinese (Simplified) in China
  #undef MODULE
  #define MODULE USER_MODULE
  #undef FALLBACK_MODULE 
  #define FALLBACK_MODULE USER_MODULE
  #define USER_TEMPLATE "{\"NAME\":\"ZB-GW03\",\"GPIO\":[0,0,3552,0,3584,0,0,0,5793,5792,320,544,5536,0,5600,0,0,0,0,5568,0,0,0,0,0,0,0,0,608,640,32,0,0,0,0,0],\"FLAG\":0,\"BASE\":1}"  // [Template] Set JSON template

  #undef LIGHT_MODE
  #define LIGHT_MODE false
  #undef USE_DOMOTICZ

  #undef OTA_URL
  #define OTA_URL ""

  #undef WEB_PASSWORD
  #define WEB_PASSWORD ""

//  #undef WEB_PORT
//  #define WEB_PORT      8888

  #undef OTA_URL
  #define OTA_URL                ""

#undef APP_TIMEZONE
#define APP_TIMEZONE 8
#undef ROTARY_V1             // Add support for Rotary Encoder as used in MI Desk Lamp (+0k8 code)
#undef ROTARY_MAX_STEPS      // Rotary step boundary
#undef USE_SONOFF_RF         // Add support for Sonoff Rf Bridge (+3k2 code)
#undef USE_RF_FLASH          // Add support for flashing the EFM8BB1 chip on the Sonoff RF Bridge. C2CK must be connected to GPIO4, C2D to GPIO5 on the PCB (+2k7 code)
#undef USE_SONOFF_SC         // Add support for Sonoff Sc (+1k1 code)
#undef USE_TUYA_MCU          // Add support for Tuya Serial MCU
#undef TUYA_DIMMER_ID        // Default dimmer Id
#undef USE_TUYA_TIME         // Add support for Set Time in Tuya MCU
#undef USE_ARMTRONIX_DIMMERS // Add support for Armtronix Dimmers (+1k4 code)
#undef USE_PS_16_DZ          // Add support for PS-16-DZ Dimmer (+2k code)
#undef USE_SONOFF_IFAN       // Add support for Sonoff iFan02 and iFan03 (+2k code)
#undef USE_BUZZER            // Add support for a buzzer (+0k6 code)
#undef USE_ARILUX_RF         // Add support for Arilux RF remote controller (+0k8 code, 252 iram (non 2.3.0))
#undef USE_SHUTTER           // Add Shutter support for up to 4 shutter with different motortypes (+11k code)
#undef USE_DEEPSLEEP         // Add support for deepsleep (+1k code)
#undef USE_EXS_DIMMER        // Add support for ES-Store Wi-Fi Dimmer (+1k5 code)
#undef EXS_MCU_CMNDS                          // Add command to send MCU commands (+0k8 code)
#undef USE_HOTPLUG                              // Add support for sensor HotPlug
#undef USE_DEVICE_GROUPS                        // Add support for device groups (+5k5 code)
#undef DEVICE_GROUPS_ADDRESS // Device groups multicast address
#undef DEVICE_GROUPS_PORT                   // Device groups multicast port
#undef USE_DEVICE_GROUPS_SEND                   // Add support for the DevGroupSend command (+0k6 code)
#undef USE_PWM_DIMMER                           // Add support for MJ-SD01/acenx/NTONPOWER PWM dimmers (+2k3 code, DGR=0k7)
#undef USE_PWM_DIMMER_REMOTE                    // Add support for remote switches to PWM Dimmer (requires USE_DEVICE_GROUPS) (+0k6 code)
#undef USE_KEELOQ                               // Add support for Jarolift rollers by Keeloq algorithm (+4k5 code)
#undef USE_SONOFF_D1     // Add support for Sonoff D1 Dimmer (+0k7 code)
#undef USE_SHELLY_DIMMER // Add support for Shelly Dimmer (+3k code)
#undef SHELLY_CMDS       // Add command to send co-processor commands (+0k3 code)
#undef SHELLY_FW_UPGRADE // Add firmware upgrade option for co-processor (+3k4 code)
#undef SHELLY_VOLTAGE_MON                     // Add support for reading voltage and current measurment (-0k0 code)
//#undef USE_AUTOCONF
#undef USE_BERRY

  // -- Optional light modules ----------------------
#undef USE_LIGHT                         // Add support for light control
#undef USE_WS2812                        // WS2812 Led string using library NeoPixelBus (+5k code, +1k mem, 232 iram) - Disable by //
                                          //  #define USE_WS2812_DMA                         // ESP8266 only, DMA supports only GPIO03 (= Serial RXD) (+1k mem). When USE_WS2812_DMA is enabled expect Exceptions on Pow
//#define USE_WS2812_RMT 0                  // ESP32 only, hardware RMT support (default). Specify the RMT channel 0..7. This should be preferred to software bit bang.
                                          //  #define USE_WS2812_I2S  0                      // ESP32 only, hardware I2S support. Specify the I2S channel 0..2. This is exclusive from RMT. By default, prefer RMT support
                                          //  #define USE_WS2812_INVERTED                    // Use inverted data signal
#undef USE_WS2812_HARDWARE                // Hardware type (NEO_HW_WS2812, NEO_HW_WS2812X, NEO_HW_WS2813, NEO_HW_SK6812, NEO_HW_LC8812, NEO_HW_APA106, NEO_HW_P9813)
#undef USE_WS2812_CTYPE                   // Color type (NEO_RGB, NEO_GRB, NEO_BRG, NEO_RBG, NEO_RGBW, NEO_GRBW)
#undef USE_MY92X1                        // Add support for MY92X1 RGBCW led controller as used in Sonoff B1, Ailight and Lohas
#undef USE_SM16716                       // Add support for SM16716 RGB LED controller (+0k7 code)
#undef USE_SM2135                        // Add support for SM2135 RGBCW led control as used in Action LSC (+0k6 code)
#undef USE_SM2335                        // Add support for SM2335 RGBCW led control as used in SwitchBot Color Bulb (+0k7 code)
#undef USE_BP5758D                       // Add support for BP5758D RGBCW led control as used in some Tuya lightbulbs (+0k8 code)
#undef USE_SONOFF_L1                     // Add support for Sonoff L1 led control
#undef USE_ELECTRIQ_MOODL                // Add support for ElectriQ iQ-wifiMOODL RGBW LED controller (+0k3 code)
#undef USE_LIGHT_PALETTE                 // Add support for color palette (+0k7 code)
#undef USE_LIGHT_VIRTUAL_CT              // Add support for Virtual White Color Temperature (+1.1k code)
#undef USE_DGR_LIGHT_SEQUENCE            // Add support for device group light sequencing (requires USE_DEVICE_GROUPS) (+0k2 code)
#undef USE_LSC_MCSL                             // Add support for GPE Multi color smart light as sold by Action in the Netherlands (+1k1 code)

#define USE_ZIGBEE
#undef USE_ZIGBEE_ZNP
#define USE_ZIGBEE_EZSP
#define USE_UFILESYS
#define USE_ZIGBEE_EEPROM // T24C512A
#define USE_TCP_BRIDGE
#undef USE_ZIGBEE_CHANNEL
#define USE_ZIGBEE_CHANNEL 11 // (11-26)

#define USE_ETHERNET
#undef ETH_TYPE
#define ETH_TYPE 0 // ETH_PHY_LAN8720
#undef ETH_CLKMODE
#define ETH_CLKMODE 3 // ETH_CLOCK_GPIO17_OUT
#undef ETH_ADDRESS
#define ETH_ADDRESS 1 // PHY1
#endif

```

4. In the repository directory, create a new file named "platformio_override.ini" with the following content:

```ini
; ***  Example PlatformIO Project Configuration Override File   ***
; ***  Changes done here override settings in platformio.ini    ***
;
; *****************************************************************
; ***  to activate rename this file to platformio_override.ini  ***
; *****************************************************************
;
; Please visit documentation for the options and examples
; http://docs.platformio.org/en/stable/projectconf.html

[platformio]
; For best Gitpod performance remove the ";" in the next line. Needed Platformio files are cached and installed at first run
;core_dir = .platformio
; For unrelated compile errors with Windows it can help to shorten Platformio project path
;workspace_dir = c:\.pio

; *** Build/upload environment
default_envs            =
; *** Uncomment the line(s) below to select version(s)
                          tasmota
;                          tasmota-debug
;                          tasmota-minimal
;                          tasmota-lite
;                          tasmota-knx
;                          tasmota-sensors
;                          tasmota-display
;                          tasmota-zbbridge
;                          tasmota-ir
;                          tasmota32
;                          tasmota32-zbbrdgpro
;                          tasmota32-bluetooth
;                          tasmota32-webcam
;                          tasmota32-knx
;                          tasmota32-sensors
;                          tasmota32-lvgl
;                          tasmota32-ir
;                          tasmota32solo1
;                          tasmota32c3
;                          tasmota32c3cdc
;                          tasmota32s2
;                          tasmota32s2cdc
;                          tasmota32s3
;                          tasmota32s3cdc
;                          tasmota32-odroidgo
;                          tasmota32-core2
;                          tasmota32-nspanel


[env]
; Activate Development core by removing ";" the next lines
;platform                = https://github.com/platformio/platform-espressif8266.git
;platform_packages       = framework-arduinoespressif8266 @ https://github.com/esp8266/Arduino.git
;                          mcspr/toolchain-xtensa @ ~5.100300.211127
;                          platformio/tool-esptoolpy @ ~1.30300
;build_unflags           = ${common.build_unflags}
;                          -Wswitch-unreachable
;build_flags             = ${common.build_flags}
;                          -D PIO_FRAMEWORK_ARDUINO_MMU_CACHE16_IRAM48_SECHEAP_SHARED
;                          -Wno-switch-unreachable
; *** Optional Debug messages
;                         -DDEBUG_TASMOTA_CORE
;                         -DDEBUG_TASMOTA_DRIVER
;                         -DDEBUG_TASMOTA_SENSOR
; Build variant 1MB = 1MB firmware no filesystem (default)
board                   = ${common.board}
; Build variant 2MB = 1MB firmware, 1MB filesystem (most Shelly devices)
;board                   = esp8266_2M1M
; Build variant 4MB = 1MB firmware, 1MB OTA, 2MB filesystem (WEMOS D1 Mini, NodeMCU, Sonoff POW)
;board                   = esp8266_4M2M
;board_build.f_cpu       = 160000000L
;board_build.f_flash     = 40000000L
;monitor_speed           = 115200
; *** Serial port used for erasing/flashing the ESP82xx
;upload_port             = COM5
extra_scripts           = ${esp_defaults.extra_scripts}
;                          pio-tools/obj-dump.py
lib_ignore              =
                          Servo(esp8266)
                          ESP8266AVRISP
                          ESP8266LLMNR
                          ESP8266NetBIOS
                          ESP8266SSDP
                          SP8266WiFiMesh
                          Ethernet(esp8266)
                          GDBStub
                          TFT_Touch_Shield_V2
                          ESP8266HTTPUpdateServer
                          ESP8266WiFiMesh
                          EspSoftwareSerial
                          SPISlave
                          Hash
; Disable next if you want to use ArduinoOTA in Tasmota (default disabled)
                          ArduinoOTA
lib_extra_dirs          = ${library.lib_extra_dirs}


[env:tasmota32_base]
; *** Uncomment next lines ";" to enable development Tasmota Arduino version ESP32
;platform                = https://github.com/tasmota/platform-espressif32.git
;platform_packages       = framework-arduinoespressif32 @ https://github.com/Jason2866/esp32-arduino-lib-builder/releases/download/1088/framework-arduinoespressif32-release_v4.4-a0113c7bfe.zip
;                          framework-arduino-solo1 @ https://github.com/Jason2866/esp32-arduino-lib-builder/releases/download/1092/framework-arduinoespressif32-solo1-release_v4.4-a0113c7bfe.zip
;                          framework-arduino-ITEAD @ https://github.com/Jason2866/esp32-arduino-lib-builder/releases/download/1091/framework-arduinoespressif32-ITEAD-release_v4.4-a0113c7bfe.zip
;build_unflags           = ${esp32_defaults.build_unflags}
;build_flags             = ${esp32_defaults.build_flags}
;board                   = esp32
;board_build.f_cpu       = 240000000L
;board_build.f_flash     = 40000000L
;board_build.flash_mode  = qio
;board_build.flash_size  = 8MB
;board_upload.maximum_size = 8388608
;board_upload.arduino.flash_extra_images =
;board_build.partitions  = partitions/esp32_partition_app2944k_fs2M.csv
; *** Serial port used for erasing/flashing the ESP32
;upload_port             = COM4
;monitor_port            = COM4
;upload_speed            = 115200
monitor_speed           = 115200
upload_resetmethod      = ${common.upload_resetmethod}
extra_scripts           = ${esp32_defaults.extra_scripts}
;                          pio-tools/obj-dump.py
lib_ignore              =
                          HTTPUpdateServer
                          ESP RainMaker
                          WiFiProv
                          USB
                          SPIFFS
                          ESP32 Azure IoT Arduino
                          ;ESP32 Async UDP
                          ESP32 BLE Arduino
;                          SimpleBLE
                          NetBIOS
                          ESP32
                          Preferences
                          BluetoothSerial
; Disable next if you want to use ArduinoOTA in Tasmota32 (default disabled)
                          ArduinoOTA

lib_extra_dirs           = ${library.lib_extra_dirs}
; *** ESP32 lib. ALWAYS needed for ESP32 !!!
                          lib/libesp32
; *** comment the following line if you dont use LVGL in a Tasmota32 build. Reduces compile time
                          lib/libesp32_lvgl
; *** comment the following line if you dont use ESP32 Audio in a Tasmota32 build. Reduces compile time
;                          lib/libesp32_audio
; *** uncomment the following line if you use Bluetooth or Apple Homekit in a Tasmota32 build. Reduces compile time
;                          lib/libesp32_div
; *** uncomment the following line if you use Epaper driver epidy in your Tasmota32 build. Reduces compile time
;                          lib/libesp32_eink


[library]
shared_libdeps_dir      = lib
; *** Library disable / enable for variant Tasmota(32). Disable reduces compile time
; *** !!! Disabling needed libs will generate compile errors !!!
; *** The resulting firmware will NOT be different if you leave all libs enabled
; *** Disabling by putting a ";" in front of the lib name
; *** If you dont know what it is all about, do not change
lib_extra_dirs           =
; *** Only disabled for Tasmota minimal and Tasmota light. For all other variants needed!
                           lib/lib_basic
; **** I2C devices. Most sensors. Disable only if you dont have ANY I2C device enabled
                           lib/lib_i2c
; *** Displays. Disable if you dont have any Display activated
                           lib/lib_display
; *** Bear SSL and base64. Disable if you dont have SSL or TLS activated
                           lib/lib_ssl
; *** Audio needs a lot of time to compile. Mostly not used functions. Recommended to disable
                           lib/lib_audio
; *** RF 433 stuff (not RF Bridge). Recommended to disable
                           lib/lib_rf
; *** Mostly not used functions. Recommended to disable
                           lib/lib_div

[env:tasmota32-ZB-GW03-EN]
extends                 = env:tasmota32
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-AD]
extends                 = env:tasmota32
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=ca_AD -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-AF]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=af_AF -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-BG]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=bg_BG -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-BR]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=pt_BR -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-CN]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=zh_CN -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-CZ]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=cs_CZ -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-DE]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=de_DE -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-ES]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=es_ES -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-FR]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=fr_FR -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-FY]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=fy_NL -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-GR]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=el_GR -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-HE]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=he_HE -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-HU]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=hu_HU -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-IT]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=it_IT -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-KO]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=ko_KO -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-NL]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=nl_NL -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-PL]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=pl_PL -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-PT]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=pt_PT -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-RO]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=ro_RO -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-RU]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=ru_RU -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-SE]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=sv_SE -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-SK]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=sk_SK -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-TR]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=tr_TR -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-TW]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=zh_TW -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-UK]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=uk_UA -DFIRMWARE_EASYIOT

[env:tasmota32-ZB-GW03-VN]
extends                 = env:tasmota32_base
board_build.f_cpu       = 240000000L
board_build.f_flash     = 40000000L
build_flags             = ${env:tasmota32_base.build_flags} -DMY_LANGUAGE=vi_VN -DFIRMWARE_EASYIOT
```

5. Open the terminal and enter one of the following commands on the command line to build firmware in your own language

```bash
pio run -e tasmota32-ZB-GW03-EN
pio run -e tasmota32-ZB-GW03-AD
pio run -e tasmota32-ZB-GW03-AF
pio run -e tasmota32-ZB-GW03-BG
pio run -e tasmota32-ZB-GW03-BR
pio run -e tasmota32-ZB-GW03-CN
pio run -e tasmota32-ZB-GW03-CZ
pio run -e tasmota32-ZB-GW03-DE
pio run -e tasmota32-ZB-GW03-ES
pio run -e tasmota32-ZB-GW03-FR
pio run -e tasmota32-ZB-GW03-FY
pio run -e tasmota32-ZB-GW03-GR
pio run -e tasmota32-ZB-GW03-HE
pio run -e tasmota32-ZB-GW03-HU
pio run -e tasmota32-ZB-GW03-IT
pio run -e tasmota32-ZB-GW03-KO
pio run -e tasmota32-ZB-GW03-NL
pio run -e tasmota32-ZB-GW03-PL
pio run -e tasmota32-ZB-GW03-PT
pio run -e tasmota32-ZB-GW03-RO
pio run -e tasmota32-ZB-GW03-RU
pio run -e tasmota32-ZB-GW03-SE
pio run -e tasmota32-ZB-GW03-SK
pio run -e tasmota32-ZB-GW03-TR
pio run -e tasmota32-ZB-GW03-TW
pio run -e tasmota32-ZB-GW03-UK
pio run -e tasmota32-ZB-GW03-VN
```

