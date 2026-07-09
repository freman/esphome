# esphome

A collection of [ESPHome](https://esphome.io/) configs for the ESP32/ESP8266 boards I use
around the house - mostly cheap relay/switch modules from AliExpress and similar, turned
into reusable, well-commented YAML.

[ESPHome](https://esphome.io/) is an open-source firmware/tooling system for ESP32, ESP8266,
RP2040, and a few other microcontrollers. You describe a device's hardware and behavior in
YAML, and it compiles that down to real firmware - no C++ required for the common cases. It
integrates natively with [Home Assistant](https://www.home-assistant.io/) (auto-discovery,
entities, diagnostics) but also works standalone via its built-in web server and API.

## Structure

Configs are organized by chip family, then by board:

```
esphome/
├── esp32/
│   └── esp32_relay_x2/
│       ├── esp32_relay_x2.yaml
│       ├── README.md
│       ├── board.jpg
│       └── board_bottom.jpg
└── esp8266/
    └── ...
```

Each board directory contains the YAML config itself, a README with the confirmed pinout and
a rundown of what the config does, and a photo or two of the actual board for reference -
handy since a lot of these cheap boards get resold under different names with different
pinouts despite looking identical.

## Usage

Each config is written to be substitution-driven, so a single YAML file can be reused across
many physical devices without copy-pasting. Reference one directly as an ESPHome
[`packages:`](https://esphome.io/components/packages.html) base and override just the
substitutions you need per device:

```yaml
packages:
  base: github://freman/esphome/esp32/esp32_relay_x2/esp32_relay_x2.yaml@master

substitutions:
  name: "garage-door"
  friendly_name: "Garage Door"
  room: "Garage"
```

See each board's own README for the full list of available substitutions and what they do.