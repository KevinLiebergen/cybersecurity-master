# Sesion 3 - Acceso inicial

## Entrega martes 9 

1. Trabajo (4 personas)
   * Índice
   * Objetivos
2. Herramienta (2 personas)
   * Decir cuál
   * ¿Por qué?
3. Laboratorio (Individual)
   * Actividades
   * Cuaderno de bitácora


## Noticia de la semana

* https://www.microsoft.com/security/blog/2021/01/28/zinc-attacks-against-security-researchers/
  * Microsoft llama al grupo de vulnerabilidades por __minerales__
  * Cada empresa de seguridad lo llama de de una determinada manera


* __Segunda noticia__ 
  * https://thedfirreport.com/2021/01/31/bazar-no-ryuk/
  * Intrusiones reales, habitualmente están asociadas a ransom pero utilizan técnicas red team

## Reconocimiento UAH

* Mirar en Shodan:
  * `hostname:uah.es`
  * Mirar el rango que tiene
    * Con  `whois`
    * __Preguntar de donde salen las imágenes de diapo 5__
  * * Han pasado del rango 64.0 al 80.0
  * 256 ips * 15 = 14.098


* Rango 192.146.56.0 - 193.146.58.255 




* Teniendo el rango, buscar:
  * `net:212.128.64.0/20`
    * 3.712 dispositivos

  * `net:193.146.56.0/22`
    * 260 dispositivos


  * 212.128.77.0 - 212.128.79.255
  * Rango raro, no entra en ninguna mascara



* Shodan te permite ver components del json para ver qué tecnologías usan

# Táctica: Acceso inicial

Conjunto de __actividades__ desarrolladas por un adversario que tiene por conseguir __establecer__ un __punto de entrada__ en la organización.


## Técnicas

### Drive-by compromise


* Un ejemplo es por medio de inserción de publicidad

* __Interesante:__ La realidad que nadie sabe es que la publicidad se "subasta" en tiempo real, algunos se pelean por meter fraudes y exploits
  * En verano la publicidad es más barata



## Exploit public-facing application

* Explotar fallos de configuración
* No siempre es el camino más directo

## External remote services

* Servicio SMB, RDP
* La mayoría de incidenes ransomware van por External remote services, o por correo electrónico

## Hardware Additions

* Introducir algún elemento adicional de código

## Phishing

* Orientado al robo de credenciales

## Replication through removable media

* USBs
  * __Stuxnet__, entender como entraba la gente, a donde iba esa gente, introdujeron el USB con payload 
  * REconocida como la pimera víctima de guerra porque murió de una persona

## Supply chain compromise

* CCleaner, solarWinds, 

## Trusted relationship

## Valid Accounts

* Robo de credenciales



## Descubrimiento: nmap

* Ver un host expuesto
* Ver para un host en concreto cuáles son los servicios que se exponen


* nmap __no__ es solo un escaneador de puertos, __conjunto de funncionalidades añadidas__
  * Motor de scripting NSE que permite entender su funcionalidad básica
  * Programado en LUA

## Barridos de red

* __Escaneo__, cerciorarme de que tenemos autorización para ello
  * ¡rules of engagement!
  * Definido en el alcance: Decir que puedes hacer __sin autorizacion__ y el __qué con__, no porque sea ilegal sino porque te __bloquean__

* Para escanear, pillar maquina en ovh y escanear desde allí o algo del rollo

* ¿__Cómo funciona nmap__?
  * Nmap envía un paquete __ICMP Echo Request__ a un rango de direcciones IP
    * Si hay respuesta, la dirección está en uso y procede a escanear puertos
    * Si no hay respuestala dirección no está en uso
      * Es posible que el host bloquee los pings, para ello empleamos el flag __-Pn__ para que no haga ping y escanee puertos directamente

  * Cuando se ejecuta como usuario __privilegiado__ nmap envía los siguientes paquetes:
    * ICMP Echo Request
    * TCP SYN al puerto 443
    * TCP ACK al puerto 80
    * ICMP Timestamp Request
  * Si hay respuesta, está vivo

