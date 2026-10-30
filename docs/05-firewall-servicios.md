# 05 — Firewall y servicios de red

**Fecha:** 30/10/2026 · **Tipo:** inspección, sin cambios en reglas

## Inspección

Se revisaron las políticas de UFW, las direcciones de escucha de los servicios y una vista filtrada de las reglas nftables

## Resultados observados

- UFW activo, con política restrictiva para conexiones entrantes
- Acceso administrativo y servicios web autorizados según su función
- Configuración de IPv4 e IPv6 presente
- Servicios examinados de base de datos y caché vinculados a interfaces locales
- Cadena de Fail2ban presente en el filtrado del sistema
- No se observaron redirecciones NAT en la salida **filtrada** examinada

No se modificaron las reglas de UFW ni se realizó una nueva prueba de penetración. Una vista filtrada no permite demostrar la ausencia absoluta de otras reglas o exposiciones

## Criterios

Mínimo privilegio, exposición reducida, control de acceso administrativo y separación entre servicios internos y públicos
