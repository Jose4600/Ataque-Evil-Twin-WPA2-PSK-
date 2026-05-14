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

### ¿Que es Airgeddon?
Airgeddon es un framework de auditoría de redes WiFi de código abierto desarrollado en Bash. Funciona como una herramienta "todo en uno" que integra y automatiza múltiples utilidades ya existentes (como aircrack-ng, hostapd, dnsmasq, lighttpd, etc.) en un único menú interactivo, simplificando procesos que de otro modo requerirían ejecutar y coordinar varios comandos de forma manual.
Entre sus funcionalidades principales están la captura de handshakes WPA/WPA2, ataques de desautenticación, auditoría de redes WEP, y varios tipos de ataques Evil Twin con portal cautivo.

### ¿Por qué lo usamos en esta práctica concretamente?

Lo elegimos por tres razones principales:

**Integración completa del ataque Evil Twin**: Airgeddon automatiza todas las fases del ataque (modo monitor, escaneo, captura de handshake, lanzamiento del AP falso, desautenticaciones continuas y portal cautivo) desde un único entorno, sin tener que coordinar herramientas por separado.

**Verificación automática de la contraseña**: A diferencia de otras herramientas, Airgeddon valida en tiempo real la contraseña que introduce la víctima en el portal cautivo contra el handshake WPA2 previamente capturado. Si la clave es incorrecta, el portal la rechaza y sigue pidiendo; si es correcta, el ataque se detiene y la muestra en texto claro. Esto elimina la necesidad de un proceso posterior de fuerza bruta.

**Facilidad de uso en entorno de laboratorio**: Al ser un script interactivo con menús guiados, resulta ideal para un entorno educativo donde el objetivo es entender el flujo del ataque, no memorizar decenas de parámetros de línea de comandos.

## Impacto de este tipo de ataque

El ataque Evil Twin permite al atacante obtener la contraseña WPA2 de una red corporativa en texto claro, sin necesidad de realizar fuerza bruta offline. Una vez en posesión de la clave, puede conectarse a la red legítima, interceptar tráfico interno y escalar el acceso a otros sistemas. Dado que se apoya en ingeniería social (el portal cautivo), resulta efectivo incluso contra contraseñas robustas que serían inviables de crackear por diccionario.

## Condiciones necesarias para que el ataque pueda suceder

<div>
  <ul>
  <li>Proximidad física a la red objetivo (cobertura WiFi).
  <li>La tarjeta WiFi del atacante debe soportar modo AP (Master).
  <li>Existencia de al menos un cliente conectado a la red legítima (para capturar el handshake y para enviarlo al AP falso).
  <li>La víctima debe introducir la contraseña en el portal cautivo (componente de ingeniería social).
  </ul>
</div>

## Ataque en entorno controlado
###  Paso a paso del ataque


<img width="1024" height="579" alt="image" src="https://github.com/user-attachments/assets/193aa2ce-8fe9-4ddf-825b-d2362d8a1c7a" />

<img width="1024" height="141" alt="image" src="https://github.com/user-attachments/assets/e1f7af9b-df70-41cf-9b10-efff5113066b" />

<img width="1024" height="366" alt="image" src="https://github.com/user-attachments/assets/ac236732-7f6a-48e6-884e-f891e5841358" />

<img width="1024" height="341" alt="image" src="https://github.com/user-attachments/assets/23b1d209-0192-4acb-ba43-88e46208670a" />

<img width="992" height="1024" alt="image" src="https://github.com/user-attachments/assets/5574e5c0-21a9-486c-b253-6551b02b6a91" />

<img width="1024" height="253" alt="image" src="https://github.com/user-attachments/assets/298f3bbb-806c-47b6-bb31-d5913cb41dfe" />

<img width="1024" height="342" alt="image" src="https://github.com/user-attachments/assets/8f0891ae-ebc5-4974-8e18-9ac23c3b2318" />

<img width="1024" height="294" alt="image" src="https://github.com/user-attachments/assets/8f093e4f-372d-40c4-a7aa-0d9e5989525d" />

<img width="1024" height="431" alt="image" src="https://github.com/user-attachments/assets/1a35ffd1-fed9-41e2-add5-f5d8b1ef454b" />

<img width="1919" height="894" alt="Captura de pantalla 2026-05-14 191047" src="https://github.com/user-attachments/assets/2246fc16-15e8-421e-95cf-9f2c90ec0763" />

<img width="1024" height="323" alt="image" src="https://github.com/user-attachments/assets/516b2e68-9c05-4f81-8fa8-83599490f0be" />

<img width="1024" height="332" alt="image" src="https://github.com/user-attachments/assets/9f8640bd-1a63-49d9-94b7-e50bc86bb935" />

## Modos de mitigación

**802.11w (Management Frame Protection - MFP)**: Cifra los frames de gestión (incluidos los deauth), dificultando que el atacante desconecte a los clientes de la red legítima.

**WIDS/WIPS (Wireless Intrusion Detection/Prevention System)**: Detecta la presencia de APs con el mismo SSID y alerta al administrador o bloquea activamente el AP falso.

**Certificados en redes empresariales (WPA2-Enterprise / 802.1X)**: Elimina el factor PSK compartido; cada usuario se autentica individualmente con credenciales o certificados, lo que hace inviable el portal cautivo.

**Formación y concienciación**: Instruir a los usuarios para que no introduzcan contraseñas WiFi en portales inesperados y que verifiquen el certificado SSL del portal si lo hay.

## Conclusión

El ataque Evil Twin demuestra que la mayor vulnerabilidad de una red WPA2-PSK no siempre es criptográfica, sino humana. Al combinar la suplantación técnica del AP con un portal cautivo creíble, el atacante puede obtener credenciales sin necesidad de fuerza bruta. La protección real requiere adoptar autenticación por certificados (WPA2-Enterprise), activar MFP/802.11w y disponer de un sistema de detección de intrusos inalámbrico.
Resumen final:
<div>
  <ul>
  <li>Invisibilidad: El AP falso es indistinguible del legítimo para el cliente promedio.
  <li>Gravedad: Obtención de credenciales en texto claro sin fuerza bruta.
  <li>Prevención: WPA2-Enterprise, 802.11w y concienciación del usuario son las contramedidas más efectivas.
 </ul>
</div>

