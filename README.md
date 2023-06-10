# Practica ESP32 CON SENSOR DE DISTANCIA Y PANTALLA LCD 16x2 (I2C).
Este repositorio muestra como podemos programar una ESP32 con el sensor ultrasonico y mostrar los resultados en una pantalla 16x2 (I2C).

## Introducción

### Descripción

La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor ultrasonico para adquirir la distancia del sensor con el muro que se vera reflejado en una pantalla lcd 16x2 (I2C), ademas mostrara el nombre del creador del programa; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor ultrasonico
- Pantalla lcd 16x2 (I2C)



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:


#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 27;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
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




  lcd.setCursor(0, 0);
  lcd.print("  Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  lcd.print(" Jorge Roldan       ");
  delay(1000);
}


2. Instalar la libreria de *LiquidCrystal I2C* como se muestra en la siguente imagen.

![](https://github.com/jroldanap/ESP32ULTRASONIC/blob/main/library.png?raw=true)

3. Hacer la conexion de *DHT22*, pantalla *lcd16x2(I2C)* con la *ESP32* como se muestra en la siguente imagen.

![](https://github.com/jroldanap/ESP32ULTRASONIC/blob/main/diagrama.png?raw=true)

### Instrucciónes de operación

1. Iniciar simulador dando click en el boton verde de play.
2. Visualizar los datos en el monitor serial y en el lcd16x2(I2C) .
3. Colocar la distancia  dando doble click al sensor *ultrasonico* 

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial y lcd16x2(I2C) como se muestra en la siguente imagen.

![](https://github.com/jroldanap/ESP32ULTRASONIC/blob/main/code.png?raw=true)



## Evidencias de programa corriendo

![](https://github.com/jroldanap/ESP32ULTRASONIC/blob/main/code.png?raw=true)



# Créditos

Desarrollado por Jorge Alberto Roldan Aponte

- [GitHub](https://github.com/jroldanap)