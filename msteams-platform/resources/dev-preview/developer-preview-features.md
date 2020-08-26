---
title: Características de la versión preliminar para desarrolladores públicos
description: Detalla las características de la vista previa de Microsoft Teams para desarrolladores públicos
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874845"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características de la versión preliminar para desarrolladores públicos para Microsoft Teams

La vista previa para desarrolladores incluye las siguientes características nuevas:

## <a name="tabs-single-sign-on-sso"></a>Inicio de sesión único (SSO) de pestañas

Ahora puede usar el inicio [de sesión único (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en el escritorio y en el móvil mediante el SDK de Teams para JavaScript desde una página de contenido Web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; una vez que hayan dado su consentimiento a la aplicación mediante su perfil: se iniciará sesión automáticamente en su pestaña (incluido el móvil).

Nuestra vista previa para desarrolladores está disponible en las versiones 1,5 y posteriores del manifiesto. Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener más API de Graph con nuestra API de autenticación existente.

## <a name="calls-and-online-meeting-bots"></a>Llamadas y bots de reuniones en línea

Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. Estas API le permiten agregar nuevas características de aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar llamadas y los bots de reuniones en línea, comenzando por la [información general](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

## <a name="image-enlarge-support"></a>Compatibilidad con Image ampliado

Ahora es posible que los bots indiquen qué imágenes compartidas en las tarjetas adaptables de Teams se pueden ampliar. Esto es útil para escenarios como compartir guías visuales paso a paso a través de bots que podrían resultar difíciles de leer para los usuarios en caso contrario. Para hacer que una imagen sea expansible, simplemente debe marcarla `allowExpand: true` como se muestra a continuación.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Esto provocará que el cliente web/de escritorio de Microsoft Teams represente un elemento al pasar sobre la imagen para permitir que el usuario expanda la imagen.

