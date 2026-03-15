//Include relevant libraries that the program will need
#include <math.h>
#include <Time.h>

//Constants to be used for voltage-temperature conversion
float A = 0.001129148;
float B = 0.000234125;
float C = 0.0000000876741;

const int pumpPin = 9; // the number of the pump pin
const int ledPin = 7; // the number of the LED pin
const int analogInPin = A1; // the number of the analogPin
int sensorValue = 0;
int sensorPump;
int sensorLow = 0;
int sensorHigh = 50;

//Function to convert measured voltage to temperature in fahrenheit
double voltageToTemp(int voltage) {

  double res;
  double temp;
  bool LED;
  //res variable to hold the value of natural log of thermal resistance valu
  res = log(10000.0*((1024.0/voltage-1)));
  /* Convert the thermal resistance value to temperature with equation
  * T=1/(A + Bln(R) + Cln(R)^3)
  */

  temp = 1 / (A + (B * res) + (C * res * res * res) );
  /* Convert the temp value from Kelvin to Celcius to Fahrenheit using equations:
  * Celcius = Kelvin - 273.15
  * Fahrenheit = ( (9.0/5.0) * Celcius ) + 32.0
  */
  //*INSERT CODE HERE*
  temp = temp - 273.15;
  temp = ( (9.0/5.0) * temp ) + 32.0;

return temp;
}

void setup() {
// initialize the pump pin as an output:
pinMode(pumpPin, OUTPUT);
//Establishing a serial communication with baud rate 9600
Serial.begin(9600);
Serial.println("Time (s), Temperature (F)");
pinMode(ledPin, OUTPUT);
pinMode(pumpPin, OUTPUT);
while (millis() < 5000) {
    sensorPump = analogRead(A1);
    digitalWrite(pumpPin, LOW);
    if (sensorPump > sensorHigh) {
    sensorHigh = sensorPump; // assign values to sensor High and sensor Low
    }
    if (sensorPump < sensorLow) {
    sensorLow = sensorPump;
    }
  }
}

void loop() {
  //define variables
  int volt;
  int times;
  double temperature;

  //Read values from pin A0 into variable volt
  //*INSERT CODE HERE*
  volt = analogRead(A0);
  sensorValue = analogRead(analogInPin);

  //Call voltage to temperature function for conversion
  temperature=voltageToTemp(volt);
  //Get time of running program, in milliseconds and convert to seconds
  times = millis()/1000;

  Serial.print(times);
  Serial.print(", ");
  Serial.println(temperature);
  delay(5000); // time seperation

  Serial.print("Sensor = " );
Serial.print(sensorValue / 10); // printing out the sensor value in percentage
Serial.println("%");
delay(0);

  if (temperature >= 85){
      digitalWrite(ledPin, LOW); // turning off the LED/Heating devices when
  temperature is over 85
    }else{
      digitalWrite(ledPin, HIGH); // turning on the LED/Heating devices when
  temperature is under 85
  }
sensorPump = analogRead(A1); // read the value from analogPin A1
digitalWrite(pumpPin, LOW);
 if (sensorPump < 50) {
      digitalWrite(pumpPin, LOW); // turn off/ make the waterpump on when the
  sensor pump value is lower than 50
  }
    else{
      digitalWrite(pumpPin, HIGH); // turn on/ make the water pump off when the
  sensor pump value is higher than 50
  }
}
