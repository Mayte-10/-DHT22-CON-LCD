# REPORTE-SENSOR-DTH22- LCD
## USO DEL LCD
### Reporte: Sensor DHT22 con LCD con Tarjeta ESP32

- Introducción
Leer temperatura y humedad desde un sensor DHT22 y mostrarlas en un LCD I2C usando un ESP32.

El sensor DHT22 es un dispositivo digital utilizado para medir temperatura y humedad relativa. Su combinación con la tarjeta ESP32 permite el monitoreo ambiental mediante transmisión y procesamiento de datos en tiempo real.

- Materiales Utilizados

  1. Sensor DHT22
  2. Tarjeta ESP32
  3. LCD 
  4. WOKWI SIMULATOR (https://wokwi.com)
![](https://github.com/Mayte-10/-DHT22-CON-LCD/blob/main/WhatsApp%20Image%202025-11-30%20at%2019.54.34.jpeg)

- PROCEDIMIENTO 

- Ingresar a  WOKWI SIMULATOR y seleccionar el microcontrolador ESP32

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2021.14.00%20(1).jpeg)
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2020.50.01.jpeg)

- Colocar el sensor DHT22 y la LCD
- Realizar la conexión correspondiente
  ![](h    )

- Colocar el siguiente código
- 
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("BIENVENIDOS");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("MODULO 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("MAYTE TORRES");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(1000);

  delay(1000);
} 
```
ADJUNTAR LAS LIBRERÍAS CORRESPONDIENTES 
- FUNCIONAMIENTO 
El ESP32 inicializa el sensor DHT22 y el LCD.
el ESP32 a traves del DHT22:
Lee la temperatura (°C).
Lee la humedad (%). 
Imprime los valores en el LCD

![](h    )
![](h    )
![](h    )
![](https://github.com/Mayte-10/-DHT22-CON-LCD/blob/main/WhatsApp%20Image%202025-11-30%20at%2019.57.37.jpeg)




