# Componentes 
Placa ESP32  
Smartphone Android con Bluetooth
LED de 5 mm
Resistencia de 330 ohmios
Sensor de temperatura DS18B20
Resistencia de 4,7k ohmios
Cables de puente
Tablero de circuitos

# Código
```
#include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif

BluetoothSerial SerialBT;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("ESP32test"); //Bluetooth device name
  Serial.println("The device started, now you can pair it with bluetooth!");
}

void loop() {
  if (Serial.available()) {
    SerialBT.write(Serial.read());
  }
  if (SerialBT.available()) {
    Serial.write(SerialBT.read());
  }
  delay(20);
```





#Cómo funciona el código
Este código establece una comunicación Bluetooth serie bidireccional entre dos dispositivos.

El código comienza por incluir la biblioteca BluetoothSerial.
Las siguientes tres líneas comprueban si Bluetooth está habilitado correctamente.
Luego, crea una instancia de BluetoothSerial llamada SerialBT:
En la configuración (), inicialice una comunicación en serie a una velocidad de 115200
Inicialice el dispositivo serie Bluetooth y pase como argumento el nombre del dispositivo Bluetooth. De forma predeterminada, se llama ESP32test, pero puedes cambiarle el nombre y darle un nombre único.
En el bucle (), envía y recibe datos a través de Bluetooth serie.

En la primera declaración if, verificamos si se están recibiendo bytes en el puerto serie. Si los hay, envíe esa información a través de Bluetooth al dispositivo conectado.

SerialBT.write () envía datos usando la serie bluetooth.

Serial.read () devuelve los datos recibidos en el puerto serie.

La siguiente declaración if, comprueba si hay bytes disponibles para leer en el puerto serie Bluetooth. Si los hay, escribiremos esos bytes en Serial Monitor.
