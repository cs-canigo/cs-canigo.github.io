+++
date = "2020-06-17"
title = "Autoservei d'usuaris"
description = "Autoservei d'usuaris SIC 2.0 mitjançant GitLab"
aliases = [
    "/sic/autoservei-usuaris/",
    "/noticies/2017-07-18-SIC-Autoservei-usuaris-SIC2.0/"
]
sections = "SIC"
taxonomies = []
toc = true
weight = 4
+++

## Introducció

El SIC 2.0 proporciona un servei de gestió d'usuaris per a que els lots d'aplicacions disposin d'autonomia a l'hora d'assignar permisos d'accés sobre els diferents serveis. <br/>
Abans d'entrar en el funcionament de l'autoservei d'usuaris, explicarem breument l'estructura actual de permisos del SIC.

## Estructura de permisos

El SIC té estructurada la seva seguretat en diferents tipus de grups:

* Grups per a lots i proveïdors d'aplicacions
* Grups per a CPDs i LdTs
* Altres grups

### Grups per a lots i proveïdors d'aplicacions

Aquests tipus de grups contenen a desenvolupadors i altres perfils que componen l'amalgama de perfils requerits per desenvolupar una aplicació. Dins d'aquests tipus de grups, distingim dos subtipus:

* Release Managers
* Responsables de lot

A continuació, descriurem cadascun d'aquests subtipus.
<br/><br/>

#### Release Managers

Aquest tipus de grup recull als Release Managers, és a dir, a tots els usuaris amb perfil Release Manager que pertanyen a un codi d'aplicació concret. Els membres d'un grup Release Managers són perfils que poden:

* Operar amb servei de **custòdia de codi**.
* **Concedir permisos** a altres companys per accedir com a Developers o Mantainers al codi d'aplicació corresponent, passant aquests últims a ser Release Managers a tots els efectes.
* **Crear nous projectes** dins del grup de l'aplicació.
* Accedir als serveis d'**integració contínua**.
* Accedir al servei de gestió de **binaris** per dipositar i recollir arxius.

#### Responsables de lot

