---
title: Integrar Selector de personas
author: Rajeshwari-v
description: Cómo usar Teams SDK de cliente de JavaScript para integrar el control selector de personas
keywords: control de selector de personas
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 0c4bac7a92042d339f35c4b3eeb2c7302e5f0e1a
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212583"
---
# <a name="integrate-people-picker"></a>Integrar Selector de personas  

Selector de personas es un control para buscar y seleccionar personas. Esta es una funcionalidad nativa disponible en Teams plataforma. Puedes integrar Teams de entrada del selector de personas nativo con tus aplicaciones web. Puede seleccionar entre una o varias selecciones y configuraciones, como limitar la búsqueda en un chat, canales o en toda la organización.

Puedes usar Microsoft Teams [SDK de cliente de JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)que proporciona API para integrar el Selector de personas dentro de la aplicación `selectPeople` web. 

## <a name="advantages-of-integrating-the-native-people-picker"></a>Ventajas de integrar el selector de personas nativo 

* El control selector de personas funciona en todas Teams superficies, como un módulo de tareas, un chat, un canal, una pestaña de reunión y una aplicación personal.
* Este control le permite buscar y seleccionar usuarios dentro de un chat, canal o toda la organización.
* El Selector de personas ayuda con escenarios que implican la asignación de tareas, el etiquetado y la notificación a un usuario. 
* Puedes usar este control fácilmente disponible en la aplicación web. Ahorra el esfuerzo y el tiempo de forma significativa para crear un control de este tipo por su cuenta.

Debes llamar a la API para integrar el control selector de personas `selectPeople` en tu Teams aplicación. Para una integración eficaz, debe comprender el fragmento de [código](#code-snippet) para llamar a la API. Es importante familiarizarse con los errores de respuesta [de la API](#error-handling) para controlar los errores de la aplicación web.

> [!NOTE] 
> Actualmente, Microsoft Teams compatibilidad con el selector de personas solo está disponible para clientes móviles.

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`La API le permite agregar Teams nativa `People Picker input control` a las aplicaciones web.  
La descripción de la API es la siguiente:

| API      | Descripción  |
| --- | --- |
|**selectPeople**|Inicia un selector de personas y permite al usuario buscar y seleccionar una o más personas de la lista.<br/><br/>Esta API devuelve el identificador, el nombre y la dirección de correo electrónico de los usuarios seleccionados a la aplicación web de llamada.<br/><br/>En caso de una aplicación personal, el control busca en toda la organización. Si la aplicación se agrega a un chat o canal, el contexto de búsqueda se configura según el escenario. La búsqueda está restringida dentro de los miembros de ese chat, canal o disponible en toda la organización.|

La `selectPeople` API incluye las siguientes configuraciones de entrada:

|Parámetro Configuration|Tipo|Descripción| Valor predeterminado|
|-----|------|--------------|------|
|`title`| Cadena| Es un parámetro opcional. Establece el título del control Selector de personas. | Seleccionar personas|
|`setSelected`|Cadena| Es un parámetro opcional. Debe pasar los Azure AD de las personas que se elegirán previamente. Este parámetro preselecciona a los usuarios al iniciar el control Selector de personas. En caso de selección única, solo el primer usuario válido se prepopultó ignorando el resto. |Null| 
|`openOrgWideSearchInChatOrChannel`|Booleano | Es un parámetro opcional. Cuando se establece en true, inicia el Selector de personas en el ámbito de toda la organización incluso si la aplicación se agrega a un chat o canal. |Falso|
|`singleSelect`|Boolean|Es un parámetro opcional. Cuando se establece en true, inicia el Selector de personas que restringe la selección a un solo usuario. |Falso|

En la siguiente imagen se muestra la experiencia del selector de personas en una aplicación web de ejemplo:

![Experiencia de aplicación web del selector de personas](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a>Fragmento de código

**Llamada `selectPeople` API** para seleccionar personas de una lista:

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a>Control de errores

Debes asegurarte de controlar los errores correctamente en la aplicación web. En la tabla siguiente se enumeran los códigos de error y las condiciones en las que se generan los errores: 

|Código de error |  Nombre del error     | Condición|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | La API no se admite en la plataforma actual.|
| **500** | INTERNAL_ERROR | Se produce un error interno al iniciar el Selector de personas.|
| **4000** | INVALID_ARGUMENTS | La API se invoca con argumentos obligatorios incorrectos o insuficientes.|
| **8000** | USER_ABORT |El usuario canceló la operación.|
| **9000** | OLD_PLATFORM | El usuario se encuentra en una compilación de plataforma antigua donde la implementación de la API no está presente.  La actualización de la compilación resuelve el problema.|

## <a name="see-also"></a>Vea también

* [Integrar funcionalidades multimedia en Teams](mobile-camera-image-permissions.md)
* [Integrar la funcionalidad de escáner de código QR o código de barras en Teams](qr-barcode-scanner-capability.md)
* [Integrar las capacidades de ubicación en Teams](location-capability.md)
