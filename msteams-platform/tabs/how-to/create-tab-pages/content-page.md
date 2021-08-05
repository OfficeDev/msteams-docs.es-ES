---
title: Creación de una página de contenido
author: surbhigupta
description: cómo crear una página de contenido
keywords: Canal de grupo de pestañas de teams configurable estático
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6d1a0f6dd3593209f94966140ea94b33ac0c8d10
ms.sourcegitcommit: ec79bbbc3a8daa1ad96de809fc6d17367e8f0c6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2021
ms.locfileid: "53726876"
---
# <a name="create-a-content-page-for-your-tab"></a>Crear una página de contenido para la pestaña

Una página de contenido es una página web que se representa en el Teams cliente. Estos son parte de:

* Pestaña personalizada de ámbito personal: en este caso, la página de contenido es la primera página que encuentra el usuario.
* Pestaña personalizada de canal o grupo: la página de contenido se muestra después de que el usuario anclar y configure la pestaña en el contexto adecuado.
* Un [módulo de](~/task-modules-and-cards/what-are-task-modules.md)tareas: puede crear una página de contenido e insertarla como vista web dentro de un módulo de tareas. La página se representa dentro de la ventana emergente modal.

Este artículo es específico para usar páginas de contenido como pestañas; sin embargo, la mayoría de las instrucciones aquí se aplican independientemente de cómo se presente la página de contenido al usuario.

## <a name="tab-content-and-design-guidelines"></a>Directrices de diseño y contenido de tabulación

El objetivo general de la pestaña es proporcionar acceso al contenido significativo y atractivo que tiene un valor práctico y un propósito evidente. Debes centrarte en hacer que el diseño de la pestaña sea limpio, la navegación intuitiva y el contenido envolvente.

Para obtener más información, vea [directrices de diseño de](~/tabs/design/tabs.md) [pestañas y Microsoft Teams directrices de validación del almacén.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>Integre el código con Teams

Para que la página se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página. 

El siguiente código proporciona un ejemplo de cómo se comunican la página y Teams cliente:

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

Puede obtener acceso a contenido adicional mediante el SDK para interactuar con Teams, crear vínculos profundos, usar módulos de tareas y comprobar si los dominios de dirección URL se incluyen en la `validDomains` matriz.

### <a name="use-the-sdk-to-interact-with-teams"></a>Use el SDK para interactuar con Teams

El [SDK Teams cliente de JavaScript](~/tabs/how-to/using-teams-client-sdk.md) proporciona muchas funciones adicionales que puede encontrar útiles al desarrollar la página de contenido.

### <a name="deep-links"></a>Vínculos profundos

Puede crear vínculos profundos a entidades en Teams. Se usan para crear vínculos que naveguen al contenido y a la información de la pestaña. Para obtener más información, vea [crear vínculos profundos al contenido y las características en Teams](~/concepts/build-and-test/deep-links.md).

### <a name="task-modules"></a>Módulos de tareas

Un módulo de tareas es una experiencia emergente modal que puede desencadenar desde la pestaña. En una página de contenido, puede usar módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o presentar al usuario información adicional. Los módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente con tarjetas adaptables. Para obtener más información, vea [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios url usados en las pestañas se incluyan en la `validDomains` matriz del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, [vea validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema de manifiesto.

> [!NOTE]
> La funcionalidad principal de la pestaña existe en Teams y no fuera de Teams.

## <a name="show-a-native-loading-indicator"></a>Mostrar un indicador de carga nativo

A partir [del esquema de manifiesto v1.7,](../../../resources/schema/manifest-schema.md)puede proporcionar un indicador de carga [nativo](../../../resources/schema/manifest-schema.md#showloadingindicator). Por ejemplo, [página de contenido de tabulación,](#integrate-your-code-with-teams)página de [configuración,](configuration-page.md) [página de](removal-page.md)eliminación y [módulos de tareas en pestañas](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).

> [!NOTE]
> * El comportamiento de los clientes móviles no se puede configurar a través de la propiedad del indicador de carga nativo. Los clientes móviles muestran este indicador de forma predeterminada en las páginas de contenido y los módulos de tareas basados en iframe. Este indicador en el móvil se muestra cuando se realiza una solicitud para capturar contenido y se descarta en cuanto se completa la solicitud.

Si indicas en el manifiesto de la aplicación, todas las páginas de configuración, contenido y eliminación de pestañas y todos los módulos de tareas basados en iframe deben `showLoadingIndicator : true`  seguir estos pasos:

**Para mostrar el indicador de carga**

1. Agregue `"showLoadingIndicator": true` al manifiesto.
1. Llamar a `microsoftTeams.initialize();`.
1. Como paso **obligatorio,** llama para `microsoftTeams.appInitialization.notifySuccess()` notificar a Teams que la aplicación se ha cargado correctamente. Teams oculta el indicador de carga, si procede. Si `notifySuccess`  no se llama en 30 segundos, se supone que la aplicación ha pasado el tiempo de espera y aparece una pantalla de error con una opción de reintento.
1. **Opcionalmente,** si está listo para imprimir en la pantalla y desea cargar de forma diferida el resto del contenido de la aplicación, puede ocultar manualmente el indicador de carga llamando a `microsoftTeams.appInitialization.notifyAppLoaded();` .
1. Si la aplicación no se carga, puede llamar para Teams `microsoftTeams.appInitialization.notifyFailure(reason);` que se produjo un error. Se muestra una pantalla de error al usuario. El código siguiente proporciona un ejemplo de motivos de error de la aplicación:

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a>Consulte también

* [Teams pestañas](~/tabs/what-are-tabs.md)
* [Crear una pestaña personal](~/tabs/how-to/create-personal-tab.md)
* [Crear una pestaña de canal o grupo](~/tabs/how-to/create-channel-group-tab.md)
* [Creación de una página de contenido](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Creación de una página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md)
