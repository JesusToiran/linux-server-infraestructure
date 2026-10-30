# 04 — Endurecimiento de Nginx

**Fecha:** 30/10/2026

## Cambio aplicado

Se creó un virtual host predeterminado independiente, sustituyendo el comportamiento de bienvenida inicial

- Para solicitudes HTTP con nombre desconocido se configuró `return 444`
- Para conexiones HTTPS con SNI desconocido se configuró `ssl_reject_handshake on`
- Se preservaron los virtual hosts legítimos y sus certificados
- Se incluyeron listeners IPv4 e IPv6 en la configuración de rechazo

## Método de cambio

1. Inventario de archivos habilitados
2. Respaldo de la configuración y comprobación de legibilidad
3. Preparación de un archivo de rechazo separado
4. Cambio controlado de enlaces habilitados
5. Validación mediante `nginx -t`
6. Recarga controlada y comprobaciones funcionales

## Resultados

La prueba HTTP con Host desconocido terminó sin respuesta HTTP, como corresponde al mecanismo 444. La negociación TLS con SNI desconocido fue rechazada

La aplicación existente siguió operativa y su redirección HTTP a HTTPS respondió con código 301

El cambio reduce exposiciones accidentales pero no elimina ataques contra sitios conocidos

Ver [ejemplo de rechazo](../examples/catch-all.conf.example) — archivo ilustrativo, no copia de producción
