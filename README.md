# wm tool

DISCLAIMER: I didn't write this. I just discover this tool in [github0null/w800_cmake_sdk/tools/w800](https://github.com/github0null/w800_cmake_sdk/tree/master/tools/w800) and add a `CMakeLists.txt` to build it.

(Also found in [IOsetting/wm-sdk-w806](https://github.com/IOsetting/wm-sdk-w806), so I think it comes with the origin SDK)

```bash
mkdir build
cd build
cmake .. -G Ninja
ninja -j$(nproc)
```

TODO: rewrite `wm_tool` with Rust.

## Usage

```bash
Usage: wm_tool [-h] [-v] [-b] [-o] [-sb] [-ct] [-it] [-ua] [-ra] [-ih] [-nh] [-un] [-df] [-vs] [-l] [-c] [-ws] [-ds] [-rs] [-eo] [-dl] [-sl]

WinnerMicro firmware packaging and programming tool

options:

  -h                    , show usage
  -v                    , show version

  -b  binary            , original binary file
  -o  output_name       , output firmware file
                          the default is the same as the original binary file name
  -sb second_boot       , second boot file, used to generate fls file
  -fc compress_type     , whether the firmware is compressed, default is compressed
                          <0 | 1> or <uncompress | compress>
  -it image_type        , firmware image layout type, default is 0
                          <0 | 1>
  -ua update_address    , upgrade storage location (hexadecimal)
                          the default is 8090000
  -ra run_address       , runtime position (hexadecimal)
                          the default is 8002400
  -ih image_header      , image header storage location (hexadecimal)
                          the default is 8002000
  -nh next_image_header , next image header storage location (hexadecimal)
                          the default is 0
  -un upd_no            , upd no version number (hexadecimal)
                          the default is 0
  -df                   , generate debug firmware for openocd
  -vs version_string    , firmware version string, cannot exceed 16 bytes

  -l                    , list the local serial port
  -c  serial_name       , connect a serial port
                          e.g: tty.usbserial0 tty.usbserial3 tty.usbserial7
  -ws baud_rate         , set the serial port speed during normal work, default is 115200
                          <1200 - 2000000> or <1M | 2M>
  -ds baud_rate         , set the serial port speed when downloading, default is 115200
                          <115200 | 460800 | 921600 | 1000000 | 2000000> or <1M | 2M>
  -rs reset_action      , set device reset method, default is manual control
                          <none | at | rts>
                           none - manual control device reset
                           at   - use the at command to control the device reset
                           rts  - use the serial port rts pin to control the device reset
  -eo erase_option      , firmware area erase option
                          <all>
                           all  - erase all areas
  -dl download_firmware , firmware file to be downloaded, default download compressed image
  -sl display_format    , display the log information output from the serial port
                          <0 | 1> or <str | hex>
                           str - string mode display
                           hex - hexadecimal format
```

example from [here](https://github.com/github0null/w800_cmake_sdk/blob/243bee265ad73515025a440b033f05821420a3ce/tools/flash_firmware.sh.in#L43)

```bash
./wm_tool -dl firmware.fls -ws 2M -ds 2M -rs rts -c $port -sl str -ws 115200
```
