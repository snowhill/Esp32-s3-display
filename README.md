# ESP32-S3 High-Resolution Display Test

ESPHome test configuration for verifying that an **ESP32-S3 (N16R8 — 16 MB Flash / 8 MB PSRAM)** can drive an ST7789V 320×240 TFT display at **full 16-bit colour depth** with complex rendering.

## What This Tests

| Page | Name | What It Proves |
|------|------|----------------|
| 1 | **Colour Test** | Full 16-bit RGB colour bars, smooth rainbow gradient, greyscale ramp — no banding artefacts |
| 2 | **Shapes Test** | Filled & outlined circles, overlapping rectangles, nested outlines, coloured line strips |
| 3 | **Font Test** | Six font sizes (12 px → 36 px) including bold weight — readability at every size |
| 4 | **Performance** | Live FPS, render time (ms), free internal heap, free PSRAM, uptime |
| 5 | **Stress Test** | Concentric circles, 120-cell colour grid, animated diagonal lines — heavy draw-call load |

Pages auto-cycle every 8 seconds.  You can also press **"Next Test Page"** from Home Assistant.

## Key Differences vs. Original ESP32 Config

| | ESP32 (original) | ESP32-S3 N16R8 (this test) |
|---|---|---|
| Colour depth | 8-bit (`eightbitcolor: true`) | Full 16-bit RGB565 |
| Framework | Arduino | ESP-IDF (better PSRAM support) |
| PSRAM | None | 8 MB Octal @ 80 MHz |
| SPI speed | Default | 80 MHz |
| Display buffer | Internal RAM only | PSRAM-backed |

## Wiring

```
ESP32-S3 Pin    Display Pin    Function
────────────    ───────────    ─────────────
GPIO12          SCK            SPI Clock
GPIO11          SDA            SPI Data (MOSI)
GPIO10          CS             Chip Select
GPIO13          DC             Data / Command
GPIO14          RES            Reset
GPIO21          BLK            Backlight (PWM)
3.3 V           VCC            Power
GND             GND            Ground
```

> **Important:** On the N16R8 module, GPIO 26–37 are used by the octal flash/PSRAM interface and must **not** be used for anything else.

## How to Flash

1. Copy `esp32s3-display-test.yaml` into your ESPHome config directory.
2. Create or update your `secrets.yaml` with:
   ```yaml
   wifi_ssid: "YourSSID"
   wifi_password: "YourPassword"
   api_encryption_key: "your-base64-key"
   ota_password: "your-ota-password"
   ```
3. Compile and flash:
   ```bash
   esphome run esp32s3-display-test.yaml
   ```

## What to Look For

- **Colour bars** should be vivid with no visible banding between them.
- **Gradients** should be perfectly smooth — any stepping/posterisation means colour depth is wrong.
- **Fonts** should be crisp at every size with no pixel corruption.
- **FPS** on the Performance page should be steady (typically 5-15 FPS depending on page complexity).
- **Free PSRAM** should show several MB free, confirming the display buffer lives in PSRAM.
- **Stress test** render time should stay under ~100 ms without watchdog resets.
