# EN FASE CONSTRUCCIÓ


# Integracio-AOC-SOAPUI

Oferim un Projecte SOAPUI amb XMLs de peticions d'exemple per a que els integradors puguin fer les validacions oportunes a nivell de missatgeria PCI + Específica de cada servei.

---
<span style="color:red">Important, **has d'estar autoritzat per consumir el servei, modalitat i finalitat en la PCI.** </span>.
---

---

En cas contrari, heu de seguir les passes indicades en la [FAQ][URL1].

[URL1]: https://www.aoc.cat/knowledge-base/quines-dades-necessita-consorci-aoc-me-integrar-servei/

Per qualsevol dubte o aclariment, podeu obrir tiquet a través del [formulari][URLFORM].

[URLFORM]: https://www.aoc.cat/portal-suport/peticio-integradors/

Per altra banda, oferim el WSDL adaptat que s’haurà de descarregar perquè el projecte SOAP funcioni.

## Accions a realitzar

1. Descarregueu el Projecte.
2. Descarregueu el WSDL i el configureu.
3. Configuració del [certificat][link1]

[link1]: https://github.com/ConsorciAOC/Integracio-AOC-SOAPUI#configuraci%C3%B3-certificat-per-fer-els-consums



---

## Configuració certificat per fer els consums

---
***A nivell de PCI hi ha dues vies per autoritzar els consums***

- Presentant un certificat de client autoritzat pel canal [SSL][URL2].

[URL2]: https://www.soapui.org/docs/soap-mocking/securing-mockservices-with-ssl/

- Adjuntant les capçaleres [WSS][URL3] amb la signatura corresponent de la petició amb el certificat autoritzat.

[URL3]: https://www.soapui.org/docs/security-testing/ws-security-settings/

---

### Configuració per canal SSL

~~~~
La configuració per SSL es recomana per MTOM, no obstant, tambè es factible per serveis no MTOM
~~~~

En l'apartat de "Preferences anirem a "SSL Settings" i configurem el certificat. En aquest cas és el SEGELL_AOC.jks 

El certificat de proves (Serveis_Administracio_Electronica.cer) el podem trobar en la ruta de xarxa : ***\\\192.168.166.135\tecnologia\SUPORT_TECNIC\CERTIFICATS\SEGELL\Segell Administracio Electronica_Gener_2019***

![wsdl](capturas/SSL1.png)

### Configuració per WSS

En el projecte que hem generat, donem doble click en la carpeta i anem a "WS-Security Configurations"

AFegim el certificat, en l'apartat de "keystore"

![wsdl](capturas/wss0.png)

Afegimamb el "+" el certificat en "outgoing WS - Security Configurations

![wsdl](capturas/wss2.png)

Premem el "+" i afegim el "Timestamp" on el TTL ha de ser 300

![wsdl](capturas/wss4.png)

Premem el "+" i afegim el certificat de proves i en keysotre seleccionem el que hem configurat.

![wsdl](capturas/wss3.png)

---
***la clau és marcar "use single cert for signing" d'aquesta manera el valor ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3".***

---

### Afegim la capçelera de segurat per WSS

En la petició XML afegim capçelera de seguretat, abem a "Auth (Basic) i seleccionem el certificat que hem configurat per WSS.

![wsdl](capturas/wss5.png)

# Consums per MTOM

Per consumir per MTOM, no ha de tindre Capçalera de seguretat. Hem fet la configuració tal qual indica la web de [SOAP-Ui][URL4]

[URL4]: https://www.soapui.org/docs/soap-and-wsdl/attachments/

---
*   ***Enable MTOM***  → True
*   ***Disable multiparts*** → True
---

Els adjunts, els fiquem dintre del tag Ficheros i en "Contenido" (1) (tal com indica la imatge i en el "+" afegim el document a adjuntar (2).

![wsdl](capturas/MTOM1.png)






