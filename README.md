# ESP32-S3 Display Quality Test

Minimal ESPHome configuration to test high-resolution display capability on **ESP32-S3 with 16MB Flash and 8MB PSRAM**.

## What it tests
- **Full 16-bit color** (65K colors) - no 8-bit color reduction
- **320×240 ST7789V display** - color gradients, text sharpness, FPS
- **Display performance** - real-time FPS and free RAM display

## Hardware
- **Board**: ESP32-S3 (16MB flash, 8MB PSRAM)
- **Display**: ST7789V 240×320, SPI
- **Pins** (match your incubator display):
  - SPI CLK: GPIO18, MOSI: GPIO23
  - CS: GPIO27, DC: GPIO14, Reset: GPIO4

## Usage
1. Copy `esp32-s3-display-quality-test.yaml` to your ESPHome configs
2. (Optional) Uncomment WiFi/OTA section and add credentials for wireless flashing
3. Build and flash: `esphome run esp32-s3-display-quality-test.yaml`
4. Or flash via USB: `esphome run esp32-s3-display-quality-test.yaml --device /dev/ttyUSB0`

## Expected result
- Color gradient background
- Color bars (red, green, blue, cyan, magenta, yellow, white, black)
- Info panel with FPS and free RAM
- Sharp text rendering
- "ESP32-S3 16MB/8MB PSRAM OK" status at bottom