+++
date        = "2021-02-17"
title       = "Estàndard pel full de ruta del programari"
description = "Estàndard pel full de ruta del programari"
weight		= 3
type = "estandard"
toc         = true
versio      = "1.0"
responsable = "Unitat d'arquitectura"
estandards =  ["programari"]
codi = "35.080.03"

+++
## Part 1: Abast


L’elevat volum de productes que estan desplegats als CPDs de la Generalitat de Catalunya i als seus
entorns de treball i la seva heterogeneïtat de versions fa que resulti cada cop més difícil mantenir
vigents les versions de programari de les diferents tecnologies..

Com a peça facilitadora, i amb la intenció de donar una visió de l’estat de l’art de cadascuna de les
tecnologies usades (o previstes d’usar) en els nous sistemes d’informació a desplegar s’ha elaborat el
full de ruta de versions de programari.

El full de ruta de versions de programari és un document que té com a objectiu **normalitzar i
racionalitzar el desplegament de tecnologies**, alhora que es concreta tant el ventall de productes
disponibles per a una determinada tecnologia, com la versió recomanada d’un programari concret. 

Per cadascuna de les tecnologies se’n proporciona:

- Una classificació bàsica del producte en funció del grau de coneixement i implantació de la
tecnologia.
- L’estat de maduresa del producte per facilitar la determinació tant de la versió a utilitzar en el
moment de la seva implantació com el grau d’obsolescència dels productes que estan
actualment en ús.


## Part 2: Referències 

## Part 3: Termes i definicions

##### Maduresa d'una tecnologia

La visió de la maduresa de la tecnologia consisteix en reflectir de forma objectiva el nivell de suport en què es troba una tecnologia concreta, tant si es tracta de versions que s’utilitzen des de fa temps com si es tracta de versions a utilitzar en un futur més o menys immediat.

Al full de ruta es presenta la maduresa des de dos punts de vista diferents:

- Des del punt de vista del grau de suport intern
- Des del punt de vista del grau de suport del fabricant de programari 

A l'annex <a href='{{<relref "#maduresa" >}}'>Maduresa d'una tecnologia</a> es recullen les diferents visions de maduresa incloses al full de ruta


##### Mètode de classificació

Per cada tecnologia inclosa en el full de ruta se li associa el **Grup de tecnologies** al que pertany (base de dades, gestió documental, sistema operatiu, etc.)

## Part 4: Requisits del programari

1. Quan es defineixi la necessitat d'un nou programari **s'ha d'usar el programari estandarditzat pel CTTI**, segons les taules recollides a l'annex A l'annex <a href='{{<relref "#fullruta" >}}'>Programari estandarditzat</a>

1. Si un programari no es troba al full de ruta no vol dir ni que no es pugui utilitzar ni que no estigui subjecte als mateixos criteris d’obsolescència que la resta de productes. En cas de dubtes sobre algun programari podeu adreçar-vos a la Unitat d’Arquitectura Corportiva de CTTI.

1. Arran del dinamisme de les versions de les diferents tecnologies per part dels fabricants, el full de ruta ha de ser revisat quadrimestralment. D’aquesta forma cada full de ruta publicat contindrà les dates de la darrera revisió i validesa de la informació que conté.

# ANNEX A (normatiu) Programari estandarditzat
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.18/css/jquery.dataTables.min.css">
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/responsive/2.2.2/css/responsive.dataTables.min.css">
<link rel="stylesheet" type="text/css" href="https://canigo.ctti.gencat.cat/drafts/FullRuta20/tableStyle.css">
<script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.3.1.js"></script>
<script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.10.18/js/jquery.dataTables.min.js"></script>
<script type="text/javascript" language="javascript" src="https://cdn.datatables.net/responsive/2.2.2/js/dataTables.responsive.min.js"></script>

<table id="Revisio" class="display" style="width:50%">
<thead>
<tr>
<th>Darrera revisió realitzada</th>
<th> Revisió de full de ruta vigent fins</th>
</tr>
<tr>
<td>juliol de 2020 </td>
<td>octubre de 2020</td>
</tr>
</thead>
</table>
<font size="20">
<table id="Titol_CPD" class="display" style="width:100%">
        <thead>
	    <tr>
                <th  colspan="8" align="center" style="font-weight:bold">  Programari estandarditzat per Servidors</th>
            </tr>
 </thead>
