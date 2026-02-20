# ESP32‑S3 display quality test

This repo includes a minimal ESPHome configuration to stress-test an SPI TFT at **full 16‑bit color (RGB565)** on an **ESP32‑S3 (16MB flash / 8MB PSRAM modules such as “16N8”)**.

## Files

- `esp32-s3-st7789v-high-quality-display-test.yaml`: display-only stress test (no sensors / no incubator logic)

## How to use

1. Open `esp32-s3-st7789v-high-quality-display-test.yaml`
2. Edit the `substitutions:` pinout (`tft_*`) + `tft_width` / `tft_height` / `tft_rotation` to match your display.
3. Compile/flash with ESPHome.

### Notes

- The test runs around **30 FPS** by default (`update_interval: 33ms`). For more stress, try `16ms`.
- If you do **not** have a controllable backlight pin, remove the `output:` and `light:` sections and the `on_boot:` backlight call.