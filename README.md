# Practica-4-ESP32-con-ULTRASONICO
## Introducción
### Material de trabajo 
WOKWI
TARJETA ESP 32
SENSOR DHT11
SENSOR LiquidCrystal I2C

### INSTRUCCIONES 
Entrar a la plataforma WOKWI para poder usar el sensor
Posterior colacamos abrimos el programa y colocamos el codigo de programación 

#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
   lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms

  lcd.clear();
lcd.setCursor(0,0);
lcd.print("Distancia:" + String(d) + "cm");
delay(2000);
lcd.clear();
lcd.setCursor(0,0);
lcd.print("Ing. Roberto");
lcd.setCursor(0,1);
lcd.print("Mecanico");
}

Siguiente instlamos la libreria **DHT sensor library for ESPx** y la libreria **LiquidCrystal I2C**

Por ultimo hacemos la conexion de los sensores **Ultrasonic Distance Sensor** y **ESP32** con el sensor **LCD 16X2 (l2C)** y agregamos **VCC Symbol** y **GND Symbol** como se muestra en la imagen
![](https://github.com/RobertoPalacios17/Pr-ctica-4-ESP32-con-ULTRASONICO/blob/main/SENSOR%205.png)

### RESULTADOS
Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![]
