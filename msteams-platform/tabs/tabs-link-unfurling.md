---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Obtenga información sobre cómo desenrollar un vínculo, abrir la vista fase y anclar una pestaña con Microsoft Teams aplicación. Obtenga información sobre la vista de fase y cómo invocarla mediante tarjeta adaptable mediante ejemplo de código y ejemplo.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 043129d6a81543ac00acf8b64da49f75282823a2
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104087"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Expansión del vínculo de la pestaña y vista de fases

Vista de fase es un nuevo componente de interfaz de usuario (UI), que permite representar el contenido que se abre en pantalla completa en Teams y se ancla como una pestaña.

## <a name="stage-view"></a>Vista de fase

Vista de fase es un componente de interfaz de usuario de pantalla completa que puede invocar para exponer el contenido web. El servicio de desplegamiento de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat. Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se desplegó en una tarjeta adaptable. El usuario puede seleccionar **Ver** en la tarjeta y anclar el contenido como una pestaña directamente desde vista de fase.

## <a name="advantage-of-stage-view"></a>Ventaja de la vista de fase

Vista de fase ayuda a proporcionar una experiencia más fluida de visualización de contenido en Teams. Los usuarios pueden abrir y ver el contenido proporcionado por la aplicación sin salir del contexto, y pueden anclar el contenido al chat o canal para un acceso rápido futuro que conduce a una mayor interacción del usuario con la aplicación.

## <a name="stage-view-vs-task-module"></a>Vista de fase frente al módulo de tareas

|Vista de fase|Módulo de tareas|
|:-----------|:-----------|
|La vista de fase es útil cuando tiene contenido enriquecido para mostrar a los usuarios, como una página, un panel, un archivo, etc. Proporciona características enriquecidas que ayudan a representar el contenido en el lienzo de pantalla completa.|[El módulo de tareas](../task-modules-and-cards/task-modules/task-modules-tabs.md) es especialmente útil para mostrar mensajes que requieren atención del usuario o recopilar información necesaria para pasar al paso siguiente.|
  
## <a name="invoke-stage-view"></a>Invocación de la vista de fase

Puede invocar la vista de fase de las siguientes maneras:

* [Invocación de la vista de fase desde la tarjeta adaptable](#invoke-stage-view-from-adaptive-card)
* [Invocación de la vista de fase a través de un vínculo profundo](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Invocación de la vista de fase desde la tarjeta adaptable

Cuando el usuario escribe una dirección URL en el Teams cliente de escritorio, se invoca el bot y devuelve una [tarjeta adaptable](../task-modules-and-cards/cards/cards-actions.md) con la opción de abrir la dirección URL en una fase. Una vez que se inicia una fase y `tabInfo` se proporciona , puede agregar la capacidad de anclar la fase como una pestaña.  

Las imágenes siguientes muestran una fase abierta desde una tarjeta adaptable:

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
>
> * `invoke` el flujo de trabajo es similar al flujo de trabajo actual `appLinking` .
> * Para mantener la coherencia, se recomienda asignar un nombre `Action.Submit` a .`View`
> * `websiteUrl` es una propiedad necesaria que se va a pasar en el `TabInfo` objeto .

A continuación se muestra el proceso para invocar la vista de fase:

* Cuando el usuario selecciona **Ver**, el bot recibe una `invoke` solicitud. El tipo de solicitud es `composeExtension/queryLink`.
* `invoke` la respuesta del bot contiene una tarjeta adaptable con el tipo `tab/tabInfoAction` en él.
* El bot responde con un `200` código.

> [!NOTE]
> En Teams clientes móviles, la invocación de stage view para las aplicaciones distribuidas a través de la [tienda Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) y no tener una experiencia optimizada para moblie abre el explorador web predeterminado del dispositivo. El explorador abre la dirección URL especificada en el `websiteUrl` parámetro del `TabInfo` objeto .

## <a name="invoke-stage-view-through-deep-link"></a>Invocación de la vista de fase a través de un vínculo profundo

Para invocar la vista de fase a través del vínculo profundo desde la pestaña, debe encapsular la dirección URL del vínculo profundo en la `microsoftTeams.executeDeeplink(url)` API. El vínculo profundo también se puede pasar a través de una `OpenURL` acción en la tarjeta.

### <a name="syntax"></a>Sintaxis

A continuación se muestra la sintaxis de deeplink:

https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}
 
### <a name="examples"></a>Ejemplos

Cuando un usuario escribe una dirección URL, se desplegó en una tarjeta adaptable.

A continuación se muestran los ejemplos de vínculos profundos para invocar la vista de fase:

**Ejemplo 1: Dirección URL con threadId**

Dirección URL no codificada:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={"contentUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes:Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

Dirección URL codificada:

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D

**Ejemplo 2: Dirección URL sin threadId**

Dirección URL no codificada:

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={"contentUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes:Miscellaneous"}

Codificado

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D

> [!NOTE]
> Todos los vínculos profundos deben codificarse antes de pegar la dirección URL. No se admiten direcciones URL no codificadas.
>
> * `name` es opcional en vínculo profundo. Si no se incluye, el nombre de la aplicación lo reemplaza.
> * El vínculo profundo también se puede pasar a través de una `OpenURL` acción.
> * Al iniciar una fase desde un contexto determinado, asegúrese de que la aplicación funciona en ese contexto. Por ejemplo, si la vista de fase se inicia desde una aplicación personal, debes asegurarte de que la aplicación tiene un ámbito personal.

## <a name="tab-information-property"></a>Propiedad de información de tabulación

| Nombre de propiedad | Tipo | Número de caracteres | Descripción |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Cadena | 64 | Esta propiedad es un identificador único para la entidad que muestra la pestaña. Este campo es obligatorio.|
| `name` | Cadena | 128 | Esta propiedad es el nombre para mostrar de la pestaña en la interfaz del canal. Este campo es opcional.|
| `contentUrl` | String | 2048 | Esta propiedad es la dirección URL de https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams. Este campo es obligatorio.|
| `websiteUrl?` | Cadena | 2048 | Esta propiedad es la dirección URL https:// a la que apuntar, si un usuario selecciona ver en un explorador. Este campo es obligatorio.|
| `removeUrl?` | String | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario que se mostrará cuando el usuario elimine la pestaña. Este es un campo opcional.|

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Pestaña en la vista de fase |Microsoft Teams aplicación de ejemplo de pestaña para mostrar la pestaña en la vista de fase.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Vea también

* [Se desplegó el vínculo de extensiones de mensaje](~/messaging-extensions/how-to/link-unfurling.md)
* [pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
