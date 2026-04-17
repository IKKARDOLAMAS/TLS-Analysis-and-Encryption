# Análisis de Cifrado - La Barrera del Protocolo TLS

En el laboratorio anterior (Día 7), logramos interceptar credenciales en texto plano. Hoy, el objetivo fue analizar cómo el protocolo **HTTPS (SSL/TLS)** protege la información incluso cuando un atacante logra posicionarse en medio de la comunicación (MITM).

## 🎯 Objetivo
Validar la efectividad del cifrado de extremo a extremo y comparar la visibilidad de los datos entre protocolos HTTP y HTTPS mediante el análisis de paquetes.

## 🛠️ Herramientas Utilizadas
* **Kali Linux:** Máquina de monitoreo.
* **Ettercap:** Ejecución de ARP Spoofing para desviar el tráfico.
* **Wireshark:** Captura y análisis de flujos de datos cifrados.
* **Portátil física:** Generación de tráfico real hacia sitios seguros (Wikipedia/GitHub).

## 🔍 Observación Técnica
Al interceptar el tráfico de la portátil mientras navegaba por sitios con certificado SSL, se identificaron los siguientes puntos clave:

### 1. El Handshake (Apretón de manos)
En Wireshark se visualizaron los paquetes `Client Hello` y `Server Hello`, donde el navegador y el servidor negocian las llaves de cifrado.

### 2. Confidencialidad de Datos
Al intentar reconstruir la sesión mediante **Follow TCP Stream**, el resultado fue **Ciphertext** (Texto cifrado). A diferencia del Día 7, la información es totalmente ilegible para el atacante.



## 📊 Comparativa: Ataque MITM y Captura de Credenciales (Sinkhole) vs. TLS-Analysis-and-Encryption

| Característica | (HTTP) | (HTTPS) |
| :--- | :--- | :--- |
| **Visibilidad** | Texto plano (Legible) | Cifrado (Ilegible) |
| **Protocolo** | TCP / Puerto 80 | TLS / Puerto 443 |
| **Resultado MITM** | Robo de credenciales | Captura de ruido (Inútil) |

## 💡 Conclusión
Este laboratorio demuestra que el **ARP Spoofing** permite interceptar los paquetes, pero el cifrado **TLS** garantiza la confidencialidad. Sin la llave privada del servidor, el contenido interceptado no tiene valor para el atacante.

