# gps-logger-esp32

## Short Description

This project utilizes an ESP32 microcontroller to receive GPS data and log latitude, longitude, and speed to the Serial Monitor.  It leverages the TinyGPS++ library for efficient GPS parsing.

## Project Setup

### Components:

*   ESP32 Development Board
*   GPS Module (e.g., Ublox NEO-6M)
*   USB Cable
*   Jumper Wires (for connecting GPS module to ESP32)

### Libraries:

*   **TinyGPS++:** This library is crucial for parsing GPS NMEA sentences.  You'll need to install it.  Instructions for this are included in the uploading and running section.

## Uploading and Running Instructions

1.  **Install the necessary libraries:**
    *   Open the Arduino IDE.
    *   Go to **Sketch > Include Library > Manage Libraries**.
    *   Search for "TinyGPS++" and install the library.

2.  **Connect your ESP32:** Connect the ESP32 to your computer via USB.

3.  **Upload the code:** Copy the provided code into a new Arduino sketch. Ensure your GPS module is connected to the correct RX/TX pins.  **Crucially, the code has a missing `TXD2` definition.  Replace `TXD2` with the actual TX pin of your GPS module.**

   ```C++
   #define RXD2 16 // or the correct RX pin
   #define TXD2 17 // or the correct TX pin
   ```
   Choose the appropriate RX and TX pins for your GPS module configuration and update the code accordingly.

4.  **Start the Serial Monitor:** Open the Serial Monitor in the Arduino IDE.  Set the baud rate to 115200.

5.  **Power the GPS module:** Ensure the GPS module is powered and communicating.

**Alternative method for a serial connection outside of the Arduino IDE (if needed):**

Use the `Serial.begin()` function outside of `setup()` only if your project requires serial communication outside the Arduino environment. This prevents any serial conflict during program execution.

```C++
void setup() {
    // ... other setup code
}

void loop() {
  while(1){
     // ... your code
  }
}
```

## Expected Output

The Serial Monitor will display the latitude, longitude, and speed (in km/h) of the GPS location every second.


```
LAT: 37.77493333
LONG: -122.41940000
SPEED (km/h) = 
```


The output format may vary slightly depending on the specific GPS module and environmental conditions.

## Troubleshooting Tips

*   **No GPS data:**
    *   Check the GPS module's power connection.
    *   Ensure the GPS module is communicating correctly with the ESP32.
    *   Verify the correct RX/TX pin assignments.
    *   Verify your GPS module's output, you might need to change the baud rate in the `#define` or the module setup.
*   **Inconsistent data:**
    *   Check for obstructions that might be interfering with GPS signal reception.
    *   Ensure the GPS module is in a location with good satellite visibility.
*   **Error messages:**
    *   Review your code for syntax errors and ensure your libraries are installed properly.


## Additional Considerations

*   **Data logging:** For more complex projects, consider saving the GPS data to a file for later analysis using SD cards or other data storage solutions.

*   **Error handling:** Implement error handling (e.g., checking for `gps.location.isValid()`) for robustness in case of GPS signal loss or issues.



## Contributing and Feedback

This project was developed with the help of ChatGPT, Reddit and Arduino forum communities.  If you have suggestions or improvements, please feel free to contribute to the project or open a discussion issue on GitHub.

```
