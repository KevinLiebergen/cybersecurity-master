# Sesion 6

https://threatfox.abuse.ch/

https://urlhaus.abuse.ch/


## Noticia de la semana

[Hafnium targeting Exchange Server with 0 day exploits](https://www.microsoft.com/security/blog/2021/03/02/hafnium-targeting-exchange-servers/)

Valoración del sistema que puede estar comprometido


Lo baja de internet lo almacena en memoria

Campañas de explotación, ver red teams


## Noticia mensajes falsos FEdEx

* Envían mensajes a partir de números comprometidos

* El command and control suele ser de un wordpress vulnerado
* El APK es un banker

* Si no tienes tarifa plana envia muchos mensajes, además te van a quitar mucho dinero y te roban las credenciales

* Empresa prodaft, han bautizado esto como [flubot](https://www.xataka.com/basics/flubot-que-sabemos-ahora-virus-sms-fedex-como-funciona).


## Persistencia y elevación de privilegios

* __Persistencia__: Cualquier ténica q nos

Consejos CC:
* Borrar pruebas de antes cuando llegas a controlar un cc
* Parchear donde has entrado para que nadie entre


* Tema Ryuk con Ransomware As A Service, explotan una vulnerabilidad (acceso nicial) se conectan al comand and control para tener persistencia
* Así no vuelves a usar el primer acceso inicial

### Credenciales

Una forma, manipular o crear cuentas de usuario para tener acceso al sistema, es ruidoso (aunqe no todas las compañías tienen un alto nivel de madurez)



### Noticia del Sepe 

* Ransomware __Ryuk__, este es el final de la intrusión.
* La gente ha tenido un proceso previo (se encontraban desde hace 1/2 semanas)

* ¿Cómo han consegudo acceso inicial
  * Enrique se juega un mano y parte de otro a que es mediante:
  * Campaña de malspam [UNC1878](https://malpedia.caad.fkie.fraunhofer.de/actor/unc1878)

La fase es la siguiente:

* Envío de correos con un enlace, este link es legítimo
* Nos permite tener una landing page (p.ej. getresponse.com) y este enlace no se puede bloquear porque es legítimo, aquí cascan un segundo enlace.

* El enlace lleva a un Google Drive y te descargas un fichero que es un ejecutable  (aaa.pdf.exe) con icono de pdf.

* __Exige__ que el usuario __ejecute__ el fichero.

* Esto es un __loader__, que a su vez lo que hace es cargar la siguiente fase que es con Cobalt Strike, que es con lo que ellos establecen la persistencia, se comunican con el C&C.

* Este loader está __firmado__, por una entidad de la república Checa denominada CERTUM (que por lo que parece ni miran lo que firman) para la conexión con el C&C.

* Después crear un administrador de dominios distinto al tuyo (suelen poner el mismo usuario), en el caso de ryuk martinstevens


* Otra forma de tener un canal encubierto (como HTTPS) es por DNS, como es más complicado utilizan como canal encubierto, se utiliza un ancho de banda más pequeño pero es más sigiloso.

## Boot or logon autostart execution

Scripts que se ejecutan al inicio


### Create or modify system process: Window Service
  