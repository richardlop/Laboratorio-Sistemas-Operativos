//Este es el codigo funcional en aplicacion Arduino
int ledPin = 13;
int motorPin = 12;
float temp;
int sensorValue;

void setup()
{
  pinMode(ledPin, OUTPUT);
  pinMode(motorPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("### Temperatura monitor ###");
}

void loop()
{
  sensorValue = analogRead(A0);
  Serial.print("sensor value: ");    
  Serial.println(sensorValue);

  temp = sensorValue * (5.0 / 1023.0) * 100;
  Serial.print("Temperatura: ");
  Serial.println(temp);  

  if (temp < 5.0) {
    digitalWrite(ledPin, HIGH);
    delay(500);
    digitalWrite(ledPin, LOW);
    delay(500);
  }
  else if (temp >= 6.0 && temp <= 20.0) {
    digitalWrite(ledPin, LOW);
    digitalWrite(motorPin, LOW);
  }
  else if (temp >= 20.0) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(motorPin, HIGH);
  }

  delay(1000);
}
//Este es el codigo funcional en aplicacion TinkerCad

void setup()
{
  pinMode(A0, INPUT);
  pinMode(8, OUTPUT);
  pinMode(13, OUTPUT);
  Serial.begin(9600);
  // Pin en el que se conectará el LED
#define tiempoEncendido 500 	// Tiempo que permanece el LED encendido en ms (1000 ms = 1 s)
#define tiempoApagado 500
}

void loop()
{
  if ((-40 + 0.488155 * (analogRead(A0) - 20)) <= 5) {
    //  Se lee sensor de temperatura y se compara con 5
    // Si es menor o igual a 5 enciende led 
    digitalWrite(8, HIGH);	
  delay(tiempoEncendido);   // Se mantiene encendido durante 1 segundo (1000 ms)
  digitalWrite(8, LOW);    // Apaga el LED
  delay(tiempoEncendido);
  }
  if ((-40 + 0.488155 * (analogRead(A0) - 20)) >25) {
    // Se lee sensor de temperatura y se compara con 25
    // Si es mayor o igual a 25 enciende led 
    digitalWrite(8, HIGH);	//Se enciende el led
    digitalWrite(13, HIGH); //Se enciende el motor
  }
  if ((-40 + 0.488155 * (analogRead(A0) - 20) >= 5) && 
      (-40 + 0.488155 * (analogRead(A0) - 20) <= 25)) 
    // Se lee sensor de temperatura y se compara con 5 y 25
    // Si es mayor o igual a 5 apaga el led y motor 
    // Se es menor o igual que 25 se apaha el led y motor
  {
    digitalWrite(8, LOW);
    digitalWrite(13, LOW);
}
  delay(2000); // Wait for 2000 millisecond(s)
  Serial.println((-40 + 0.488155 * (analogRead(A0) - 20)));
}
