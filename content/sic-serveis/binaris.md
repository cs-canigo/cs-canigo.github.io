+++
date = "2020-05-25"
title = "Servei de Binaris"
description = "Eina SIC per al lliurament d'artefactes a CPD/LldT"
sections = "SIC"
aliases = [
  "/noticies/2017-07-05-SIC-Gestio-binaris/"
]
toc = true
taxonomies = []
weight = 3
+++

## Introducció

El **Servei de Binaris del SIC** és un servei a disposició dels proveïdors de lots d’aplicacions i CPD per al lliurament i descarrega d’artefactes de cara al desplegament d’aplicacions.

<br/>
Cobreix les següents funcions i requeriments del servei SIC:

* **Unificar** el sistema d'intercanvi d’artefactes entre lots d'aplicacions i CPD/LldT
* **Potenciar la custòdia de codi font** al SIC de les aplicacions
* Fer ús d'un **únic repositori d’artefactes**, tant per llibreries com per artefactes desplegables
* Reforçar el **compliment normatiu** en el versionat de les aplicacions
* Possibilitat de tenir un servei a usar com a **procediment de contingència** en el desplegament d’aplicacions

## Accés al servei

Podrà accedir mitjançant el següent enllaç: https://bin.sic.intranet.gencat.cat <br/>

<CENTER>![Binaris](/images/news/SIC-GestioBinarisPortal_20.png)</center>
<br/>

Haurà d'autenticar-se amb de les seves credencials d'accés GICAR, de forma que:

* Els **Release Manager i responsables de lot** disposaran d'accés al servei de pujada de binaris i també a la descàrrega dels mateixos.
* Els **tècnics de CPD i llocs de treball** només disposaran d’accés a la descàrrega de binaris.

En cas de no disposar d’accés haureu de fer ús de l'[Autoservei d'usuaris] (/sic-serveis/autoservei-usuaris/) i/o sol·licitar-ho al seu responsable.

## Dipositar artefactes al SIC

Permet fer el **lliurament d'artefactes** mitjançant l'aplicació web. En la següent imatge s'explica el seu funcionament:

<CENTER>![Binaris](/images/news/SIC-GestioBinarisPortal_20_2.png)</center>

<br/>
Aquest servei està destinat a aplicacions que, ja sigui per estar desenvolupades amb una tecnologia no suportada o per particularitats del
procés de construcció, no es poden construir i desplegar mitjançant [Integració Contínua] (/sic-serveis/ci/). No obstant, també està pensat
per a fer-ne ús com a **procediment de contingència** en el desplegament d’aplicacions.

<br/>
Es realitzen les següents comprovacions:

* Dades obligatòries informades: **codi de diàleg, projecte, versió i binari a pujar**
* El codi de **versió** acompleix l’estàndard de versions: https://qualitat.solucions.gencat.cat/estandards/estandard-versions-programari/
* El codi de **projecte** està composat de lletres i números permetent addicionalment els caràcters: ‘-’, ‘_’ i ‘.’
* Si l’aplicació no està exempta de la custòdia de codi, es verificarà que s’hagi **actualitzat el codi font en els últims 20 dies**
* El fitxer té una **mida màxima de 500MB**. No es tracta d'un servei pensat per a la pujada de binaris i arxius pesats que no siguin permesos al GIT
doncs, amb aquest finalitat, s'ha habilitat el servei [GIT-LFS (Large File Storage)](/howtos/2019-10-09-sic-Howto-Git-lfs/).

<br/>
En finalitzar la pujada es mostrarà per pantalla la llista de binaris lliurats i la URL de descàrrega associada. Aquesta llista mostrada es podrà utilitzar
per tal d’emplenar la petició de desplegament.

<CENTER>![Binaris](/images/news/SIC-GestioBinarisPortal_20_3.png)</center>

<br/>

<div class="message information">
Els artefactes pujats al repositori de binaris <b>podran ser sobreescrits</b> sempre i quan es proporcioni la mateixa
informació al formulari de pujada (codi de diàleg, projecte, versió, nom fitxer). Per tant, en cas d'haver sol·licitat ja el desplegament del binari i haver
emplenat la petició de desplegament, no serà necessari fer cap canvi doncs les URL's es mantenen operatives.
</div>

## Recuperar artefactes del SIC

Permet la **descàrrega d'artefactes lliurats** pels responsables de l'aplicació per a procedir a fer el desplegament.
Aquesta opció el dirigirà cap al repositori de binaris (al que també pot accedir mitjançant l'enllaç https://hudson.intranet.gencat.cat/nexus/#browse/browse:binaris) on
podrà cercar l'entrada i l'artefacte que vol descarregar.
O simplement pot fer ús de la **URL que el proveïdor d'aplicacions ha indicat a la petició** de desplegament per accedir a la descàrrega directa.

<CENTER>![Binaris](/images/news/SIC-GestioBinarisPortal_20_4.png)</center>

Aquest servei és accessible per **Release Managers, responsables de lot i tècnics de CPD/LldT** en mode lectura, **no permetent pujar noves entrades, editar o eliminar**
informació. S'ofereixen diverses opcions de cerca i visualització.

<CENTER>![Binaris](/images/news/SIC-GestioBinarisPortal_20_5.png)</center>


La **URL de descàrrega** seguirà el següent patró:
```
https://hudson.intranet.gencat.cat/nexus/repository/binaris/_codi_diàleg_/_projecte_/_versió_/_artefacte_
```


El sistema permet la consulta i descàrrega remota d’artefactes:

```
curl -X GET [ u user:pwd ]
"https://hudson.intranet.gencat.cat/nexus/binaris/projecte/1.0.0/bin/DesktopOK.zip" -O
curl -X GET [ u user:pwd ]
"https://hudson.intranet.gencat.cat/nexus/service/rest/v1/assets?q=projecte/1.0.0/*& binaris
```

<br/><br/>
<div class="message information">
<b>L'anterior sistema de descàrrega d'artefactes romandrà actiu fins el 30/09/2020</b>. Durant aquest període, es podrà seguir accedint mitjançant
el següent enllaç: https://bin.sic.intranet.gencat.cat/binaris/
</div>

<!---
## Eliminació de binaris
S'executa un procés diari nocturn d'esborrat de binaris de forma que **únicament es respectaran les últimes 5 versions** repositades per codi
d'aplicació i projecte; i, pel que fa a versions anteriors, es respectaran si aquestes han estat pujades durant l'últim mes (30 dies). No està concebut, per tant, com un servei de custòdia permanent de binaris si no com un sistema d'intercanvi de binaris per al desplegament d'aplicacions.
--->

<br/><br/><br/>
Podeu accedir al [**Material formatiu**](/related/sic/2.0/formacio-binaris-20.pdf). <br/>
Si voleu més informació podeu consultar la secció de [**HOWTOs i manuals**](/sic/manuals/). <br/>
Si teniu qualsevol dubte o problema assegureu-vos de no trobar resposta a les [**FAQ**] (/sic/faq) i utilitzeu el canal de [**Suport**] (/sic/suport) o
contacteu amb l'Oficina Tècnica Canigó CTTI a través del correu electrònic: **oficina-tecnica.canigo.ctti@gencat.cat**.