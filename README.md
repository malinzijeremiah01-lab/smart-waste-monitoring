# smart-waste-monitoring
IoT-based waste monitoring system for university
// Smart Dustbin using Ultrasonic Sensor

// Pin definitions
const int trigPin = 9;
const int echoPin = 10;
const int ledPin = 6;
const int buzzerPin = 7;

// Variables
long duration;
int distance;

// Set threshold (in cm)
int threshold = 10; // Adjust depending on bin size

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);

  Serial.begin(9600);
}

void loop() {
  // Clear trigger
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Send pulse
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read echo
  duration = pulseIn(echoPin, HIGH);

  // Calculate distance (cm)
  distance = duration * 0.034 / 2;

  // Display distance
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Check if bin is full
  if (distance <= threshold) {
    digitalWrite(ledPin, HIGH);     // Turn ON LED
    digitalWrite(buzzerPin, HIGH);  // Turn ON buzzer
    Serial.println("BIN FULL!");
  } else {
    digitalWrite(ledPin, LOW);      // Turn OFF LED
    digitalWrite(buzzerPin, LOW);   // Turn OFF buzzer
  }

  delay(500); // small delay
}
