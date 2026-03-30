
#define BLYNK_PRINT Serial

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "YOUR_BLYNK_AUTH_TOKEN";
char ssid[] = "Energy Meter";
char pass[] = "passw";

#define VOLTAGE_PIN A0   // ZMPT101B
#define CURRENT_PIN A0   // CT sensor (same pin via circuit)

BlynkTimer timer;

// Calibration values (adjust during testing)
float voltageCal = 230.0;  
float currentCal = 5.0;    

void sendData() {
  int sensorValue = analogRead(A0);

  // Convert ADC to voltage (0–3.3V)
  float adcVoltage = sensorValue * (3.3 / 1023.0);

  // Approximate calculations (needs calibration)
  float voltage = adcVoltage * voltageCal;
  float current = adcVoltage * currentCal;

  float power = voltage * current;

  Serial.print("Voltage: "); Serial.println(voltage);
  Serial.print("Current: "); Serial.println(current);
  Serial.print("Power: "); Serial.println(power);

  // Send to Blynk
  Blynk.virtualWrite(V0, voltage);
  Blynk.virtualWrite(V1, current);
  Blynk.virtualWrite(V2, power);
}

void setup() {
  Serial.begin(9600);
  Blynk.begin(auth, ssid, pass);

  timer.setInterval(2000L, sendData);
}

void loop() {
  Blynk.run();
  timer.run();
}