</table>
</font>
<table id="FullRutaCPD" class="display" style="width:100%">
        <thead>
            <tr>
                <th></th>
                <th>Grup de Tecnologies</th>
                <th>Producte</th>
                <th>Obsolet</th>
                <th>Suportat</th>
                <th>Versió Actual CTTI</th>
                <th>En Roadmap</th>
                <th>Emergent</th>
            </tr>
        </thead>
</table>
<font size="20">
<table id="Titol_LLT" class="display" style="width:100%">
        <thead>
	    <tr>
                <th  colspan="8" align="center" style="font-weight:bold">  Programari estandarditzat per Lloc de Treball  </th>
            </tr>
 </thead>
</table>
</font>
<table id="FullRutaLLT" class="display" style="width:100%">
        <thead>
	    <tr>
                <th></th>
                <th>Grup de Tecnologies</th>
                <th>Producte</th>
                <th>Obsolet</th>
                <th>Suportat</th>
                <th>Versió Actual CTTI</th>
                <th>En Roadmap</th>
                <th>Emergent</th>
            </tr>
        </thead>
</table>
<!--
<font size="20">
<table id="Titol_Conn" class="display" style="width:100%">
        <thead>
	    <tr>
                <th  colspan="8" align="center" style="font-weight:bold">  Programari estandarditzat per Connectivitat de l'Entorn de Treball </th>
            </tr>
 </thead>
</table>
</font>
-->
<!--
<table id="FullRutaCONN" class="display" style="width:100%">
        <thead>
	    <tr>
                <th>Grup de Tecnologies</th>
                <th>Producte</th>
                <th>Obsolet</th>
                <th>Suportat</th>
                <th>Versió Actual CTTI</th>
                <th>En Roadmap</th>
                <th>Emergent</th>
            </tr>
        </thead>
</table>
-->

<font size="20">
<table id="Titol_HOST" class="display" style="width:100%">
        <thead>
	    <tr>
                <th  colspan="8" align="center" style="font-weight:bold">  Programari estandarditzat per Mainframe i AS400 </th>
            </tr>
 </thead>
</table>
</font>
<table id="FullRutaHOST" class="display" style="width:100%">
        <thead>
	    <tr>
                <th>Grup de Tecnologies</th>
                <th>Producte</th>
                <th>Obsolet</th>
                <th>Suportat</th>
                <th>Versió Actual CTTI</th>
                <th>En Roadmap</th>
                <th>Emergent</th>
            </tr>
        </thead>
</table>

