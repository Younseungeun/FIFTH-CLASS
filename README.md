# FIFTH-CLASS

## TOPIC
- TEMPERTURE sensor(DHT11)
### TEMPERTURE sensor(DHT11)
![image](https://user-images.githubusercontent.com/102523600/173327234-841e0e62-b08d-4ad5-9896-eefd074dcb9f.png)
- DHT11 was not found, so I replaced it with another sensor
### CODE
1. #include <SimpleDHT.h>
2. #include <Wire.h> 
3. #include <LiquidCrystal_I2C.h>        //header file
4. LiquidCrystal_I2C lcd(0x27,16,2);     
5. // for DHT11, 
6. //      VCC: 5V or 3V
7. //      GND: GND
8. //      DATA: 6
9. int pinDHT11 = 6;
10. SimpleDHT11 dht11(pinDHT11);
11. void setup() {
12. Serial.begin(9600);
13. lcd.init();                         
14. lcd.backlight();                
15. }
16. void loop() {
17. // start working...
18. Serial.println("=================================");
19. Serial.println("Sample DHT11..."); // read without samples.
20. byte temperature = 0;
21. byte humidity = 0;
22. int err = SimpleDHTErrSuccess;
23. if ((err = dht11.read(&temperature, &humidity, NULL)) != SimpleDHTErrSuccess) {
24. Serial.print("Read DHT11 failed, err="); 
25. Serial.print(SimpleDHTErrCode(err));
26. Serial.print(","); 
27. Serial.println(SimpleDHTErrDuration(err)); 
28. delay(1000);
29. return;
30. }
31. Serial.print("Sample OK: ");
32. Serial.print((int)temperature); Serial.print(" *C, "); 
33. Serial.print((int)humidity); Serial.println(" H");
34. lcd.clear();                   
35. lcd.setCursor(0,0);             
36. lcd.print("temperature="); 
37. lcd.setCursor(12,0);             
38. lcd.print((int)temperature); 
39. lcd.setCursor(14,0);             
40. lcd.print((char)0xDF); 
41. lcd.setCursor(15,0);             
42. lcd.print("C"); 
43. lcd.setCursor(0,1);          
44. lcd.print("humidity=");  
45. lcd.setCursor(9,1);            
46. lcd.print((int)humidity); 
47. lcd.setCursor(11,1);           
48. lcd.print("%"); 
49. // DHT11 sampling rate is 1HZ.
50. delay(1500);
51. }
