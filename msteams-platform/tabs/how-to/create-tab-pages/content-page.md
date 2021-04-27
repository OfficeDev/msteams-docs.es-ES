---
title: Creación de una página de contenido
author: laujan
description: cómo crear una página de contenido
keywords: Canal de grupo de pestañas de teams configurable estático
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc6c73d877d9355c5d4a9653e0d8ed669fb347e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020383"
---
# <a name="create-a-content-page-for-your-tab"></a>Crear una página de contenido para la pestaña

Una página de contenido es una página web que se representa en el cliente de Teams. Por lo general, estos son parte de:

* Pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que encuentra el usuario.
* Una pestaña personalizada de canal o grupo: después de que el usuario anclar y configure la pestaña en el contexto adecuado, se muestra la página de contenido.
* Un [módulo de](~/task-modules-and-cards/what-are-task-modules.md) tareas: puede crear una página de contenido e insertarla como vista web dentro de un módulo de tareas. La página se representará dentro del elemento emergente modal.

Este artículo es específico para usar páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplicarían independientemente de cómo se presente la página de contenido al usuario final.

## <a name="tab-content-and-style-guidelines"></a>Directrices de estilo y contenido de tabulación

El objetivo general de la pestaña debe ser proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito evidente. Eso no significa que debas renunciar a un estilo agradable, pero debes centrarte en minimizar el desorden haciendo que el diseño de pestaña sea limpio, intuitivo de navegación y que el contenido sea envolvente. Consulta [Contenido y conversaciones, todo a la vez](~/tabs/design/tabs.md) con pestañas y instrucciones del proceso de aprobación de aplicaciones de Microsoft [Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)

## <a name="integrate-your-code-with-teams"></a>Integrar el código con Teams

Para que la página se muestre en Teams, debe incluir el SDK de cliente [de JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) de Microsoft Teams e incluir una llamada después `microsoftTeams.initialize()` de que se cargue la página. Así se comunican su página y el cliente de Teams:

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="accessing-additional-content"></a>Acceso a contenido adicional

### <a name="using-the-sdk-to-interact-with-teams"></a>Uso del SDK para interactuar con Teams

El [SDK de JavaScript del cliente de Teams](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede resultar útiles al desarrollar la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Teams. Normalmente, se usan para crear vínculos que naveguen al contenido y a la información de la pestaña. Consulte [Crear vínculos profundos al contenido y las características en Microsoft Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia emergente modal que se puede desencadenar desde la pestaña. Normalmente, en una página de contenido no desea navegar por el usuario a través de varias páginas. En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o en cualquier otro momento que necesite presentar al usuario información adicional. Los módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente con tarjetas adaptables. Consulte [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios url usados en las pestañas se incluyen en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema de manifiesto. Sin embargo, tenga en cuenta que la funcionalidad principal de la pestaña existe dentro de Teams y no fuera de Teams.

## <a name="reorder-static-personal-tabs"></a>Reordenar pestañas personales estáticas

A partir de la versión 1.7 del manifiesto, los desarrolladores pueden reorganizar todas las pestañas de su aplicación personal. En concreto, un desarrollador puede mover la pestaña de chat del *bot,* que siempre se sitúa de forma predeterminada en la primera posición, en cualquier lugar del encabezado de pestaña de la aplicación personal. Hemos declarado dos palabras clave entityId de pestaña reservadas, *conversaciones* y *acerca de*.

Si creas un bot con un *ámbito personal,* aparecerá en la primera posición de pestaña de una aplicación personal de forma predeterminada. Si desea moverlo a otra posición, debe agregar un objeto tab estático al manifiesto con la palabra clave reservada, *conversaciones*. La *pestaña de* conversación aparece en la web o en el escritorio en función de dónde agregue la pestaña *de* conversación en la `staticTabs` matriz. 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a>Mostrar un indicador de carga nativo

A partir del esquema de manifiesto [v1.7,](../../../resources/schema/manifest-schema.md)puede proporcionar un indicador de carga nativo donde se cargue el contenido web en Teams, por [ejemplo,](#integrate-your-code-with-teams)página de contenido de [pestaña,](configuration-page.md)página de [configuración,](removal-page.md) página de eliminación y módulos de tareas en [pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md). [](../../../resources/schema/manifest-schema.md#showloadingindicator)

> [!NOTE]
> 1. El comportamiento de los clientes móviles no se puede configurar a través de esta propiedad de manifiesto. Los clientes móviles muestran un indicador de carga nativo de forma predeterminada en las páginas de contenido y los módulos de tareas basados en iframe. Este indicador en el móvil se muestra cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.
> 2. Si indicas en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de pestañas y todos los módulos de tareas basados en iframe deben seguir el protocolo obligatorio, a  `"showLoadingIndicator : true`  continuación:


1. Para mostrar el indicador de carga, agregue `"showLoadingIndicator": true` al manifiesto. 
2. Recuerde llamar `microsoftTeams.initialize();` a .
3. **Opcional**. Si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **Obligatorio**. Por último, llama `microsoftTeams.appInitialization.notifySuccess()` para notificar a Teams que la aplicación se ha cargado correctamente. Teams ocultará el indicador de carga si procede. Si  `notifySuccess`  no se llama en 30 segundos, se supone que la aplicación ha pasado el tiempo de espera y aparecerá una pantalla de error con una opción de reintento.
5. Si la aplicación no se carga, puede llamar para que `microsoftTeams.appInitialization.notifyFailure(reason);` Teams sepa que hubo un error. A continuación, se mostrará al usuario una pantalla de error:

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
