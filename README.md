# Laboratorio 2: Dulce Hogar (Equipo 03)

Servidor web Apache en WSL2/Ubuntu con Virtual Host `dulcehogar.local`,
reverse proxy hacia un backend Express/TypeScript y HTTPS local con mkcert.

## Contenido del repo

| Archivo | Qué contiene |
|---|---|
| `fase1-dimensionamiento.txt` | Dimensionamiento y decisión nube/local |
| `fase2-apache.txt` | Instalación y verificación de Apache |
| `fase3-virtualhost.txt` | Virtual Host, proxy y permisos |
| `fase4-https.txt` | Certificados mkcert y Virtual Host SSL |
| `config/` | Archivos de configuración de Apache |
| `capturas/` | Evidencia del entorno propio |

## Quién hizo qué

| Integrante | Rol | Fases |
|---|---|---|
| Oscar Aguilar | Coordinador / Git | 1 y transversal |
| Jorge Lara | Adm. de Servidor Base | 2 |
| Jonathan De la O | Adm. de Redes / Proxy | 3 |
| Julio Ventura  | Adm. de Certificados | 4 |
| Ezequiel Reyes | Adm. de Permisos | 3 y 4 |
| Isvi Castillo | Documentador / QA | todas |

## Errores encontrados

| Error | Causa | Solución |
|-------|-------|----------|
| Puerto 9000 ocupado por blog.local | El contenedor de la Clase 19 estaba corriendo en Windows | Decidimos crear un contenedor nuevo en WSL2 (dulcehogar) |
| nohup no mantenía el contenedor | El proceso se detenía al cerrar la terminal | Usar systemd para que se reinicie automáticamente |
| ReferenceError: app is not defined | El index.js quedó incompleto al editarlo con nano | Reescribir el archivo completo con require, app, rutas y listen |
| 503 Service Unavailable | El contenedor Express no estaba corriendo cuando Apache intentó hacer el proxy | sudo systemctl restart dulcehogar y verificar con curl localhost:9000 |
| Could not resolve host dulcehogar.local | Faltaba la entrada en /etc/hosts (WSL2) y en el hosts de Windows | Agregar 127.0.0.1 dulcehogar.local y ::1 dulcehogar.local |
| Puerto 8900 no escuchaba | Faltaba Listen 8900 en /etc/apache2/ports.conf | Agregar la directiva y reiniciar Apache |
| CRYPT_E_NO_REVOCATION_CHECK | curl.exe en Windows no puede verificar la revocación de la CA local | Usar curl.exe --ssl-no-revoke o probar directo en el navegador |
