#include <MFRC522.h>
#include <Servo.h>
#define SS_PIN 9 //define ss pin for RFID
#define RST PIN 8 //define pin for RST pin for RFID
MFRC522 mfrc522(SS_PIN, RST_PIN); // Create MFRC522 instance.
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 20, 4);
Servo myServo; //define first servo name
Servo myServo1; //define first servo name
#define ir_carl 2 //define pin of first IR Sensor
#define ir_car2 3 //define pin of second IR Sensor
#define ir_car3 4 //define pin of third IR Sensor
#define ir_car4 5 //define pin of fourth IR Sensor
#define ir_exiti 10 //define pin of exit1 IR Sensor
#define ir_exit2 11 //define pin of exit2 IR Sensor
int slot;

void setup() {
pinMode(ir_carl, INPUT); //input pin of first IR Sensor
pinMode(ir car2, INPUT); //input pin of second IR Sensor
pinMode(ir car3, INPUT); //input pin of third IR Sensor
pinMode(ir car4, INPUT); //input pin of fourth IR Sensor
pinMode(ir_exitl, INPUT); //input pin of exitl IR Sensor
pinMode(ir_exit2, INPUT); //input pin of exit1 IR Sensor
pinMode(23, OUTPUT); //output for first slot Red LED
pinMode(25, OUTPUT); //output for first slot Green LED
pinMode(27, OUTPUT); //output for first slot Blue LED
lcd.init();    // initialize the lcd
lcd.backlight(); // turn on the backlight
lcd.setCursor(0, 1);
lcd.print("    Car parking   ");
lcd.setCursor(0, 2);
lcd.print("    System    ");
delay(2000);
lcd.clear();
Serial.begin(9600); // Initiate a serial communication
SPI.begin();// Initiate SPI bus
mfrc522.PCD_Init(); // Initiate MFRC522
myServo.attach(6);  //servo pin
myServo.write(170); //servo start position
Serial.println("Put your card to the reader...");
Serial.println();
myServo1.attach(7); //servol pin
myServo1.write(85); //servol start position

void loop() {
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 1){ slot = 4; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 0){ slot = 1; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 0){ slot = 1; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 0){ slot = 1; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 1){ slot = 1; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 0){ slot = 2; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 1){ slot = 2; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 1){ slot = 2; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 0){ slot = 2; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 1){ slot = 2; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 1){ slot = 2; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 0){ slot = 4; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 0){ slot = 3; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 1){ slot = 3; }
if (digitalRead(ir_car) == 1 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 1){ slot = 3; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 1 && digitalRead(ir_car3) == 1 && digitalRead(ir_car4) == 1){ slot = 3; }
if (digitalRead(ir_car) == 0 && digitalRead(ir_car2) == 0 && digitalRead(ir_car3) == 0 && digitalRead(ir_car4) == 0){ slot = 0; }
lcd.setCursor(0, 3);
lcd.print("Sorry Parking Full ");
} else {
lcd.setCursor(0, 3);
}
lcd.print("               ")
lcd.setCursor(0, 1);
if (digitalRead(ir_carl) == 0) {
lcd.print("S1: Full ");
analogWrite(23, 0);
analogWrite(25, 0);
analogWrite(27, 255);
} else {
}
lcd.print("S1:Empty");
analogWrite(23, 0);
analogWrite(25, 255);
analogWrite(27, 0);
lcd.setCursor(10, 1);
if (digitalRead(ir_car2) == 0) {
lcd.print("S2: Full ");
} else {
lcd.print("S2:Empty");
}
lcd.setCursor(0, 2);
if (digitalRead(ir_car3) == 0) {
lcd.print("S3: Full ");
} else {
lcd.print("S3: Empty");
}
lcd.setCursor(10, 2);
if (digitalRead(ir_car4) == 0) {
lcd.print("S4: Full");
} else {
lcd.print("54: Empty");
}
lcd.setCursor(0, 0);
lcd.print(" Have Slot: ");
lcd.print(slot);
lcd.print("   ");
if (digitalRead(ir_exit1) == 0) { myServo1.write(0); }
if (digitalRead(ir_exit2) = 0) {
delay(2000);
myServo1.write(85);
}

if (Infrc522.PICC_IsNewCardPresent()) { return; }
if (!mfre522.PICC _ReadCardSerial()) { return; }
//Show UID on serial monitor
Serial.print("UID tag :");
String content = "";
byte letter;
for (byte i=0; i < mfrc522.uid.size; i++) {
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? "0" : " "));
content.concat(String(mfrc522.uid.uidByte[i], HEX));
}
Serial.println();
Serial.print("Message: ");
content.toUpperCase();
if (content.substring(1) == "5313981298", "971115914710", "02770534", "331013394") //change here the UID of the card/cards that you we
Serial.println("Authorized access");
Serial.println();
myServo.write(85);
delay(3000);
myServo.write(170);
} else {
Serial.println(" Access denied");
}
}
