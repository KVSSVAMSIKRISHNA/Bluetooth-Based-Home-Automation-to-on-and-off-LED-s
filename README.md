#include "BluetoothSerial.h" 
// init Class:
BluetoothSerial ESP_BT; 
// init PINs: assign any pin on ESP32
int led_pin_1 = 4;
int led_pin_2 = 0;
int led_pin_3 = 2; // On some ESP32 pin 2 is an internal LED, mine did not have one
// Parameters for Bluetooth interface
int incoming;
void setup() {
 Serial.begin(19200);
 ESP_BT.begin("KLU"); //Name of your Bluetooth interface -> will show up on your phone
 pinMode (led_pin_1, OUTPUT);
 pinMode (led_pin_2, OUTPUT);
 pinMode (led_pin_3, OUTPUT);
}
void loop() {
 
 // -------------------- Receive Bluetooth signal ----------------------
 if (ESP_BT.available()) 
 {
 incoming = ESP_BT.read(); //Read what we receive 
 // separate button ID from button value -> button ID is 10, 20, 30, etc, value is 1 or 0
 int button = floor(incoming / 10);
 int value = incoming % 10;
 
 switch (button) {
 case 1: 
 Serial.print("Button 1:"); Serial.println(value);
 digitalWrite(led_pin_1, value);
 break;
 case 2: 
 Serial.print("Button 2:"); Serial.println(value);
 digitalWrite(led_pin_2, value);
 break;
 case 3: 
 Serial.print("Button 3:"); Serial.println(value);
 digitalWrite(led_pin_3, value);
 break;
 }
 }
}
