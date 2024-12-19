# ULTRASONICO-CON-LCD

# Practica ESP32 con HC-SR04 y LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor ultrasonico HC-SR04 para medir distancias y una pantalla LCD que nos muestre la información recibida por el sensor  HC-SR04. de igual manera como extra se aprobecha la pantalla para poder mostras datos personales a la distancia en misma pantalla con un determinado tiempo.

## Introducción

### Descripción

La ```ESP32``` la utilizamos en un entorno de adquisición de datos, en esta práctica ocuparemos un sensor (```HC-SR04```) para adquirir los datos de cierta distancia y una pantalla LCD para poder visualizar los datos leídos por dicho sensor.  Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor HC-SR04
- Pantalla LCD 16x2 ILC



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:

```
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

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
  
lcd.clear(); 
  lcd.setCursor(4, 0); //Coordenadas para imprimir en la LCD
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(2000);

lcd.clear(); //Limpiar el texto en la LCD
  lcd.setCursor(2, 0);
  lcd.print("RICARDO RAMOS");
  lcd.setCursor(2, 1);
  lcd.print("ING. MECANICA");
  delay(2000);
  
lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  delay(2000);

  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(2000);          //Hacemos una pausa de 200ms
}
```
2. Instalar la librería:
- **LiquidCrystal I2C**

![](https://github.com/Ricardoramosdelapaz/ULTRASONICO-CON-LCD/blob/main/LIB%203.PNG?raw=true).

3. Hacer la conexion de **HC-SR04** con la **ESP32** y la pantalla LCD como se muestra en la siguiente imagen.

![](https://github.com/Ricardoramosdelapaz/ULTRASONICO-CON-LCD/blob/main/CON%203.PNG?raw=true).

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando *doble click* al sensor **HC-SR04** 

## Resultados

Al iniciar la simulacion, verás los datos creados y los resultados de la distancia dada por el sensor ultrasonico dentro del monitor serial y la pantalla LCD como se muestra en la siguente imagen.

![](https://github.com/Ricardoramosdelapaz/ULTRASONICO-CON-LCD/blob/main/RES3.PNG?raw=true).
![](https://github.com/Ricardoramosdelapaz/ULTRASONICO-CON-LCD/blob/main/RES3.1.PNG?raw=true).
![](https://github.com/Ricardoramosdelapaz/ULTRASONICO-CON-LCD/blob/main/RES3.2.PNG?raw=true).



# Créditos

Desarrollado por Ing. Ricardo Ramos De la paz

- [GitHub](https://github.com/Ricardoramosdelapaz)
