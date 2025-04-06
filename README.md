```markdown
# gps-logger-esp32

A simple GPS logger project for ESP32 using the TinyGPS++ library. This project reads data from a GPS module via Serial2 and prints the latitude, longitude, and speed to the Serial Monitor.

## Description

This project provides a basic framework for logging GPS data using an ESP32 and a GPS module. It initializes Serial2 to communicate with the GPS module, reads NMEA sentences, parses them using the TinyGPS++ library, and displays the latitude, longitude, and speed on the Serial Monitor. It's a starting point for building more complex GPS-based applications like tracking devices, navigation systems, or geocaching tools.

## Setup Instructions

### Components Required

*   ESP32 Development Board
*   GPS Module (e.g., GY-GPS6MV2, NEO-6M, or similar)
*   Jumper Wires

### Wiring

Connect the GPS module to the ESP32 as follows:

| GPS Module | ESP32 |
|------------|-------|
| VCC        | 3.3V  |
| GND        | GND   |
| TX         | RX2 (GPIO 16 or similar configurable in code)  *See Important Note Below*
| RX         | TX2 (GPIO 17 or similar configurable in code)  *See Important Note Below*

**Important Notes about RX2 and TX2 Pins:**

*   The `gpsSerial.begin()` function in the code allows you to define the RX and TX pins to be used for Serial2.  The default code uses GPIO16 (RX2) and GPIO17 (TX2) which is defined as RXD2 and TXD2. This project uses RXD2 as 1, but TXD2 is not correctly defined. Edit the `#define TXD2` statement to properly define the pin you will use.
*   Verify the pinout of your specific ESP32 development board. Some boards may have different default assignments or limitations.
*   The ESP32's Serial2 pins might also be connected to other functions on the board, so review the documentation.

### Library Installation

1.  Open the Arduino IDE.
2.  Go to Sketch > Include Library > Manage Libraries.
3.  Search for "TinyGPS++" by Mikal Hart.
4.  Install the latest version of the TinyGPS++ library.

## Uploading and Running Instructions

1.  Connect the ESP32 to your computer via USB.
2.  Open the `gps-logger-esp32.ino` file in the Arduino IDE.
3.  **Important:** Modify the `#define TXD2` statement in the code to reflect the actual GPIO pin you connected the GPS TX to on the ESP32.
4.  Select the correct board and port in the Arduino IDE (Tools > Board > ESP32 Dev Module or similar, and Tools > Port > COMx or /dev/ttyACMx).
5.  Click the "Upload" button to upload the code to the ESP32.
6.  Open the Serial Monitor (Tools > Serial Monitor) and set the baud rate to 115200.
7.  You should see "Serial 2 started at 9600 baud rate" printed in the Serial Monitor.
8.  Wait for the GPS module to acquire a satellite fix.  This may take several minutes, especially when first used or after long periods of inactivity.
9.  Once a fix is acquired, the latitude, longitude, and speed will be printed to the Serial Monitor.

## Expected Output

The Serial Monitor should display the following output (after the GPS module acquires a satellite fix):

```
Serial 2 started at 9600 baud rate
LAT: 37.774900
LONG: -122.419400
SPEED (km/h) = 10.50
```

The latitude, longitude, and speed values will change based on the GPS location and movement.

## Troubleshooting Tips

*   **No Output:**
    *   Double-check the wiring between the GPS module and the ESP32.
    *   Ensure that the GPS module is powered correctly (usually 3.3V).
    *   Make sure the correct board and port are selected in the Arduino IDE.
    *   Verify the `TXD2` define is using the correct GPIO pin number.
    *   Ensure the GPS module has a clear view of the sky for satellite acquisition.  Initial fix may take a long time.
    *   Check that the baud rate in the code (GPS_BAUD) matches the baud rate of your GPS module (usually 9600).
    *   Try swapping the RX and TX wires in case they are reversed.

*   **Incorrect Data:**
    *   The GPS module may not have a satellite fix yet. Wait longer for it to acquire a fix.
    *   Ensure that the GPS module is configured correctly (if applicable).
    *   Verify that the TinyGPS++ library is installed correctly.

*   **Serial Monitor Issues:**
    *   Ensure the Serial Monitor's baud rate is set to 115200.
    *   Close and reopen the Serial Monitor if it's not displaying data.

## Acknowledgments

This project was created with the help of the following resources:

*   TinyGPS++ library documentation: [http://arduiniana.org/libraries/tinygpsplus/](http://arduiniana.org/libraries/tinygpsplus/)
*   Chat GPT: For assistance in creating the README and code structure.
*   Arduino Forums:  Discussions and solutions related to GPS and Serial communication on ESP32.
*   Reddit:  Information and community support related to ESP32 and GPS projects.
```