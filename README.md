# Smart-Blind-Assistance-System-
// Pin Definitions
#define trigPin 9
#define echoPin 10
#define buzzer 8

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // Clear trigPin
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

  Serial.print("Distance: ");
  Serial.println(distance);

  // Condition for buzzer
  if (distance > 0 && distance <= 30) {
    digitalWrite(buzzer, HIGH); // continuous beep (very close)
  }
  else if (distance > 30 && distance <= 100) {
    digitalWrite(buzzer, HIGH);
    delay(200);
    digitalWrite(buzzer, LOW);
    delay(200); // slow beep
  }
  else {
    digitalWrite(buzzer, LOW); // no obstacle
  }

  delay(100);
}
