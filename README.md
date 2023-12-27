# Rotary-Encoder-Input-with-Arduino-
Read input from a rotary encoder and display the count on the serial monitor.
#define encoderPinA 2
#define encoderPinB 3

volatile int encoderPos = 0;
int aState;
int aLastState;

void setup() {
  pinMode(encoderPinA, INPUT_PULLUP);
  pinMode(encoderPinB, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(encoderPinA), updateEncoder, CHANGE);
  aLastState = digitalRead(encoderPinA);
  Serial.begin(9600);
}

void loop() {
  aState = digitalRead(encoderPinA);
  if (aState != aLastState) {
    if (digitalRead(encoderPinB) != aState) {
      encoderPos++;
    } else {
      encoderPos--;
    }
    Serial.println(encoderPos);
  }
  aLastState = aState;
}

void updateEncoder() {}
