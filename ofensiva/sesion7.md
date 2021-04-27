# Sesión 7 - Acceso a credenciales y autenticación en directorio activo



__NTLM__

Relay
Pass-the-hash
Responder


__Kerberos__

F. bruta
Pass-the-ticket
Golden ticket
Silver ticket
AS-RePoasting



__Protocolo de autenticación__:

* Verificación de identidades
* Mutuo o de un sentido

__Protocolo de intercambio de claves__:
* Simétrica

* Asimétrica
  * Certificado



Tanto NTLM como kerberos son protocolos __simétricos__
* Kereros autenticaión mutua
* NTLM Autenticación de un sentido


Cliente -------- Servidor [Ks]

Problema criptografía simétrica, la __escalabilidad__

Secreto compartido: Password

Problema:
* Almacenamiento de contraseñas
  * Hash
  * Función de derivación de clave (Lentas, no tienen que ir bien en hardware!)
* Envío (canal cifrado)


Importante autenticador


## Noticia de la semana

Qué rapido se explota la vulnerabilidad, de exchange

usos, desde espionaje hasta despliegue de ransomware o minado

siempre se usan ests cosas para minado


se democratiza las capacidades de explotación, ya por fin esta en metasploit




### Inicio de sesión en Windows

LSA (Local Sevice Authority)


Basicamente e enarga de la autorizacion de lo susuarios

cunadno recibe un usuario y contraseña lo primer es determinar si es usuario local o de dominio

__LSASS (LSA Subsystem Service)__

* Proceso muy importante, porceso Windows q gestionar el LSA
* q mantiene en memoria la información relativa a las credenciales de los usuarios
* Va desde credenciales en claro a Hashes de distintos tipos
* 3 tipos:
  * Credenciales, hashes, tickets


Podemos coger información q hemos tenido  ee intectarla dentro del proceso, para q entienda q tiene q usar esas crdenciales

las manipulacion de KSASS va a ser ka ase de los araques verenos hoy





si es local verificar las credenciales de manera local
con independencia de los usuarios de dominio pueden ser locales




las credenciales se almacenan en LSASSS y ahora quiero acceder a recursos de la red, windows arbitra o define un conjunto de protocolos para acceder a esos recursos de red, en cada uno de esos accesos debemos acreditarnos, si nosotros no tenemos un protocoo q nos diga eso, tebdrenis q decurki a¡cada ez


protocolo de inicio de sesion unica (Single Sing-On) guarda una evidencia que has mostrado tu identidad y la usa cuando la necesites

En ambito Web, protocolo SAML de inicio de sesií única


LM /NTLM/NTLMv2 protocolos con problemas de seguridad importantes, deberiamos deshabilitar su uso, sin embargo se siguen usando, es un problema de por sí

2 problemas fundamentales

* lm ntlm utiliza mecanismos criptograficos q son débiles
* Susceptibles a atques de interceptación y reenvío

Autenticación de red en Windows, 


va a haber un cliente utilizando un mecanismo de autenticacion de red

el server generara un access token impersonation

### protocolo de red que vamos a utilizar, el NTLM


protocolo de desafío-respuesta

C - S

1. ataque, capturo los hshes y lo crackeo
2. NTLM Relay
3. Responder
   1. un valor derivado de la ocntrasñea del usuario offline...



### Ataque NTLM: Pass the hash

Autenticación NTLM




memoria del proceso el lsass para cuentas con privilegios de dominio

__ntds.dit__: 
* base de datos de credenciales de un controlador de dominio


### DCSync

existe funcionalidad para forzar la replicacion de ntds.dit en otro dominio, vamos a forzar esta funcinalidad para q se el controlador de dominio asumiendo q somos un controlador q de forma legitima queremos hacer esto

### DShadow

en vez de querer replicar



# Protocolo Kerberos

protocolo de autenticavcion



el usuario como paso previa se va a autenticar contra el DC,

va a haber un 1 proceso en el q el usuairo se va a conectr contra el CD, el CD le da un valor q servira de garantía, ete 1 paso significa para decir al CD que somos quien decimos ser


cuando queremos acceder a un servicio, 


hacemos x nos da un valor q debemos d presentar el valor q me ha dado

a estos valores les llamamos tickets

tenemos un ticket para preetnarnos a nosotros, y otro para preentar a los demás ordenadores cuando queremos hacer otr cosa

1. ticket de autenticacion TGT
2. Ticket grant SErvice TGS
3. ticket para el tercero


el usuario siempre se accede autenticadose contra el CD


Campos:
Se genera el mensaje, AUTH Request
SPN krbtgt Nombre del serivcio y maquina donde esta 
el none
valor q demuestra mi identidad

firmo el timestamp (para evitar ataques de repetición)
* esto obliga al sincronismo de __tiempos__

1º ataque, si este mensaje lo mando y fallo, el DC me va a decir clave erronea, puedo hacer f. bruta

CD lo compara, si da el OK genera el mensaje;
* username
* User hash (cifrado, yo puedo descifrarlo)
* Clave de sesión (clave temporal q sirve para cifrar mensajes)
* krbtgt generar y cifrar esos tickets, el cliente puede recibir ese vaor pero no puede modificarlo, 


pra suplantar al usuario solo necesitamos el hash, no la contraseña

solicitud de acceso a un servicio

## Ataque Silver Ticket

