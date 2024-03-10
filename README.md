#include <BluetoothSerial.h>

#define RELAY_PIN 12  // Pin connected to the relay module

BluetoothSerial SerialBT;

void setup() {
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, LOW); // Turn off the relay initially
  
  Serial.begin(115200); // For debugging
  SerialBT.begin("ESP32_BT_Control"); // Bluetooth serial communication initialization
}

void loop() {
  if (SerialBT.available()) {
    char command = SerialBT.read(); // Read the command from Bluetooth

    // Check the received command and take action accordingly
    switch (command) {
      case '1':
        digitalWrite(RELAY_PIN, HIGH); // Turn on the relay
        Serial.println("Relay turned ON");
        break;
      case '0':
        digitalWrite(RELAY_PIN, LOW); // Turn off the relay
        Serial.println("Relay turned OFF");
        break;
      default:
        Serial.println("Invalid command");
        break;
    }
  }
}
