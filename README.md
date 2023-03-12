# Sistema de riego automatico

![](./images/Licencia_CC_peque.png) 

by @javacasm - José Antonio Vacas


[http://bit.ly/RiegoCruzRoja](http://bit.ly/RiegoCruzRoja)

Vamos a realizar un sistema de riego automático (en función de la humedad del suelo) y que también podremos activar remotamente vía wifi

## Hardware

Usaremos la placa ESP32 Wemos D1 R32, compatible con Arduino y que nos permite conexiones wifi y bluetooth

![](./images/wemos_D1_R32.png)

Este placa tiene el mismo formato que el conocido Arduino UNO y es compatible con esta placa a nivel de conexión.

Para facilitar la conexión de los sensores y actuadores usaremos una placa "Sensor Shield v5"

![](./images/arduino_sensor_shield.png)

Que nos proporciona conexión para V, GND, Señal para cada sensor. Por ello usaremos sensores en formato módulo que nos facilita la conexión, puesto que los módulos tiene las mismas 3 conexiones: V, GND y S

## Programación con bloques

Para programar usaremos una herramienta web de programación con bloques Arduinoblocks

Comenzaremos usando [ArduinoBlocks.com](http://www.arduinoblocks.com): una herramienta de programación con bloques ideal para iniciarse.

Instalamos [ArduinoBlock Connector](http://www.arduinoblocks.com/web/site/abconnector5) que nos permite sincronizar el programa en el estamos trabajando con la placa

![](./images/ArduinoBlockConnector.png)

[Creamos nuestra cuenta](http://www.arduinoblocks.com/web/site/register) donde se guardarán nuestros proyectos:

![](./images/ArduinoBlocks_registro.png)

## Creando proyectos

Creamos proyecto personal con la placa ESP32 STEAMakers, que no es exactamente la nuestra pero sí es compatible

![](./images/arduinoblocks_creando_proyecto.png)

Documentaremos la descripción del proyecto y los componentes que vamos a usar en cada montaje.

## Encendiendo el LED de la placa

Usaremos el led que incluye la placa Wemos D1 que está conectado al pin 2

No necesitamos conectar nada

![](./images/arduinoblocks_led_2.png)

[Led 2 Steamakers](http://www.arduinoblocks.com/web/project/999667)


## Controlando el brillo de un led

Vamos a controlar ahora el brillo de un led analógicamente

[led 2 PWM](http://www.arduinoblocks.com/web/project/999877)

![](./images/arduinoblocks_led2_PWM.png)

Necesitamos:

* Wemos R32 D1
* Cable USB

Veremos como el led va cambiando su brillo en 4 niveles.

### Relé

Ahora vamos a conectar un relé para poder controlar dispositivos de más potencia

1. ¿Qué es un **relé**? un relé es un interruptor eléctrico que podemos accionar electrónicamente con una pequeña corriente y que funciona casi siempre electromecánicamente (un electroimán que atrae un contacto eléctrico) de ahí el 'clic-clic' que hacen al funcionar. 
![](./images/rele-electromagnetico.png)
1. Uso: los usaremos para controlar dispositivos que necesitan más potencia  que nuestra placa y/o que funcionan a mayores voltajes.
1. Control: para activar/desactivar los relés sólo tenemos que activar/desactivar el pin de nuestra placa al que está conectado
1. Alimentación y Consumo: el control de varios relés requiere de una mayor potencia de la que puede suministrar el puerto USB, por lo que usaremos un alimentación más potente si es posible.
1. Puesto que las señales de control de las placas son de 3.3V pudiera ser que algunos relés no se activen correctamente, aunque la mayoría sí. Lo que es importante es que alimentemos el relé (patilla V o Vcc) con 5V.

Conectamos el relé al pin 26

![](./images/montaje_rele_26.png)

Necesitamos:

* Wemos R32 D1
* Sensor Shield
* Cable USB
* Relé


El [programa](http://www.arduinoblocks.com/web/project/1001410) será el siguiente

![](./images/arduinoblocks_rele_26.png)

Activamos la consola, seleccionamos la velocidad adecuada y pulsamos "Conectar"

![](./images/ConsolaSerie.png)



## Controlando relés

Una aplicación directa de lo que hemos visto activando leds, puede ser controlar un módulo con varios relés al mismo tiempo.

![](./images/modulo_8xreles.jpeg)

Como hemos dicho, un relé es un dispositivo que nos permite controlar un dispositivo conectado a la corriente con una salida de nuestro dispositivo y sus modestos 5 voltios. Es decir, el relé actúa como un interruptor electrónico y al activar la patilla que lo controla se cierra el contacto que deja pasar la corriente al dispositivo

![](./images/steamakers_rgb_rele_bb.png)

En el montaje del ejemplo vemos como el relé 1 actúa como interruptor del circuito de alimentación de la bombilla. Al activar la salida 18, que controla el relé 1 (por estar conectada a IN1) cerrará la salida del relé y la alimentación llegará a la bombilla. Podemos poner la alimentación desde un enchufe o desde cualquier otra fuente de alimentación. Los relés funcionan como un interruptor eléctrico.

![](./images/steamakers_rgb_rele_motor_bb.png)

Los dos circuitos eléctricos, de alta potencia (el motor) y el de baja potencia (la placa) están aislados entre sí. No obstante **hay que tener cuidado al manejar la parte de alto voltaje/potencia**

## Sistema de riego

Podemos hacer distintas versiones:

* Tiempo: actúa como un temporizador, que se activará con cierta frecuencia. Tiene el inconveniente de que puede que reguemos sin necesidad, si ha llovido por ejemplo
* Humedad del suelo: medimos la humedad del suelo y por debajo o encima de un valor activamos o apagamos el riego
* Humedad y lluvia: detecta si llueve para en ese caso no activar el riego


## Medida de humedad

Medimos la humedad del suelo y por encima/debajo de un valor activamos/apagamos el riego. 

![](./images/Medidor_humedad.png)

[Proyecto](http://www.arduinoblocks.com/web/project/1001668)

Necesitamos:

* Wemos R1
* Cable USB
* Relé
* Bomba de riego
* Pila de 9v
* Sensor de humedad

![](./images/wemos_medidor_humedad_bb.png)

Tenemos que determinar el valor de nuestro sensor que vamos a usar como umbral


## Wifi

Creamos una red wifi a la que nos conectamos para poder controlar el riego

[Proyecto wifi](http://www.arduinoblocks.com/web/project/1005666)

![](./images/riego_wifi.png)

![](./images/wemos_riego_wifi.png)

Para ver el resultado o para controlarlo tenemos que conectarnos al wifi y en un navegador abrir la dirección http://192.168.4.1 

Desde ahí podemos activar o desactivar el riego

## Pantalla LCD

Vamos a conectar una pantalla LCD (como las máquinas de vending)

La conexión es muy sencilla puesto que la LCD tiene las mismas 4 conexiones que la placa Sensor Shield

![](./images/wemos-medidor-humedad-LCD_bb.png)


* Wemos R32 D1
* relé - pin 26
* pila 9v
* cable usb
* bomba de riego - contectada al relé
* sensor de humedad - pin 4
* Pantalla LCD I2C

En el [programa](http://www.arduinoblocks.com/web/project/1148717) añadimos la configuración de la pantalla donde necesitamos saber el número de caracteres que tiene (2 filas y 16 columnas) y la dirección que es un número que nos da el fabricante (0x27 en la mayoría) 

Mostraremos en la pantalla el valor de la humedad del suelo y el estado del riego

![](./images/wemos_riego_wifi_lcd.png)

## Riego + LCD + Sensor de humedad y temperatura DHT11 

Vamos a añadir ahora un sensor de temperatura y humedad DHT11 conectado al pin 14

![](./images/wemos-medidor-humedad-LCD-DHT11_bb.png)


* Wemos R32 D1
* relé - pin 26
* pila 9v
* cable usb
* bomba de riego - contectada al relé
* sensor de humedad - pin 4
* Pantalla LCD I2C
* sensor DHT11 en pin 1

Mostraremos los datos de los sensores y el estado del riego/relé en la pantalla

[Proyecto](http://www.arduinoblocks.com/web/project/1148733)

![](./images/wemos_riego_wifi_lcd_dht11.png)

## Apéndice ESP32

Vamos a ver los detalles de la placa

![Pinout](./images/ESP32Pinout.png)

```
CPU: Xtensa dual-core 32-bit LX6 microprocessor 160 o 240 MHz hasta 600 DMIPS
Ultra low power (ULP) co-processor
Memoria: 520 KiB SRAM
Wi-Fi: 802.11 b/g/n
Bluetooth: v4.2 BR/EDR and BLE
12-bit SAR ADC en 18 canales
2 × 8-bit DACs
10 × sensores capacitivos GPIOs
4 × SPI
2 × I²S interfaces
2 × I²C interfaces
3 × UART
SD/SDIO/CE-ATA/MMC/eMMC 
SDIO/SPI slave 
Ethernet MAC con DMA 
CAN bus 2.0
Controlador Infrarrojo (TX/RX, en 8 canales)
Motor PWM
LED PWM (up to 16 channels)
Sensor de efecto Hall 
Ultra low power analog pre-amplifier
```

[Más detalles](http://kio4.com/arduino/100_Wemos_ESP32.htm)

## Correspondencia Arduino UNO - [Wemos D1 R32](https://solectroshop.com/product-spa-1993-Wemos-D1-ESP32-R32-WROOM-32-WiFi-y-Bluetooth.html)

```
Alimentación: 5-12VDC
WiFi 802.11 b/g/n/e/i (802.11n hasta 150 Mbps)
Bluetooth v4.2 BR/EDR y BLE.
Compatible con shields de Arduino Uno.
6 Entrada analógica.
20 Entradas/Salidas digitales (3.3V) (con funciones PWM, interrupción).
Comunicación UART, SPI, I2C.
Tamaño: 68×53 mm
Conexión micro USB.
4Mbytes Flash Memoria 520Kb
Reloj: 240Mhz (un núcleo dedicado al procesaro WiFi)
Temperatura: -40C+85C
Corriente: 250mA (max)
Corriente en modo ahorro: 0.15mA
Corriente de funcionamiento: 20mA (sin WiFi)
```

![](./images/Pinout-Arduino-WemosD1R32.png)
![](./images/Correspondencia-Arduino-WemosD1R32.png)

Imágenes cortesía de 
[Leopoldo Armesto Ángel](https://www.slideshare.net/LeopoldoArmestongel), Lecturer at Universitat Politècnica de València (UPV)

## Configuración del IDE de Arduino

Si queremos usar el código de los programas tendremos que configurar el IDE de Arduino

En el menú Preferencias 

![](./images/ESP32Preferencias.png)

Añadimos la direccion del paquete de hardware de Espressif 

[https://dl.espressif.com/dl/package_esp32_index.json](https://dl.espressif.com/dl/package_esp32_index.json)


![](./images/ESP32AddURL.png)

Ahora en gestor de tarjetas 

![](./images/ESP32GestorTarjetas.png)

buscamos **ESP32**

![](./images/ESP32-Instalar.png)

Y lo instalamos.

Ahora podremos seleccionar las placas de tipo **ESP32**

Aunque no viene nuestra placa, podemos seleccionar una compatible: **DOIT ESP32 DEVKIT V1**


![](./images/Configuracion-IDE-Arduino.png)

## Driver

[Drivers para CH341 en windows](http://kio4.com/arduino/imagenes/ch341ser_win.zip)


