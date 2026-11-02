# Infraestructura Linux: Nginx y seguridad web

Documentación técnica de una intervención real en un VPS Linux con dos sitios independientes: una aplicación web y un portfolio estático

El repositorio documenta decisiones de arquitectura, cambios controlados, verificaciones y limitaciones, sin publicar configuraciones de producción ni información privada de terceros

## Documentación

- [Arquitectura y distribución de tráfico](docs/01-arquitectura.md)
- [Auditoría inicial de Nginx](docs/02-auditoria-nginx.md)
- [Certificados y HTTPS](docs/03-certificados-tls.md)
- [Endurecimiento del servidor predeterminado](docs/04-hardening-nginx.md)
- [Firewall y servicios](docs/05-firewall-servicios.md)
- [Despliegue del portfolio y DNS](docs/06-despliegue-portfolio.md)
- [Verificaciones, alcance y pendientes](docs/07-verificaciones-pendientes.md)
- [Mantenimiento y actualización de Ubuntu Server](docs/08-mantenimiento-actualizaciones.md)
- [Política de publicación segura](SECURITY.md)

Los archivos de `examples/` son ilustrativos y **no reproducen** la configuración real del servidor

## Tecnologías

Ubuntu Server, Nginx, Let's Encrypt / Certbot, TLS, UFW, Fail2ban, nftables, SSH, PHP-FPM y herramientas de diagnóstico Linux

## Alcance

El trabajo acredita las comprobaciones descritas, no una auditoría de penetración completa ni una garantía de ausencia de vulnerabilidades
