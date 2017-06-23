# yumeng

#include<CapacitiveSensor.h>
#include <Stepper.h> // Hinzufügen der Programmbibliothek.

int Trigger=8; 
int Echo=9; 
long dauer=0; 
int Entfernung=0; 

int LEDRot=46;
int LEDGelb=50;
int LEDGruen=47;


void setup()
{
Serial.begin (9600); 
pinMode(Trigger, OUTPUT); 
pinMode(Echo, INPUT);                                                                                               
pinMode(LEDRot, OUTPUT); 
pinMode(LEDGelb, OUTPUT); 
pinMode(LEDGruen, OUTPUT); 

}

void loop()
{
  digitalWrite(Trigger, LOW); 
//delay(5); 
digitalWrite(Trigger, HIGH); 
//delay(10);
digitalWrite(Trigger, LOW);
dauer = pulseIn(Echo, HIGH); 
Entfernung = (dauer/2) * 0.03432;  
if (Entfernung >= 500 || Entfernung <= 0) 
{
Serial.println("Kein Messwert"); 
digitalWrite(LEDGruen, LOW);
digitalWrite(LEDGelb, LOW);
digitalWrite(LEDRot, LOW);
}
else 
{
Serial.print(Entfernung); 
Serial.println(" cm"); 
}
if(Entfernung<=5)
    {
       digitalWrite(LEDGruen, HIGH); 
       digitalWrite(LEDGelb, LOW);
       digitalWrite(LEDRot, LOW);
    }
else  if(5<Entfernung<10)

    {  digitalWrite(LEDGelb, HIGH);
       digitalWrite(LEDGruen, LOW);
       digitalWrite(LEDRot, LOW);
       
    }
else
    {
       digitalWrite(LEDRot, HIGH); 
       digitalWrite(LEDGruen, LOW);
       digitalWrite(LEDGelb, LOW);
    }

}
