
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
**dig www.marca.com**
;; ANSWER SECTION:
www.marca.com.		135	IN	CNAME	unidadeditorial.map.fastly.net.
unidadeditorial.map.fastly.net.	38 IN	A	199.232.197.50
unidadeditorial.map.fastly.net.	38 IN	A	199.232.193.50
_El ttl neste caso e de 38s_

**dig www.amazon.com**
;; ANSWER SECTION:
www.amazon.com.		293	IN	CNAME	tp.47cf2c8c9-frontier.amazon.com.
tp.47cf2c8c9-frontier.amazon.com. 60 IN	CNAME	www.amazon.com.edgekey.net.
www.amazon.com.edgekey.net. 19163 IN	CNAME	e15316.dsca.akamaiedge.net.
e15316.dsca.akamaiedge.net. 20	IN	A	2.22.222.61

_www.amazon.com. (293 seconds)_: El registro CNAME para www.amazon.com tiene un TTL de 293 segundos (casi 5 minutos). Esto significa que tu servidor DNS local puede almacenar la información de que www.amazon.com apunta a tp.47cf2c8c9-frontier.amazon.com durante ese tiempo antes de volver a consultar con los servidores DNS autoritativos.


_tp.47cf2c8c9-frontier.amazon.com. (60 seconds)_: El registro CNAME para tp.47cf2c8c9-frontier.amazon.com tiene un TTL de 60 segundos (1 minuto).

_www.amazon.com.edgekey.net. (19163 seconds)_: El registro CNAME para www.amazon.com.edgekey.net tiene un TTL alto, 19163 segundos (poco más de 5 horas y media).

_e15316.dsca.akamaiedge.net. (20 seconds)_: El registro A final para e15316.dsca.akamaiedge.net tiene un TTL bajo, solo 20 segundos. Esto indica que la dirección IP asociada a este dominio puede cambiar con frecuencia, por lo que se actualiza con mayor frecuencia.

9. Determina o TTL máximo (original) dun nome de dominio.

10. Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?
Hice dos consultas con **dig www.google.es** e saironme duas maquinas distintas, unha coa IP 142.250.184.163 e a utra con 142.250.200.99

11. Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo
**dig @J.ROOT-SERVERS.NET www.google.es**

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> @J.ROOT-SERVERS.NET www.google.es
; (2 servers found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27841
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 9
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1472
;; QUESTION SECTION:
;www.google.es.			IN	A

;; AUTHORITY SECTION:
es.			172800	IN	NS	a.nic.es.
es.			172800	IN	NS	c.nic.es.
es.			172800	IN	NS	g.nic.es.
es.			172800	IN	NS	h.nic.es.

;; ADDITIONAL SECTION:
a.nic.es.		172800	IN	A	194.69.254.1
c.nic.es.		172800	IN	A	194.0.34.53
g.nic.es.		172800	IN	A	204.61.217.1
h.nic.es.		172800	IN	A	194.0.33.53
a.nic.es.		172800	IN	AAAA	2001:67c:21cc:2000::64:41
c.nic.es.		172800	IN	AAAA	2001:678:44::53
g.nic.es.		172800	IN	AAAA	2001:500:14:7001:ad::1
h.nic.es.		172800	IN	AAAA	2001:678:40::53

;; Query time: 48 msec
;; SERVER: 192.58.128.30#53(J.ROOT-SERVERS.NET) (UDP)
;; WHEN: Tue Oct 15 17:28:54 CEST 2024
;; MSG SIZE  rcvd: 286

La respuesta te brinda las direcciones IP de los servidores DNS autoritativos para el dominio ".es" (España).
No te da la IP final para www.google.es porque ese trabajo lo realizan los servidores DNS autoritativos de ".es".
_La respuesta confirma que el servidor raíz no acepta el modo recursivo (resolver la consulta por completo)._

12. Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados
**sudo tcpdump -i any port 53** con este comando capturra todo el tefico del DNS.
dig www.timesonline.co.uk
;; ANSWER SECTION:
www.timesonline.co.uk.	300	IN	CNAME	alsop-n.uk.
alsop-n.uk.		60	IN	A	34.240.28.43
alsop-n.uk.		60	IN	A	54.76.240.177
alsop-n.uk.		60	IN	A	52.208.17.106




13. Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org
 **dig danielcastelao.org MX**
;; ANSWER SECTION:
danielcastelao.org.	900	IN	MX	80 aspmx.l.google.com.
danielcastelao.org.	900	IN	MX	90 alt1.aspmx.l.google.com.
danielcastelao.org.	900	IN	MX	110 aspmx2.googlemail.com.
danielcastelao.org.	900	IN	MX	120 aspmx3.googlemail.com.
danielcastelao.org.	900	IN	MX	100 alt2.aspmx.l.google.com.
danielcastelao.org.	900	IN	MX	130 aspmx4.googlemail.com.
danielcastelao.org.	900	IN	MX	140 aspmx5.googlemail.com.


14. Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
**dig www.facebook.com AAAA**
;; communications error to 127.0.0.53#53: timed out

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.facebook.com AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47916
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.facebook.com.		IN	AAAA

;; ANSWER SECTION:
www.facebook.com.	19	IN	CNAME	star-mini.c10r.facebook.com.
star-mini.c10r.facebook.com. 50	IN	AAAA	2a03:2880:f104:83:face:b00c:0:25de

;; Query time: 22 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 15 20:54:46 CEST 2024
;; MSG SIZE  rcvd: 102

