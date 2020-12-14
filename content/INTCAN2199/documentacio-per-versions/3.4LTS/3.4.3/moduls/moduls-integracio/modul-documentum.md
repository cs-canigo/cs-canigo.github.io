+++
date        = "2020-03-27"
title       = "Documentum"
description = "Accés al gestor documental corporatiu del CTTI."
sections    = "Canigó. Documentació versió 3.x"
weight      = 4
+++

<div class="message warning">

A partir de la publicació de Canigó 3.4.3 el 26/03/2020 aquest mòdul quedarà deprecat, pel que no es preveu seguir evolucionant aquest mòdul.

</div>

## Propòsit

L'objectiu d’aquest article és **descriure la metodologia a seguir en la utilització del connector al sistema *Documentum* des de qualsevol aplicació Java del Framework J2EE**.
L'abast d'aquest sistema es fonamenta una interfície Java per a accedir a Documentum, permetent emmagatzemar i recuperar documents a més d'altres operacions relacionades com la creació de carpetes o assignació de propietats.


## Instal·lació

### Instal·lació del DFC (Documentum Foundation Classes)

Com a requisit previ a la utilització del servei, cal **instal·lar a la màquina de desenvolupament/servidor la DFC (Documentum Foundation Classes) de la versió de *Documentum* que s'utilitzarà: 5.3, 6.5 o 7.1**.
En cas de no comptar amb aquests instal·lables, es poden sol·licitar mitjançant la bústia de la OT Canigó: <oficina-tecnica.canigo.ctti@gencat.cat>.


Els passos a seguir en la instal·lació, que són similars a les tres versions, són els següents:

![Instal·lació documentum pas 1](/related/canigo/documentacio/modul-documentum/image005.jpg "Instal·lació documentum pas 1")

![Instal·lació documentum pas 2](/related/canigo/documentacio/modul-documentum/image006.jpg "Instal·lació documentum pas 2")

![Instal·lació documentum pas 3](/related/canigo/documentacio/modul-documentum/image007.jpg "Instal·lació documentum pas 3")

![Instal·lació documentum pas 4](/related/canigo/documentacio/modul-documentum/image008.jpg "Instal·lació documentum pas 4")

En aquest punt, indicarem el **host i el port del docBroker** que conté el magatzem de claus.

![Instal·lació documentum pas 5](/related/canigo/documentacio/modul-documentum/image009.jpg "Instal·lació documentum pas 5")

![Instal·lació documentum pas 6](/related/canigo/documentacio/modul-documentum/image010.jpg "Instal·lació documentum pas 6")

![Instal·lació documentum pas 7](/related/canigo/documentacio/modul-documentum/image011.jpg "Instal·lació documentum pas 7")

![Instal·lació documentum pas 8](/related/canigo/documentacio/modul-documentum/image012.jpg "Instal·lació documentum pas 8")

![Instal·lació documentum pas 9](/related/canigo/documentacio/modul-documentum/image013.jpg "Instal·lació documentum pas 9")

![Instal·lació documentum pas 10](/related/canigo/documentacio/modul-documentum/image014.jpg "Instal·lació documentum pas 10")

<br/>
Com a resultat de la instal·lació es generarà un **arxiu amb la configuració d'accés a Documentum**:

<br/>
* **Versió 5.3**: l'arxiu es generarà per defecte a `C:\WINDOWS\dmcl.ini` i tindrà el següent format:

```
[DOCBROKER_PRIMARY]
host =es-hg2r02j
port =1489

[DMAPI_CONFIGURATION]
cache_queries = T
token_storage_enabled=F
token_storage_path=D:\Documentum\apptoken
```

<br/>
* **Versions 6.5 i 7.1**: l'arxiu es generarà per defecte a `C:\Documentum\config\dfc.properties` i tindrà el següent format:

```
dfc.data.dir=C\:/Documentum
dfc.registry.mode=windows
dfc.search.ecis.enable=false
dfc.search.ecis.host=
dfc.search.ecis.port=
dfc.tokenstorage.dir=C\:/Documentum/apptoken
dfc.tokenstorage.enable=false
dfc.docbroker.host[0]=nomHostDocumentum
dfc.docbroker.port[0]=PortHostDocumentum
dfc.globalregistry.repository=NomRepositoriClaus
dfc.globalregistry.username=usernameRepositoriClaus
dfc.globalregistry.password=passRepositoriClaus
```

### Instal·lació del connector

Per tal d'**instal·lar el Mòdul de Documentum** es pot optar per incloure’l automàticament a través de l'eina de suport al desenvolupament o bé afegir
manualment la següent dependència en el fitxer `pom.xml` de l’aplicació:

<br/>
* **Versió 5.3**:

```
<canigo.integration.documentum.version>[1.2.0,1.3.0)</canigo.integration.documentum.version>

<dependency>
          <groupId>cat.gencat.ctti</groupId>
          <artifactId>canigo.integration.documentum</artifactId>
          <version>${canigo.integration.documentum.version}</version>
</dependency>
```

<br/>
* **Versió 6.5**:

```
<canigo.integration.documentum.version>[2.2.0,2.3.0)</canigo.integration.documentum.version>

<dependency>
          <groupId>cat.gencat.ctti</groupId>
          <artifactId>canigo.integration.documentum</artifactId>
          <version>${canigo.integration.documentum.version}</version>
</dependency>
```

<br/>
* **Versió 7.1**:

```
<canigo.integration.documentum.version>[3.1.0,3.2.0)</canigo.integration.documentum.version>

<dependency>
          <groupId>cat.gencat.ctti</groupId>
          <artifactId>canigo.integration.documentum</artifactId>
          <version>${canigo.integration.documentum.version}</version>
</dependency>
```

