# 03 — Certificados TLS y HTTPS

## Inventario y evolución

En la inspección inicial se identificó un certificado ECDSA válido para el sitio existente, administrado mediante Certbot

En un documento interno del 29/10/2026 consta la presencia de `certbot.timer` y una simulación de renovación satisfactoria del certificado entonces existente. Esa evidencia **no cubre** el nuevo certificado emitido posteriormente

El 30/10/2026 se emitió un segundo certificado ECDSA para el portfolio y su variante `www` mediante validación DNS-01 manual

## Verificación

- Certbot mostró el nuevo certificado como válido
- Tras aplicar la configuración en Nginx, la conexión HTTPS local respondió satisfactoriamente y validó el certificado
- La variante `www` del portfolio respondió públicamente por HTTPS

## Pendiente

El certificado nuevo se emitió con autenticación manual sin hook automatizado: **su renovación automática no quedó resuelta**. No debe describirse como renovable de forma desatendida

El inventario y las fechas fueron válidos en el momento de la intervención, no constituyen una supervisión permanente
