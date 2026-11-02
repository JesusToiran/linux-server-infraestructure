# Mantenimiento y actualización de Ubuntu Server

**Fecha:** 2 de noviembre de 2026  
**Sistema:** Ubuntu Server 24.04 LTS  
**Entorno:** servidor Linux con aplicaciones web en producción

## Objetivo

Actualizar los paquetes del sistema sin cambiar la versión principal de Ubuntu ni intervenir en el código de las aplicaciones. Antes de instalar, se revisaron los cambios previstos, el estado de los servicios y las opciones de recuperación.

## Revisión previa

Se actualizó el índice de paquetes y se consultaron las versiones disponibles:

```bash
sudo apt update
apt list --upgradable
sudo apt-get -s upgrade
```

La simulación mostró **55 paquetes actualizables**, ninguno nuevo y ninguna eliminación. Se dejó pendiente una biblioteca de procesamiento de imágenes (`libgd3`), cuya versión candidata procedía de un repositorio externo. La actualización de ese paquete se evaluará por separado.

También se comprobó el estado de los servicios con `systemctl` y el espacio libre con `df -hT`. No había unidades fallidas ni un reinicio pendiente antes de la intervención. Los servicios principales estaban activos.

## Copias de seguridad

Antes de instalar los paquetes se generaron respaldos de:

- Las bases de datos de las aplicaciones y los datos administrativos de MariaDB
- Los directorios de las aplicaciones web
- La configuración del sistema, incluidos los servicios y sus ajustes de seguridad

Los archivos se guardaron inicialmente en una ubicación restringida del servidor. Se aplicaron permisos de lectura y escritura solo para el administrador y se comprobó que los archivos comprimidos podían leerse. En el respaldo SQL se revisó la presencia de las bases previstas y el marcador de finalización del volcado. Las tablas de las bases de aplicación utilizaban InnoDB, compatible con el volcado transaccional empleado.

Se calcularon huellas **SHA-256**, se transfirieron las copias a un equipo externo mediante **SCP sobre SSH** y se compararon las huellas completas después de la descarga. Las tres comparaciones fueron correctas. Finalmente se eliminó la carpeta temporal utilizada para transferir los archivos.

**Alcance de la verificación:** la integridad de la transferencia quedó comprobada. No se realizó una restauración completa en un entorno aislado, por lo que la recuperabilidad de extremo a extremo sigue pendiente de prueba. Los respaldos y sus contenidos no forman parte de este repositorio.

## Actualización del sistema

Antes de instalar se repitió la simulación y se comprobó que no había una operación de APT o DPKG en marcha. Después se ejecutó:

```bash
sudo apt-get upgrade
```

El gestor de paquetes presentó el mismo plan revisado previamente: **55 paquetes actualizados, ninguno instalado adicionalmente, ninguno eliminado y uno retenido**.

Durante la instalación se reiniciaron varios servicios del sistema, entre ellos el servicio SSH y el proceso PHP-FPM. Otros reinicios de servicios quedaron aplazados por el gestor de reinicios. La sesión remota siguió disponible. El sistema no solicitó reiniciar el servidor al terminar.

No se ejecutaron `full-upgrade`, `autoremove` ni una actualización mayor de distribución.

## Comprobaciones posteriores

Tras la instalación se revisaron los siguientes puntos:

| Comprobación | Resultado |
|---|---|
| Servicios web, base de datos, caché, PHP-FPM, protección SSH y acceso remoto | Activos |
| Unidades fallidas de systemd | Ninguna |
| Reinicio del sistema | No requerido |
| Paquetes pendientes | Solo `libgd3` |
| Respuesta HTTPS de los dos sitios publicados | HTTP 200 en ambos |
| Sintaxis de configuración de nginx | Correcta |
| PHP en consola y extensiones necesarias | Disponibles |
| Conectividad local de MariaDB | Correcta |
| Respuesta de Redis a `PING` | `PONG` |
| Consola de Laravel | Ejecuta correctamente |
| Consulta de esquema de base de datos desde Laravel | Correcta |

La aplicación Laravel seguía en modo producción, con depuración y mantenimiento desactivados. Se verificó además que conservaba el enlace de almacenamiento público. Estas pruebas comprueban disponibilidad y conectividad básicas; no equivalen a una prueba funcional completa de todos los procesos de negocio.

## Pendientes

- Evaluar por separado la actualización de `libgd3` y el repositorio del que procede
- Probar la restauración de los respaldos en un entorno aislado
- Definir una política de copias automáticas y de conservación externa
- Revisar los paquetes propuestos por `autoremove` antes de eliminar nada
- Programar pruebas funcionales de las operaciones principales de las aplicaciones

## Criterios de seguridad aplicados

Se evitó modificar configuraciones de producción sin necesidad, cambiar permisos de los archivos originales para su transferencia o publicar información sensible. Se utilizaron conexiones SSH existentes, respaldos con acceso restringido y verificaciones de integridad. No se publican volcados SQL, archivos `.env`, claves, certificados privados, direcciones de acceso administrativo ni detalles internos de red.

## Conclusión

La actualización de mantenimiento terminó sin servicios fallidos ni necesidad de reiniciar el servidor. Los sitios publicados respondían correctamente y las comprobaciones básicas de la aplicación y sus dependencias fueron satisfactorias. Se mantuvo un paquete pendiente para revisarlo aparte y se conservaron copias externas verificadas antes de intervenir.
