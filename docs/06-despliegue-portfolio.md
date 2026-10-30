# 06 — Incorporación del portfolio y publicación DNS

**Fecha:** 30/10/2026

## Preparación

Se creó una raíz pública independiente para un portfolio estático, con permisos de escritura para el responsable del despliegue y lectura para el servidor web

Se publicó inicialmente una página HTML provisional y se configuró un virtual host específico

## Despliegue gradual

1. Prueba HTTP local satisfactoria
2. Restricción temporal de acceso desde fuera del servidor
3. Obtención de certificado TLS mediante desafío DNS-01
4. Activación y validación de HTTPS
5. Prueba de rechazo externo durante la fase restringida
6. Sustitución de la restricción temporal por una configuración de publicación con HTTPS
7. Actualización de registros A de los nombres web en el proveedor DNS

Se conservaron los servidores de nombres del proveedor y los registros ajenos al alojamiento web

## Estado al cierre

La variante `www` fue accesible públicamente mediante HTTPS y entregó la página HTML provisional. El DNS del dominio raíz ya respondía con la dirección nueva en la consulta al servidor del proveedor, aunque un resolvedor público conservaba temporalmente el valor anterior

Por tanto, **no se afirma** que la propagación global del dominio raíz hubiera concluido al momento de la evidencia

El contenido web mostrado era todavía una demo provisional, no un portfolio finalizado
