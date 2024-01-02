1. download archive with amperka board https://github.com/amperka/amperka-boards
2. unzip in folder `amperka`
3. create `boards` folder 
4. create file `boards/Amperka_ATmega328PB.json` with content
```
{
    "build": {
        "core": "arduino",
        "extra_flags": "-DARDUINO_AVR_NANO -include $PROJECT_DIR/amperka/variants/iskra-nano-pro/io_328pb.h",
        "f_cpu": "16000000L",
        "mcu": "atmega328p",
        "variant": "iskra-nano-pro",
        "variants_dir": "amperka/variants"
    },
    "bootloader": {
        "file": "$PROJECT_DIR/amperka/bootloaders/optiboot/optiboot_atmega328pb_16mhz.hex", 
        "efuse": "0xF4",
        "hfuse": "0xDE",
        "lfuse": "0xFF",
        "lock_bits": "0xCF",
        "unlock_bits": "0xFF"
    },
    "frameworks": [
        "arduino"
    ],
    "name": "Amperka Iskra Nano Pro",
    "upload": {
        "maximum_ram_size": 2048,
        "maximum_size": 32256,
        "require_upload_port": true,
        "speed": 115200,
        "protocol": "custom",
        "command": "avrdude -v -p atmega328pb -C $PROJECT_PACKAGES_DIR/tool-avrdude/avrdude.conf -c arduino -b $UPLOAD_SPEED -v -D -P $UPLOAD_PORT -U flash:w:$SOURCE:i"
    },
    "url": "https://github.com/amperka/amperka-boards",
    "vendor": "Amperka"
}
```
5. in platform.ini add following
```
[env:amperka_atmega328pb]
platform = atmelavr
board = Amperka_ATmega328PB
framework = arduino
upload_port = COM7

```
board - name of created json file
upload_port - com port name. Use `serial monitor` to figure out this name. 


issues in platformio https://github.com/platformio/platform-atmelavr/issues/327
