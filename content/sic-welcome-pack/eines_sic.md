+++
date = "2019-01-07"
title = "Quin són els serveis del SIC i com fer-ne ús"
description = "Guia amb la informació més rellevant per a l'ús dels serveis que proporciona el SIC"
sections = "SIC"
toc = true
taxonomies = []
weight = 1
+++

## Introducció

El SIC proporciona una sèrie de serveis: custòdia de codi font (GitLab), integració contínua (Jenkins i Nexus) i binaris. Aquests serveis resulten d'**obligat ús excepte si les aplicacions utilitzen altres sistemes homologats o n'estan exemptes**. Si no és el cas i la tecnologia de l'aplicació permet desplegar-la automàticament via SIC, esdevindrà requisit imprescindible per al pas a producció.

Tots els serveis del SIC basen la gestió d'usuaris en la identitat **GICAR** associada proporcionant un **autoservei d'usuaris** per a disposar d’autonomia a l'hora d'atorgar-hi accés a la resta de membres de l'equip de desenvolupament.

## Modalitats d'integració

Per tant, es contemplen tres tipus de modalitats d'ús dels serveis:

* **Automatitzada**: 
	- Es realitza custòdia de codi i les fonts s'actualitzen en cada lliurament.
	- S'utilitzen les eines de construcció i desplegament automatitzat d'artefactes, lliurant els artefactes per al desplegament de preproducció i producció mitjançant el servei de binaris (excepte Cloud que es desplega automàticament en aquests entorns).
* **Sense automatització**, per aplicacions que no es poden desplegar automàticament perquè la seva tecnologia o especificitats no ho permeten:
    - Es realitza custòdia de codi i les fonts s'actualitzen en cada lliurament.
	- Els arxius es lliuren a CPD/LdT mitjançant el servei de binaris.
* **Sense integrar**, per aplicacions exemptes de custòdia de codi:
    - Si no es fa ús d'un altre sistema homologat, els arxius es lliuren a CPD/LdT mitjançant el servei de binaris.

Les modalitats **Sense automatització** i **Sense integrar** són casos excepcionals que han de ser validats per l'Àrea d'Arquitectura del CTTI.
    
## Custòdia de codi (GitLab)

* **Com accedir**: https://git.intranet.gencat.cat mitjançant usuari GICAR.
* **Tipus de solució**: servei de control de versions.
* **Com crear un compte**: introduir credencials d'accés GICAR, essent imperatiu disposar d'adreça de correu associada, i realitzar el procés d'alta del perfil.
* **Qui pot accedir**: els Release Manager, responsables de lot, tècnics de CPD i els membres de l'equip de desenvolupament als que s'atorgui accés.
* **Com disposar d'accés**: sol·licitar al seu responsable que l'incorpori com a membre del/s projecte/s, ja sigui com a desenvolupador (Developer) o com a nou integrant del grup de Release Manager (Mantainer).
* **Com organitzar els projectes**: els projectes s'ubiquen dins el grup del codi d'aplicació, creant tants projectes com conjunts de codi susceptibles de ser versionats de forma independent.
* **Quan i com fer el lliurament d'una nova versió**: un cop validat als entorns de desenvolupament, es consolidarà, es realitzarà l'increment de versió i es pujarà al repositori. Si el projecte disposa d'una tasca de construcció i desplegament automàtic i l'actualització s'ha fet sobre la branca MASTER, es dispararà la tasca corresponent al Jenkins.

Per a més informació: [Custòdia de codi font] (/sic-serveis/scm/)

## Integració contínua

### Jenkins

* **Com accedir**: https://hudson.intranet.gencat.cat/hudson/ mitjançant usuari GICAR.
* **Tipus de solució**: servei per a la integració contínua (construcció, anàlisi, desplegament, proves... etcètera).
* **Qui pot accedir**: els Release Manager, responsables de lot i tècnics de CPD.
* **Com disposar d'accés**: sol·licitar al seu responsable que l'incorpori com a membre del/s projecte/s al servei de control de versions (Gitlab) com a nou integrant del grup de Release Manager (Mantainer). A l'endemà, l'usuari haurà passat a ser Release Manager disposant del corresponent accés al servei.
* **Com fer el lliurament d'una nova versió**: l'actualització del codi de la branca MASTER dispararà la tasca de construcció i desplegament (job de tipus "pipeline").
* **Quines passes componen el desplegament automàtic**: construcció, generació de tags i desplegament als diferents entorns. Es contempla l'execució de tests unitaris, tests d'integració i anàlisi de codi font que s'aniran afegint progressivament que no es podran desactivar pel desenvolupador a no ser que hi hagi una causa que ho justifiqui.
* **Quines passes de desplegament requereixen conformitat**: el pas a preproducció i producció requeriran de conformitat prèvia (etapes anteriors verificades). En funció de si el desplegament és semiautomàtic o automàtic per CPD, aquesta conformitat serà responsabilitat del grup de Release Managers o dels tècnics de CPD (respectivament).

### Nexus

* **Com accedir**: https://hudson.intranet.gencat.cat/nexus/.
* **Tipus de solució**: servei per a l'administració central de biblioteques.
* **Qui pot accedir**: no requereix autenticació, tothom pot accedir en mode lectura.
* **Com publicar noves llibreries**: per a la publicació de noves llibreries no públiques (pròpies o de tercers) caldrà sol·licitar-ho a l'equip de SIC.

<br/>
Per a més informació: [Integració contínua] (/sic-serveis/ci/)

## Servei de binaris

* **Com accedir**: https://bin.sic.intranet.gencat.cat/ mitjançant usuari GICAR.
* **Tipus de solució**: servei de lliurament i recuperació d'artefactes.
* **Qui pot accedir**: els Release Manager, responsables de lot i tècnics de CPD.
* **Com disposar d'accés**: sol·licitar al seu responsable que l'incorpori com a membre del/s projecte/s al servei de control de versions (Gitlab) com a nou integrant del grup de Release Manager (Mantainer). A l'endemà, l'usuari haurà passat a ser Release Manager disposant del corresponent accés al servei.
* **Com dipositar nous artefactes**: executar la tasca de pujada d'artefactes indicant, com a mínim: codi d'aplicació, projecte, versió i l'arxiu a dipositar. Pot incloure documentació associada. Si l'aplicació no està exempta de repositar codi al Git, abans de cada pujada haurà d'assegurar-se d'haver **actualitzat el codi font** o el sistema no li permetrà realitzar la operació.
* **Com recuperar artefactes**: localitzar el codi d'aplicació, projecte i versió i podrà descarregar el contingut necessari.

Per a més informació: [Servei de binaris] (/sic-serveis/binaris/)

<br/><br/><br/>
Es tracta d’una guia ràpida per a informar dels aspectes més rellevants a tenir en compte per a l'ús de les eines del SIC.
<br/>
Si voleu més informació podeu consultar la secció de [**HOWTOs i manuals**](/sic/manuals/). <br/>
Si teniu qualsevol dubte o problema assegureu-vos de no trobar resposta a les [**FAQ**] (/sic/faq) i utilitzeu el canal de [**Suport**] (/sic/suport) o contacteu amb l'Oficina Tècnica Canigó CTTI a través del correu electrònic: **oficina-tecnica.canigo.ctti@gencat.cat**.