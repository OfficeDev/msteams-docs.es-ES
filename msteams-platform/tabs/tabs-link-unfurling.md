---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Obtenga información sobre la vista de fase, un componente de interfaz de usuario de pantalla completa invocado para exponer el contenido web. La desplegamiento de vínculos se usa para convertir direcciones URL en una pestaña mediante tarjetas adaptables.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 41fce323ff65dd264e8dca71120ea126ddfcf16f
ms.sourcegitcommit: 93c2fcd78a2fbb4550d180d295d98d1b3944ca67
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2022
ms.locfileid: "68484923"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Expansión del vínculo de la pestaña y vista de fases

La vista de fase es un nuevo componente de interfaz de usuario. Permite representar el contenido que se abre en pantalla completa en Teams y se ancla como una pestaña.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="stage-view"></a>Vista de extendida

Vista extendida es un componente de interfaz de usuario de pantalla completa que puede invocar para mostrar el contenido web. El servicio de desplegamiento de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat. Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se desplega en una tarjeta adaptable. El usuario puede seleccionar **Ver** en la tarjeta y anclar el contenido como una pestaña directamente desde la Vista extendida.

## <a name="advantage-of-stage-view"></a>Ventaja de vista extendida

Stage View helps provide a more seamless experience of viewing content in Teams. Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access leading to a higher user engagement with your app.

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

* When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
* `invoke` respuesta del bot contiene una tarjeta adaptable con el tipo `tab/tabInfoAction` en ella.
* El bot responde con un código de `200`.

> [!NOTE]
>
> En los clientes móviles de Teams, al invocar la vista de fase para las aplicaciones distribuidas a través de la [tienda de Teams](~/concepts/deploy-and-publish/apps-publish-overview.md) y no tener una experiencia optimizada para dispositivos móviles, se abre el explorador web predeterminado del dispositivo. `websiteUrl` El explorador abre la dirección URL especificada en el parámetro del objeto`TabInfo`.

## <a name="invoke-stage-view-through-deep-link"></a>Invocación de la Vista extendida a través de un vínculo profundo

Para invocar la Vista extendida a través de un vínculo profundo desde la pestaña, debe encapsular la dirección URL del vínculo profundo en la API de `app.openLink(url)`. El vínculo profundo también se puede pasar a través de una acción `OpenURL` en la tarjeta.

### <a name="syntax"></a>Sintaxis

A continuación se muestra la sintaxis de vínculo profundo:

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

### <a name="examples"></a>Ejemplos

Cuando un usuario escribe una dirección URL, se desplegó en una tarjeta adaptable.

Estos son los ejemplos de vínculos profundos para invocar la Vista extendida:

**Ejemplo 1: dirección URL con threadId**

Dirección URL sin codificar:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

Dirección URL codificada:

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

**Ejemplo 2: Dirección URL sin threadId**

Dirección URL sin codificar:

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

Codificado

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

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
| `contentUrl` | Cadena | 2048 | This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas. This is a required field.|
| `websiteUrl?` | Cadena | 2048 | This property is the https:// URL to point at, if a user selects to view in a browser. This is a required field.|
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
