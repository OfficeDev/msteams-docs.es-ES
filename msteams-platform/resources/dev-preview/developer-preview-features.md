---
title: Características de la versión preliminar para desarrolladores públicos
description: Describe las características de la versión preliminar para desarrolladores públicos de Microsoft Teams.
keywords: características para desarrolladores de Team Preview
ms.openlocfilehash: abec097d9f3b6fb48a4a50cb26d73cf811151149
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675740"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Características de la versión preliminar para desarrolladores públicos para Microsoft Teams

La vista previa para desarrolladores incluye las siguientes características nuevas:

## <a name="mention-support-in-adaptive-cards"></a>Mencione la compatibilidad en tarjetas adaptables

Ahora puede Agregar @ menciones dentro de un cuerpo de tarjeta adaptable para bots y respuestas de extensiones de mensajería. las @ menciones de las tarjetas siguen la misma lógica de notificación y representación que una de las menciones normales basadas en los mensajes. Tenga en cuenta que las menciones basadas en tarjetas solo se admiten en los clientes Web y de escritorio de hoy en día, con compatibilidad para la representación en clientes móviles próximamente.

## <a name="adaptive-12-support"></a>Compatibilidad adaptable de 1,2

Microsoft Teams ahora es compatible con la [versión adaptable 1,2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) en Developer Preview. Tenga en cuenta que [los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten todavía.

## <a name="tabs-single-sign-on"></a>Inicio de sesión único de pestañas

Ahora puede usar el inicio [de sesión único (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) para iniciar sesión y autenticar a un usuario en el escritorio y en el móvil mediante el SDK de Teams para JavaScript desde una página de contenido Web. Una de las ventajas es que un usuario nunca tiene que iniciar sesión; una vez que hayan dado su consentimiento a la aplicación mediante su perfil: se iniciará sesión automáticamente en su pestaña (incluido el móvil).

Nuestra vista previa para desarrolladores está disponible en las versiones 1,5 y posteriores del manifiesto. Nuestra implementación actual solo puede obtener una cantidad limitada de API de Graph, pero proporcionamos una solución alternativa para obtener más API de Graph con nuestra API de autenticación existente.

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>Aplicaciones personales (pestañas estáticas y bots de 1-1) habilitados en dispositivos móviles

Las aplicaciones personales instaladas (pestañas estáticas y bots 1-1) ahora están disponibles en la bandeja de la aplicación en dispositivos móviles. Vea [directrices de diseño para Mobile](~/tabs/design/tabs-mobile.md) for Design Guidance. Las aplicaciones solo se pueden instalar desde un cliente de escritorio o Web, y pueden tardar hasta 4 horas en estar disponibles en dispositivos móviles después de la instalación.

Esto incluye la posibilidad de que un administrador del sistema Prefije una aplicación a través de [las directivas de configuración](/microsoftteams/teams-app-setup-policies)de la aplicación. Las aplicaciones que se han anclado se mostrarán en el cajón de la aplicación.

## <a name="calls-and-online-meeting-bots"></a>Llamadas y bots de reuniones en línea

Con la adición de las [API de Microsoft Graph para las llamadas y las reuniones en línea](/graph/api/resources/communications-api-overview?view=graph-rest-beta), las aplicaciones de Microsoft Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. Estas API le permiten agregar nuevas características de aplicación, como la respuesta interactiva de voz (IVR), el control de llamadas y el acceso a secuencias de audio o vídeo en tiempo real para llamadas y reuniones, incluido el uso compartido de aplicaciones y escritorio.

Hemos agregado una nueva sección sobre cómo crear y desarrollar llamadas y los bots de reuniones en línea, comenzando por la [información general](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).