<br/>
#### Dependències amb llibreries del DFC instal·lat
Els connectors tenen dependències amb llibreries de la versió del DFC instal·lat.
Aquestes llibreries s'inclouen durant la instal·lació del DFC a la carpeta `C:\Program Files\Documentum\Shared\`.
No obstant, caldrà instal·lar-les al repositori de Maven local per a que es puguin resoldre.

<br/>
Per a la **versió 7.1**, seran necessàries les següents:

```
mvn install:install-file -Dfile="dfc.jar" -DgroupId=dfc -DartifactId=dfc -Dversion=7.1 -Dpackaging=jar
mvn install:install-file -Dfile="certj.jar" -DgroupId=certj -DartifactId=certj -Dversion=5.2 -Dpackaging=jar
mvn install:install-file -Dfile="configservice-api.jar" -DgroupId=configservice -DartifactId=configservice-api -Dversion=7.1 -Dpackaging=jar
mvn install:install-file -Dfile="configservice-impl.jar" -DgroupId=configservice -DartifactId=configservice-impl -Dversion=7.1 -Dpackaging=jar
mvn install:install-file -Dfile="jcmFIPS.jar" -DgroupId=jcmFIPS -DartifactId=jcmFIPS -Dversion=6.1 -Dpackaging=jar
mvn install:install-file -Dfile="jcifs-krb5-1.3.1.jar" -DgroupId=jcifs-krb5 -DartifactId=jcifs-krb5 -Dversion=1.3.1 -Dpackaging=jar
mvn install:install-file -Dfile="cryptojce.jar" -DgroupId=cryptojce -DartifactId=cryptojce -Dversion=6.1 -Dpackaging=jar
mvn install:install-file -Dfile="cryptojcommon.jar" -DgroupId=cryptojcommon -DartifactId=cryptojcommon -Dversion=6.1 -Dpackaging=jar
```

## Configuració

La configuració es realitza automàticament a partir de la eina de suport al desenvolupament.

### Propietats del DFC
Caldrà incloure al CLASSPATH del projecte el fitxer `dfc.properties` generat durant la instal·lació del DFC.

Ubicació: `<PROJECT_ROOT>/src/main/resources/dfc.properties`

### Propietats del connector

Ubicació: `<PROJECT_ROOT>/src/main/resources/config/props/documentum.properties`

Propietat                   | Requerit | Descripció
--------------------------- | -------- | ----------
*.documentum.user           | Sí       | Usuari de Documentum
*.documentum.password       | Sí       | Password de Documentum
*.documentum.docBase        | Sí       | Doc base
*.documentum.dir            | Sí       | Directori de Documentum
*.documentum.pathDirectori  | No       | Path directori
*.documentum.pathFitxer     | No       | Path arxiu
*.documentum.nomFitxer      | No       | Nom d'arxiu
*.documentum.extFitxer      | No       | Extensió d'arxiu
*.documentum.pathFitxer2    | No       | Path segon arxiu
*.documentum.nomFitxer2     | No       | Nom del segon arxiu
*.documentum.extFitxer2     | No       | Extensió d'un segon arxiu
*.documentum.pathFitxerOut  | No       | Directori de sortida
*.documentum.dir3           | No       | Directori
*.documentum.user2          | No       | Usuari 2
*.documentum.password2      | No       | Password 2
*.documentum.ACL            | No       | ACL
*.documentum.ACLDomain      | No       | ACL Domain
*.documentum.cicleVida      | No       | Cicle vida
*.documentum.estat          | No       | Estat
*.documentum.grup           | No       | Grup

## Funcionament

En aquest exemple tenim dues classes: *DocumentumServiceController*, que és l'Endpoint del servei, i *DocumentumAplicacioService*, que és la classe
Java en la que s’implementa la lògica de l'operació i s'invoca al mòdul de *Documentum*.

### DocumentumServiceController.java

```java
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.http.MediaType;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;

   import cat.gencat.plantilla32.service.DocumentumAplicacioService;

   @RestController
   @RequestMapping("/documentum")
   public class DocumentumServiceController {

      @Autowired
      DocumentumAplicacioService documentumAplicacioService;

      @PostMapping(produces = { MediaType.APPLICATION_JSON_VALUE })
      public String testLogin() throws Exception {
         return documentumAplicacioService.testLogin();
      }
   }
```

### DocumentumAplicacioService.java

```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.context.annotation.Lazy;
   import org.springframework.stereotype.Service;

   import cat.gencat.ctti.canigo.arch.integration.documentum.DocumentumConnector;
   import cat.gencat.ctti.canigo.arch.integration.documentum.DocumentumService;
   import cat.gencat.ctti.canigo.arch.integration.documentum.impl.DocumentumConfigurator;

   @Service("documentumAplicacioService")
   @Lazy
   public class DocumentumAplicacioService {

      private static final Logger log = LoggerFactory.getLogger(DocumentumAplicacioService.class);

      @Autowired
      private DocumentumService service;

      @Autowired
      private DocumentumConnector documentum;

      @Autowired
      private DocumentumConfigurator configurator;

      /**
       * Comprovem que es pot fer login al sistema de Documentum
       */
      public String testLogin(){
         String message = null;
         try{
            service.login(configurator.getUser(), configurator.getPassword(),configurator.getDocBase(), this.documentum);
         }catch(Exception e){
            message = "Error al realitzar login";
            log.error(e.getMessage(), e);
         }
         message = "Login correcte";
         return message;
      }

   }
```
