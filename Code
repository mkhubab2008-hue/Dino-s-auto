#include <Servo.h>
Servo myservo;
int light;

void setup() {
  pinMode(8, OUTPUT);
  myservo.attach(8);
  Serial.begin(9600);
}

void loop() {
  light = analogRead(A0);
  if (light > 330) {
    myservo.write(90);
  }
  else {
    myservo.write(0);
  }
  Serial.println(light);
}
