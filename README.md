# -DHT22-CON-LCD





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
