# 07 — Verificaciones, alcance y pendientes

## Evidencias positivas

| Área | Comprobación observada |
|---|---|
| Nginx | Sintaxis correcta y servicio activo después de recarga |
| Servidor predeterminado HTTP | Cierre de conexión ante Host desconocido |
| Servidor predeterminado HTTPS | Rechazo de SNI desconocido |
| Aplicación existente | Carga desde navegador y redirección HTTP 301 |
| Portfolio HTTPS | Respuesta local satisfactoria con certificado validado |
| Aislamiento previo del portfolio | Respuesta 403 desde equipo externo |
| Publicación de la demo | Contenido accesible mediante `www` por HTTPS |
| DNS raíz | Dirección nueva visible en servidor DNS del proveedor |
| UFW y servicios | Reglas y sockets inspeccionados, sin cambios |

## Pendientes a fecha de intervención

- Renovación desatendida del certificado DNS-01 manual del portfolio
- Confirmación de propagación del dominio raíz entre resolvedores
- Investigación concluyente de ciertas respuestas históricas HTTP 200 a solicitudes sospechosas
- Evaluación externa de protocolos TLS aceptados, no acreditada por la auditoría inicial

## Límites

La revisión no es una auditoría exhaustiva. No se publica información sensible de clientes, infraestructura o eventos de seguridad. Una comprobación satisfactoria refleja su alcance y fecha concretos
