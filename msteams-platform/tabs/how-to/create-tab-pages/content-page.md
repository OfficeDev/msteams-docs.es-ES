---
title: Creación de una página de contenido
author: surbhigupta
description: Obtenga información sobre la página web dentro del cliente de Teams y forma parte de la pestaña personalizada personal, de canal o de grupo. Crear página de contenido e insertarla como vista web dentro del módulo de tareas.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 34e106bfa0fdfa6b881d1a2fcd5685c022ac5d87
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450376"
---
# <a name="create-a-content-page"></a>Creación de una página de contenido

Una página de contenido es una página web que se representa dentro del cliente de Teams, que forma parte de:

* Una pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que se encuentra el usuario.
* Una pestaña personalizada de canal o grupo: la página de contenido se muestra después de que el usuario ancle y configure la pestaña en el contexto adecuado.
* Un [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md): puede crear una página de contenido e insertarla como una vista web dentro de un módulo de tareas. La página se representa dentro del elemento emergente modal.

Este artículo es específico del uso de páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplican independientemente de cómo se presente la página de contenido al usuario.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tab-content-and-design-guidelines"></a>Instrucciones de diseño y contenido de pestañas

El objetivo general de la pestaña es proporcionar acceso al contenido significativo y atractivo que tiene un valor práctico y un propósito evidente.

Debe centrarse en hacer que el diseño de la pestaña sea limpio, intuitivo de navegación y envolvente de contenido. Para obtener más información, vea [Directrices de diseño de pestañas](~/tabs/design/tabs.md) y Directrices de validación de [almacén de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).

## <a name="integrate-your-code-with-teams"></a>Integrar el código con Teams

Para que la página se muestre en Teams, debe incluir el [SDK de cliente de JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada a `app.initialize()` después de que se cargue la página.

> [!NOTE]
> Los cambios de contenido o interfaz de usuario tardan entre 24 y 48 horas en reflejarse en la aplicación de pestaña debido a la caché.

El código siguiente proporciona un ejemplo de cómo se comunican la página y el cliente de Teams:

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js'></script>
...
<body>
...
    <script type="module">
        import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
        await app.initialize();
    </script>
...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

## <a name="access-additional-content"></a>Acceso a contenido adicional

Puede acceder a contenido adicional mediante el SDK para interactuar con Teams, crear vínculos profundos, usar módulos de tareas y comprobar si se incluyen dominios de dirección URL en la matriz de `validDomains`.

### <a name="use-the-sdk-to-interact-with-teams"></a>Usar el SDK para interactuar con Teams

El [SDK de JavaScript del cliente de Teams](~/tabs/how-to/using-teams-client-sdk.md) proporciona varias funciones adicionales que pueden ser de utilidad al desarrollar la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Teams. Se usan para crear vínculos que naveguen hasta el contenido y la información de la pestaña. Para obtener más información, consulte [Creación de vínculos profundos al contenido y las características en Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia emergente modal que puede desencadenar desde la pestaña. En una página de contenido, use módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento de una lista o presentar al usuario información adicional. Los propios módulos de tareas pueden ser páginas de contenido adicionales o pueden crearse por completo mediante Tarjetas adaptables. Para obtener más información, consulte [Usar módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios de dirección URL que se usan en las pestañas están incluidos en la matriz `validDomains` del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, consulte [validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia de esquema del manifiesto.

> [!NOTE]
> La funcionalidad principal de la pestaña se da dentro de Teams y no fuera.

## <a name="show-a-native-loading-indicator"></a>Mostrar un indicador de carga nativo

A partir del [esquema de manifiesto v1.7](../../../resources/schema/manifest-schema.md), puede proporcionar un [indicador de carga nativo](../../../resources/schema/manifest-schema.md#showloadingindicator). Por ejemplo, [página de contenido de pestaña](#integrate-your-code-with-teams), [página de configuración](configuration-page.md), [página de eliminación](removal-page.md) y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
>
> * El comportamiento en los clientes móviles no se puede configurar a través de la propiedad de indicador de carga nativa. Los clientes móviles muestran este indicador de forma predeterminada en las páginas de contenido y en los módulos de tareas basados en iframe. Este indicador en dispositivos móviles aparece cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.

Si indica `showLoadingIndicator : true`  en el manifiesto de la aplicación, toda la configuración de pestañas, el contenido, las páginas de eliminación y los módulos de tareas basados en iframe deben seguir los siguientes pasos:

Para mostrar el indicador de carga:

1. Agregar `"showLoadingIndicator": true` al manifiesto.
1. Llamar a `app.initialize();`.
1. Como paso **obligatorio**, llame a `app.notifySuccess()` para notificarle a Teams que la aplicación se ha cargado correctamente. A continuación, Teams oculta el indicador de carga, si procede. Si `notifySuccess`  no se llama a en un plazo de 30 segundos, Teams supone que la aplicación agotó el tiempo de espera y muestra una pantalla de error con una opción de reintento.
1. **Opcionalmente**, si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `app.notifyAppLoaded();`.
1. Si la aplicación no se carga, puede llamar `app.notifyFailure({reason: app.FailedReason.Timeout, message: "failure message"});` a para informar a Teams sobre el error y, opcionalmente, proporcionar un mensaje de error. Se muestra al usuario una pantalla de error. En el código siguiente se muestra la enumeración que define las posibles razones que puede indicar para que la aplicación no se cargue:

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
