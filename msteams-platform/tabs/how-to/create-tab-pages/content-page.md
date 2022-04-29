---
title: Creación de una página de contenido
author: surbhigupta
description: cómo crear una página de contenido
keywords: pestañas de equipos, canal de grupo configurable estático
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 68ce03e9b1ef303bd66043baed39baf954fb1d0f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111433"
---
# <a name="create-a-content-page-for-your-tab"></a>Creación de una página de contenido para una pestaña

Una página de contenido es una página web que se representa en el cliente de Teams. Forman parte de:

* Una pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que se encuentra el usuario.
* Una pestaña personalizada de canal o grupo: la página de contenido se muestra después de que el usuario ancle y configure la pestaña en el contexto adecuado.
* Un [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md): puede crear una página de contenido e insertarla como una vista web dentro de un módulo de tareas. La página se representa dentro del elemento emergente modal.

Este artículo se centra en el uso de páginas de contenido como pestañas. Sin embargo, la mayoría de las instrucciones aquí expuestas se aplican independientemente de cómo se presente la página de contenido al usuario.

## <a name="tab-content-and-design-guidelines"></a>Instrucciones de diseño y contenido de pestañas

El objetivo general de la pestaña es proporcionar acceso a contenido significativo y atractivo que tenga un valor práctico y un propósito que sea evidente. Debe centrarse en hacer que el diseño de la pestaña sea claro, intuitivo a la hora de navegar y con contenido envolvente.

Para obtener más información, vea [instrucciones de diseño de pestañas](~/tabs/design/tabs.md) y [directrices de validación de Microsoft Teams store](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Integrar el código con Teams

Para que la página se muestre en Teams, debe incluir el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página.

El código siguiente proporciona un ejemplo de cómo se comunican la página y el cliente de Teams:

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.10.0/js/MicrosoftTeams.min.js'></script>
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

## <a name="access-additional-content"></a>Acceso a contenido adicional

Puede acceder a contenido adicional mediante el SDK para interactuar con Teams, crear vínculos profundos, usar módulos de tareas y comprobar si se incluyen dominios de dirección URL en la matriz de `validDomains`.

### <a name="use-the-sdk-to-interact-with-teams"></a>Usar el SDK para interactuar con Teams

El [SDK de JavaScript del cliente de Teams](~/tabs/how-to/using-teams-client-sdk.md) proporciona varias funciones adicionales que pueden ser de utilidad al desarrollar la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Teams. Se usan para crear vínculos que navegan hasta el contenido y la información dentro de la pestaña. Para obtener más información, consulte [Crear vínculos profundos al contenido y las características en Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia emergente modal que puede desencadenarse desde la pestaña. En una página de contenido, se pueden usar módulos de tareas para presentar formularios y, así, recopilar información adicional, mostrar los detalles de un elemento en una lista o presentar al usuario información adicional. Los propios módulos de tareas pueden ser páginas de contenido adicionales o pueden crearse por completo mediante Tarjetas adaptables. Para obtener más información, consulte [Usar módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios de dirección URL que se usan en las pestañas están incluidos en la matriz `validDomains` del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, consulte [validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia de esquema del manifiesto.

> [!NOTE]
> La funcionalidad principal de la pestaña se da dentro de Teams y no fuera.

## <a name="show-a-native-loading-indicator"></a>Mostrar un indicador de carga nativo

A partir del [esquema de manifiesto v1.7](../../../resources/schema/manifest-schema.md), puede proporcionar un [indicador de carga nativo](../../../resources/schema/manifest-schema.md#showloadingindicator). Por ejemplo, [página de contenido de pestaña](#integrate-your-code-with-teams), [página de configuración](configuration-page.md), [página de eliminación](removal-page.md) y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * El comportamiento en los clientes móviles no se puede configurar a través de la propiedad del indicador de carga nativa. Los clientes móviles muestran este indicador de forma predeterminada en las páginas de contenido y en los módulos de tareas basados en iframe. Este indicador en dispositivos móviles aparece cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.

Si indica `showLoadingIndicator : true`  en el manifiesto de la aplicación, toda la configuración de pestañas, el contenido, las páginas de eliminación y los módulos de tareas basados en iframe deben seguir los siguientes pasos:

Para mostrar el indicador de carga:

1. Agregar `"showLoadingIndicator": true` al manifiesto.
1. Llamar a `microsoftTeams.initialize();`.
1. Como paso **obligatorio**, llame a `microsoftTeams.appInitialization.notifySuccess()` para notificarle a Teams que la aplicación se ha cargado correctamente. A continuación, Teams ocultará el indicador de carga, si procede. Si no se llama a `notifySuccess`  en 30 segundos, se entiende que la aplicación ha agotado el tiempo de espera y aparecerá una pantalla de error con una opción para reintentar.
1. De forma **opcional**, si está listo para imprimir en pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();`.
1. Si la aplicación no se carga, puede llamar a `microsoftTeams.appInitialization.notifyFailure(reason);` para que Teams sepa que se ha producido un error. Se muestra al usuario una pantalla de error. El código siguiente proporciona un ejemplo con motivos de error de la aplicación:

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="see-also"></a>Consulte también

* [Pestañas de Teams](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Expansión del vínculo de pestañas y la Vista de fases](~/tabs/tabs-link-unfurling.md)
* [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [DevTools para pestañas de Microsoft Teams](~/tabs/how-to/developer-tools.md)
