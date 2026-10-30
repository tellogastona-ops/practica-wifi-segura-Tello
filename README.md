# Informe de Auditoría de Red Wi-Fi Insegura

## 1. Introducción
Este informe documenta los riesgos técnicos asociados a la navegación en redes Wi-Fi públicas mediante la auditoría de una conexión HTTP sin cifrar, evidenciando cómo la falta de seguridad en la capa de transporte expone los datos de los usuarios.

## 2. Sitio Analizado
* **URL Objetivo:** `http://funinnershinyjoke.neverssl.com/online/`
* **Motivo de selección:** Sitio de pruebas empleado para forzar el uso del protocolo HTTP clásico sin redirección automática a HTTPS.

## 3. Evidencia Observada (Herramientas de Desarrollador)
A partir de la inspección de la red (`Network`), se registraron los siguientes parámetros reales de la petición:
* **Request URL:** `http://funinnershinyjoke.neverssl.com/online/`
* **Request Method:** `GET`
* **Status Code:** `200 OK` (con una dirección IP remota `34.223.124.45:80`, utilizando el puerto 80 estándar de HTTP).
* **Cabeceras de Respuesta (Response Headers):**
  * **Server:** `Apache/2.4.68`
  * **Content-Type:** `text/html; charset=UTF-8`
* **Cabeceras de Petición (Request Headers):**
  * **Host:** `funinnershinyjoke.neverssl.com`
  * **User-Agent:** `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36...`
  * **Referer:** `http://neverssl.com/`

## 4. Riesgos Encontrados en Redes Wi-Fi Públicas
Navegar mediante HTTP en una red inalámbrica abierta expone al usuario a las siguientes vulnerabilidades:
* **Intercepción y Escucha (Sniffing):** Al no existir cifrado (TLS/SSL), cualquier atacante conectado a la misma red puede capturar los paquetes de datos y leer información como las cabeceras, el User-Agent o las cookies en texto plano.
* **Ataques de Intermediario (MitM):** Un atacante puede suplantar el tráfico o inyectar contenido malicioso al no haber validación criptográfica de la identidad del servidor.

## 5. Cómo Ayuda una VPN
La utilización de una Red Privada Virtual (VPN) soluciona este escenario mediante:
* **Cifrado de extremo a extremo:** Los datos son encriptados en el dispositivo antes de salir al router inalámbrico de la red pública.
* **Túnel seguro:** Todo el tráfico viaja encapsulado, de modo que si un atacante intercepta los paquetes, solo visualizará ruido cifrado e ilegible.
* **Privacidad:** Oculta el destino real de las peticiones web al enrutar las consultas a través del servidor seguro de la VPN.

## 6. Las 3 Reglas de Oro para Redes Wi-Fi Públicas
1. **Verificar siempre el uso de HTTPS:** No ingresar credenciales, datos bancarios ni información personal en sitios que operen bajo el protocolo HTTP.
2. **Activar una VPN de confianza:** Utilizar un túnel cifrado antes de navegar o realizar cualquier transmisión de datos en redes abiertas de cafés o aeropuertos.
3. **Evitar la conexión automática:** Desactivar la opción de conectarse automáticamente a redes públicas abiertas para prevenir ataques de redes gemelas (*Evil Twin*).