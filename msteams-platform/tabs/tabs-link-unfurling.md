---
title: Expansión del vínculo de la pestaña y vista de fases
author: Rajeshwari-v
description: Cómo deshacer un vínculo, abrir la vista fase y anclar una pestaña con Microsoft Teams aplicación.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: a76bf6f5d97114655893dd80ebf0de81fc242ea4d6b444516565b952aab883fe
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708692"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Expansión del vínculo de la pestaña y vista de fases

> [!NOTE]
> Esta característica solo está disponible en [la versión preliminar del](../resources/dev-preview/developer-preview-intro.md) desarrollador público.

Stage View es un nuevo componente de interfaz de usuario (UI), que te permite representar el contenido que se abre en pantalla completa en Teams y anclado como una pestaña.
 
> [!NOTE]
> Actualmente, Teams los clientes móviles no admiten el desafusado y la vista fase. Los clientes móviles usan el atributo proporcionado por el desarrollador para abrir la página en el `websiteUrl` explorador web del dispositivo.

## <a name="stage-view"></a>Vista fase

Stage View es un componente de interfaz de usuario de pantalla completa que puedes invocar para mostrar el contenido web. El servicio de desamuestración de vínculos existente se actualiza para que se use para convertir direcciones URL en una pestaña mediante una tarjeta adaptable y servicios de chat. Cuando un usuario envía una dirección URL en un chat o canal, la dirección URL se despliega en una tarjeta adaptable. El usuario puede seleccionar **Ver en** la tarjeta y anclar el contenido como una pestaña directamente desde vista fase.

## <a name="advantage-of-stage-view"></a>Ventaja de la vista fase

Stage View ayuda a proporcionar una experiencia más fluida de visualización de contenido en Teams. Los usuarios pueden abrir y ver el contenido proporcionado por la aplicación sin salir del contexto y pueden anclar el contenido al chat o canal para un acceso rápido futuro. Esto lleva a una mayor interacción del usuario con la aplicación.

## <a name="stage-view-vs-task-module"></a>Módulo vista fase frente a tarea

|Vista fase|Módulo de tareas|
|:-----------|:-----------|
|La vista fase es útil cuando tiene contenido enriquecido para mostrar a los usuarios, como una página, un panel, un archivo, y así sucesivamente. Proporciona características enriquecciones que ayudan a representar el contenido en el lienzo de pantalla completa.|[El módulo de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tareas es especialmente útil para mostrar mensajes que requieren atención del usuario o recopilar información necesaria para pasar al paso siguiente.|
  
## <a name="invoke-stage-view"></a>Invocar vista fase

Puede invocar la vista fase de las siguientes maneras:

* [Invocar la vista fase desde la tarjeta adaptable](#invoke-stage-view-from-adaptive-card)
* [Invocar vista de fase a través de un vínculo profundo](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Invocar la vista fase desde la tarjeta adaptable

Cuando el usuario escribe una dirección URL en el cliente de escritorio [](../task-modules-and-cards/cards/cards-actions.md) Teams, el bot se invoca y devuelve una tarjeta adaptable con la opción de abrir la dirección URL en una fase. Después de iniciar una fase y de proporcionarla, puede agregar la capacidad de anclar `tabInfo` la fase como una pestaña.  

Las siguientes imágenes muestran una fase abierta desde una tarjeta adaptable:

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

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

El `invoke` tipo de solicitud debe ser `composeExtension/queryLink` .

> [!NOTE]
> * `invoke` flujo de trabajo es similar al flujo de trabajo `appLinking` actual. 
> * Para mantener la coherencia, se recomienda nombrar `Action.Submit` como `View` .
> * `websiteUrl` es una propiedad necesaria que se debe pasar en el `TabInfo` objeto.

A continuación se muestra el proceso para invocar la vista fase:

* Cuando el usuario selecciona **Ver,** el bot recibe una `invoke` solicitud. El tipo de solicitud es `composeExtension/queryLink` .
* `invoke` respuesta del bot contiene una tarjeta adaptable con tipo `tab/tabInfoAction` en él.
* El bot responde con un `200` código.

> [!NOTE]
> Actualmente, Teams los clientes móviles no admiten la funcionalidad Vista de fase. Cuando un usuario selecciona **Ver** en un cliente móvil, el usuario se toma en el explorador del dispositivo. El explorador abre la dirección URL especificada en el `websiteUrl` parámetro del `TabInfo` objeto.

## <a name="invoke-stage-view-through-deep-link"></a>Invocar vista de fase a través de un vínculo profundo

Para invocar la vista de fase a través del vínculo profundo desde la pestaña, debe ajustar la dirección URL del vínculo profundo en la `microsoftTeams.executeDeeplink(url)` API. El vínculo profundo también se puede pasar a través de una `OpenURL` acción en la tarjeta.

La siguiente imagen muestra una vista de fase invocada a través de un vínculo profundo:

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a>Sintaxis

A continuación se muestra la sintaxis de vínculo profundo:  
 
https://teams.microsoft.com/l/stage/{appId}/0?context={"contentUrl":"[contentUrl]","websiteUrl":"[websiteUrl]","name":"[name]"}

### <a name="examples"></a>Ejemplos

Cuando un usuario escribe una dirección URL, se despliega en una tarjeta adaptable.

A continuación se muestran los ejemplos de vínculos profundos para invocar la vista fase:

**Ejemplo 1**

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name"Contoso"}

**Ejemplo 2**

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={"contentUrl":"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","websiteUrl https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx","name"Contoso"}

> [!NOTE]
> * El `name` vínculo es opcional en profundidad. Si no se incluye, el nombre de la aplicación lo reemplaza.
> * El vínculo profundo también se puede pasar a través de una `OpenURL` acción.
> * Actualmente, Teams los clientes móviles no admiten la funcionalidad Vista de fase. Cuando los usuarios seleccionan un vínculo profundo a una vista de fase, se les traslada al explorador web de su dispositivo. El explorador web abre la dirección URL especificada en el `websiteUrl` parámetro del vínculo profundo.
> * Cuando inicies una fase desde un contexto determinado, asegúrate de que la aplicación funciona en ese contexto. Por ejemplo, si la vista fase se inicia desde una aplicación personal, debes asegurarte de que la aplicación tenga un ámbito personal.

## <a name="tab-information-property"></a>Propiedad tab information

| Nombre de la propiedad | Tipo | Número de caracteres | Descripción |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | Cadena | 64 | Esta propiedad es un identificador único para la entidad que muestra la pestaña. Este campo es obligatorio.|
| `name` | Cadena | 128 | Esta propiedad es el nombre para mostrar de la pestaña en la interfaz de canal. Este campo es opcional.|
| `contentUrl` | Cadena | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario de la entidad que se va a mostrar en el Teams usuario. Este campo es obligatorio.|
| `websiteUrl?` | Cadena | 2048 | Esta propiedad es la https:// url a la que apuntar, si un usuario selecciona ver en un explorador. Este campo es obligatorio.|
| `removeUrl?` | Cadena | 2048 | Esta propiedad es la dirección URL https:// que apunta a la interfaz de usuario que se va a mostrar cuando el usuario elimina la pestaña. Este es un campo opcional.|

## <a name="see-also"></a>Vea también

* [Desafutización de vínculos de extensiones de mensajería](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Crear pestañas de conversación](~/tabs/how-to/conversational-tabs.md)