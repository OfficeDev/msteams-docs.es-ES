---
title: Características de la versión preliminar para desarrolladores públicos
description: Describe las características de la versión preliminar para desarrolladores públicos de Microsoft Teams.
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210704"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características de la versión preliminar para desarrolladores públicos para Microsoft Teams

La vista previa para desarrolladores incluye las siguientes características nuevas:

## <a name="adaptive-cards-v12-support"></a>Compatibilidad con tarjetas adaptables v 1.2

La compatibilidad con [tarjetas adaptables v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) en Teams ya está disponible para el público en general. Sin embargo, [los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten actualmente en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.

## <a name="tabs-single-sign-on-sso"></a>Inicio de sesión único (SSO) de pestañas

Ahora puede usar el inicio [de sesión único (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en el escritorio y en el móvil mediante el SDK de Teams para JavaScript desde una página de contenido Web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; una vez que hayan dado su consentimiento a la aplicación mediante su perfil: se iniciará sesión automáticamente en su pestaña (incluido el móvil).

Nuestra vista previa para desarrolladores está disponible en las versiones 1,5 y posteriores del manifiesto. Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener más API de Graph con nuestra API de autenticación existente.

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>Aplicaciones personales (pestañas estáticas y bots de 1-1) habilitados en dispositivos móviles

Las aplicaciones personales instaladas (pestañas estáticas y bots 1-1) ahora están disponibles en la bandeja de la aplicación en dispositivos móviles. Vea [directrices de diseño para Mobile](~/tabs/design/tabs-mobile.md) for Design Guidance. Las aplicaciones solo se pueden instalar desde un cliente de escritorio o Web, y pueden tardar hasta 4 horas en estar disponibles en dispositivos móviles después de la instalación.

Esto incluye la posibilidad de que un administrador del sistema Prefije una aplicación a través de [las directivas de configuración](/microsoftteams/teams-app-setup-policies)de la aplicación. Las aplicaciones que se han anclado se mostrarán en el cajón de la aplicación.

## <a name="calls-and-online-meeting-bots"></a>Llamadas y bots de reuniones en línea

Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. Estas API le permiten agregar nuevas características de aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar llamadas y los bots de reuniones en línea, comenzando por la [información general](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).
