
1. Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)
ig danielcastelao.org
 
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36680
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;danielcastelao.org.		IN	A

;; ANSWER SECTION:
danielcastelao.org.	900	IN	A	178.211.133.37

;; Query time: 155 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:18:18 CEST 2024
;; MSG SIZE  rcvd: 63

2. Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org  

		dig moodle.danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> moodle.danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 63687
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;moodle.danielcastelao.org.	IN	A

;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300

;; Query time: 301 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:30:40 CEST 2024
;; MSG SIZE  rcvd: 113

 		
 		dig www.danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39495
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.danielcastelao.org.		IN	A

;; ANSWER SECTION:
www.danielcastelao.org.	900	IN	A	178.211.133.37

;; Query time: 124 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:31:03 CEST 2024
;; MSG SIZE  rcvd: 67

As diferenzas son:

-Status-> no caso de moodle.danielcastelao.org aparece NXDOMAN, que significa que o dominio non existe. No caso de www.danielcastelao.org pon NOERROR por que o DNS pudo resolver correctamente a consulta.

-ANSWER-> ANSWER 0 por que non ten resposta.ANSWER 1 hai unha resposta valida que e a IP 178.211.133.37, que pertenece a www.danielcastelao.org 

-AUTHORITY-> AUTHORITY 0 e por que a resposta conten o registro solicitado e non e necesario facer referencia a autoridad 

-Query time-> no caso de www.danielcastelao.org tarda menos por que si existe o dominio mentres que con moodle.danielcastelao.org tuvo que comprobar a inexistencia.

-MSG SIZE rcvd-> o mensaje de moodle.danielcastelao.org e mais longo xa que tuvo que añadir o registro SOA 



3.  Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?

**dig NS danielcastelao.org**
ns1.hover.com.	216.40.47.26
ns2.hover.com.	64.98.148.13

Utilizase dous servidores para proporcionar unha mayor fiabilidad, rendimiento e flexibilidad. Distribulle la carga de taballo e garantiza a continuacion do servicio. 

4. Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.

**dig -x 130.206.164.68**

;; ANSWER SECTION:
68.164.206.130.in-addr.arpa. 4795 IN	PTR	pluto.tlm.unavarra.es.
68.164.206.130.in-addr.arpa. 4795 IN	PTR	s164m68.unavarra.es.

**dig -x 8.8.8.8**
;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.	4700	IN	PTR	dns.google.

**dig -x 52.206.14.32**
;; ANSWER SECTION:
32.14.206.52.in-addr.arpa. 300	IN	PTR	ec2-52-206-14-32.compute-1.amazonaws.com.

5. A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?

nslookup podemos ver que a ip que do DNS que utiliza e 127.0.0.53

Con **nslookup** server 127.0.0.55 cambiamos a configuracion do sistema

6. Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org. 
Le preguntamos al DNS de google con **dig @8.8.8.8 moodle.danielcastelao.org SOA** que nos muestra que ns1.hov.com es el servidor primario.
;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300

Preguntamoslle o servidor primario directamente con **dig @ns1.hover.com moodle.danielcastelao.org SOA**

7. Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?

 8. Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?

 9. Determina o TTL máximo (original) dun nome de dominio.

10. Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

13. Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo

14. Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados

13. Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org

14. Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
