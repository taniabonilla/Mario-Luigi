#include <Servo.h>

int counter1 = 0;     // declaracions de variable "contador1"
int counter2 = 0;     // declaracions de variable "contador2"
int b1 = 9;           // declaracions de variable "botó1"
int b2 = 6;           // declaracions de variable "botó1"
int led1 = 8;         // declaracions de leds
int led2 = A1;         // declaracions de leds
int led3 = 10;         // declaracions de leds
int led4 = A2;         // declaracions de leds
int led5 = 11;         // declaracions de leds
int led6 = A3;         // declaracions de leds
int led7 = 12;         // declaracions de leds
int led8 = A4;         // declaracions de leds
int led9 = 13;         // declaracions de leds
int led10 = A5;         // declaracions de leds
int servo1 = 3;         // declaracions de servo
int servo2 = 5;         // declaracions de servo
int angulo = 90;         // declaracions de l'angle

int lastState1 = LOW;
int lastState2 = LOW;

Servo servomotor1;         // activació del servo1
Servo servomotor2;         // activació del servo2

void setup() {
  // put your setup code here, to run once:
  servomotor1.attach(3); //Pin 3 del Arduino
  servomotor2.attach(5); //Pin 5 del Arduino
  pinMode (b1, INPUT);
  pinMode (b2, INPUT);
  pinMode (led1, OUTPUT);
  pinMode (led2, OUTPUT);
  pinMode (led3, OUTPUT);
  pinMode (led4, OUTPUT);
  pinMode (led5, OUTPUT);
  pinMode (led6, OUTPUT);
  pinMode (led7, OUTPUT);
  pinMode (led8, OUTPUT);
  pinMode (led9, OUTPUT);
  pinMode (led10, OUTPUT);
  pinMode (servo1, OUTPUT);
  pinMode (servo2, OUTPUT);

  servomotor1.write(90); //posiciona el servo inicialmente en la mitad (90Âº)
  servomotor2.write(90); //posiciona el servo inicialmente en la mitad (90Âº)

  Serial.begin(9600);
  Serial.println("Ready...");
  delay(1500);

}

void loop() {
  int buttonState1 = digitalRead(b1);
  int buttonState2 = digitalRead(b2);
  if (buttonState1 == LOW && buttonState2 == LOW) {

    digitalWrite(led1, HIGH);
    digitalWrite(led2, HIGH);
    digitalWrite(led3, HIGH);
    digitalWrite(led4, HIGH);
    digitalWrite(led5, HIGH);
    digitalWrite(led6, HIGH);
    digitalWrite(led7, HIGH);
    digitalWrite(led8, HIGH);
    digitalWrite(led9, HIGH);
    digitalWrite(led10, HIGH);
    delay(1000);
  }
  if (buttonState1 == HIGH && buttonState2 == HIGH) {
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    delay(1000);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
    delay(1000);
    digitalWrite(led5, LOW);
    digitalWrite(led6, LOW);
    delay(1000);
    digitalWrite(led7, LOW);
    digitalWrite(led8, LOW);
    delay(1000);
    digitalWrite(led9, LOW);
    digitalWrite(led10, LOW);
    Serial.println("Start!");
  }

  if (buttonState1 == LOW && lastState1 == HIGH) {
    counter1 ++;
    Serial.print("Player 1 has ");
    Serial.println(counter1);
    if (counter1 == 5) {
      digitalWrite(led1, HIGH);
    }
    if (counter1 == 10) {
      digitalWrite(led3, HIGH);
    }
    if (counter1 == 15) {
      digitalWrite(led5, HIGH);
    }
    if (counter1 == 20) {
      digitalWrite(led7, HIGH);
    }
    if (counter1 == 25) {
      digitalWrite(led9, HIGH);
      Serial.println("Player 1 wins!");

      servomotor1.write(0);
      delay (5000);
      counter1 = 0;
      digitalWrite(led1, LOW);
      digitalWrite(led3, LOW);
      digitalWrite(led5, LOW);
      digitalWrite(led7, LOW);
      digitalWrite(led9, LOW);
      Serial.println("Ready...");
      servomotor1.write(90);
      delay(1500);
      Serial.println("Start!");
    }
  }

  if (buttonState2 == LOW && lastState2 == HIGH) {
    counter2 ++;
    Serial.print("Player 2 has ");
    Serial.println(counter2);
    if (counter2 == 5) {
      digitalWrite(led2, HIGH);
    }
    if (counter2 == 10) {
      digitalWrite(led4, HIGH);
    }
    if (counter2 == 15) {
      digitalWrite(led6, HIGH);
    }
    if (counter1 == 20) {
      digitalWrite(led8, HIGH);
    }
    if (counter1 == 25) {
      digitalWrite(led10, HIGH);
      Serial.println("Player 2 wins!");

      servomotor2.write(0);
      delay (5000);
      counter2 = 0;
      digitalWrite(led2, LOW);
      digitalWrite(led4, LOW);
      digitalWrite(led6, LOW);
      digitalWrite(led8, LOW);
      digitalWrite(led10, LOW);
      Serial.println("Ready...");
      servomotor2.write(90);
      delay(1500);
      Serial.println("Start!");
    }
  }

  lastState1 = buttonState1;
  lastState2 = buttonState2;

}
