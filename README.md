# ESP32 + BME280 MQTT IoT Sensor Driver

This is the driver code for an [ESP32](https://en.wikipedia.org/wiki/ESP32) micro-controller connected to a [BM280](https://www.bosch-sensortec.com/products/environmental-sensors/humidity-sensors-bme280/) sensor which publishes temperature, humidity and pressure data to my [Home IoT Network](https://github.com/robingread/home_weather_station) via [MQTT](https://en.wikipedia.org/wiki/MQTT).

The project uses the [VSCode](https://code.visualstudio.com/) [PlatformIO](https://platformio.org/) extension to build and flash the binaries to the ESP32. Communication to the BME280 is done via I2C.

## Hardware

This project has been developed and tested on the following hardware.

- [A-Z Delivery ESP32 DevKit C V2 (ESP32 WROOM-32)](https://www.az-delivery.uk/products/esp32-developmentboard)
- [Pimoroni BME280 Breakout Board](https://shop.pimoroni.com/products/bme280-breakout)

## MQTT Senor Data Format

The readings from the sensor are published via MQTT when a trigger signal is received. This allows the frequency and (rough) synchronization of readings to be controller via a signal point.

Data on the topic is formatted as a JSON string, for example:

```json
{
    "device_id": "esp32",
    "readings": [
        {"name": "pressure", "value": 0.0},     // Units: hectoPascals (hPa)
        {"name": "humidity", "value": 0.0},     // Units: Percentage
        {"name": "temperature", "value": 0.0},  // Units: Degrees Celsius
    ]
}
```

## Configuration

The credentials for the WiFi and MQTT should be added to the `src/credentials.h` file, using the `credentials.h.template` as a template file.

This file requires values for the following parameters:

| Parameter | Type | Description |
|---|---|---|
| `BME280_I2C_ADDR` | `hex` | I2C address of the BME280 sensor (e.g., `0x76`, `0x77`).
| `DEVICE_ID` | `str` | Unique (user defined) Device ID.
| `MQTT_HOST` | `str` | IP Address or URL of the MQTT Broker to connect to (e.g., `192.168.0.2`).
| `MQTT_PORT` | `int` | Port ID for the MQTT Broker (e.g., `1883`).
| `MQTT_USERNAME` | `str` | Username the MQTT Broker connection.
| `MQTT_PASSWORD` | `str` | User password for the MQTT Broker connection.
| `WIFI_SSID` | `str` | SSID of the WiFi network the ESP32 should connect to.
| `WIFI_PASSWORD` | `str` | Password for the WiFi network.
