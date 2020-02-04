---
title: Crear una página de contenido
author: laujan
description: ''
keywords: canal de grupo de pestañas de Teams configurable estático
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675961"
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

Un módulo de tareas es una experiencia modal de tipo popup que puede desencadenar desde su pestaña. normalmente, en una página de contenido no desea explorar al usuario a través de varias páginas. En su lugar, usará módulos de tareas para presentar formularios para recopilar información adicional, mostrar los detalles de un elemento en una lista o cualquier otro momento en que necesite presentar al usuario información adicional. Los propios módulos de tareas pueden ser páginas de contenido adicionales o crearse completamente mediante tarjetas adaptables. Consulte [uso de módulos de tareas en pestañas](~/task-modules-and-cards/task-modules/task-modules-tabs.md) para obtener información completa.

### <a name="valid-domains"></a>Dominios válidos

Asegúrese de que todos los dominios de dirección URL usados en las pestañas `validDomains` se incluyen en la matriz del [manifiesto](~/concepts/build-and-test/apps-package.md). Para obtener más información, vea [validDomains](~/resources/schema/manifest-schema.md#validdomains) en la referencia del esquema del manifiesto. Sin embargo, tenga en cuenta que la funcionalidad principal de su pestaña existe en Microsoft Teams y no fuera de Microsoft Teams.
