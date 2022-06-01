# PRACTICA 6 : Buses de comunicación II (SPI)



## 6.1: _LECTURA/ESCRITURA DE MEMORIA SD_

### SPI en ESP32:

Esquema de los pines a assignar para el bus SPI

| SPI  | MOSI    | MISO    | CLK     | CS      |
| ---- | ------- | ------- | ------- | ------- |
| VSPI | GPIO 23 | GPIO 19 | GPIO 18 | GPIO 5  |
| HSPI | GPIO 13 | GPIO 12 | GPIO 14 | GPIO 15 |

- CÓDIGO:
  
```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>
File myFile;
void setup()
{
  Serial.begin(9600);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(4)) 
  {
  Serial.println("No se pudo inicializar");
  return;
  }
  Serial.println("inicializacion exitosa");
  myFile = SD.open("archivo.txt");//abrimos el archivo
  if (myFile) 
  {
      Serial.println("archivo.txt:");
      while (myFile.available()) 
      {
        Serial.write(myFile.read());
      }
      myFile.close(); //cerramos el archivo
  } 
  else
  {
    Serial.println("Error al abrir el archivo");
  }
}
void loop()
{

}

```

- SALIDA POR PUERTO SERIE:


El puurto muestra el contenido del archivo de texto creado i guardado en la tarjeta sd 'archivo.txt'.

- FUNCIONAMIENTO:

Incluimos las librerias de: 

· Arduino 

· SPI 

· SD  

Creamos una variable de tipo File llamada 'MyFile'

```CPP
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>
File myFile;
```

En el set up inicializamos el serial i la sd con el metodo.begin i fijamos la velocidad de monitoreo a 9600.
En cuanto a la SD creamos un if que muestre por el serial si se ha podido realizar la inicializacion del spi.

Seguidamente, asignamosla variable MyFile a el recientemente creaso archivo de la sd 'archivo.txt' con la funcion SD.Open();
creamos un bucle para que mientras se esté dentro del 'archivo.txt', si Myfile.avialable(), entonces que se escriba por el Serial lo que se lee en el Myfile, es decir, se va a mostra por el monitor lo que hay dentro del 'archivo.txt' que se guarda dentro de la variable MyFile.


```cpp
void setup()
{
  Serial.begin(9600);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(4)) 
  {
  Serial.println("No se pudo inicializar");
  return;
  }
  Serial.println("inicializacion exitosa");
  myFile = SD.open("archivo.txt");//abrimos el archivo
  if (myFile) 
  {
      Serial.println("archivo.txt:");
      while (myFile.available()) 
      {
        Serial.write(myFile.read());
      }
      myFile.close(); //cerramos el archivo
  } 
  else
  {
    Serial.println("Error al abrir el archivo");
  }
}
```
El loop está vacío.
```cpp
void loop()
{

}
```