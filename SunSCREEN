// SunSCREEN

// Include libraries
#include <millisDelay.h>
#include <Wire.h>
#include "Adafruit_VEML6070.h"

Adafruit_VEML6070 uv = Adafruit_VEML6070();

millisDelay buzzDelay;

// Define variables
int greenLED = 7;
int yellowLED = 6;
int redLED = 5;

int s1 = 3;
int buzz = 4;

// Setup
void setup(){
  Serial.begin(9600);
  uv.begin(VEML6070_1_T);

  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);

  pinMode(s1, INPUT_PULLUP);
  pinMode(buzz, OUTPUT);
  
}

// Loop
void loop(){
  // Define variables
  int switchVal = digitalRead(s1);

  // Print to Serial Monitor
  Serial.print("The value of the switch: ");
  Serial.println(switchVal);

  Serial.print("UV detected: ");
  Serial.println(uv.readUV());

   // IF the uv sensor is in the clear.
  if (uv.readUV() >= 0 && uv.readUV()  < 150){
    // Turn off any on lights
    digitalWrite(yellowLED, LOW);
    digitalWrite(redLED, LOW);
     
    digitalWrite(greenLED, HIGH);

    noTone(buzz);
   }

  // IF the uv sensor recommends sunscreen use
  else if (uv.readUV() >= 150 && uv.readUV() < 295){
    // Turn off any on lights
    digitalWrite(greenLED, LOW);
    digitalWrite(redLED, LOW);
     
    digitalWrite(yellowLED, HIGH);

    noTone(buzz);
   }

   // IF the uv sensor REQUIRES sunscreen use
  else if (uv.readUV() >= 295){
    // Turn off any on lights
    digitalWrite(greenLED, LOW);
    digitalWrite(yellowLED, LOW);
     
    digitalWrite(redLED, HIGH);


    // Alert Tone
    if (switchVal == HIGH){
      tone(buzz, 1800);
      delay(450);
      tone(buzz, 900);
      delay(400);
    }
    else{
      noTone(buzz);
    }
  }
}
