# Sesión 5 - Ejeccuión

* Prueba escrita 2 Marzo

* Punto de control de lo que hemos hecho

## Noticia de la semana


Francia vincula a los hackers rusos del [gusano](https://threatravens.com/france-links-russian-sandworm-hackers-to-hosting-provider-attacks/)  con los ataques a proveedores de alojamiento.

[Noticia](https://www.cert.ssi.gouv.fr/cti/CERTFR-2021-CTI-005/)


* __IoC__: Cualquier elemento de información que se puede corresponder con un activo malicioso, url, hash, firma, etc
* [Proyecto](https://www.misp-project.org/) financiado por la Unión Europea
  * SW libre
  * Ligero relativamente
  * manual extraordinario
  * Comunidad que aporta muchísimo, vídeos, etc

* TIP (Threat Intelligence Platform)
* Documentos de francia muy bien explicados, oro puro

## Ejecución

### Explotación por parte del usuario

Característica de seguridad que contrla las condiciones en las que PowerShell carga los archivos de configuración y ejecuta los scripts

Políticas:

* __Restricted__: No puede ejecutarse ningún script local, remoto o descargado en el sistema
* __AllSigned__: el script debe estar firmado para poder ejecutarse
* __RemoteSigned__: los scripts remotos o descargados deben estar firmados para poder ejecutarse
* __Unrestricted__: no es necesario que estén firmados


[Maneras de evadirlo](https://blog.netspi.com/15-ways-to-bypass-the-powershell-execution-policy/)

### Herramientas de despliegue de software
  * SCCM

  * invoke-expression
    * fileless
  * start-process
    * toca disco

* Powershell execution policies
  * Para los sysadmins si ejecutan algo sin querer
  * Se puede evadir


* Tareas programadas

  * Para escalada de privilegios

  * diskcleanup -> silent cleanup

  * modificando la variable Windir

  * Fuerzas una nueva tarea / programa para abrir un powershell como administrador



### living-off-the land binaries and scripts

* aka LoL

* Abuso de __binarios y scripts preinstalados en el sistema__

* [lolbas-project](https://lolbas-project.github.io)

* Para ser considerado un Lol debe estar presente en el sistema por defecto o deben haber sido instalados por usuarios.

* __BITSADMIN__: Herramienta de línea de órdenes que permite controlarlos trabajos del servicio BITS (Background Intelligent Transfer Service) de Windows que permite descargar o subir ficheros mediante HTTP o SMB.

* __CERTUTIL__: Herramienta de línea de órdenes para la manipulación de certificados x509.


* Equivalente en unix: [gtfobin](https://gtfobins.github.io)

### Uso de RUNDLL32

* Podemos emplear rundll32 para ejecutar una dll de nuestra elección

* Permite ejecutar código indirecamente que nos permite evadir mecanismos de listas blancas de aplicaciones
* También podemos ejecutar scripts en JS

### Uso de COM/DCOM

* COM (Component Object Model) y su extensión para entornos distribuidos (DCOM) son protocolos para la comunicación entre procesos de diferentes aplicaciones y lenguajes 
* Modelo de objetos distribuidos que cada uno tiene sus funcionaliddes que sean invocados por otros objetos
* Un cliente puede invocar métodos de otros servidores, que suelen ser DLLs o ejecutables
* DCOM es un middleware que permite extender la funcionalidad de COM a u entorno distribuido
  * Basado en RCP (__Remote Procedure Call__)


### Uso de Windows Managemen Instrumentation (WMI)

* WMI es un subsistema de PowerShell que habilita el __acceso a un conjunto de herramientas de monitorización y gestión del sistema__
  * Establecer configuraciones de seguridad
  * Recopilar información sobre redes y sistemas
  * Modificar permisos de usuarios y grupos
  * Configurar y editar distintas propiedades del sistema
  * Programar tareas
  * ...
* Podemos emplear WMI para:
  * Descubrimiento
  * Ejecución
  * Persistencia
  * Movimiento lateral

### Conceptos WMI

* La información del sistema operativo se represent como objetos WMI. Vda objeto es una instancia de una clase

### Windows remote Management (WINRM)

* WinRM es un servicio que pemite la interacción con un sistema remoto
* __Nos va a permitir crear una sesión remota de powershell__


### Metasploit Web_delivery

`use exploit/multi/script/web_Delivery`

### Windows Remote Management (WinRM)

Protocolo WS-Management

evil-winrm github

### Powershell remoting: ejemplo