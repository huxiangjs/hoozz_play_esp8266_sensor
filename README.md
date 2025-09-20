# Hoozz Play ESP8266 Sensor
Various sensors

# ESP8266_RTOS_SDK Version
```shell
$ git branch
* release/v3.3

$ git log --oneline | head -n 3
2bc42667 Merge branch 'bugfix/constrain_cryptography_v3.3' into 'release/v3.3'
4cab385e Tools: Constrain the cryptography package for avoiding breaking changes
6c438bce Merge branch 'bugfix/queue_arith_overflow_v3.3' into 'release/v3.3'

Toolchain version: crosstool-ng-1.22.0-100-ge567ec7b
Compiler version: 5.2.0
```

## Pull source code
```shell
git clone https://github.com/huxiangjs/hoozz_play_esp8266_sensor.git --recurse-submodules
```

## Build and Flash

* first step: open the sdkconfig file, modify `CONFIG_ESPTOOLPY_PORT` to your serial.

```shell
cd hoozz_play_esp8266_sensor/MCU
make -j$(nproc)
make flash
make monitor    # Monitor UART log output
```

## You can also directly burn the released bin file

1. Download the latest release zip package from the Releases column
2. Unzip the zip and you will see the following files:
   ```
   $ tree
   .
   |-- bootloader
   |   `-- bootloader.bin
   |-- partitions.bin
   `-- sensor.bin

   1 directory, 3 files
   ```
3. Open the latest official download tool `flash_download_tool` (official download address: [other-tools](https://www.espressif.com/en/support/download/other-tools))
4. Use the following options: (1) `Chip Type [ESP8266]`; (2) `WorkMode [Develop]`; (3) `LoadMode [UART]`;
5. Set the burn parameters according to the following table:

   |    Parameters  |     Value   |
   | :------------: | :---------: |
   | bootloader.bin | 0x0000      |
   | sensor.bin     | 0x10000     |
   | partitions.bin | 0x8000      |
   | SPI SPEED      | 40MHz       |
   | SPI MODE       | DIO         |
   | DoNotChgBin    | √           |
   | COM            | (Your port) |
   | BAUD           | 115200      |

6. Finally click **Start** to burn