<script>
// Funció que dona format a la taula interna del Full de Ruta de Lloc de Treball
function formatLLT(d) {
    return '<table cellpadding="7" cellspacing="1" style="padding-left:50px;border-collapse:collapse;width:100%">'+
        '<tr>'+
            '<th>Versions per Lot </th>'+
	    '<th width="300">LT1</th>'+
            '<th width="300">LT2A</th>'+
            '<th width="300">LT2B</th>'+
            '<th width="300">LT2C</th>'+
        '</tr>'+
        '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Versió producte a W8.1</th>'+
            '<td>NO APLICA</td>'+
	    '<td>'+d.lt2avw8+'</td>'+
            '<td>'+d.lt2bvw8+'</td>'+
            '<td>'+d.lt2cvw8+'</td>'+
        '</tr>'+
	'<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Versió producte a W10</th>'+
            '<td>NO APLICA</td>'+
	    '<td>'+d.lt2avw10+'</td>'+
            '<td>'+d.lt2bvw10+'</td>'+
            '<td>'+d.lt2cvw10+'</td>'+
	  '</tr>'+
	  '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Versió plataforma</th>'+
            '<td>'+d.lt1+'</td>'+
	    '<td>NO APLICA</td>'+
             '<td>'+d.lt2bpl+'</td>'+
            '<td>'+d.lt2cpl+'</td>'+
	  '</tr>'+
        '<tr>'+
	        '<th>   </th>'+
	        '<th  colspan="4">   </th>'+
	    '</tr>'+
	    '<tr>'+
            '<th>Observacions:</th>'+
            '<td colspan="4">'+d.observacions+'</td>'+
        '</tr>'+
    '</table>';
}
$(document).ready(function() {
    var taulaFullRutaLLT = $('#FullRutaLLT').DataTable( {
    "columnDefs": [
        { "width": "10%", "targets": 0 }
    ],
    "paging": false,
	"info" : false,
	"ordering": false,
	"responsive": {
            details: false
    	},
    	"language":{
	        	"search" : "<strong>Cerca:</strong> ",
		        "infoEmpty": "No hi ha registres",
	        	"zeroRecords": "No s'han trobat registres"
        },
        "ajax": "../FullRuta20/inventariLLT.json",
        "columns": [
            {
                "className":      'details-control',
                "orderable":      false,
                "data":           null,
                "defaultContent": '',
	        "width": "10%"
            },
            { "data": "categoria",
	      "width": "30%" },
            { "data": "producte", 
	      "className":      'intern',
	      "width": "30%"
	    },
            { "data": "obsolet",
	      "width": "20%" },
            { "data": "suportat",
	      "width": "80%" },
            { "data": "versioactual",
	      "className":      'intern',
	      "width": "80%"
	    },
            { "data": "roadmap",
	      "width": "100%" },
            { "data": "emergent",
	      "width": "100%" }
        ],
        "order": [[1, 'asc']],
           "initComplete": function () {
            this.api().columns().every( function (col_index) {
                var column = this;
                if (col_index !==1 && col_index !==2){
	                	$("<p>&nbsp;</p>").appendTo($(column.header()));
	                	return;
                }
                var select = $('<select><option value=""></option></select>')
                    .appendTo( $(column.header()) )
                    .on( 'change', function () {
                        var val = $.fn.dataTable.util.escapeRegex(
                            $(this).val()
                        ); 
                        column
                            .search( val ? '^'+val+'$' : '', true, false )
                            .draw();
                    } ); 
                column.data().unique().sort().each( function ( d, j ) {
                    select.append( '<option value="'+d+'">'+d+'</option>' )
                } );
            } );
        }
    });
     // Add event listener for opening and closing details
  $('#FullRutaLLT tbody').on('click', 'td.details-control', function () {
        var tr = $(this).closest('tr');
        var row = taulaFullRutaLLT.row( tr );
        if ( row.child.isShown() ) {
            // This row is already open - close it
            row.child.hide();
            tr.removeClass('shown');
        }
        else {
            // Open this row
            row.child( formatLLT(row.data()) ).show();
            tr.addClass('shown');
        }
    });

});
// Funció que dona format a la taula interna del Full de Ruta de Connectivitat de l'Entorn de Treball
function formatCONN(d) {
    return '<table cellpadding="7" cellspacing="1" style="padding-left:50px;border-collapse:collapse;width:100%">'+
        '<tr>'+
            '<th>Versions per Lot </th>'+
            '<th width="300">LT2A</th>'+
            '<th width="300">LT2B</th>'+
            '<th width="300">LT2C</th>'+
        '</tr>'+
        '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Versions disponibles</th>'+
            '<td>'+d.lt2a+'</td>'+
            '<td>'+d.lt2b+'</td>'+
            '<td>'+d.lt2c+'</td>'+
        '</tr>'+
        '<tr>'+
	        '<th>   </th>'+
	        '<th  colspan="3">   </th>'+
	    '</tr>'+
	    '<tr>'+
            '<th>Observacions:</th>'+
            '<td colspan="3">'+d.observacions+'</td>'+
        '</tr>'+
    '</table>';
}
$(document).ready(function() {
    var taulaFullRutaCONN = $('#FullRutaCONN').DataTable( {
    "columnDefs": [
        { "width": "10%", "targets": 0 }
    ],
    "paging": false,
	"info" : false,
	"ordering": false,
	"responsive": {
            details: false
    	},
    	"language":{
	        	"search" : "<strong>Cerca:</strong> ",
		        "infoEmpty": "No hi ha registres",
	        	"zeroRecords": "No s'han trobat registres"
        },
        "ajax": "../FullRuta20/inventariCONN.json",
        "columns": [
//            {
//                "className":      'details-control',
//                "orderable":      false,
//                "data":           null,
//                "defaultContent": '',
//	        "width": "10%"
//            },
            { "data": "categoria",
	      "width": "30%" },
            { "data": "producte", 
	      "className":      'intern',
	      "width": "30%"
	    },
            { "data": "obsolet",
	      "width": "20%" },
            { "data": "suportat",
	      "width": "80%" },
            { "data": "versioactual",
	      "className":      'intern',
	      "width": "80%"
	    },
            { "data": "roadmap",
	      "width": "100%" },
            { "data": "emergent",
	      "width": "100%" }
        ],
        "order": [[1, 'asc']],
           "initComplete": function () {
            this.api().columns().every( function (col_index) {
                var column = this;
                if (col_index !==7){
	                	$("<p>&nbsp;</p>").appendTo($(column.header()));
	                	return;
                }
                var select = $('<select><option value=""></option></select>')
                    .appendTo( $(column.header()) )
                    .on( 'change', function () {
                        var val = $.fn.dataTable.util.escapeRegex(
                            $(this).val()
                        ); 
                        column
                            .search( val ? '^'+val+'$' : '', true, false )
                            .draw();
                    } ); 
                column.data().unique().sort().each( function ( d, j ) {
                    select.append( '<option value="'+d+'">'+d+'</option>' )
                } );
            } );
        }
    });
     // Add event listener for opening and closing details
/*  $('#FullRutaCONN tbody').on('click', 'td.details-control', function () {
        var tr = $(this).closest('tr');
        var row = taulaFullRutaCONN.row( tr );
        if ( row.child.isShown() ) {
            // This row is already open - close it
            row.child.hide();
            tr.removeClass('shown');
        }
        else {
            // Open this row
            row.child( formatCONN(row.data()) ).show();
            tr.addClass('shown');
        }
    });
*/
});
// Funció que dona format a la taula interna del Full de Ruta de HOST
function formatHOST(d) {
    return '<table cellpadding="7" cellspacing="1" style="padding-left:50px;border-collapse:collapse;width:100%">'+
        '<tr>'+
            '<th>Versions per Lot </th>'+
            '<th width="300">LT2A</th>'+
            '<th width="300">LT2B</th>'+
            '<th width="300">LT2C</th>'+
        '</tr>'+
        '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Versions disponibles</th>'+
            '<td>'+d.lt2a+'</td>'+
            '<td>'+d.lt2b+'</td>'+
            '<td>'+d.lt2c+'</td>'+
        '</tr>'+
        '<tr>'+
	        '<th>   </th>'+
	        '<th  colspan="3">   </th>'+
	    '</tr>'+
	    '<tr>'+
            '<th>Observacions:</th>'+
            '<td colspan="3">'+d.observacions+'</td>'+
        '</tr>'+
    '</table>';
}
$(document).ready(function() {
    var taulaFullRutaHOST = $('#FullRutaHOST').DataTable( {
    "columnDefs": [
        { "width": "10%", "targets": 0 }
    ],
    "paging": false,
	"info" : false,
	"ordering": false,
	"responsive": {
            details: false
    	},
    	"language":{
	        	"search" : "<strong>Cerca:</strong> ",
		        "infoEmpty": "No hi ha registres",
	        	"zeroRecords": "No s'han trobat registres"
        },
        "ajax": "../FullRuta20/inventariHOST.json",
        "columns": [
//            {
//                "className":      'details-control',
//                "orderable":      false,
//                "data":           null,
//                "defaultContent": '',
//	        "width": "10%"
//            },
            { "data": "categoria",
	      "width": "30%" },
            { "data": "producte", 
	      "className":      'intern',
	      "width": "30%"
	    },
            { "data": "obsolet",
	      "width": "20%" },
            { "data": "suportat",
	      "width": "80%" },
            { "data": "versioactual",
	      "className":      'intern',
	      "width": "80%"
	    },
            { "data": "roadmap",
	      "width": "100%" },
            { "data": "emergent",
	      "width": "100%" }
        ],
        "order": [[1, 'asc']],
           "initComplete": function () {
            this.api().columns().every( function (col_index) {
                var column = this;
                if (col_index !==7){
	                	$("<p>&nbsp;</p>").appendTo($(column.header()));
	                	return;
                }
                var select = $('<select><option value=""></option></select>')
                    .appendTo( $(column.header()) )
                    .on( 'change', function () {
                        var val = $.fn.dataTable.util.escapeRegex(
                            $(this).val()
                        ); 
                        column
                            .search( val ? '^'+val+'$' : '', true, false )
                            .draw();
                    } ); 
                column.data().unique().sort().each( function ( d, j ) {
                    select.append( '<option value="'+d+'">'+d+'</option>' )
                } );
            } );
        }
    });
     // Add event listener for opening and closing details
/*  $('#FullRutaHOST tbody').on('click', 'td.details-control', function () {
        var tr = $(this).closest('tr');
        var row = taulaFullRutaHOST.row( tr );
        if ( row.child.isShown() ) {
            // This row is already open - close it
            row.child.hide();
            tr.removeClass('shown');
        }
        else {
            // Open this row
            row.child( formatHOST(row.data()) ).show();
            tr.addClass('shown');
        }
    });
*/
});
// Funció que dona format a la taula interna del Full de Ruta de CPD
function formatCPD(d) {
    // `d` is the original data object for the row
    return '<table cellpadding="7" cellspacing="1" style="padding-left:50px;border-collapse:collapse;width:100%">'+
        '<tr>'+
            '<th>Tipus Serveis i versions </th>'+
            '<th width="300">CPD1</th>'+
            '<th width="300">CPD2</th>'+
            '<th width="300">CPD3</th>'+
            '<th width="300">CPD4</th>'+
            '<th width="300">Azure</th>'+
        '</tr>'+
        '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Cloud Privat</th>'+
            '<td>'+d.cpd1v1+'</td>'+
            '<td>'+d.cpd2v1+'</td>'+
            '<td>'+d.cpd3v1+'</td>'+
            '<td>'+d.cpd4v1+'</td>'+
            '<td>'+d.azurev1+'</td>'+
        '</tr>'+
        '<tr>'+
            '<th style="border: 1px solid rgb(165, 165, 165);">Container Cloud</th>'+
            '<td style="border: 1px solid rgb(165, 165, 165);">'+d.cpd1v2+'</td>'+
	//Container cloud CPD2 es realment el servei bluemix
            '<td style="border: 1px solid rgb(165, 165, 165);">'+d.bluemixv2+'</td>'+ 
            '<td style="border: 1px solid rgb(165, 165, 165);">'+d.cpd3v2+'</td>'+
            '<td style="border: 1px solid rgb(165, 165, 165);">'+d.cpd4v2+'</td>'+
            '<td style="border: 1px solid rgb(165, 165, 165);">'+d.azurev2+'</td>'+
        '</tr>'+
        '<tr>'+
	        '<th>   </th>'+
	        '<th  colspan="6">   </th>'+
	    '</tr>'+
	    '<tr>'+
            '<th >Desplegable al SIC</th>'+
            '<td colspan="6">'+d.desplegablesicv1+'</td>'+
        '</tr>'+
        '<tr>'+
            '<th>Observacions:</th>'+
            '<td colspan="6">'+d.observacions+'</td>'+
        '</tr>'+
    '</table>';
}
$(document).ready(function() {
    var taulaFullRutaCPD = $('#FullRutaCPD').DataTable( {
    "columnDefs": [
        { "width": "10%", "targets": 0 }
    ],
    "paging": false,
	"info" : false,
	"ordering": false,
	"responsive": {
            details: false
    	},
    	"language":{
	        	"search" : "<strong>Cerca:</strong> ",
		        "infoEmpty": "No hi ha registres",
	        	"zeroRecords": "No s'han trobat registres"
        },
        "ajax": "../FullRuta20/inventariCPD.json",
        "columns": [
            {
                "className":      'details-control',
                "orderable":      false,
                "data":           null,
                "defaultContent": '',
	        "width": "10%"
            },
            { "data": "categoria",
	      "width": "30%" },
            { "data": "producte", 
	      "className":      'intern',
	      "width": "30%"
	    },
            { "data": "obsolet",
	      "width": "20%" },
            { "data": "suportat",
	      "width": "80%" },
            { "data": "versioactual",
	      "className":      'intern',
	      "width": "80%"
	    },
            { "data": "roadmap",
	      "width": "100%" },
            { "data": "emergent",
	      "width": "100%" }
        ],
        "order": [[1, 'asc']],
           "initComplete": function () {
            this.api().columns().every( function (col_index) {
                var column = this;
                if (col_index !==1 && col_index !==2){
	                	$("<p>&nbsp;</p>").appendTo($(column.header()));
	                	return;
                }
                var select = $('<select><option value=""></option></select>')
                    .appendTo( $(column.header()) )
                    .on( 'change', function () {
                        var val = $.fn.dataTable.util.escapeRegex(
                            $(this).val()
                        ); 
                        column
                            .search( val ? '^'+val+'$' : '', true, false )
                            .draw();
                    } ); 
                column.data().unique().sort().each( function ( d, j ) {
                    select.append( '<option value="'+d+'">'+d+'</option>' )
                } );
            } );
        }
    });
     // Add event listener for opening and closing details
    $('#FullRutaCPD tbody').on('click', 'td.details-control', function () {
        var tr = $(this).closest('tr');
        var row = taulaFullRutaCPD.row( tr );
        if ( row.child.isShown() ) {
            // This row is already open - close it
            row.child.hide();
            tr.removeClass('shown');
        }
        else {
            // Open this row
            row.child( formatCPD(row.data()) ).show();
            tr.addClass('shown');
        }
    });
});
</script>

