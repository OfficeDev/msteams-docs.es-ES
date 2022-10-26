---
title: Usar las API de Graph para capturar transcripciones
description: Describe las API que capturan transcripciones de reuniones
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 2142bc1346a032f27d8612f6081156d2c4927e8f
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699181"
---
# <a name="use-graph-apis-to-fetch-transcript"></a>Usar las API de Graph para capturar transcripciones

Use las API de REST de Graph para obtener transcripciones de una reunión determinada. La aplicación captura las transcripciones en función del id. de usuario del organizador de la reunión y del id. de la reunión.

Para capturar transcripciones se usan las siguientes API:

- [List callTranscripts](#list-calltranscripts)
- [Get callTranscript](#get-calltranscript)
- [Get callTranscript content](#get-calltranscript-content)

### <a name="list-calltranscripts"></a>List callTranscripts

Esta API se usa para obtener una lista de todos los objetos de `callTranscript` según el id. de usuario y el id. de reunión. Devuelve los metadatos de las transcripciones de la reunión, que contienen el id de transcripción y la fecha y hora de creación de dicha transcripción.

**Solicitud HTTP**

```http
GET /me/onlineMeetings('{meetingId}')/transcripts
GET /users('{userId}')/onlineMeetings('{meetingId}')/transcripts
```

**Parámetros de consulta opcionales**

Este método admite los parámetros `$skipToken` y `$top` de [consulta OData](/graph/query-parameters) para ayudar a personalizar la respuesta.

**Patrones de consulta admitidos**

| Patrón                | Compatible | Sintaxis                                 | Notas |
| ---------------------- | ------- | -------------------------------------- | ----- |
| Paginación del lado servidor |     ✓     | `@odata.nextLink`                      | Obtener un token de continuación en la respuesta, cuando un conjunto de resultados abarca varias páginas. |
| Límite de página             |     ✓     | `/transcripts?$top=20` | Obtener transcripciones con tamaño de página en 20. El límite de página predeterminado es de 10. El límite máximo de páginas es de 100. |

**Encabezados de solicitud**

| Encabezado       | Valor |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

**Cuerpo de solicitud**

No proporcione un cuerpo de solicitud para este método.

**Respuesta**

Si se ejecuta correctamente, este método devuelve un código de respuesta `200 OK` y la colección de objetos `callTranscript` en el cuerpo de la respuesta.

<br>
<details>
<summary><b>Ejemplo: Lista de callTranscript</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts
```

<br>
<b>Respuesta</b>
<br>

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts",
    "@odata.count": 3,
    "@odata.nextLink": "https://graph.microsoft.com/beta/users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts?$skiptoken=MSMjMCMjMjAyMS0wOS0xNlQxMzo1OToyNy4xMjEwMzgzWg%3d%3d",
    "value": [
        {
            "id": "MSMjMCMjZDAwYWU3NjUtNmM2Yi00NjQxLTgwMWQtMTkzMmFmMjEzNzdh",
            "createdDateTime": "2021-09-17T06:09:24.8968037Z"
        },
        {
            "id": "MSMjMCMjMzAxNjNhYTctNWRmZi00MjM3LTg5MGQtNWJhYWZjZTZhNWYw",
            "createdDateTime": "2021-09-16T18:58:58.6760692Z"
        },
        {
            "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
            "createdDateTime": "2021-09-16T18:56:00.9038309Z"
        }        
    ]
}
```

</details>

### <a name="get-calltranscript"></a>Get callTranscript

La aplicación analiza la lista de identificadores de transcripción que se han recibido como respuesta de la API `List callTranscripts` para obtener el id. de transcripción necesario. Esta API se usa para obtener metadatos de transcripción únicos basados en el id. de usuario, el id. de reunión y el id. de transcripción.

**Solicitud HTTP**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
```

**Encabezados de solicitud**

| Encabezado       | Valor |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

**Cuerpo de solicitud**

No proporcione un cuerpo de solicitud para este método.

**Respuesta**

Si se ejecuta correctamente, este método devuelve un código de respuesta `200 OK` y el objeto `callTranscript` en el cuerpo de la respuesta.

<br>
<details>
<summary><b>Ejemplo: Obtener un callTranscript</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4
```

<br>
<b>Respuesta</b>
<br>

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts/$entity",
    "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
    "createdDateTime": "2021-09-17T06:09:24.8968037Z"
}
```

</details>

### <a name="get-calltranscript-content"></a>Get callTranscript content

Esta API se usa para obtener la transcripción del id. de transcripción seleccionado que se obtuvo en la respuesta de la API `Get callTranscript`. Devuelve el contenido de la transcripción.

**Solicitud HTTP**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
```

**Parámetros de consulta opcionales**

Este método admite el [parámetro de consulta OData](/graph/query-parameters) `$format` que permite la personalización de la respuesta.

Los tipos de formato admitidos son `text/vtt` para vtt o `application/vnd.openxmlformats-officedocument.wordprocessingml.document` para el formato docx.

**Encabezados de solicitud**

| Encabezado       | Valor |
|:---------------|:--------|
| Autorización  | Bearer {token}. Required.  |
| Aceptar  | text/vtt o  application/vnd.openxmlformats-officedocument.wordprocessingml.document. Opcional.  |

**Cuerpo de solicitud**

No proporcione un cuerpo de solicitud para este método.

**Respuesta**

Si se ejecuta correctamente, este método devuelve un código de respuesta `200 OK` y contiene bytes para el objeto callTranscript en el cuerpo de la respuesta. El encabezado `content-type` especifica el tipo de contenido de la transcripción.

**Ejemplos**
<br>
<details>
<summary><b>Ejemplo: Obtener un contenido callTranscript</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
```

<br>
<b>Respuesta</b>
<br>

La respuesta contiene bytes para la transcripción en el cuerpo. El encabezado `content-type` especifica el tipo de contenido de la transcripción.

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-type: text/vtt

WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Ejemplo: Obtener un contenido callTranscript que especifica el parámetro de consulta $format</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
 ```

<br>
<b>Respuesta</b>
<br>

La respuesta contiene bytes para la transcripción en el cuerpo. El encabezado `content-type` especifica el tipo de contenido de la transcripción.

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Ejemplo: Obtener un contenido callTranscript que especifica el encabezado Accept</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Respuesta</b>
<br>

La respuesta contiene bytes para la transcripción en el cuerpo. El encabezado `content-Type` especifica el tipo de contenido de la transcripción.

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
    
0:0:0.0 --> 0:0:5.320
User Name
This is a transcript test.
```

</details>
<br>
<details>
<summary><b>Ejemplo: Obtener un contenido callTranscript con prioridad de $format sobre el encabezado accept</b></summary>
<br>
<b>Solicitud</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Respuesta</b>
<br>

La respuesta contiene bytes para la transcripción en el cuerpo. El encabezado `content-Type` especifica el tipo de contenido de la transcripción.

> [!NOTE]
> El objeto de respuesta que se muestra aquí puede estar acortado para mejorar la legibilidad.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
   
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>

