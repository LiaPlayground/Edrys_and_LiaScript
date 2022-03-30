<!--
author:   Your Name

email:    your@mail.org

version:  0.0.1

language: de

narrator: US English Female

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md

-->

# TUBAF - Status der Implementierung

https://github.com/LiaPlayground/Edrys_and_LiaScript/

## Edrys

![edrys-logo](https://raw.githubusercontent.com/edrys-org/edrys/main/brand/logo.png)<!-- style="width:100%" -->

__The Open Remote Teaching Platform__

__Projekt: https://edrys.org __

__GitHub: https://github.com/edrys-org/edrys __

### Fetatures

* __Live Classrooms:__ Click on a student to talk to them, or create rooms and
  drag students in & out
* __Remote Labs:__ Allow students to interact with your real lab equipment
  remotely & asynchronously
* __Modular:__ Build your class by combining Modules or make your own with an
  easy real-time API
* __Easy to start:__ Download and run to start, no databases or any other
  dependencies to set up
* __Privacy-friendly:__ Passwordless auth with minimal student PII stored
* __Fast & Modern:__ Based on Deno and Vue with a deliberately small codebase
* __Free and Open Source, forever:__ No paywalled features or lock-in

### Wie Funktioniert es

    {{1-2}}
__Rollen:__ Student/Teacher/Station

    {{1-2}}
![stations](https://raw.githubusercontent.com/edrys-org/edrys/main/docs/stations/structure.png)

    {{2}}
![arduino-stations](https://raw.githubusercontent.com/edrys-org/edrys/main/docs/stations/arduino-lab.png)

    {{2}}
__Orte:__ Lobby/Room/Station

#### Kommunikation

``` html
<script src="https://edrys-org.github.io/edrys/module/edrys.js"></script>
```

                 {{1}}
***********************************************************

__Konfiguration__

``` js
// Is one of "teacher", "student", or "station"
console.log(Edrys.role);

// Always available
console.log(Edrys.module.config);

// Only available when this module is loaded to a student
console.log(Edrys.module.studentConfig);
// Only available when this module is loaded to a teacher
console.log(Edrys.module.teacherConfig);
// Only available when this module is loaded on a station
console.log(Edrys.module.stationConfig);
```
***********************************************************


                 {{2}}
***********************************************************

__Senden und Empfangen__

``` js
// To send a message:
Edrys.sendMessage("subject", "body");

// To receive messages:
Edrys.onMessage(({ from, subject, body }) => {
  console.log("Got new message: ", from, subject, body)
});
```
***********************************************************

                 {{3}}
***********************************************************
__Promiskuität__

``` js
// To receive messages:
Edrys.onMessage(
  ({ from, subject, body, module }) => {
    console.log("Got new message: ", from, subject, body, module)
  }, promiscuous=true);
```
***********************************************************

## Live demo

### Klassenraum

__LiaScript Module:__ https://github.com/edrys-org/module-liascript

__Konfiguration:__

```json
{
  "course": "https://raw.githubusercontent.com/LiaPlayground/Edrys_and_LiaScript/main/README.md"
}
```

#### Synchronisierung

__Quiz:__ Was ist Edrys?

[[ ]] Ein Learning Management System (LMS)
[[X]] Eine Möglichkeit Klassenräume kollaborativ zu gestallten
[[ ]] Ein online Game

---

__Umfrage:__ Wie fanden Sie die Vorstellung bis jetzt?

[(Note 1)] sehr gut
[(Note 2)] gut
[(Note 3)] befriedigend
[(Note 4)] ausreichend
[(Note 5)] noch nicht ganz ausreichend

---

__Umfrage:__ Was wünschen Sie sich (Begriffe können mit Komma getrennt werden)?

[[___]]

#### Lokales testen

<div id="example">
<wokwi-led color="red"   pin="13" label="13"></wokwi-led>
<wokwi-led color="green" pin="12" label="12"></wokwi-led>
<wokwi-led color="blue"  pin="11" label="11"></wokwi-led>
<wokwi-led color="blue"  pin="10" label="10"></wokwi-led>
<span id="simulation-time"></span>
</div>

``` cpp
byte leds[] = {13, 12, 11, 10};
void setup() {
  Serial.begin(115200);
  for (byte i = 0; i < sizeof(leds); i++) {
    pinMode(leds[i], OUTPUT);
  }
}

int i = 0;
void loop() {
  Serial.print("LED: ");
  Serial.println(i);
  digitalWrite(leds[i], HIGH);
  delay(250);
  digitalWrite(leds[i], LOW);
  i = (i + 1) % sizeof(leds);
}
```
@AVR8js.sketch(example)



#### Live Coding

https://github.com/edrys-org/module-code

``` bash
arduino-cli sketch new ./arduino
rm ./arduino/*
echo "Writing Code-----------------------------------"
echo $CODE | base64 --decode > ./arduino/arduino.ino
echo "Compiling Code---------------------------------"
arduino-cli compile ./arduino -b arduino:avr:uno -v --output-dir ./arduino
echo "Uploading Code---------------------------------"
arduino-cli upload ./arduino -b arduino:avr:uno -p /dev/ttyACM0
```

``` arduino
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

---

__Konfiguration__

```json
{
  "editorText": "// the setup function runs once when you press reset or power the board\nvoid setup() {\n  // initialize digital pin LED_BUILTIN as an output.\n  pinMode(LED_BUILTIN, OUTPUT);\n}\n\n// the loop function runs over and over again forever\nvoid loop() {\n  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)\n  delay(1000);                       // wait for a second\n  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW\n  delay(1000);                       // wait for a second\n}",
  "terminalText": "Starting text in terminal...",
  "commands": "arduino-cli sketch new ./arduino\nrm ./arduino/*
  echo \"Writing Code-----------------------------------\"\necho $CODE | base64 --decode > ./arduino/arduino.ino\necho \"Compiling Code---------------------------------\"\narduino-cli compile ./arduino -b arduino:avr:uno -v --output-dir ./arduino\necho \"Uploading Code---------------------------------\"\narduino-cli upload ./arduino -b arduino:avr:uno -p /dev/ttyACM0\n",
  "language": "cpp",
  "theme": "light"
}
```


### Global

__Heroku:__ https://thawing-peak-50396.herokuapp.com/


## Ausblick


* {{1}} Headless Browser via [puppeteer](https://puppeteer.github.io/puppeteer/)

* {{2}} WebViz & ROS:

  {{2}}
  !?[WebView Ros](https://open-source-webviz-ui.s3-us-west-2.amazonaws.com/landing/rawvelodyne.webm)<!-- autoplay -->
