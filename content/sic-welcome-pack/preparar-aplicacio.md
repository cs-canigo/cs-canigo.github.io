+++
date = "2020-06-25"
title = "Com preparar una aplicació per desplegar-la automàticament"
description = "Guia amb la informació més rellevant a tenir en compte per la integració al SIC del desplegament d'una aplicació"
sections = "SIC"
toc = true
taxonomies = []
weight = 2
+++

## Introducció

En el cas que l’aplicació utilitzi el servei de custòdia de codi i la seva tecnologia permeti la construcció i desplegament automatitzat d’artefactes,
s’hauran d’acomplir una sèrie de **requeriments per a que es pugui dur a terme la construcció de les corresponents pipelines de desplegament**.

Es tracta d’una guia ràpida per a informar dels aspectes més rellevants a tenir en compte quan una aplicació es vol integrar amb el SIC.

## Lliurament de codi font

Cal que es pugi el codi font de l’aplicació al sistema de gestió de codi font (SCM - Source Code Management) del SIC:

* Els projectes han de crear-se dins el **codi de diàleg** adient, de forma que tota la gestió posterior de jobs i creació de peticions Remedy s'associïn a l'aplicació corresponent.
* **No es poden incloure binaris** de llibreries ni d’altres mòduls ni executables (JAR, WAR, EAR, DLL, EXE...) i la mida màxima dels arxius serà de 25MB. A tal efecte,
s’ha habilitat un sistema de gestió de [Binaris](bin.sic.intranet.gencat.cat).
* No es permet l'ús de versions **snapshot**, per lo que s'impedirà la pujada del fitxer `pom.xml` si aquest les referencia.
* No es permet la pujada del fitxer `package-lock.json` en el cas dels frontals.
* Aquest repositori **no és un entorn de desenvolupament**, per lo que només les persones assignades com a Release Managers seran les encarregades de consolidar el codi i
lliurar-lo. Aquest codi font ja haurà d'estar validat en entorns de desenvolupament i es lliurarà quan es decideixi distribuir als entorns dels serveis TIC centrals.
* Els repositoris poden tenir tantes branques com siguin necessàries, però sempre s’haurà d’incloure la **branca MASTER** i el contingut d’aquesta branca serà amb el que
treballaran les pipelines de construcció i desplegament.
* Les pipelines seran les encarregades de generar els **TAGS** corresponents. Es generaran TAGs de build un cop s’aconsegueixi construir els artefactes i TAGS de versió
definitiva un cop finalitzada la verificació a l’entorn de PREPRODUCCIÓ.

## Estructura de projectes
L'estructura de projectes i el seu contingut ha de ser compatible amb el sistema establert d'Integració Contínua:

* Dins del grup del codi de diàleg, es tindran **tant projectes com a conjunts de codi font susceptibles de ser versionats** de forma independent a la resta de projectes.
Pot tractar-se d’una llibreria, un microservei, un mòdul, un conjunt d'scripts o un programa sense fragments independents.

* Cal proporcionar **procesos de construcció** d'artefactes independents de les màquines i plataformes on s'executen, de forma que siguin aplicables tant en els entorns de
desenvolupament com en els entorns del SIC.
<div class="message information">
El SIC actualment utilitza la <a href="https://www.docker.com/">tecnologia Docker</a> per a disposar d'un entorn aïllat i immutable de construcció que, a més pugui ser utilitzat i testejat pels propis proveïdors.
Addicionalment, es contempla l'ús d'entorns propis de construcció proporcionats pels proveïdors (DockerFile) que opcionalment podran estendre del catàleg d'imatges corporatiu.<br/>
<a href="https://canigo.ctti.gencat.cat/howtos/2020-06-26-SIC-Howto-utilitzar-imatges-docker-builder/">Howto utilitzar imatges Docker Builder</a>
</div>

* Els artefactes es construiran una sola vegada i seran els que es desplegaran als diferents entorns. No es contempla, per tant, condicionar la construcció d’artefactes a l’entorn
on es desplegaran (ús profiles maven o similar).

* Si el projecte és multimòdul maven, és necessari que el fitxer `pom.xml` pare i els submòduls estiguin correctament configurats per a poder fer la construcció a partir d'un goal en el fitxer `pom.xml` pare i no un goal per cada submòdul.

* Tots els projectes hauran de disposar de la carpeta /sic/ al primer nivell de la carpeta de codi de projecte i, dins d’aquesta carpeta, caldrà crear l’arxiu `sic.yml` que contindrà
la versió funcional del projecte. Per exemple: `version: 1.1.0`
<div class="message information">
Les aplicacions Canigò disposen d'un generador mitjançant un plugin de Maven que, a partir de la construcció de l'aplicació, generen automàticament el fitxer sic.yml amb la versió del POM.<br/>
<a href="https://canigo.ctti.gencat.cat/noticies/2018-03-23-Canigo-Configuracio-multientorn-SPA/">Canigo-Configuracio-multientorn-SPA</a>
</div>

* Per tal d’automatitzar la creació de pipelines, els projectes hauran de disposar de l’arxiu de configuració `aca.yml` que caldrà ubicar dins la mateixa carpeta /sic/.
Veure [Com construir el fitxer ACA](/sic-welcome-pack/fitxer-aca/).

* Si es contempla l'execució de scripts de desplegament/migració de  BBDD, cal preparar el fitxer de `plans` i scripts a una carpeta independent.


## Llibreries
Respecte a les llibreries requerides pels projectes, en funció del seu tipus, cal tenir en compte les següents premisses:

