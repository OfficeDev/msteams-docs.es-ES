---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Obtenga información sobre cómo desanclar un vínculo, abrir la Vista extendida y anclar una pestaña con la aplicación Microsoft Teams. Obtenga información sobre la Vista extendida y cómo invocarla utilizando tarjeta adaptable mediante ejemplos de código.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: d752e55777a07834663f564632bd6a9ff220fdaf
ms.sourcegitcommit: 6f1bd36b1071e256bdc14e6ccb31dfdda9ca6d6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2022
ms.locfileid: "66048986"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Expansión del vínculo de la pestaña y vista de fases

La vista de fase es un nuevo componente de interfaz de usuario. Permite representar el contenido que se abre en pantalla completa en Teams y se ancla como una pestaña.

## <a name="stage-view"></a>Vista de extendida

Vista extendida es un componente de interfaz de usuario de pantalla completa que puede invocar para mostrar el contenido web. El servicio de desplegamiento de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat. Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se desplega en una tarjeta adaptable. El usuario puede seleccionar **Ver** en la tarjeta y anclar el contenido como una pestaña directamente desde la Vista extendida.

## <a name="advantage-of-stage-view"></a>Ventaja de vista extendida

Vista extendida ayuda a proporcionar una experiencia más fluida de visualización de contenido en Teams. Los usuarios pueden abrir y ver el contenido proporcionado por la aplicación sin salir del contexto y pueden anclar el contenido al chat o canal para un acceso rápido futuro, lo que conduce a una mayor interacción del usuario con la aplicación.

## <a name="stage-view-vs-task-module"></a>Vista extendida frente a módulo de tareas

|Vista de extendida|Módulo de tareas|
|:-----------|:-----------|
|La vista extendida es útil cuando usted tiene contenido enriquecido para mostrar a los usuarios, como es una página, un panel, un archivo, etc. Proporciona características enriquecidas que ayudan a representar el contenido en el lienzo de pantalla completa.|[Módulo de tareas](../task-modules-and-cards/task-modules/task-modules-tabs.md) es especialmente útil para mostrar mensajes que requieren la atención del usuario o recopilar la información necesaria para pasar al paso siguiente.|
  
## <a name="invoke-stage-view"></a>Invocar Vista extendida

Puede invocar la vista extendida de las maneras siguientes:

* [Invocar Vista extendida desde tarjeta adaptable](#invoke-stage-view-from-adaptive-card)
* [invocar Vista extendida a través de vínculo profundo](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Invocar Vista extendida desde tarjeta adaptable

Cuando el usuario escribe una dirección URL en el cliente de escritorio de Teams, el bot se invoca y devuelve una [Tarjeta adaptable](../task-modules-and-cards/cards/cards-actions.md) con la opción de abrir la dirección URL en una fase. Una vez que se inicia una fase y se proporciona el `tabInfo`, usted puede agregar la capacidad de anclar la fase como una pestaña.  

Las siguientes imágenes muestran una fase abierta desde una tarjeta adaptable:

[![abrir una fase desde tarjeta adaptable](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![abrir una fase](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox)

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

El tipo de solicitud `invoke` debe ser `composeExtension/queryLink`.

> [!NOTE]
>
> * `invoke` El flujo de trabajo es similar al flujo de trabajo actual `appLinking`.
> * Para mantener la coherencia, se recomienda asignar un nombre a `Action.Submit` como `View`.
> * `websiteUrl` es una propiedad necesaria que se debe pasar en el objeto `TabInfo`.

A continuación se muestra el proceso para invocar la vista extendida:

* Cuando el usuario selecciona **Ver**, el bot recibe una solicitud de `invoke`. El tipo de solicitud es `composeExtension/queryLink`.
* `invoke` respuesta del bot contiene una tarjeta adaptable con el tipo `tab/tabInfoAction` en ella.
* El bot responde con un código de `200`.

> [!NOTE]
> En Teams clientes móviles, la invocación de stage view para las aplicaciones distribuidas a través de la [aplicación de Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md) y el no tener una experiencia optimizada para moblie abre el explorador web predeterminado del dispositivo. `websiteUrl` El explorador abre la dirección URL especificada en el parámetro del objeto`TabInfo`.

## <a name="invoke-stage-view-through-deep-link"></a>Invocación de la Vista extendida a través de un vínculo profundo

Para invocar la Vista extendida a través de un vínculo profundo desde la pestaña, debe encapsular la dirección URL del vínculo profundo en la API de `microsoftTeams.executeDeeplink(url)`. El vínculo profundo también se puede pasar a través de una acción `OpenURL` en la tarjeta.

### <a name="syntax"></a>Sintaxis

A continuación se muestra la sintaxis de vínculo profundo:

<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}

### <a name="examples"></a>Ejemplos

Cuando un usuario escribe una dirección URL, se desplegó en una tarjeta adaptable.

Estos son los ejemplos de vínculos profundos para invocar la Vista extendida:

**Ejemplo 1: dirección URL con threadId**

Dirección URL sin codificar:

<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}

Dirección URL codificada:

<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>

**Ejemplo 2: Dirección URL sin threadId**

Dirección URL sin codificar:

<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}

Codificado

<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>

> [!NOTE]
> Todos los vínculos profundos deben codificarse antes de pegar la dirección URL. No se admiten direcciones URL sin codificar.
>
> * El `name` es opcional en el vínculo profundo. Si no se incluye, el nombre de la aplicación lo reemplaza.
> * El vínculo profundo también se puede pasar a través de una acción `OpenURL`.
> * Al iniciar una fase desde un contexto determinado, cerciórese de que la aplicación funciona en ese contexto. Por ejemplo, si la Vista extendida se inicia desde una aplicación personal, debe cerciorarse de que la aplicación tiene un ámbito personal.

## <a name="tab-information-property"></a>Propiedad de información de pestaña

| Nombre de propiedad | Tipo | Número de caracteres | Descripción |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Cadena | 64 | Esta propiedad es un identificador único para la entidad que muestra la pestaña. Este campo es obligatorio.|
| `name` | Cadena | 128 | Esta propiedad es el nombre para mostrar de la pestaña en la interfaz del canal. Este campo es opcional.|
| `contentUrl` | Cadena | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario de la entidad que se mostrará en el lienzo de Teams. Este campo es obligatorio.|
| `websiteUrl?` | Cadena | 2048 | Esta propiedad es la dirección URL de https:// a la que apuntar si un usuario selecciona ver en un explorador. Este campo es obligatorio.|
| `removeUrl?` | Cadena | 2048 | Esta propiedad es la dirección URL de https:// que apunta a la interfaz de usuario que se mostrará cuando el usuario elimine la pestaña. Se trata de un campo opcional.|

## <a name="code-sample"></a>Ejemplo de código

| Ejemplo de nombre | Descripción | C# |Node.js|
|-------------|-------------|------|----|
|Pestaña en la vista extendida |Aplicación de ejemplo de pestaña de Microsoft Teams para mostrar la pestaña en la vista extendida.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Consulte también

* [Vínculo extensiones de mensaje desenlazándose](~/messaging-extensions/how-to/link-unfurling.md)
* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de grupo o canal personalizado](~/tabs/how-to/create-channel-group-tab.md)