Aquest tipus de grup recull als responsables de lot. <br/>
Al SIC 1.0, els membres d'aquest tipus de grup eren els encarregats de sol·licitar accés per a un Release Manager. Actualment, al SIC 2.0, aquesta funcionalitat perd valor gràcies a l'autoservei d'usuaris, mitjançant el qual els propis Release Managers poden concedir accés a la resta de companys. <br/>
Aquest grup, per tant, ha passat a ser un agregador de totes les aplicacions del lot disposant d'una **participació transversal a tots els codis de les aplicacions** i podent realitzar les mateixes accions que un Release Manager. <br/>
Aquests grups estaran gestionats per l’aplicació de [Control d’Accés de Recursos de GICAR](https://gicar.intranet.gencat.cat/gdi/controlaccesrecursos/) en mode autoservei per l’aplicació “SIC”.

### Grups de CPDs i LdTs

Aquests tipus de grups recullen als responsables dels diferents centres de processament de dades (CPD) i a llocs de treball (LdT). Els membres d'aquest tipus de grups tenen **accés en mode lectura als repositoris i al servei de gestió de binaris**, a més poden executar a Jenkins jobs de desplegament automàtic per CPD per als codis d'aplicació corresponents. <br/>
Aquests grups estaran gestionats per l’aplicació de [Control d’Accés de Recursos de GICAR](https://gicar.intranet.gencat.cat/gdi/controlaccesrecursos/) en mode autoservei per l’aplicació “SIC”.

### Altres grups

Es tracta de grups especials per a la gestió del servei i altres funcionalitats: **Administració, Responsables d'àmbit, Oficina de Qualitat, Oficina de Seguretat**,... etcètera. És a dir, són grups necessaris per al correcte funcionament dels serveis i per a la integració amb la resta d'agents del CTTI. <br/>
Aquests grups estaran gestionats per l’aplicació de [Control d’Accés de Recursos de GICAR](https://gicar.intranet.gencat.cat/gdi/controlaccesrecursos/) en mode autoservei per l’aplicació “SIC”.

## Funcionament

A continuació, ens centrarem en la gestió de membres del grup de **Release Managers mitjançant l'autoservei d'usuaris**.
Aquest servei es realitza mitjançant l'eina de custòdia de codi font implantada: [GitLab](https://git.intranet.gencat.cat/).

### Accés al servei

Podrà accedir mitjançant el següent enllaç: https://git.intranet.gencat.cat <br/>
Haurà d'autenticar-se amb de les seves credencials d'accés **GICAR**. Els Release Manager, responsables de lot i tècnics de CPD disposaran d'accés al servei. Si no disposa d'accés, haurà de sol·licitar-ho al seu responsable.

### Creació de comptes d'usuari

Per a poder accedir al servei caldrà disposar d'un usuari GICAR operatiu i crear el compte corresponent. Per a fer-ho, haurà d'introduir l'identificador d'usuari i contrasenya i, en cas de tractar-se d'un nou compte, el sistema el redirigirà a la plana de perfil per a que pugui dur a terme el procés d'alta. <br/>

**IMPORTANT**: És imprescindible que la identitat GICAR de l'usuari tingui informada l'**adreça de correu** i que l'usuari es trobi bolcat a l'**LDAP del SIC** (adreça de correu inclosa). Per tant, tant si el sistema el redirigeix contínuament a la pàgina de perfil per informar l'adreça de correu, com si no pot accedir al servei perquè es produeix un error d'autenticació amb unes credencials vàlides, caldrà fer una petició de suport al servei GICAR a través de SAU-Remedy.

### Estructura de grups i projectes

Els **Grups** tindran com a identificador el codi de diàleg de les aplicacions. Els usuaris Release Manager hauran de crear **Projectes** dins aquests grups per tal de disposar dels repositoris Git on fer la pujada de codi font de les aplicacions.

Per a més informació: [Custòdia de codi font] (/sic-serveis/scm/)

### Comptabilitat amb SIC 1.0

Els usuaris que ja eren **"Release Manager Lot x Àmbit"** al sistema SIC 1.0, mantindran el mateix rol al sistema SIC 2.0. Per tant, en accedir al portal del GitLab (mitjançant les credencials GICAR corresponents) disposaran d'accés als grups per codi de diàleg de les seves aplicacions.

**AVÍS**: durant el primer accés al GitLab no es comptarà amb visibilitat sobre els grups d'aplicacions. Caldrà esperar a l'endemà del primer login per tal de disposar d'accés als grups i projectes corresponents.

<center>![RML a SIC 1.0 VS SIC 2.0](/images/news/autoserveiUsuaris_1.PNG)</center>
<br/>

### Permisos d'accés

En crear projectes dins els grups d'aplicació, la resta d'usuaris del lot que no siguin Release Manager no disposaran de visibilitat.

<CENTER>![Visibilitat resta usuaris Lot](/images/news/autoserveiUsuaris_2.PNG)</center>
<br/>
Els mateixos usuaris Release Manager podran consultar, editar, afegir i eliminar membres del projecte, però ho hauran de fer **a nivell de projecte**, no de grup de projectes.

<CENTER>![Proporcionar accés a Projecte](/images/news/autoserveiUsuaris_3.PNG)</center>
<br/>
Per a concedir accés sobre un projecte caldrà:

* Accedir al **projecte**.
* Mitjançant el menú superior cal seleccionar "**Settings**" i, dins aquest ,"**Members**".
* Al formulari que apareix, cercar l'usuari al qual es vol donar accés. La cerca es pot realitzar per nom o NIF. S'aconsella **cercar per NIF**.
* Escollir el **rol** que ha de tenir l'usuari dins el projecte:
	* Rol Mantainer: permetrà treballar amb el projecte en qüestió, crear nous projectes dins el grup de l'aplicació i proporcionar accés a altres usuaris als projectes dins el grup.
	* Rol Developer: únicament permetrà treballar amb el projecte en qüestió (descàrrega i pujades).
* Prémer el botó de "**Add to Project**"

<CENTER>![Proporcionar accés a Projecte](/images/news/autoserveiUsuaris_4.PNG)</center>
<br/>

En el cas que el rol escollit per a l'usuari hagués estat de **Mantainer**, l'endemà de l'assignació, l'usuari haurà adquirit accés a la resta de projectes del grup de l'aplicació, convertint-se a efectes pràctics en un nou Release Manager del codi d'aplicació. Aquesta **promoció a Release Manager** permetrà l'accés a la resta de serveis del SIC: custòdia de codi, gestió de binaris i integració contínua.
<CENTER>![Visibilitat adquirida segons Rol](/images/news/autoserveiUsuaris_5.PNG)</center>
<br/>

**AVÍS**: Si desitja concedir permisos a un usuari per a un grup que no disposa de cap projecte, caldrà prèviament crear el projecte per a poder dur a terme l'assignació desitjada.

<br/><br/><br/>
Si voleu més informació podeu consultar la secció de [**HOWTOs i manuals**](/sic/manuals/). <br/>
Si teniu qualsevol dubte o problema assegureu-vos de no trobar resposta a les [**FAQ**] (/sic/faq) i utilitzeu el canal de [**Suport**] (/sic/suport) o contacteu amb l'Oficina Tècnica Canigó CTTI a través del correu electrònic: **oficina-tecnica.canigo.ctti@gencat.cat**.