# cfpl-boat
#include <Servo.h>
Servo myservo;  // 定义舵机对象
int pos=0;
const int TrigPin = 8; 
const int EchoPin = 9; 
float cm; 
void setup()
{
  Serial.begin(9600); 
  pinMode(TrigPin, OUTPUT); 
  pinMode(EchoPin, INPUT); 
  pinMode(A5,OUTPUT);   //让模拟口A5作为数字口输出
  myservo.attach(9);  // 设置舵机控制针脚
  
}
 
void loop()
{
 int n=analogRead(A0);
 if (n>=1) 
 {
 
   digitalWrite(A5, HIGH);  
 
pinMode(A2,OUTPUT);     //蜂鸣器频响 0.5秒
  tone(A2,800);
  delay(500);
pinMode(A2,INPUT); 
 
 
  digitalWrite(A5, LOW);   
  delay(500);      
 }
 
  digitalWrite(TrigPin, LOW); //低高低电平发一个短时间脉冲去TrigPin 
  delayMicroseconds(2); 
  digitalWrite(TrigPin, HIGH); 
  delayMicroseconds(10); 
  digitalWrite(TrigPin, LOW); 
 
  cm = pulseIn(EchoPin, HIGH) / 58.0; //将回波时间换算成cm 
  Serial.print(cm); 
  Serial.print("cm"); 
  Serial.println(); 
  delay(1000); 
   for(pos = 0; pos < 180; pos += 1)  
     {  
        myservo.write(pos);  
        delay(15); 
      }
      // 180到0旋转舵机，每次延时15毫秒 
      for(pos = 180; pos>=1; pos-=1)
      {                               
        myservo.write(pos);
        delay(15);
      }
  
}


