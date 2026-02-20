# ESP32-S3 Display Quality Test

This repository includes a minimal ESPHome test config to validate
high-quality display rendering on an ESP32-S3 16N8 board.

## Purpose

- Test only the TFT display performance and visual quality
- No sensors, no incubator logic, no extra components
- Full-screen animated stress pattern at ~30 FPS

## Test YAML

- `esp32-s3-display-hq-test.yaml`

## Hardware Target

- MCU: ESP32-S3 (16MB Flash + 8MB PSRAM)
- Display driver: ST7789V
- Framework: ESP-IDF (set in YAML)

## Current Pin Mapping (in YAML)

- `SPI CLK`  -> `GPIO18`
- `SPI MOSI` -> `GPIO11`
- `TFT CS`   -> `GPIO10`
- `TFT DC`   -> `GPIO14`
- `TFT RST`  -> `GPIO4`

If your board uses different pins, edit only these pins in the YAML.

## Run / Compile

```bash
esphome config esp32-s3-display-hq-test.yaml
esphome compile esp32-s3-display-hq-test.yaml
```

## Flash

USB flash:

```bash
esphome run esp32-s3-display-hq-test.yaml
```

OTA flash (if already online):

```bash
esphome upload esp32-s3-display-hq-test.yaml --device <ip-address>
```

## Notes

- Color mode is 16-bit (`eightbitcolor: false`) for better quality.
- Update interval is `33ms` to stress display throughput.
