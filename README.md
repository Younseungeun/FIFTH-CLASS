# FIFTH-CLASS

## TOPIC
- TEMPERTURE sensor(DHT11)
### TEMPERTURE sensor(DHT11)
![image](https://user-images.githubusercontent.com/102523600/173249725-bf132c18-567f-4779-8b6a-cc3f0bd1c388.png)
- DHT11 was not found, so I replaced it with another sensor
### CODE
#include <SimpleDHT.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>        //header file
LiquidCrystal_I2C lcd(0x27,16,2);     

// for DHT11, 
//      VCC: 5V or 3V
//      GND: GND
//      DATA: 6
int pinDHT11 = 6;
SimpleDHT11 dht11(pinDHT11);

void setup() {
  Serial.begin(9600);
  lcd.init();                         
     lcd.backlight();                
 
}
  
void loop() {
  // start working...
     Serial.println("=================================");
  Serial.println("Sample DHT11..."); // read without samples.
  byte temperature = 0;
  byte humidity = 0;
  int err = SimpleDHTErrSuccess;
  if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess) {
    Serial.print("Read DHT11 failed, err="); 
    Serial.print(SimpleDHTErrCode(err));
    Serial.print(","); 
    Serial.println(SimpleDHTErrDuration(err)); 
    delay(1000);
    return;
  }
  
  Serial.print("Sample OK: ");
  Serial.print((int)temperature); Serial.print(" *C, "); 
  Serial.print((int)humidity); Serial.println(" H");
  lcd.clear();                   
     lcd.setCursor(0,0);             
     lcd.print("temperature="); 
     lcd.setCursor(12,0);             
     lcd.print((int)temperature); 
      lcd.setCursor(14,0);             
     lcd.print((char)0xDF); 
     lcd.setCursor(15,0);             
     lcd.print("C"); 
     lcd.setCursor(0,1);          
     lcd.print("humidity=");  
      lcd.setCursor(9,1);            
     lcd.print((int)humidity); 
     lcd.setCursor(11,1);           
     lcd.print("%"); 
  // DHT11 sampling rate is 1HZ.
  delay(1500);
}
