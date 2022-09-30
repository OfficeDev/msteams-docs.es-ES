---
title: API web de tablas virtuales
author: surbhigupta
description: En este módulo, obtenga información sobre la aplicación de control de api web de tablas virtuales para colaboración, la ordenación de tablas virtuales y el filtrado en Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: b15c7972dfc0152d458e4ad895ed6d4f7e45cd4c
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243552"
---
# <a name="virtual-tables-web-api"></a>API web de tablas virtuales

Cuando se usa dataverse Web API para recuperar varios registros de una tabla virtual, se pueden incluir parámetros de consulta adicionales para admitir la ordenación, el filtrado y la paginación. Estas características no se admiten uniformemente en las tablas virtuales de controles de colaboración porque se basan en la compatibilidad proporcionada por microsoft Graph API. Consulte Virtual Tables Entity Reference (Referencia de entidad de tablas virtuales) para obtener más información sobre lo que admite cada tabla virtual.

> [!NOTE]
> Actualmente, los controles de colaboración solo están disponibles en la [versión preliminar del desarrollador público](~/resources/dev-preview/developer-preview-intro.md).

## <a name="virtual-table-sorting"></a>Ordenación de tablas virtuales

Con las tablas virtuales, puede usar el parámetro de consulta OData $orderby para establecer criterios sobre cómo se debe ordenar el conjunto de resultados. Use el sufijo asc o desc para especificar el orden ascendente o descendente, respectivamente. El valor predeterminado es ascendente si no se aplica el sufijo.  

**Tablas admitidas**: cada tabla virtual admite la misma funcionalidad de ordenación que su recurso de Graph correspondiente. Las tablas virtuales, que admiten la ordenación son:  

* Elemento de unidad de grafo
* Graph (evento)

> [!NOTE]
> No se admite la ordenación en todos los atributos de los recursos de Graph correspondientes. Si un usuario intenta ordenar en una tabla virtual con un atributo no admitido, este conjunto de resultados tendrá su orden predeterminado. Este es el mismo comportamiento que dataverse web API en columnas que no admiten la ordenación.

Ejemplos:

* GET [URI de la organización]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '000000000-0000-0000-0000-00000000000'&$orderby=m365_name desc
* GET [URI de la organización]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '00000000-0000-0000-0000-000000000000'$orderby=m365_subject asc

## <a name="virtual-table-filtering"></a>Filtrado de tablas virtuales

Con las tablas virtuales, puede usar el parámetro de consulta OData $filter para establecer los criterios para los que se devuelven las filas. Las tablas virtuales se consultan con los mismos operadores de OData compatibles con dataverse Web API.

* **Operadores de comparación**

  |Operador|Descripción|Ejemplo|
  |----|----|----|
  |eq|Igual|$filter=m365_name eq 'Contoso'|
  |ne|No es igual|$filter=m365_name ne "Contoso"|
  |gt|Mayor que|$filter=m365_price gt 50.0|
  |ge|Mayor o igual|$filter=m365_price ge 50,0|
  |lt|Menor que|$filter=m365_price lt 50.0|
  |le|Menor o igual|$filter=m365_price le 50.0|

* **Operadores lógicos**

  |Operador|Descripción|Ejemplo|
  |----|----|----|
  |y|Lógico y |$filter=m365_name eq 'Contoso' y m365_price eq 50.0|
  |o|Lógico o |$filter=m365_name ne "Contoso" o m365_price eq 50.0|
  |
not|Negociación lógica |$filter=not contains(m365_name,'Contoso')|

* **Operadores de agrupación**

  |Operador|Descripción|Ejemplo|
  |----|----|----|
  |( )|Agrupación de prioridad |$filter=(m365_name eq 'Contoso' y m365_price eq 50.0) o contains(m365_subject,'Team Sync')|

* **Funciones de consulta**

  |Función |Ejemplo |
  |----|----|
  |contains|$filter=contains(m365_name,'Contoso')|
  |endswith|$filter=endswith(m365_name,'Contoso')|
  |startswith|$filter=startswith(m365_name,'Contoso')|

**Tablas admitidas**: cada tabla virtual admite la misma funcionalidad de filtrado que su recurso de Graph correspondiente. Las tablas virtuales, que admiten el filtrado son:

* Cita de reserva de Graph
* Elemento de unidad de grafo
* Graph (evento)

> [!Note]
> El filtrado no se admite en todos los atributos de los recursos de Graph correspondientes. Si un usuario intenta filtrar por una tabla virtual con un atributo no admitido, este filtro se omite. Este es el mismo comportamiento que dataverse web API en columnas que no admiten el filtrado.

