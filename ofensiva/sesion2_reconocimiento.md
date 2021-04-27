# Sesión 2 - Reconocimiento

* Lectura recomendada acerca de [SolarWinds](https://www.microsoft.com/security/blog/2021/01/20/deep-dive-into-the-solorigate-second-stage-activation-from-sunburst-to-teardrop-and-raindrop/).

* Explicación de como empezó a finales del 2019 el proyecto, como pasaron de tener una backdoor a ejecutar códio en la víctima.

* Lo más flipante es cómo el malware __no es relacional__, la preocupación del comportamiento del malware es que es super  __difícil__ de __relacionar__ entre otras empresas, es decir, no puedes saber si una empresa está infectada o no.

* Han conseguido realizar varias instrucciones en paralelo y que no parezca que tengan que ver entre las empresas afectadas.

## Entramos en materia..

* __Reconocimiento__: Conjunto de actividades desarrolladas por un adversario que tiene por objetivo la __recolección de información__ de todo tipo acerca de una __organización__.

* Relacionado con técnias de OSINT


* El modelo de trabajo que vamos a utilizar es mediante el framework MITRE ATT&CK para realizar una taxonomía estructurada. Se organizan en tácticas, técnicas y procedimientos (Ver [TFG](https://github.com/KevinLiebergen/priv-escalation) acerca de escalada de privilegios)
* Se van a analizar las tácticas que aparecen en la matriz MITRE, esta sesión se dedicará a la táctica de reconocimiento:

## 1. Gather Victim Host Information

Recolección de información del host víctima

Existen diversos ataques, por ejemplo ataques phishing, buscar presencia de información en Internet.

### Hardware

* Existen diversos puntos de entrada (firewall)
* Dispositivos de control de acceso
* Ver documentos de __portal de contratación__, al ser servicios públicos aparece información importante. 
  * Puedes conocer la tecnología en algún sector público
  * http://www.madrid.org/cs/Satellite?pagename=PortalContratacion/Page/PCON_home
* Los TFGs/TFMs tambien incluyen configuración de sistemas en producción en empresas

### Software

* Cadenas de suministro
* Ejemplo SolarWinds

## 2. Gather victim identity information

* Recolección de información sobre la identidad de la víctima

* [emails] -> Bruteforce, diccionario, passwrd spraying, secuenciación de contraseñas (`felipe1` por `felipe2`)

* Con los emails sacas el username, ids, nombres de gente que trabaja en la empresa

* Varias maneras de conseguir correos e información:
  * Phishing for information
  * Phishing

* Cosas que hacer ante el __phishing__
  * Buscar para saber de donde han sacado el correo electrónico
  * Ver fugas de información de datos de la empresa
  * Ver cuentas válidas
  
* Ver correos en Leaks  y DB como Collection #1

* En https://virustotal.com/ es posible buscar IOCs, correos electrónicos, etc
  * Filtrar por expresiones regulares.
  * Sección search, `content: "@uah.es"` Necesario tener cuenta premium
* https://pwndb2am4tzkvold.onion.ws/
  * Bases de datos con leaks 
* https://intelx.io/ 
  * Motor de búsqueda orientado a correos electrónicos, dominios, URLS, IPs, CIDRs, carteras bicoind, hashes, etc
* Buscar por nombres de empleados


## 3. Gather victim network information

* Recolección de información de red de la víctima
* Rangos de dirección de red, nombres de dominio

1. Dominios
   1. Subdominios
   2. RIR = Registros Regionales de Internet
     * Se consultan mediante `whois`
2. IPs públicas
   1. Rango?
   2. DNS?
3. Servicio nube (Blackboard, dropbox / Google)


* __Passive DNS__: Registra peticiones DNS que realizan las muestras, guarda indormación DNS, IPs, etcs para posteriormente analizarlos.

* Búsqueda de dominios por el término:
  * Es necesario buscar los dominios que existen, con ello buscar DNS y listar las IPs (mediante herramientas que ofrezcan información de DNS pasivos)
  * Después es necesario enumerar los subdominios mediante herramienta de reconocimiento y recolección de información.
  * [AMASS](https://github.com/OWASP/Amass)
    * BuiltWith: Servicio de scrapping, similar a Whatweb
    * ComonCrawl
    * Circl
    * DNSDB (DNS pasivo)
    * ¡__PassiveTotal__!
    * Robtex (búsquedas inversas)
    * URLscan: Como virus total pero con URLs


* __Shadow IT__ = Todos sistema de información fuera del control centralizado
  * Cualquier tipo de etructura utilizada sin la aprobación del área TI, por ejemplo macros de excel, software, nube, etc.


* https://domainbigdata.com/ __Muy importante__
  * Por ejmplo buscar con `policia.es` en el buscador
  * Por temas de RGPD puedes hacer que no aparezca nada si quieres

* https://www.virustotal.com/gui/ __Muy importante__
  * Sección `search`, buscar por ejemplo `www.policia.es/`
  * Sección `relations` y después `siblings` permite ver direcciones y sacar rangos de red
  * Podemos ver que la empresa ha montado la enfraestructura de un tercero, por ejemplo

* https://securitytrails.com/
  * Búsqueda: `politecnica.es` (por ejemplo)
  * Si observamos en `MX records` (Mail Exchanger) vemos que algunos dominios pueden utilizar Office 365 (outlook).
    * Por ejemplo, a lo mejor es más fácil colarse por el servidor de correo del departamento de automáica de una facultad que por el servidor de correo de Office
  * En la sección `TXT` podemos sacar que utiliza un mailjet en algunos casos.


  * Podemos ver todos los subdominios, ¿Cómo?
    * Mediante DNS caché, crawling, consultas, __certificados__, fuerza bruta

### Propiedades de dominio

* https://www.domaintools.com/


### DNS

* Como se ha comentado, hay que ver las entradas DNS, es posible colarse por el servidor de correo del departamento de automática de alguna universidad que por el de Office, por ejemplo.

### Dependencias de confianza de la red

* Si se que la empresa tiene un proveedor X, petar a ese proveedor (por ejemplo APT10)
* Explotar relaciones de confianza

### Direcciones IPs

* RIR = Regional Internet Registries
* APNIC, AFRINIC, RIPE NCC, ARIN, LACNIC

### Dispositivos de seguridad en la red

* Fortinet es un appliance
* Antiguamente se compraban credenciales válidas VPN para entrar en el sistema

## 4. Recolección de informatión de la organización

* Dejar "USBs perdidos"

## 5. Búsqueda en bases de datos abiertas

### DNS / DNS pasivos

* Forward DNS
* https://www.sonar.io/

### Certificados digitales

* ¡https://crt.sh/!  
  * Super chulo, información de cerificado, dominios, autoridad certificadora, fecha, etc.

### Escaneo de bases de datos
* https://www.onyphe.io/
* https://www.shodan.io/
* https://www.zoomeye.org/

## 6. Búsqueda de sitios webs / dominios

### Social media

* Exploit kit

### Motores de búsqueda

* Google Hacking Database (GHDB)

## 7. Buscar sitios web propiedad de las víctimas

* https://commoncrawl.org/