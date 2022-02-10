---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Aprende a desplegar un vínculo, abrir la vista fase y anclar una pestaña con Microsoft Teams aplicación. Obtenga información sobre la vista de fase e invocarla mediante tarjeta adaptable mediante el ejemplo de código y el ejemplo.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 48c7ae69b10702d58be933b5619fd6bdeb8cecf3
ms.sourcegitcommit: 3332ca6f61d2d60ddb20140f6d163905ea177157
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/10/2022
ms.locfileid: "62516522"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Expansión del vínculo de la pestaña y vista de fases

Stage View es un nuevo componente de interfaz de usuario (UI), que te permite representar el contenido que se abre en pantalla completa en Teams y anclado como una pestaña.
 
## <a name="stage-view"></a>Vista fase

Stage View es un componente de interfaz de usuario de pantalla completa que puedes invocar para mostrar el contenido web. El servicio de desamuestración de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat. Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se despliega en una tarjeta adaptable. El usuario puede seleccionar **Ver en** la tarjeta y anclar el contenido como una pestaña directamente desde vista fase.

## <a name="advantage-of-stage-view"></a>Ventaja de la vista fase

Stage View ayuda a proporcionar una experiencia más fluida de visualización de contenido en Teams. Los usuarios pueden abrir y ver el contenido proporcionado por la aplicación sin salir del contexto, y pueden anclar el contenido al chat o canal para un acceso rápido futuro, lo que permite una mayor interacción del usuario con la aplicación.

## <a name="stage-view-vs-task-module"></a>Módulo vista fase frente a tarea

|Vista fase|Módulo de tareas|
|:-----------|:-----------|
|La vista fase es útil cuando tiene contenido enriquecido para mostrar a los usuarios, como una página, un panel, un archivo, y así sucesivamente. Proporciona características enriquecciones que ayudan a representar el contenido en el lienzo de pantalla completa.|[El módulo de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tareas es especialmente útil para mostrar mensajes que requieren atención del usuario o recopilar información necesaria para pasar al paso siguiente.|
  
## <a name="invoke-stage-view"></a>Invocar vista fase

Puede invocar la vista fase de las siguientes maneras:

* [Invocar la vista fase desde la tarjeta adaptable](#invoke-stage-view-from-adaptive-card)
* [Invocar vista de fase a través de un vínculo profundo](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Invocar la vista fase desde la tarjeta adaptable

Cuando el usuario escribe una dirección URL en el cliente de escritorio Teams, el bot se invoca y devuelve una tarjeta [](../task-modules-and-cards/cards/cards-actions.md) adaptable con la opción de abrir la dirección URL en una fase. Después de iniciar una fase y `tabInfo` de proporcionarla, puede agregar la capacidad de anclar la fase como una pestaña.  

Las siguientes imágenes muestran una fase abierta desde una tarjeta adaptable:

[![Abrir una fase desde la tarjeta adaptable](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Abrir una fase](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox) 

### <a name="example"></a>Ejemplo

A continuación se muestra el código para abrir una fase desde una tarjeta adaptable:

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

El `invoke` tipo de solicitud debe ser `composeExtension/queryLink`.

> [!NOTE]
> * `invoke` flujo de trabajo es similar al flujo de trabajo `appLinking` actual. 
> * Para mantener la coherencia, se recomienda nombrar como `Action.Submit` `View`.
> * `websiteUrl` es una propiedad necesaria que se debe pasar en el `TabInfo` objeto.

A continuación se muestra el proceso para invocar la vista fase:

* Cuando el usuario selecciona **Ver**, el bot recibe una `invoke` solicitud. El tipo de solicitud es `composeExtension/queryLink`.
* `invoke` respuesta del bot contiene una tarjeta adaptable con tipo `tab/tabInfoAction` en él.
* El bot responde con un `200` código.

> [!NOTE]
> En Teams móviles, invocar stage view para aplicaciones distribuidas a través de la tienda [Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) y no tener una experiencia optimizada para moblie abre el explorador web predeterminado del dispositivo. El explorador abre la dirección URL especificada en el `websiteUrl` parámetro del `TabInfo` objeto.

## <a name="invoke-stage-view-through-deep-link"></a>Invocar vista de fase a través de un vínculo profundo

Para invocar la vista de fase a través del vínculo profundo desde la pestaña, debe ajustar la dirección URL del vínculo profundo en la `microsoftTeams.executeDeeplink(url)` API. El vínculo profundo también se puede pasar a través de una `OpenURL` acción en la tarjeta.

### <a name="syntax"></a>Sintaxis

A continuación se muestra la sintaxis de vínculo profundo: 

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>Ejemplos

Cuando un usuario escribe una dirección URL, se despliega en una tarjeta adaptable.

A continuación se muestran los ejemplos de vínculos profundos para invocar la vista fase:

**Ejemplo 1**

No codificado
 
https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx",websiteUrl::"websiteUrl:" "https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name"Contoso"}

Codificado

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context=%7B%22contentUrl%22%3A%22https%253A%252F%252Fmicrosoft.sharepoint.com%252Fteams%252FLokisSandbox%252FSitePages%252FSandbox-Page.aspx%22%2C%22websiteUrl%0A%3A%22https%253A%252F%252Fmicrosoft.sharepoint.com%252Fteams%252FLokisSandbox%252FSitePages%252FSandbox-Page.aspx%22%2C%22name%22%3A%22Contoso%22%7D


**Ejemplo 2**

No codificado

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl"https://microsoft.sharepoint.com/teams/LokisSandbox/SitePages/Sandbox-Page.aspx,"websiteUrl"https://microsoft.sharepoint.com/teams/LokisSandbox/SitePages/Sandbox-Page.aspx,"name"Contoso"}

Codificado

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx%22%2C%22name%22%3A%22Contoso%22%7D


> [!NOTE]
> Todos los vínculos profundos deben codificarse antes de pegar la dirección URL. No se admiten direcciones URL sin codificar.
> * El `name` vínculo es opcional en profundidad. Si no se incluye, el nombre de la aplicación lo reemplaza.
> * El vínculo profundo también se puede pasar a través de una `OpenURL` acción.
> * Cuando inicies una fase desde un contexto determinado, asegúrate de que la aplicación funciona en ese contexto. Por ejemplo, si la vista fase se inicia desde una aplicación personal, debes asegurarte de que la aplicación tenga un ámbito personal.

## <a name="tab-information-property"></a>Propiedad tab information

| Nombre de la propiedad | Tipo | Número de caracteres | Descripción |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Cadena | 64 | Esta propiedad es un identificador único para la entidad que muestra la pestaña. Este campo es obligatorio.|
| `name` | Cadena | 128 | Esta propiedad es el nombre para mostrar de la pestaña en la interfaz de canal. Este campo es opcional.|
| `contentUrl` | Cadena | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario. Este campo es obligatorio.|
| `websiteUrl?` | Cadena | 2048 | Esta propiedad es la https:// url a la que apuntar, si un usuario selecciona ver en un explorador. Este campo es obligatorio.|
| `removeUrl?` | Cadena | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario que se va a mostrar cuando el usuario elimina la pestaña. Este es un campo opcional.|

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Ficha en la vista fase |Microsoft Teams aplicación de ejemplo de pestaña para mostrar la pestaña en la vista fase.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|
    

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Vea también

* [Desafutización de vínculos de extensiones de mensajería](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