\* DB2: Versió actual CTTI (DGP) es la 10, versió actual CTTI (Corporatiu) es la 8.

### Descripció de la informació proporcionada a la taula de programari estandarditzat de CPD

A la taula de programari estandarditzat de CPD es proporciona informació respecte a les versions de programari o tecnologia i la seva <a href='{{<relref "#maduresa" >}}'>maduresa</a>, a més a la taula desplegable es pot trobar informació addicional respecte a la prestació dels serveis oferts per cada un dels CPDs per la tecnologia seleccionada, així com informació respecte a si és desplegable de forma automàtica des del SIC.

#### Definició dels tipus de serveis a cloud

- **xPaaS**: És un entorn d’execució que s’arrenca en el moment de fer el push de l’artefacte que volem fer córrer. No hi ha pre-aprovisionament. Talles flexibles. Escalat automàtic.
- **Contenidor**: Artefacte de software que inclou totes les dependències necessàries per a dur a terme la seva funció i és portable entre clouds que els suportin (Docker)
- **DBaaS**: Base de dades com a servei, és un subtipus de xPaaS. Escala automàticament.
- **PaaS**: Plataforma de programari oferta al nuvol que inclou el middleware administrat.
- **IaaS**: Màquines virtuals a cloud, on s’aprovisiona inclouen el sistema operatiu administrat i s'instal·la a sobre el programari personalitzat que es demani.

