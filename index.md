# Level 2: Introduction to IoT
## Introduction to NodeMCU
<Content>
![Caption](Img link "Hover name")

## Introduction to Blynk
<Content>
![Caption](Img link "Hover name")

## Introduction to Arduino IoT Cloud
<Content>
![Caption](Img link "Hover name")

## Requirements
* Create an account in Blynk

## Experiments
  1. [LED Control using Blynk app](#blynk)
  2. [LED Control using Arduino IoT Cloud](#arduino)
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

<a name='arduino'></a>
## LED Control using Arduino IoT Cloud
LED is made ON and OFF using a switch in the Arduino IoT platform
## Code
```c++
/* 
  Our code is added to the predefined arduino sketch

  Arduino IoT Cloud Variables description

  The following variables are automatically generated and updated when changes are made to the Thing

  bool led_control;

  Variables which are marked as READ/WRITE in the Cloud Thing will also have functions
  which are called when their values are changed from the Dashboard.
  These functions are generated with the Thing and added at the end of this sketch.
*/

#include "thingProperties.h"

void setup() {
  // Initialize serial and wait for port to open:
  Serial.begin(9600);
  pinMode(D4, OUTPUT); //D4 of NodeMCU is connected to the LED positive
  // This delay gives the chance to wait for a Serial Monitor without blocking if none is found
  delay(1500); 

  // Defined in thingProperties.h
  initProperties();

  // Connect to Arduino IoT Cloud
  ArduinoCloud.begin(ArduinoIoTPreferredConnection);
  
  /*
     The following function allows you to obtain more information
     related to the state of network and IoT Cloud connection and errors
     the higher number the more granular information you’ll get.
     The default is 0 (only errors).
     Maximum is 4
 */
  setDebugMessageLevel(2);
  ArduinoCloud.printDebugInfo();
}

void loop()
{
  ArduinoCloud.update();
  // Our code here 
}

/*
  Since LedControl is READ_WRITE variable, onLedControlChange() is
  executed every time a new value is received from IoT Cloud.
*/
void onLedControlChange()  //To control LED
{
  if (led_control == 1)
  {
    digitalWrite(D4, HIGH);
  }
  else
  {
    digitalWrite(D4, LOW);
  }
}
```
