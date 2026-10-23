# IoT-Based-Hazardous-Gas-Detection-System
An Arduino-based gas detection system that uses an MQ-series sensor to monitor gas levels. When readings exceed a predefined threshold, a buzzer and red LED alert users to potential hazards. A green LED indicates readings below the threshold, while the Serial Monitor displays real-time sensor values.

  /*
  Project: IoT Based Hazardous Gas Detection System
  Board: Arduino UNO
  Sensor: MQ-series gas sensor module
*/

const int GAS_SENSOR_PIN = A0;
const int BUZZER_PIN = 8;
const int RED_LED_PIN = 7;
const int GREEN_LED_PIN = 6;

// Adjust this threshold after testing your sensor
const int GAS_THRESHOLD = 400;

void setup() {
  pinMode(GAS_SENSOR_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(RED_LED_PIN, OUTPUT);
  pinMode(GREEN_LED_PIN, OUTPUT);

  digitalWrite(BUZZER_PIN, LOW);
  digitalWrite(RED_LED_PIN, LOW);
  digitalWrite(GREEN_LED_PIN, HIGH);

  Serial.begin(9600);

  Serial.println("Hazardous Gas Detection System");
  Serial.println("Allow MQ sensor to warm up.");
}

void loop() {
  int gasValue = analogRead(GAS_SENSOR_PIN);

  Serial.print("Gas sensor reading: ");
  Serial.println(gasValue);

  if (gasValue >= GAS_THRESHOLD) {
    digitalWrite(BUZZER_PIN, HIGH);
    digitalWrite(RED_LED_PIN, HIGH);
    digitalWrite(GREEN_LED_PIN, LOW);

    Serial.println("WARNING: Gas level above set threshold!");
  } else {
    digitalWrite(BUZZER_PIN, LOW);
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, HIGH);

    Serial.println("Reading below set threshold.");
  }

  delay(500);
}
