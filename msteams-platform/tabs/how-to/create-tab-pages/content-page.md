---
title: Creación de una página de contenido
author: laujan
description: Cómo crear una página de contenido
keywords: canal de grupo de pestañas de Teams configurable estático
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 91a7d643d3a631610989e31eae14265cd725dbd0
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818909"
---
# <a name="create-a-content-page-for-your-tab"></a>Crear una página de contenido para la pestaña

Una página de contenido es una página web que se representa dentro del cliente de Teams. Normalmente son parte de:

* Una ficha personalizada con ámbito personal en esta instancia la página de contenido es la primera página que encuentra el usuario.
* Una pestaña personalizada de canal o Grupo: después de que el usuario PIN y configure la pestaña en el contexto adecuado, se muestra la página de contenido.
* Un [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md) : puede crear una página de contenido e incrustarla como WebView dentro de un módulo de tareas. La página se representará dentro del elemento emergente modal.

Este artículo es específico para usar páginas de contenido como fichas; sin embargo, la mayoría de las instrucciones aquí aplicadas se aplican independientemente de cómo se presente la página de contenido al usuario final.

## <a name="tab-content-and-style-guidelines"></a>Contenido de la pestaña y directrices de estilo

El objetivo general de su pestaña debe ser proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito claro. Esto no significa que deba prepararse con un estilo agradable, pero debe centrarse en minimizar la confusión haciendo que el diseño de pestaña sea limpio, navegación intuitiva y contenido envolvente. Ver [contenido y conversaciones, todos a la vez mediante pestañas](~/tabs/design/tabs.md) y [Guía del proceso de aprobación de aplicaciones de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)

## <a name="integrate-your-code-with-teams"></a>Integrar el código con Microsoft Teams

Para que la página se muestre en Microsoft Teams, debe incluir el [SDK del cliente de JavaScript para Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página. Así es como se comunican la página y el cliente de Microsoft Teams:

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

## <a name="accessing-additional-content"></a>Obtener acceso a contenido adicional

### <a name="using-the-sdk-to-interact-with-teams"></a>Uso del SDK para interactuar con Microsoft Teams

El [SDK de JavaScript del cliente de Microsoft Teams](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede que le resulten útiles mientras se programa la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Microsoft Teams. Normalmente, estos se usan para crear vínculos que naveguen a contenido e información dentro de la pestaña. Consulte [crear vínculos detallados para el contenido y las características de Microsoft Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia modal de tipo popup que se puede desencadenar desde la ficha. Por lo general, en una página de contenido no desea desplazarse al usuario a través de varias páginas. En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o cualquier otro momento en que necesite presentar al usuario información adicional. Los propios módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente mediante tarjetas adaptables. Consulte [uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios de dirección URL usados en las pestañas se incluyen en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema del manifiesto. Sin embargo, tenga en cuenta que la funcionalidad principal de su pestaña existe en Microsoft Teams y no fuera de Microsoft Teams.

## <a name="show-a-native-loading-indicator"></a>Mostrar un indicador de carga nativo

Comenzando con [el esquema de manifiesto v 1.7](../../../resources/schema/manifest-schema.md), puede proporcionar un [indicador de carga nativo](../../../resources/schema/manifest-schema.md#showloadingindicator) siempre que el contenido web se cargue en Microsoft Teams, por ejemplo, [Página de contenido](#integrate-your-code-with-teams)de la ficha, página de [configuración](configuration-page.md), [Página de eliminación](removal-page.md) y [módulos de tareas en las pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
> Si indica  `"showLoadingIndicator : true`  en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de la ficha y todos los módulos de tareas basados en iframe deben seguir el protocolo obligatorio, a continuación:

1. Para mostrar el indicador de carga, agregue `"showLoadingIndicator": true` al manifiesto. 
2. Recuerde que debe llamar a `microsoftTeams.initialize();` .
3. **Opcional**. Si está listo para imprimir en la pantalla y desea cargar perezosos el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga mediante una llamada a `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **Obligatorio**. Por último, llame `microsoftTeams.appInitialization.notifySuccess()` a para notificar a los equipos que la aplicación se ha cargado correctamente. Teams ocultará el indicador de carga si procede. Si  `notifySuccess`  no se llama a en el plazo de 30 segundos, se asumirá que la aplicación ha agotado el tiempo de espera y aparecerá una pantalla de error con una opción de reintento.
5. Si la aplicación no se puede cargar, puede llamar `microsoftTeams.appInitialization.notifyFailure(reason);` para informar a Microsoft Teams de que se ha producido un error. A continuación, se mostrará una pantalla de error al usuario:

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
