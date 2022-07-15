# Gateway LoRa - Microcontrolador ESPTTGO v1

> Dispositivo disponible en: [CRCibernetica](https://www.crcibernetica.com/ttgo-esp32-with-lora-and-oled-display-us915/) - Un nodo de sensado de enlace simple privada.

Colección de proyectos IoT para el programa de Hortalizas de la Estación Experimental Fabio Baudrit [UCR](https://eeafbm.ucr.ac.cr/).


### Empezando

Estas instrucciones le proporcionarán una copia del proyecto en funcionamiento en su máquina local para fines de desarrollo y prueba. Muy útil para pruebas de rendimiento, distancia y ajustes de backend..

### Requisitos previos

Qué cosas necesita para compilar y cargar el código y cómo instalarlas

1. ESP TTGO OLED V1.1 (disponible en [CRCibernetica](https://www.crcibernetica.com/ttgo-esp32-with-lora-and-oled-display-us915/)) 

2. Windows 10, Linux, MacOS con VSCode y Platformio instalado (mi versión VSCode: 1.68.1 (Universal))

3. Cable USB con Micro-B para conectar a ESPTTGO

4. Servidor MQTT (estoy ejecutando EMQX en Docker)


### Instalación y Uso

Un paso a paso que le indica cómo poner en marcha un entorno de desarrollo/producción

1. Abra el VSCODE
2. Clone el proyecto git clone https://github.com/AgroExperimentalFB/LoRaNode_ESPTTGO.git
3. Agregue su información de red, endpoint, MQTT y servidor en user-variables.h
4. El main.cpp contiene una variable llamada SensorPin de conversión analogico a digital que recibe el valor del sensor conectado en la función readSensor().
5.El loop ejecuta sendSensorValue() después de leer el sensor para iniciar una comunicación LoRa privada y enviar el paquete a un gateway cercano. 
6. El waitingResponse() es un listener LoRa que recibe la confirmación del LoRaGateway_ESPTTGO más cercano antes de activar la función goToDeepSleep() y permancer en modo ultra ahorro de  energía según lo configurado en la variable TIME_TO_SLEEP de user/variables.h.



### Funcionamiento

El LoRaNode_ESPTTGO se activará cada X minutos (TIME_TO_SLEEP), leera el sensor y enviará el datos al LoRaGateway_ESPTTGO más cercano. 

Una vez que recibe una confirmación del gateway, entra en modo ahorro de energía nuevamente. De lo contrario esperará 30 segundos antes de volver a dormirse para conservar la carga de la batería

Este proyecto emplea una red LoRa privada entre este LoRa Nodo y un LoRa Gateway..

El envío por http no está implementado ya que recomendamos manejar las reglas de guardado en bases de datos desde un broker MQTT o en tu propio backend.

El protocolo LoRA pertence a las redes LPWAN de ultrabajo consumo de energía y largo alcance de comunicación.

### [Video Demostración](https://youtube.com/shorts/CW2P_thfWiE)


### Despliegue

Consulte las instrucciones en **Requisitos previos**


### Autores

* [ISProjectsIoTCR (colaborador)](https://github.com/ISProjectsIoTCR)

### Licencia

Momentaneament: Este proyecto tiene la licencia MIT; consulte el archivo [LICENSE.md](LICENSE.md) para obtener más información.






