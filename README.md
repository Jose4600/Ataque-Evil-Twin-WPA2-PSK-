# Ataque-Evil-Twin-WPA2-PSK
## ¿Qué es un ataque Evil Twin?

El ataque Evil Twin es una técnica de auditoría de redes WiFi en la que el atacante crea un punto de acceso (AP) falso que suplanta a una red WiFi legítima. El objetivo es conseguir que la víctima se conecte al AP malicioso, creyendo que es la red real de su empresa u organización.
El proceso se divide en varias fases: primero se identifica la red objetivo y se captura un handshake WPA2; después se lanza un AP gemelo con el mismo SSID y canal, mientras se desautentica a los clientes de la red legítima mediante paquetes deauth. Al conectarse al AP falso, se le presenta a la víctima un portal cautivo (captive portal) que solicita la contraseña WiFi con el pretexto de una "actualización de firmware" u otro motivo creíble. La contraseña introducida se valida contra el handshake previamente capturado, y si es correcta, el atacante la obtiene en texto claro.

<img width="1200" height="708" alt="image" src="https://github.com/user-attachments/assets/22a9916a-788c-4db6-885d-93e81ca3e318" />

## Entorno de laboratorio:

Para la configuración del entorno se han seguido los siguientes recursos:

https://www.youtube.com/watch?v=sIcZqmJxan4 > Instalación de Kali Linux en VirtualBox

https://www.youtube.com/watch?v=Ws9b0tWcVF4 > Configuración de tarjeta WiFi Alfa en modo monitor


### Equipos y herramientas utilizados:

**Máquina atacante**: Kali Linux con tarjeta Alfa Wireless USB AWUS036ACH (o similar que soporte modo AP/Master).

**Red objetivo**: Red WiFi con cifrado WPA2-PSK en mi caso lo realizaremos sobre la red llamada CETI.

**Herramienta principal**: Airgeddon

Para verificar que la tarjeta soporta modo AP, ejecutar:

<img width="1024" height="317" alt="image" src="https://github.com/user-attachments/assets/77918a12-475c-477d-9383-a8330ccaba2b" />


### Instalación de Airgeddon:

![OS](https://img.shields.io/badge/OS-Kali_Linux-557C94?style=flat-square&logo=kali-linux) ![Tool](https://img.shields.io/badge/herramienta-Airgeddon-FF3333?style=flat-square) ![Category](https://img.shields.io/badge/categoría-Auditoría_Wireless-E05D44?style=flat-square)


```bash
git clone https://github.com/v1s1t0r1sh3r3/airgeddon
```
