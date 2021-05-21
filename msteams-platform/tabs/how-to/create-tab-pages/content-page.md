---
title: Creación de una página de contenido
author: laujan
description: cómo crear una página de contenido
keywords: Canal de grupo de pestañas de teams configurable estático
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566680"
---
# <a name="create-a-content-page-for-your-tab"></a>Crear una página de contenido para la pestaña

Una página de contenido es una página web que se representa en el Teams cliente. Por lo general, estos son parte de:

* Pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que encuentra el usuario.
* Una pestaña personalizada de canal o grupo: después de que el usuario anclar y configure la pestaña en el contexto adecuado, se muestra la página de contenido.
* Un [módulo de](~/task-modules-and-cards/what-are-task-modules.md)tareas: puede crear una página de contenido e insertarla como vista web dentro de un módulo de tareas. La página se representará dentro del elemento emergente modal.

Este artículo es específico para usar páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplicarían independientemente de cómo se presente la página de contenido al usuario final.

## <a name="tab-content-and-design-guidelines"></a>Directrices de diseño y contenido de tabulación

El objetivo general de la pestaña debe ser proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito evidente. Eso no significa que debas renunciar a un estilo agradable, pero debes centrarte en minimizar el desorden haciendo que el diseño de pestaña sea limpio, intuitivo de navegación y que el contenido sea envolvente.

Para obtener más información, consulte las [directrices de diseño de pestañas](~/tabs/design/tabs.md) [y Microsoft Teams de validación del almacén](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>Integre el código con Teams

Para que la página se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página. Así se comunican su página y Teams cliente:

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

El [SDK Teams cliente de JavaScript](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede resultar útiles al desarrollar la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Teams. Normalmente, se usan para crear vínculos que naveguen al contenido y a la información de la pestaña. Para obtener más información, vea [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia emergente modal que se puede desencadenar desde la pestaña. Normalmente, en una página de contenido no desea navegar por el usuario a través de varias páginas. En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o en cualquier otro momento que necesite presentar al usuario información adicional. Los módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente con tarjetas adaptables. Consulte [Uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios url usados en las pestañas se incluyen en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema de manifiesto. Sin embargo, tenga en cuenta que la funcionalidad principal de la pestaña existe en Teams y no fuera de Teams.

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

A partir [del esquema de manifiesto v1.7,](../../../resources/schema/manifest-schema.md)puede proporcionar un indicador de carga nativo donde se cargue el contenido web en Teams. [](../../../resources/schema/manifest-schema.md#showloadingindicator) Por ejemplo, [página de contenido de tabulación,](#integrate-your-code-with-teams)página de [configuración,](configuration-page.md) [página de](removal-page.md)eliminación y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
> * El comportamiento de los clientes móviles no se puede configurar a través de esta propiedad de manifiesto. Los clientes móviles muestran un indicador de carga nativo de forma predeterminada en las páginas de contenido y los módulos de tareas basados en iframe. Este indicador en el móvil se muestra cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.
> * Si indicas en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de pestañas y todos los módulos de tareas basados en iframe deben seguir el protocolo obligatorio, a  `"showLoadingIndicator : true`  continuación:

**Para mostrar el indicador de carga**

* Agregue `"showLoadingIndicator": true` al manifiesto. 
* Recuerde llamar `microsoftTeams.initialize();` a .
* **Opcional:** si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();`
* **Obligatorio:** por último, llama para `microsoftTeams.appInitialization.notifySuccess()` notificar Teams que la aplicación se ha cargado correctamente. Teams ocultará el indicador de carga si procede. Si  `notifySuccess`  no se llama en 30 segundos, se supone que la aplicación ha pasado el tiempo de espera y aparecerá una pantalla de error con una opción de reintento.
* Si la aplicación no se carga, puede llamar para Teams `microsoftTeams.appInitialization.notifyFailure(reason);` que se produjo un error. A continuación, se mostrará al usuario una pantalla de error:

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