* A la hora de determinar que puertos existen, si no tengo una conexión establecida, me mandas un segmento TCP vacío con ACK, lo que establece el RFC si está cerrado responder con X y si no con Y, nmap interpreta esas respuesta para determinar o está abieto o la versión.


## Protocolos capa red

* SCTP (Stream Control Transmission Protocol)
* TCP
* UDP


- Para determinados servicios remotos  es habitual bloquear acceso desde fuera de españa

## Tipos escaneos en nmap

* `-sP` ping sweps
* `-sT` connect tcp scans
* `-sS` syn scans
* `-sA` ack scans
* `-sF` FIN scans
* `-sN` NULL scan
* `-sX` XMAS scan


* Escanear una lista
  * nmap -iL [objetivos.txt]

* Escaneo rápido
  * nmap -F objetivo 


La opción __-P__ nos permite que __tipo de descubrimiento__ de host queremos hacer:

* No realizar ping: -Pn
* TCP SYN: -PS
* TCP PING: -PT
* ICMP Ping: -PI

* Para ver más en detalle mirar en [nmap Cheatsheet](https://github.com/KevinLiebergen/ctf_walkthrough_compilations/blob/main/cheatsheets/nmap.md)


* ¡Herramienta [masscan](https://github.com/robertdavidgraham/masscan) en lugar de nmap
  *  __Mucho más rápido__!


Estados raros que devuelve nmap:

* __Filtered__: No sabemos si está abierto o no, hay un dispositivo intermedio bloqueando el puerto
* __Unfiltered__: Obtiene interacción con nmap, pero nmap no puede determinar si están abiertos o cerrados
* __Closed/filtered__: nmap no puede determinar en cuál de los dos estados se encuentra
* __Open/filtered__: nmap no puede determinar en cuál de los dos estados se encuentra


Las TTLs distintas en función de si es Linux (64) o Windows (128)


## Descubrimiento de vulnerabilidades con nmap

`$ nmap --script nmap-vulners,vulscan -sV objetivo`

Scripts de nmap útiles:

* http-enum.nse
  * Enumeración de recursos de interés en servicios web
* ssh-brute.nse
  * Verificación de credenciales predecibles en servicios SSH
* Smb-enumusers.ns3:
  * Enumeración de usuarios Windows
* Smb-check.vulns.nse:
  * Verificación de vulnerabilidad de SMB


## Escaneos a gran escala

* No utilizar nmap, no está pensado para eso
* Otras herramientas:
  * __MASScan__ (desacoplar peticiones de la respuesta, tiene varios hilos, carencia de ejecutar scripts)
  * Zmap

## Otras herramientas de escaneo de puertos
* Advanced Port Scanner
* NS2.exe
* Cuanto más raras sean nuestras tools más difícil que nos pillen!


Herramientas legítimas del sistemas para aprovecharse y orientarlo al red team
* powershell
  * LOLbins
  * net group


## Servicios de acceso remoto

* Servicios críticos de Windows (smb, rdp) lo más críticos.

* En todo los servicios con (fortinet, secur..., cisco asa) todos han tenido vulns de __crdenciales predecibles__, __importantísimo__

* Siempre q esten en el scope, ver en el alcance

* En __rdp__ podemos ver información del usuario, sistema

* Servicios SSH es un imán para ataques de fuerza bruta (posible TFM honeypot ssh con otro enfoque, preguntar)

* Citrix (serv. aceso remoto, acceso entorno virtualizado, entrar entorno virtualizado)
  * Producto de citrix: __netscaker__ con vulns criticas en los últimos años


* Restricciones geográficas: Tienen las patas muy cortas, orientados a ransomwares

# Táctica credenciales de acceso

## Fuerza bruta - Abuso de credenciales


* __Muy habitual__
* Relacionados con Valid Accounts y BruteForce
  * Reutilización de credenciales
  * F. bruta
  * Cuentas por deecto
  * Obtención de cedenciales tras expltar el Software
  * Phishing

Propuesta tfm ej. concienciación con phishing


### Descubrimiento de contraseñas - T1110.001

* F. bruta último recurso
* Hydra
* modulos auxiliares metasploit

Diccionarios:
* [SecLists](https://github.com/danielmiessler/SecLists/tree/master/Passwords)
* [apasscracker dictionares](https://apasscracker.com/dictionaries/)

Generadoras de diccionarios a partir de otros recursos:
* [princeprocessor](https://github.com/hashcat/princeprocessor)
* [crunch](https://github.com/crunchsec/crunch)
* [CeWL](https://github.com/digininja/CeWL)
* [RSMangler](https://github.com/digininja/RSMangler)


Si la contraseña te pide mínimo 8 caracteres y al menos un número, crear diccionaro con ese formato, piensa un poco.



### Password spraying - T1110.003

* En un ataque de f. bruta tienes un usuario y un montón contraseñas
* __Pasword spraying__: Un montón de uuarios y pocas contraseñs, probar un usuario con esas contraseñs, otro usuario con la misma lista de contraseñas, etc. Asi no te petan por limite de pruebas por usuario


### Credential Stuffing - T1110.004

Se aprochean de que por comodidad tendemos a reutilizar las mismas contraseñas para distintos servicios.

## Entrega por correo electrónico
  * Confiurar SMTP como legítimo, crear reputación con ese servidor
    * No hacer phishing un día después de crear el server, planificar con cierto tiempo la campaña, 30 días de antelación 
    * O subirte a un dominio que ya tiene una historia, estar atento a un dominio que haya caducado y renovarlo tu
    * Utilizacion de dominios comprometidos

* Phishing
  * [GoPhish](https://getgophish.com/)
  * Abusar de servicios de Microsoft o Google
    * Abuso de storage.googleapis.com
    * Abuso de core.windows.net

* Adjuntos ofimáticos maliciosos
  * Mejor excel, __menos cantoso__
  * Macros Office
  * MS Excel Macro 4.0
  * Inyección de plantillas remota
  * Vulnerabilidad RCE en editor de ecuaciones
  * VBA Stomping
  * Uso maldocs
  * [EvilClippy](https://outflank.nl/blog/2019/05/05/evil-clippy-ms-office-maldoc-assistanthttps://www.pentestpartners.com/security-blog/how-to-create-poisoned-office-documents-for-your-staff-awareness-training-part-1/)





* Llegan distintos tipos de ficheros, con un buen tema de conversación reutilizado, la gente lo termina abriendo y ejecutando
* Mitigación:
  * Desactivar macros
  * 2FA


* __Interesante__
  * Entorno virtualizado en word

## Entrega vía web

* magecart

## Entrega vía web: Exploit kits

paquetes de codigo se insertan en wbe, si entra un cliente con determinados privilegios, se ejecuta el exploit

navegadres se actualizan solo, menos en empresas, q controlan los ciclos de actualización

cada poco tiempo hay un 0-day de Firefox o de Chrome

imagen virtualizada de navegadr, para q no se actualizara

* [Exploit kit](https://www.enisa.europa.eu/topics/csirts-in-europe/glossary/vulnerabilities-and-exploits)

## Entrega vía web: Watering holes

* Ataques de cadena de suministro (SolarWinds)

## Entrega vía dispositivos extraíbles (USB)

* Rubber Ducky
* BadUSB
* Cables: [USBHarpoon](https://www.bleepingcomputer.com/news/security/usbharpoon-is-a-badusb-attack-with-a-twist/)

## Escáneres de vulnerabilidades

* [Nessus](https://es-la.tenable.com/products/nessus)
  * Comercial
* [Open VAS](https://www.openvas.org/)
  * Open Source
* [Acunetix](https://www.acunetix.com/vulnerability-scanner/)
  * Seguridad Web
  * [Nuclei](https://github.com/projectdiscovery/nuclei)

























