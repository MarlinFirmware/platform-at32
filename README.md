# platform-at32

Arduino platform wrapper for AT32: a PlatformIO platform for Artery AT32F403A / AT32F407 MCUs using the Arduino framework, made for [Marlin Firmware](https://github.com/MarlinFirmware/Marlin).

The framework is [MarlinFirmware/ArduinoCore-AT32F4](https://github.com/MarlinFirmware/ArduinoCore-AT32F4) (branch `marlin`), a fork of [rizacelik/ArduinoCore-AT32F4](https://github.com/rizacelik/ArduinoCore-AT32F4). `platform.json` pins it to a release tag.

## Contents

- `platform.json` — toolchain and framework packages
- `builder/main.py` — toolchain setup, ELF to BIN/HEX, size report
- `builder/frameworks/arduino.py` — runs the build script inside the framework package (`tools/platformio/platformio-build-arduino.py`), which holds the include paths, compile/link flags and driver sources
- `boards/` — board definitions

| Board | MCU | Flash | RAM | Linker script |
| --- | --- | --- | --- | --- |
| `at32f403argt7` | AT32F403ARGT7 | 1 MB | 224 KB | `AT32F403AxG_FLASH.ld` |
| `at32f403arct7` | AT32F403ARCT7 | 256 KB | 224 KB | `AT32F403AxR_FLASH.ld` |
| `at32f407rct7` | AT32F407RCT7 | 256 KB | 96 KB | `AT32F407xC_FLASH.ld` |

All boards use the `marlin_at32f403` variant from the framework.

## Usage

```ini
[env:my_board]
platform  = https://github.com/MarlinFirmware/platform-at32/archive/1.0.0.zip
framework = arduino
board     = at32f403argt7
```

Uploading is not implemented; flash the `.bin` with the board's bootloader (SD card) or an external programmer.

## Releases

Framework changes are made in the ArduinoCore-AT32F4 fork and tagged there. Update the framework URL in `platform.json`, bump `version`, tag this repo, and point Marlin's `ini/at32.ini` at the new tag.

## License

GPL-3.0. See `LICENSE`.
