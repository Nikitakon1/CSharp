/*
 *  Here is a sketch that "graphs" the accelerometer and gyroscope data coming from
 *  the Pololu L3G and LSM303 libraries--by rapidly outputting graphically-arranged
 *  strings to the Arduino serial monitor. It's much easier than strings of numbers
 *  to look at and tell whether your sensors are working properly.
 */
 
#include <Wire.h>
#include <String.h>
#include <L3G.h>
#include <LSM303.h>
 
LSM303 compass;
L3G gyro;
 
void setup() {
  Serial.begin(115200);
  Wire.begin();
  if (!gyro.init())
  {
    Serial.println("Failed to autodetect gyro type!");
    while (1);
  }
  if (!compass.init())
  {
    Serial.println("Failed to initialize compass!");
    while (1);
  }
  gyro.enableDefault();
  compass.enableDefault(); 
}
 
void loop() {
  static int barcounter = 0;
  String spacestring = "                                                                ";
  String barstring = "----------------------------------------------------------------";
  String outstring;
 
  barcounter++;
  if(barcounter==10){
    barcounter=0;
    outstring=barstring;
    outstring += millis()/100;
  }
  else outstring=spacestring;
 
  gyro.read();
  compass.read();
 
  //gyro axes are drawn with thin lines, accelerometer are drawn with thick lines
  outstring.setCharAt(11+((int)gyro.g.x)/3277, ':');
  outstring.setCharAt(11+((int)compass.a.x)/3277, 'X');
  outstring.setCharAt(32+((int)gyro.g.y)/3277, ':');
  outstring.setCharAt(32+((int)compass.a.y)/3277, 'X');
  outstring.setCharAt(53+((int)gyro.g.z)/3277, ':');
  outstring.setCharAt(53+((int)compass.a.z)/3277, 'X');   
  Serial.println(outstring);
 
  delay(20);
}
