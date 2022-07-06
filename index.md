# Level 2: Introduction to IoT
## Introduction to NodeMCU
<Content>
![Caption](Img link "Hover name")

## Introduction to Blynk
<Content>
![Caption](Img link "Hover name")

## Requirements
<Content>

## Experiments
  1. [LED Control using Blynk app](#blynk)
  2. [head.](#traffic)
  3. [head.](#chase)
  4. [head.](#button)
  5. [head.](#buzzer)
  6. [head.](#rgb)
  7. [head.](#ldr)
  8. [head.](#flame)
  9. [head.](#lm35)
  10. [head.](#ir)
  11. [head.](#pot)

<a name='blynk'></a>
## LED Control using Blynk app
LED is made ON and OFF using a switch in the Blynk IoT platform
## Code
```c++
#define BLYNK_TEMPLATE_ID   "TMPLHdKB6u23"
#define BLYNK_DEVICE_NAME   "LED control"
#define BLYNK_AUTH_TOKEN    "GK0ilSKAGX1_fz0oAJOw8psfizAcbc2h"

#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>  
#include <BlynkSimpleEsp8266.h>
 

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "m31";  // Wifi Username
char pass[] = "password";  // Wifi password

int ledpin = D4; //LED is connected to D4 pin of NodeMCU
void setup()
{     
  Serial.begin(115200);
  Blynk.begin(auth, ssid, pass);    
  pinMode(ledpin,OUTPUT);
}

BLYNK_WRITE(V0) //LED control using virtual pin
{   
  int value = param.asInt(); // Get value as integer
  digitalWrite(ledpin, value);}

void loop()
{
  Blynk.run(); 
}
```
