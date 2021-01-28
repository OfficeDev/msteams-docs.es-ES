---
title: Características de la versión preliminar pública para desarrolladores
description: Detalles de las características de la versión preliminar para desarrolladores públicos de Microsoft Teams
ms.topic: reference
keywords: Características para desarrolladores de vista previa de teams
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014358"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características de la versión preliminar para desarrolladores públicos de Microsoft Teams

La vista previa del desarrollador incluye las siguientes características nuevas:

## <a name="tabs-single-sign-on-sso"></a>Inicio de sesión único (SSO) de pestañas

Ahora puede usar el inicio de sesión único [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en dispositivos móviles y de escritorio con el SDK de JavaScript de Teams desde una página de contenido web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; y una vez que haya dado su consentimiento a la aplicación con su perfil: iniciará sesión automáticamente en su pestaña (incluido el móvil).

Nuestra versión preliminar para desarrolladores está disponible en las versiones de manifiesto 1.5 y posteriores. Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener API de Graph adicionales mediante nuestra API de autenticación existente.

## <a name="calls-and-online-meeting-bots"></a>Bots de llamadas y reuniones en línea

Con la adición de las API de [Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta)para llamadas y reuniones en línea, las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecciones mediante voz y vídeo. Estas API le permiten agregar nuevas características de la aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar bots de llamadas y reuniones en línea, empezando por la [introducción.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

## <a name="image-enlarge-support"></a>Compatibilidad con ampliación de imagen

Ahora es posible que los bots indiquen qué imágenes compartidas en tarjetas adaptables en Teams se pueden ampliar. Esto es útil para escenarios como compartir guías visuales detalladas paso a paso a través de bots que podrían resultar difíciles de leer para los usuarios de lo contrario. Para que una imagen se expanda, solo tienes que `allowExpand: true` marcarla como se muestra a continuación.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Esto hará que el cliente web o de escritorio de Teams represente un elemento al pasar sobre la imagen para permitir al usuario expandir la imagen.

