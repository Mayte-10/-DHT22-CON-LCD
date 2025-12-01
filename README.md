# REPORTE-SENSOR-DTH22- LCD
## USO DEL LCD
### Reporte: Sensor DHT22 con LCD con Tarjeta ESP32

- Introducción

El sensor DHT22 es un dispositivo digital utilizado para medir temperatura y humedad relativa. Su combinación con la tarjeta ESP32 permite el monitoreo ambiental mediante transmisión y procesamiento de datos en tiempo real.

- Materiales Utilizados

  1. Sensor DHT22
  2. Tarjeta ESP32
  3. WOKWI SIMULATOR (https://wokwi.com) 

- PROCEDIMIENTO 

- Ingresar a  WOKWI SIMULATOR y seleccionar el microcontrolador ESP32

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2021.14.00%20(1).jpeg)
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2020.50.01.jpeg)

  
- Colocar el siguiente código





- CODIGO
  
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
  delay(1000);     
  
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Bienvenidos");
  lcd.setCursor(2, 1);
  lcd.print("modulo 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Distancia: ");
  lcd.print(d);      //Enviamos serialmente el valor de la distancia
  lcd.setCursor(14, 1);
  lcd.print("cm");
  lcd.println();
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Raul Aguilar L.");
  lcd.setCursor(2, 1);
  lcd.print("Ing. Mecanico");
  delay(1000);     
       //Hacemos una pausa de 100ms
}