Ejemplos:

* GET [URI de la organización]/api/data/v9.2/m365_graphbookingappointments?$filter=m365_bookingbusinessid eq 'ContosoBank@Contoso.onmicrosoft.com' y m365_price eq 100.0
* GET [URI de la organización]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '00000000-0000-0000-0000-000000000000' y m365_name eq 'Meeting Notes.docx'
* GET [URI de la organización]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '00000000-0000-0000-0000-000000000000' y m365_subject eq 'Monthly Sync'

## <a name="virtual-table-pagination"></a>Paginación de tabla virtual

La paginación es un recurso útil para capturar un gran conjunto de registros. La paginación de tabla virtual se puede lograr de tres maneras diferentes.

Puede especificar el tamaño de página mediante el valor de `odata.maxpagesize` preferencia en el encabezado de solicitud. Si el conjunto de resultados abarca varias páginas, la respuesta incluye la `@odata.nextLink` propiedad . La solicitud y respuesta de ejemplo son las siguientes:

# <a name="request"></a>[Solicitud](#tab/request)

```http
  GET [Organization URI]/api/data/v9.2/m365_graphdriveitems 
  Accept: application/json 
  Prefer: odata.maxpagesize=2 
```

# <a name="response"></a>[Respuesta](#tab/response)

```json
{ 

  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdriveitems", 
  "value": [ 
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      …
      },
      {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      … 
      } 
      ],
      "@odata.nextLink": "[Organization URI]/api/data/v9.0/m365_graphdriveitems &$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9dGVzdCZwX0lEPTI5%22%20istracking=%22False%22%20/%3E" 
} 
```

---

Actualmente, las siguientes tablas virtuales admiten la `odata.maxpagesize` preferencia:

* Cita de reserva de Graph
* Graph Calendar (evento)
* Unidad de grafo
* Elemento de unidad de grafo

Puede especificar el número de registros que se van a devolver pasando la `$top` opción en la dirección URL. Si también necesita especificar el número de página, puede hacerlo pasando una cookie de paginación como una cadena codificada en XML como opción `$skiptoken` . Para capturar un número de página específico, puede pasar la cookie de paginación en el formato siguiente:

  `<cookie pagenumber=3 />`

# <a name="request"></a>[Solicitud](#tab/request1)

```http
     GET [Organization URL]/api/data/v9.2/m365_graphevents?$top=2&$skiptoken=<cookie pagenumber='3' /> 
```

# <a name="response"></a>[Respuesta](#tab/response1)

```json

{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphevents", 
  "value": [
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      "m365_subject": "Important meeting", 
      …
    }, 
    {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      "m365_subject": "Another important meeting", 
      …
    } 
  ] 
}

```

---

> [!Note]
> La respuesta no incluirá la `@nextLink` propiedad . Si el caso de uso requiere que se devuelva el vínculo de página siguiente, puede usar el encabezado de preferencia odata.maxpagesize descrito en la sección 1 en lugar de pasar el parámetro URI de $top.

Actualmente, las siguientes tablas virtuales admiten la captura de una página específica:

* Cita de reserva de Graph
* Graph Calendar (evento)

Puede pasar un XML de captura como una cadena codificada en XML. Con la opción capturar XML, puede especificar varias preferencias de consulta. Las opciones específicas de paginación son página (número de página) y recuento (tamaño de página). El siguiente XML especifica el número de página y el tamaño:

  `<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="<Page Number>" count="<Page Size>"></fetch>`

# <a name="request"></a>[Solicitud](#tab/request2)

```http
GET [Organization URL]/api/data/v9.2/m365_graphevents?$fetchXml=<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="3" count="2"></fetch> 

```

# <a name="response"></a>[Respuesta](#tab/response2)

```json
{ 

    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdevents", 
    "@Microsoft.Dynamics.CRM.fetchxmlpagingcookie": "<cookie pagenumber=\"3\" pagingcookie=\"\" istracking=\"False\" />", 
    "value": [ 
        { 
            "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
            "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
            "m365_subject": "Important meeting", 
            …
        }, 
        { 
            "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
            "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
            "m365_subject": "Another important meeting", 
            …
        } 
    ] 
} 

```

---

Las siguientes tablas virtuales admiten la propiedad count que se va a pasar como parte de la opción fetchXml:

* Unidad de grafo
* Elemento de unidad de grafo

Las siguientes tablas virtuales admiten la propiedad page como parte de la opción fetchXml:

* Cita de reserva de Graph
* Graph Calendar (evento)