* **Llibreries de tercers que no siguin públiques**: caldrà publicar-les manualment al Nexus, per lo que haureu d'indicar al SIC d'on baixar-les per tal d'enregistrar les llibreries oficials.
* **Llibreries pròpies**: el seu codi font haurà d'estar en projectes diferenciats al grup corresponent al codi de diàleg. Aquestes es generaran i es publicaran al Nexus mitjançant pipelines dedicades.
* **Llibreries pròpies no associades a projecte**: hauria de tractar-se d'un cas residual i justificat. Haureu de fer-les arribar al SIC per tal de publicar-les manualment al Nexus.

Es pot validar la existència o no de la dependència accedint a la següent URL: [Nexus](https://hudson.intranet.gencat.cat/nexus).

### Aplicacions APEX i PL/SQL, i migracions de BBDD

El desplegament d'aplicacions de certes tecnologies es fonamenta en l'execució de scripts a base de dades, tot i que els criteris apliquen a qualsevol migració de base de dades.
En general s'aconsella disposar d'un projecte específic de desplegament/migració de BBDD, tot i que també es pot optar per integrar-lo al desplegament d'un altre artefacte, habitualment
el backend de l'aplicació.

<br/>
En qualsevol cas, caldrà preparar:

* **sql_scripts**: directori per a emmagatzemar tots els scripts SQL/PL-SQL, que podran estar organitzat en subcarpetes si es considera.
* **plans.xml**: fitxer on es defineix el pla d'execució dels scripts, on caldrà indicar:

|Paràmetre|Tipus|Descripció|
|-----------|----------|----------|
|entorn|Opcional|Entorn per al qual s'ha d'executar o empaquetar (segons la modalitat de desplegament) el fitxer. Per defecte, aplica a tots els entorns.|
|failure|Obligatori|Indica la forma en la que s'ha de comportar el sistema en cas d'error: parar o continuar.|
|idBBDD|Obligatori|Identificador únic de la connexió amb la bbdd. En cas de pipelines generades per l’autoservei i desplegament automàtic, s’haurà de correspondre amb l’identificador del fitxer d’infraestructures que determina la cadena de connexió podent referenciar-ne diferents.|
|file|Obligatori|Fitxer que cal executar o empaquetar (segons la modalitat de desplegament).|
|execute|Opcional|Indica, en cas de modalitat de desplegament automàtica, si a més d'empaquetar el fitxer aquest s'ha d'executar. Útil pel cas de scripts anidats. Per defecte, s'executarà.|

Exemple:
```
<llista-scripts>
<script entorn="INT" failure="stop"     idBBDD="BD_INT" file="script_INT.sql"/>
<script entorn="INT" failure="continue" idBBDD="BD_INT" file="script_INT1.sql" execute="false"/>
<script entorn="INT" failure="continue" idBBDD="BD_INT" file="script_INT2.sql" execute="false"/>

<script entorn="PRE" failure="continue" idBBDD="BD_PRE" file="script_PRE.sql"/>
<script entorn="PRE" failure="continue" idBBDD="BD_PRE" file="script_PRE1.sql" execute="false"/>
<script entorn="PRE" failure="continue" idBBDD="BD_PRE" file="script_PRE2.sql" execute="false"/>

<script entorn="PRO" failure="continue" idBBDD="BD_PRO" file="script_PRO.sql"/>
<script entorn="PRO" failure="continue" idBBDD="BD_PRO" file="script_PRO1.sql" execute="false"/>
<script entorn="PRO" failure="continue" idBBDD="BD_PRO" file="script_PRO2.sql" execute="false"/>
</llista-scripts>
```


El projecte ha de contenir tot el codi de l'aplicació i el sistema de custòdia de codi permetrà gestionar diferències, versions i altres. D'acord amb aquesta filosofia,
el criteri és que cada objecte de base de dades ha de tenir el seu propi fitxer associat, especialment si sempre s'executa la mateixa instrucció (create or replace, drop + create...).

## Funcionament de les pipelines de construcció i desplegament
En realitzar una pujada de codi sobre la branca MASTER, si el projecte té una pipeline associada, automàticament s'executarà:

* Els jobs pipeline realitzen multitud de tasques encadenades mitjançant **STAGES**. En cas de produir-se alguna incidència, l'execució es cancel·larà i notificarà del que ha passat.
* Caldrà limitar la quantitat d’usuaris que realitzen aquesta acció i tenir en compte que el sistema només permetrà fer una única pujada exitosa per versió del projecte ja que, un cop desplegat, es generarà el **TAG de versió definitiva**.
* Durant el desplegament es requeriran **accions d’usuari** destinades a autoritzar l’evolució de les etapes de desplegament.
* Els jobs **notificaran** dels resultats a les adreces de correu assignades.
* En els desplegaments en modalitat semiautomàtica, es generaran **tickets Remedy** en modo “Draft” a nom de l’usuari que ha iniciat l’execució, per lo que cal tenir pressent que aquest ha de disposar de permisos per a la creació de peticions de tipus CRQ.

Per a poder efectuar certes tasques caldrà accedir a la plataforma mitjançat el formulari d’autenticació de [Jenkins](https://hudson.intranet.gencat.cat/hudson).

Per a més informació: [Integració Continua](/sic-serveis/ci/).

<br/><br/><br/>
Si voleu més informació podeu consultar la secció de [**HOWTOs i manuals**](/sic/manuals/). <br/>
Si teniu qualsevol dubte o problema assegureu-vos de no trobar resposta a les [**FAQ**] (/sic/faq) i utilitzeu el canal de [**Suport**] (/sic/suport) o contacteu amb l'Oficina Tècnica Canigó CTTI a través del correu electrònic: **oficina-tecnica.canigo.ctti@gencat.cat**.