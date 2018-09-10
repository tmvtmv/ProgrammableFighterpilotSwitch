# Programmable Fighterpilot Switch
Just a fun project using the Teensy board firing keystrokes to your computer when the fire-button is pressed.


## Schematic
![SchematicImage](https://github.com/tmvtmv/ProgrammableFighterpilotSwitch/blob/master/images/schematic.jpg)

## Requirements
Any Teensy board (See https://www.pjrc.com/store/index.html)
See https://www.pjrc.com/teensy/td_keyboard.html for all the keyboard options and possibilities.

## Example code
```
/*
  ArmAndGo v0.9 (20180830) by Ties Voskamp (ties@voskamp.nu)

  This script waits for the ARMED-switch to be turned on and
  types the KeyboardMessage when the "GO"-button is pushed.

  Requirements:
  Any Teensy board (See https://www.pjrc.com/store/index.html)
  See https://www.pjrc.com/teensy/td_keyboard.html for all the keyboard options and possibilities.
*/

// Constants

// The keyboard types this after switch is set to ARMED and the Push button is pressed.
const String KeyboardMessage = "Hello world!";  

// Settings to identify/configure used PINs:
const int ArmedPin =  2;      // the number of the ARMED-switch pin
const int PushPin  =  3;      // the number of the push button pin
const int ledPin   = 13;      // the number of the LED pin

// Variables
int ArmedState     =  0;          // variable for reading the ARMED-switch status
int PushState      =  0;          // variable for reading the push button status

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);      
  // initialize the pushbutton pin as an input:
  pinMode(ArmedPin, INPUT);
  // initialize the pushbutton pin as an input:
  pinMode(PushPin, INPUT);     
}

void loop(){
  // read the state of the ARMED switch value:
  ArmedState = digitalRead(ArmedPin);

  // check if the ARMED switch is ON.
  // if it is, the ArmedState is HIGH:
  if (ArmedState == HIGH) {     
    // turn LED on:    
    digitalWrite(ledPin, HIGH);

    // check if the Push button is pressed.
    // if it is, the PushState is HIGH:
    PushState = digitalRead(PushPin);

    // if the Push button is pressed then the configured text is typed.
    if (PushState == HIGH) {
      Keyboard.print(KeyboardMessage);
      delay(5000);
    } else {
      // Make the LED flash for extra dramatic effect while waiting for the Push button to be pressed ;-)
      delay(100);
      digitalWrite(ledPin, LOW);
      delay(100);
    }   
  }
  else {
    // turn LED off:
    digitalWrite(ledPin, LOW);
  }
}
```
