# flejebazote
La clabasa maligna

#include <Servo.h>

#include <HCSR04.h>

UltraSonicDistanceSensor distanceSensor(7, 8);  // Initialize sensor that uses digital pins 13 and 12.


int led1 = 5; // LED 1
int led2 = 6; // LED2
int led4 = 3; // LED4

Servo servoMotor;
Servo servoMotor2;

int duration, cm; // variables to store values from ping sensor

void setup() {

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led4, OUTPUT);
  Serial.begin(9600);
  servoMotor.attach(9);
  servoMotor2.attach(10);

}

void loop() {

  cm = distanceSensor.measureDistanceCm();

  Serial.println(cm);

  if (cm <= 30) // if somtehing is sensed within a distance of 30 then light up eyes
  {
    servoMotor.write(0);
    delay(150);
    servoMotor.write(120);
    servoMotor2.write(0);
    delay(250);
    servoMotor2.write(60);
    for (int i = 0; i < 155; i++) // switch on the LEDS
    {
      analogWrite(led1, i);
      analogWrite(led2, i);
      analogWrite(led4, i);
      delay(4);
    }
    analogWrite(led1, LOW); // switch off the LEDS
    analogWrite(led2, LOW);
    analogWrite(led4, LOW);
  }
}
