# 02 — Auditoría inicial de Nginx

**Comprobación inicial:** 29/10/2026 · **Tipo:** diagnóstico de solo lectura

## Objetivo

Comprobar el estado de Nginx y reconocer los bloques HTTP/HTTPS antes de incorporar otro sitio

## Herramientas usadas

```bash
nginx -v
systemctl is-active nginx
sudo nginx -t
```

`nginx -T` se utilizó en el análisis interno para revisar configuraciones e inclusiones, pero su salida completa no se publica

## Hallazgos

- Servicio web activo y configuración sintácticamente válida
- Bloque predeterminado HTTP y bloque independiente para la aplicación existente
- HTTPS con certificado TLS y backend PHP-FPM a través de socket local
- Se identificó la necesidad de evitar que el sitio existente fuese seleccionado como destino HTTPS predeterminado

La sintaxis válida no prueba por sí sola accesibilidad pública ni seguridad de la aplicación. Estas comprobaciones pertenecen a la auditoría inicial y se ampliaron con pruebas funcionales posteriores

## Observación TLS

En la auditoría inicial se detectaron directivas TLS en distintos archivos de configuración. No se acreditó en ese momento una comprobación externa exhaustiva de todas las versiones TLS realmente aceptadas
