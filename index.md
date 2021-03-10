//include libraries
#include <SoftwareSerial.h>
#include <LiquidCrystal.h>

//for bluetooth - create an object called BTserial, with RX pin at 3 and TX pin at 2
SoftwareSerial BTserial(3,2); // RX | TX

//decraration of all our variables

float reads;
int pin = A0;

float vOut = 0 ;//voltage drop across 2 points
float vIn = 5;
double R1 = 1000;
double R2 = 0;
float buffer = 0;
float TDS;

double r = 0;//resistivity 
double L = 0.06;//distance between the wires in m
double A = 0.000154;//area of cross section of wire in m^2

double C = 0;//conductivity in S/m
double Cm = 0;//conductivity in mS/cm

int rPin = 9;
int bPin = 5;
int gPin = 6;
int rVal = 255;
int bVal = 255;
int gVal = 255;

//we will use this formula to get the resistivity after using ohm's law -> R = r L/A => r = R A/L

//creating lcd object from Liquid Crystal library
LiquidCrystal lcd(8,7,10,11,12,13);

void setup() {
  //initialise BT serial and   serial monitor
  Serial.begin(9600);
  BTserial.begin(9600);

  //initialise lcd
  lcd.begin(16, 2);

  //set rgb led pins (all to be pwm pins on Arduino) as output
  pinMode(rPin,OUTPUT);
  pinMode(bPin,OUTPUT);
  pinMode(gPin,OUTPUT);
  pinMode(pin,INPUT);
  //Print stagnant message to LCD
  lcd.print("Conductivity: ");
}

void loop() {
    reads = analogRead(A0);
  
  vOut = reads*5/1023;
//  Serial.println(vOut);
  buffer = (vIn/vOut)-1;
  R2 = R1*buffer;
    //convert voltage to resistance
    //Apply formula mentioned above
      r = R2*A/L;//R=rL/A
        Serial.println(R2);
         delay(500);
    //convert resistivity to condictivity
    C = 1/r;
    Cm = C*10;
    //convert conductivity in mS/cm to TDS
    TDS = Cm *700;
    //Set cursor of LCD to next row
    lcd.setCursor(0,1);
    lcd.println(C);

    //display corresponding colours on rgb led according to the analog read
     if( reads < 600 )
  {
      if (reads <= 300){
        setColor( 255, 0, 255 ) ;
      }
      if (reads > 200){
        setColor( 200, 0, 255 ) ;
      }
  }
  else{
    if( reads <= 900 )
    {
      setColor( 0, 0, 255 ) ;
    }
    if( reads > 700 )
  {
    setColor( 0, 255, 255 ) ;
  }
    }

//send data to Ardutooth app on mobile phone through bluetooth
BTserial.print(C);
BTserial.print(",");
BTserial.print(TDS);
BTserial.print(";");
delay(500);
}


void setColor(int red, int green, int blue)
{
  analogWrite( rPin, 255 - red ) ;
  analogWrite( gPin, 255 - green ) ;
  analogWrite( bPin, 255 - blue ) ;  
}
