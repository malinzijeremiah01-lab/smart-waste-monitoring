## Wokwi Simulation

https://wokwi.com/projects/459550497732356097
# smart-waste-monitoring
IoT-based waste monitoring system for university
// Smart Dustbin using Ultrasonic Sensor

// Pin definitions


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
  // Send ultrasonic pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  
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

  // Check bin status
  if (distance <= threshold) {
    digitalWrite(ledPin, HIGH);     // Turn ON LED
    digitalWrite(buzzerPin, HIGH);  // Turn ON buzzer
    Serial.println("BIN FULL!");
  } else {
    digitalWrite(ledPin, LOW);      // Turn OFF LED
    digitalWrite(buzzerPin, LOW);   // Turn OFF buzzer
  }

  delay(1000); // small delay
}