# ANNEX B (informatiu) Maduresa d'una tecnologia {#maduresa}

### La maduresa des del punt de vista del grau de suport intern

Una tecnologia en les seves diferents versions pot passar per 5 estadis diferents. 

- **Obsolet**. Una versió d’una tecnologia es considerarà obsoleta en el moment en què estigui fora de la línia de manteniment correctiu del seu fabricant, ja sigui perquè està en període de suport extès o completament fora de suport del fabricant.

- **Suportat**. Una versió d’un producte es considerarà suportada mentre el fabricant (o una empresa de serveis especialitzada) doni suport de manteniment estàndard de la versió del programari.

- **Versió actual CTTI**. És la versió de programari que s’està desplegant actualment. Si no hi ha cap motiu que requereixi reconsiderar l’elecció, és la versió de programari que es recomana utilitzar.

- **En Roadmap CTTI**. És la versió de programari que està estudiant-se per la seva futura implantació. Un cop definida i implantada l’arquitectura de la versió, aquesta passarà a ser la “versió actual CTTI”.

- **Emergent**. És la darrera versió de programari publicada pel fabricant i reconeguda internament però que encara no està en avaluació per la seva implantació (és a dir, ni “En Roadmap CTTI” ni en “Versió actual CTTI”).

### La maduresa des del punt de vista del fabricant

Segons el fabricant d’una tecnologia, un producte en les seves diferents versions pot passar per 3 estadis diferents. 

- **No suportat**. Versió sobre la que ja no es presta suport o bé es presta un suport extès, normalment amb uns costos superiors als del manteniment habitual.

- **Suport estàndard**. Versió de programari sobre la que es presta suport evolutiu i correctiu. 

- **Actual**. Versió considerada com a actual per part del fabricant (coincideix amb les versions que estan en període de suport).
 
