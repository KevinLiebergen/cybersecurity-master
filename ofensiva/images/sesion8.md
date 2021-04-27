# Sesión 8

## Artículo del cuatrimestre

Silverfish Group

Petar un C&C de los tios q petaron SolarWinds

paneles de control donde se concentraban la actividad, q hicieron y con qué

no está permitido, entrar a un C&c y encima publicarlo


https://www.prodaft.com/m/uploads/SilverFish_TLPWHITE.pdf

tenian distintos equipos, 4 y cada uno de los hakers estaba asignado un jira, cada obrero tenia tareas en el jira, solo podia ver sus tareas no las de otros, tenian tareas, ponian comentarios

dialecto rso origen urbano

### Applications Windows discovery


### Descubrimiento de servicios del sistema

determinar si existen conexiones mirando la tabla de conexiones, 



el 90% de los ransomwares si ven que el sistema tiene lengua eslava no cifran,  no se tiran piedras a sus sistemas

## Domain trust discovery

dominios de relaciones de confianza con otros dominios




## Conceptos básidocs del AD

LDAP DNS, Kerberos


Servicio de dominio dentro del directorio (AD DS)

información cifrada de manera jerárquica, q la bdd q represene este directorio, debería estar reflejado dentro del AD


reflejo de lo q consiste la organización, cada elemento son objetos dentro del DA

cuales son los objetos permitidos

mecanismo de consulta, protocolo

mecanismo de replicación, __distribuido__
* ataques dcca dccsoun(?)


protocolo DNS para búsuqeda de rcursos


descubrimiento de elementos clave en lgún determinado dominio

registros .txt

Inteactuar con los protocolos del AD?
* DNS
  * dig
  * nslookup
* LDAP
  * openldap
  * ldapsearch
* MS-RPC
  * Samba
  * Impacket



Registros SRV

__dns-srv-enum__
* para servicio kdc

despues consultas de tipo A para saber la IP


todas las consultas pasa por el CD


__ms_rcp__
protoolos q permiten el diálogo entre equipos de un dominio


## named pipes
interfaz fifo para el intercambio de informacion


intentan permiten la funcionalidd de comunicacion d procesos 

en una maquinale doy u n nombre y cualquier proceso q escriba por ese named pipe lo recibo yo, determinados procesos q llevan a cao determinados procesos en windpws

el socket va sobre tcp, el named pipe no se asume q va sobre esa cpa de trnasporte, es un canal  va por encima __dns-rcp__

funcionalidad para movimiento lateral 


__smb-beacon__