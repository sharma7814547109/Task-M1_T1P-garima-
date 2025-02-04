# Task-M1_T1P-garima-

const int sigPin = 2;   // Signal pin for PING))) sensor
const int ledPin = 13;  // Built-in LED on Arduino Nano

void setup() {
    pinMode(sigPin, OUTPUT);  // Set signal pin as output
    pinMode(ledPin, OUTPUT);  // Set LED pin as output
    Serial.begin(9600);       // Start serial communication
}

void loop() {
    // Trigger the sensor
    pinMode(sigPin, OUTPUT);
    digitalWrite(sigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(sigPin, HIGH);
    delayMicroseconds(5);
    digitalWrite(sigPin, LOW);

    // Read the echo time
    pinMode(sigPin, INPUT);
    long duration = pulseIn(sigPin, HIGH);

    // Calculate distance in cm
    int distance = duration / 29 / 2;

    // Print distance to Serial Monitor
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    // Turn LED ON if distance is less than 10 cm
    if (distance > 0 && distance < 100) {
        digitalWrite(ledPin, HIGH);
        Serial.println("LED ON - Object Detected!");
    } else {
        digitalWrite(ledPin, LOW);
        Serial.println("LED OFF - No Object Nearby");
    }

    delay(500);  // Delay for readability
}
