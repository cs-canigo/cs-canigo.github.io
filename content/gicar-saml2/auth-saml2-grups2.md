+++
date        = "2019-11-13T00:00:00+01:00"
title       = "Control d'accés als recursos amb GICAR"
description = "Com integrar l'autorització d'una aplicació amb GICAR"
sections    = "gicar-saml2"
taxonomies  = []
weight	= 6
+++


En aquest document es presenta una la solució que ofereix GICAR, per a donar al procés d’autenticació de les funcionalitats per a poder afegir el rol que juga l’usuari dins de les aplicacions a GICAR i, d’aquesta manera, alliberar a l’aplicació d’haver de mantenir una taula d’usuari i rol, i per tant proporcionar a l’aplicació la informació per a fer l’autorització.

## Avantatges que aporta la solució proposada

1. Augmentar l’estandardització de com es construeixen les aplicacions.
2. Gestió autoservei i descentralitzada dels rols dels usuaris a les aplicacions.
3. Uns mateixos rols definits poden servir per un grup d’aplicacions.
4. Simplificació del model autoritzatiu de les aplicacions.
5. Alleugeriment d’esforços al donar d’alta un usuari en aplicacions que tenen el model autoritzatiu creuat.
6. Gestió automàtica de revocació de rols quan un usuari marxa de l’organització.
7. Auditoria centralitzada d’assignació / des-assignació de rols.
8. Capacitat d’integració de la solució definida amb Remedy.
9. Solució plenament compatible i orientada al model de directori únic futurible.

## Arquitectura d'integració amb GICAR només amb autenticació

A continuació es mostren les dades que es faciliten des de GICAR actualment quan un usuari s’autentica a una aplicació si l'autenticació es fa OK:

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-previa.png)

## Arquitectura d'integració amb GICAR incorporant l'autorització

A continuació es mostren les dades que es faciliten des de GICAR actualment quan un usuari s’autentica a una aplicació si l'autenticació es fa OK:

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-final.png)

Els rols seran transferits als frontals de les aplicacions a través de protocol SAMLv2, per tant si l'aplicació vol assolir aquesta modalitat d'integració caldrà que s'integri via SAML2 (per exemple amb agent de Shibboleth, via Out Of The Box si l'aplicació suporta SAML2, o via un ADFS).

## Com es passen els grups d'usuaris a les aplicacions:

Els rols de l'usuari viatjaran a través del claim: 

	"urn:oid:2.16.840.1.113719.1.1.4.1.25" - friendlyName="groupMembership".

Aquest claim tindrà el següent format:

	<saml2:Attribute FriendlyName="groupMembership" Name="urn:oid:2.16.840.1.113719.1.1.4.1.25" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri">
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">77_11_VISCAT_Usuaris_ADI</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">elk_kibana_user</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">ACA_ADMIN_APLICACIONS-GICARDC</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">INT_98_01 TECA_Administracio_ADD</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">GESNUS_CESICAT_PROVA-GICARDC</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">0192_MANTAINER_3162</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">PROVA_MULTIPLE-GICARGESTIODC</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">INT_77_11_VISCAT_Usuaris_ACA_ADD</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">192_206_gaudi</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">CTTI_XPACK-GICARDC</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">prova</saml2:AttributeValue>¡
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">Usuaris_ColectiuT2</saml2:AttributeValue>
		<saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">INT_90_12_ SiteTributari_TecnicAca</saml2:AttributeValue>
	<saml2:AttributeValue xmlns:xs</saml2:Attribute>

En el cas d'utilitzar un agent de Shibboleth, el claim es transforma en capçalera HTTP i serà transcrita de la següent forma:

	HTTP_GICAR_MEMBERL --> VPN_PRE-GICARDC;VPN_GENERIC-GICARDC;GESNUS_N3_Escriptura;VPN_GENERIC

Els grups estaran separats pel caràcter ";".

## Filosofia del mòdul de gestió d'autoritzacions

En el nou mòdul de GDI de gestió d'autoritzacions, existiran dos tipus de rols que es podran assignar a les identitats de GICAR:

1. Rols d’autorització simples: representen un rol/permís dins d’una aplicació.
1. Rols d’autorització múltiples: representen un conjunt de rols d’autorització simples. Al assignar un rol d’assignació múltiple s’assignen de facto tots els simples que aquest conté.

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-tipusrols.PNG)

Des d’àmbit es podran disposar de dos tipus de privilegis que permetran:

1. Operador de rols: gestionar l’assignació dels rols d’assignació simples i múltiples als usuaris de GICAR.
1. Gestor de rols: 
- Gestionar qui és l’operador de rols, 
- Definir quins rols d’autorització simples composen cada rol d’autorització múltiple. 
- Crear nous rols d’autorització simples o múltiples.

### Exemple

1. Rols d’autorització simples: representen un rol/permís dins d’una aplicació.

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-ex1.png)

1. Rols d’autorització múltiples: representen un conjunt de rols d’autorització simples. Al assignar un rol d’assignació múltiple s’assignen de facto tots els simples que aquest conté.

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-ex2.png)

## Utilització del mòdul de gestió d'autoritzacions

### Rol d'Operador

Si es disposa del rol d'Operador de rols, accedir amb un navegador al següent link https://gicar.intranet.gencat.cat/gdi/controlaccesrecursos/

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-md1.png)

Seleccionar el botó "Gestionar", en la pàgina següent apareixerà el llistat dels usuaris ja adscrits al grup seleccionat. 
En aquesta pàgina es podran gestionar les altes i les baixes individuals d'usuaris:

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-md2.png)

Per a ALTES: inserir el DNI de l'usuari  (1) o, en la seva absència l'adreça de correu electrònic i seleccionar el botó "Enviar" (2).

![Integració Aplicacions GICAR](/related/gicar/autoritzacio-md3.png)

Per a BAIXES: seleccionar el botó "esborrar" en la línia corresponent a l'usuari a eliminar del grup.

### Rol d'Administrador

Per a fer ús del rol d'administrador contacteu amb la OTGICAR.