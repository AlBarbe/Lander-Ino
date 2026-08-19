# Lander Ino

A desktop weather station and clock built into a hand-made, lunar-lander-shaped wire chassis, powered by an ESP32.

## Overview

The display shows:
- Current time and date, kept in sync over Wi-Fi via NTP
- Indoor temperature and pressure, read from an onboard BMP280 sensor
- Outdoor weather (temperature, humidity, description, sunrise/sunset, wind speed) fetched from the [OpenWeatherMap](https://openweathermap.org/api) API

Everything is drawn on a small color TFT display mounted on top of a wireframe "lander" frame with four legs, giving the whole thing the look of a miniature lunar lander.

> This is the first-generation build. See [Lander-Ino-V2](https://github.com/AlBarbe/Lander-Ino-V2) for the second-generation version, which adds a BME680 environmental sensor, touch controls, and a dimmable backlight.

## Hardware

- ESP32 dev board (`nodemcu-32s`)
- TFT display (ST7735/ST7789) driven by [TFT_eSPI](https://github.com/Bodmer/TFT_eSPI)
- BMP280 temperature/pressure sensor (I2C, address `0x76`)
- Custom hand-bent wire "lander" chassis

## Firmware

Built with [PlatformIO](https://platformio.org/) (`framework = arduino`).

Dependencies (see `platformio.ini`):
- Adafruit ST7735 and ST7789 Library
- TFT_eSPI
- Adafruit BMP280 Library
- ArduinoJson

## Project structure

```
src/main.cpp                  setup/loop: Wi-Fi, sensor + weather refresh timers
include/My_Lander_Display.h   Lander_Display class, draws clock/date/sensor/weather on the TFT
include/My_Weather.h          weatherData class, parses the OpenWeatherMap JSON payload
include/My_Time_Config.h      MyClock class, NTP time sync + day/month name helpers
```

## Configuration

Before building and flashing, edit `src/main.cpp` and set your own values:

```cpp
#define WIFI_SSID       "WIFI_NAME"
#define WIFI_PASSWORD   "WIFI_PASSWORD"

String openWeatherMapApiKey = "API-KEY";
String city = "YOUR_CITY";
String countryCode = "YOUR_COUNTRY_CODE";
```

## Build & flash

```bash
pio run --target upload
```
