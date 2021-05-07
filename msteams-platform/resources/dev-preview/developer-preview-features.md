---
title: Características de la versión preliminar de desarrolladores públicos
description: Detalles de las características de la versión Microsoft Teams public developer preview
ms.topic: reference
localization_priority: Normal
keywords: Características para desarrolladores de teams preview
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230907"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características en public developer preview for Microsoft Teams

> [!NOTE]
> Esta página estará en desuso en junio de 2021. Para obtener información sobre las características disponibles para la vista previa del desarrollador, consulta [¿Qué hay de nuevo?](~/whats-new.md)

La vista previa del desarrollador incluye las siguientes características nuevas:

## <a name="app-customization"></a>Personalización de aplicaciones

Ahora puede definir un conjunto selecto de propiedades, que un administrador de Teams puede personalizar o cambiar la marca en función de las necesidades de su organización. Para obtener más información, consulta [característica de personalización de aplicaciones](~/concepts/design/design-teams-app-overview.md).

## <a name="tabs-single-sign-on-sso"></a>Inicio de sesión único (SSO) de pestañas

Ahora puede usar el inicio de sesión único [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en escritorio y móvil mediante el SDK de JavaScript de Teams desde una página de contenido web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; y una vez que han dado su consentimiento a la aplicación con su perfil: iniciarán sesión automáticamente en su pestaña (incluido el móvil).

Nuestra vista previa para desarrolladores está disponible en las versiones 1.5 y posteriores del manifiesto. Nuestra implementación actual solo puede obtener una cantidad limitada de API Graph, pero proporcionamos una solución alternativa para obtener api Graph con nuestra API de autenticación existente.

## <a name="calls-and-online-meeting-bots"></a>Llamadas y bots de reunión en línea

Con la adición de API [de Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)para llamadas y reuniones en línea, Microsoft Teams aplicaciones ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo. Estas API te permiten agregar nuevas características de la aplicación, como la respuesta de voz interactiva (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar bots de llamadas y reuniones en línea, empezando por la [introducción](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).


## <a name="image-enlarge-support"></a>Compatibilidad con ampliación de imagen

Ahora es posible que los bots indiquen qué imágenes compartidas en tarjetas adaptables en Teams pueden ampliarse. Esto es útil para escenarios como compartir guías visuales detalladas paso a paso a través de bots que podrían ser difíciles de leer para los usuarios de lo contrario. Para que una imagen se expanda, simplemente marcala `allowExpand: true` como se muestra a continuación.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Esto hará que Teams cliente web o de escritorio represente un elemento al pasar el mouse sobre la imagen para permitir que el usuario expanda la imagen.
