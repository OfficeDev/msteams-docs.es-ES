---
title: Características de la versión preliminar para desarrolladores públicos
description: Describe las características de la versión preliminar para desarrolladores públicos de Microsoft Teams.
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819178"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características de la versión preliminar para desarrolladores públicos para Microsoft Teams

La vista previa para desarrolladores incluye las siguientes características nuevas:

## <a name="adaptive-cards-v12-support"></a>Compatibilidad con tarjetas adaptables v 1.2

La compatibilidad con [tarjetas adaptables v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) en Teams ya está disponible para el público en general. Sin embargo, [los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten actualmente en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.

## <a name="tabs-single-sign-on-sso"></a>Inicio de sesión único (SSO) de pestañas

Ahora puede usar el inicio [de sesión único (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en el escritorio y en el móvil mediante el SDK de Teams para JavaScript desde una página de contenido Web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; una vez que hayan dado su consentimiento a la aplicación mediante su perfil: se iniciará sesión automáticamente en su pestaña (incluido el móvil).

Nuestra vista previa para desarrolladores está disponible en las versiones 1,5 y posteriores del manifiesto. Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener más API de Graph con nuestra API de autenticación existente.

## <a name="calls-and-online-meeting-bots"></a>Llamadas y bots de reuniones en línea

Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. Estas API le permiten agregar nuevas características de aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar llamadas y los bots de reuniones en línea, comenzando por la [información general](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).
