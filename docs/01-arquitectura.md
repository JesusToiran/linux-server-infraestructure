# 01 — Arquitectura y distribución de tráfico

**Intervención:** 30/10/2026

## Objetivo

Alojar dos proyectos de forma independiente en un servidor Linux, manteniendo Nginx como punto de entrada HTTP/HTTPS y evitando que los nombres desconocidos lleguen accidentalmente a una aplicación legítima

```text
Clientes HTTP/HTTPS
       |
       v
     Nginx
       |
       +-- Nombre desconocido -> rechazo por servidor predeterminado
       +-- Sitio A -> aplicación web con backend PHP
       +-- Sitio B -> portfolio HTML estático
```

Nginx selecciona virtual hosts mediante el nombre solicitado y, para HTTPS, participa SNI en la negociación TLS. Cada proyecto dispone de raíz web y certificado separados

La configuración de rechazo del servidor predeterminado no impide solicitudes a nombres legítimos, ni sustituye validación, autenticación y mantenimiento de las aplicaciones

## Separación operativa

Se conservó el sitio existente y se incorporó un segundo sitio con directorio público propio. El sitio B se preparó inicialmente con acceso restringido antes de su apertura controlada

Se documentaron copias de seguridad, validación sintáctica previa y recarga en lugar de reinicio completo
