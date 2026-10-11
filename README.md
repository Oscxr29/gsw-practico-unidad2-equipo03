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
| `nssm` no se reconoce como comando | NSSM no está en el PATH de Windows | Usar la ruta completa `C:\nssm\...\nssm.exe` o copiar `nssm.exe` a `C:\Windows\System32` |
| `ts-node` falla con `Cannot read properties of undefined` | Incompatibilidad de `ts-node` con Node.js 24 | Usar `tsx` en lugar de `ts-node` (`npm install --save-dev tsx`) |
| `npx ts-node` falla con rutas UNC en WSL2 | WSL2 está usando el Node.js de Windows (`/mnt/c/Program Files/nodejs`) | Instalar Node.js dentro de WSL2 (`sudo apt install nodejs`) y verificar con `which node` |
| Error 503 Service Unavailable en Apache | El contenedor Express no está corriendo | Iniciar el servicio: `sudo systemctl start dulcehogar` |
| `Could not resolve host: dulcehogar.local` | Falta la entrada en `/etc/hosts` (WSL2) o en el hosts de Windows | Agregar `127.0.0.1 dulcehogar.local` en ambos archivos hosts |
| `Could not connect to port 8900` | Apache no está escuchando en el puerto 8900 | Agregar `Listen 8900` en `/etc/apache2/ports.conf` y reiniciar Apache |
| `CRYPT_E_NO_REVOCATION_CHECK` al usar `curl.exe` | Windows no puede verificar la revocación de un certificado de CA local | Usar `curl.exe --ssl-no-revoke` o probar directamente en el navegador |
| `ReferenceError: app is not defined` en `index.js` | El archivo `index.js` quedó incompleto (faltó la inicialización de `express`) | Reescribir el archivo completo con `const app = express();` |
| `Permission denied` al ejecutar `./node_modules/.bin/ts-node` | El binario no tiene permisos de ejecución | Usar `chmod +x` o preferir `tsx` (`./node_modules/.bin/tsx archivo.ts`) |
| `confgtest` (typo) | Error de tipeo | Escribir correctamente `configtest` |
| `a2emmod` (typo) | Error de tipeo | Escribir correctamente `a2enmod` |
| `<hl>` en lugar de `<h1>` en el comando `echo` | Error de tipeo | Usar `<h1>Dulce Hogar</h1>` |
| `:1` en lugar de `::1` en el archivo hosts | Error de tipeo | Usar `::1 dulcehogar.local` |
| `900 0` en la respuesta JSON | Error de tipeo (espacio extra) | Corregir a `9000` |
| `ss -tlmp` en lugar de `ss -tlnp` | Error de tipeo | Usar `ss -tlnp` |
| `mkcert-install` (sin espacio) | Error de tipeo | Usar `mkcert -install` (con espacio) |
| `Generator` en lugar de `Generar` | Error de tipeo | Corregir a `# 2. Generar certificado` |
| `Administrator` en lugar de `Administrador` | Error de tipeo | Corregir a `Windows PowerShell (Administrador)` |
| `[completar]` en la tabla de pruebas de integración | Placeholder sin reemplazar | Completar con la respuesta real del `curl` |
| `cp \(\)` en los comandos | Artefacto de LaTeX al exportar | Usar `cp $(mkcert -CAROOT)/rootCA.pem ...` |
| `const express \(=\)` en el código | Artefacto de LaTeX al exportar | Usar `const express = require('express');` |
| `res.json({ mensaje: 'Hola, \(\Phi\) {nombre}'` | Artefacto de LaTeX al exportar | Usar backticks: `` `Hola, ${nombre}` `` |
| `const { nombre, telefono, producto } \(=\) req.query;` | Artefacto de LaTeX y falta de punto y coma | Usar `const { nombre, telefono, producto } = req.query;` |
