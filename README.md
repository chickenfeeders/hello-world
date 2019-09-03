# hello-world
just another repository
#define BLYNK_PRINT Serial

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <TridentTD_LineNotify.h> //https://github.com/chickenfeeders/hello-world/edit/master/README.md
#include <WidgetRTC.h>
#include <DHT.h>
#include <SimpleTimer.h>

#define LINE_TOKEN   ""  //line token at https://notify-bot.line.me/en/ 
TridentTD_LineNotify myLINE(LINE_TOKEN);

// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "IU8LTdcwgvyyzYFTW8SIABV0ZpTT86lu";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "A1601-arm";
char pass[] = "1212312121";

const int pingPin = D5;
int inPin = D6;


void setup() {
Serial.begin(115200);
}

void loop()
{
long duration, cm;

pinMode(pingPin, OUTPUT);


digitalWrite(pingPin, LOW);
delayMicroseconds(2);
digitalWrite(pingPin, HIGH);
delayMicroseconds(5);
digitalWrite(pingPin, LOW);
pinMode(inPin, INPUT);
duration = pulseIn(inPin, HIGH);

cm = microsecondsToCentimeters(duration);

Serial.print(cm);
Serial.print("cm");
Serial.println();
delay(300);
}

long microsecondsToCentimeters(long microseconds)
{
// The speed of sound is 340 m/s or 29 microseconds per centimeter.
// The ping travels out and back, so to find the distance of the
// object we take half of the distance travelled.
return microseconds / 29 / 2;
}
void setup()
{
  // Debug console
  Serial.begin(9600);

  Blynk.begin(auth, ssid, pass);
  // You can also specify server:
  //Blynk.begin(auth, ssid, pass, "blynk-cloud.com", 80);
  //Blynk.begin(auth, ssid, pass, IPAddress(192,168,1,100), 8080);
}

void loop()
{
  Blynk.run();
}
