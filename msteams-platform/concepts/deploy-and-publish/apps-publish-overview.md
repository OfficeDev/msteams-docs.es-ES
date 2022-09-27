---
title: 'Información general: distribución de la aplicación'
description: En este artículo, aprenderá las opciones para publicar la aplicación Microsoft Teams, cargar e implementar la aplicación y GCC.
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: b194e435ec6152993ce1269875d431ab4ef03aef
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044675"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribución de la aplicación de Microsoft Teams

Puede proporcionar su aplicación de Microsoft Teams a una persona, equipo, organización o cualquier persona que quiera usarla. La distribución depende de varios factores, como las necesidades de los usuarios, el negocio, los requisitos técnicos y los objetivos de la aplicación.

## <a name="configure-default-install-options"></a>Configurar las opciones de instalación predeterminadas

Puede configurar las opciones de instalación predeterminadas. Por ejemplo, si la funcionalidad principal de la aplicación es un bot, puede convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.

## <a name="create-your-app-package"></a>Crear el paquete de aplicación

Para distribuir la aplicación de Teams, debe tener un paquete de aplicación válido.  Un paquete de aplicación es un archivo ZIP que contiene un **manifiesto** e **iconos de aplicación**.

## <a name="upload-your-app-in-teams"></a>Cargar la aplicación en Microsoft Teams

Transfiera localmente una aplicación para su uso personal, colaborar con su equipo, o probar y depurar. Este tipo de distribución no requiere un proceso de revisión formal.

> [!IMPORTANT]
> En este momento, la transferencia local de aplicaciones está disponible en Government Community Cloud (GCC), pero no está disponible para GCC-High ni para el Departamento de Defensa (DOD).

Para más información, consulte [Cargar la aplicación en Teams](apps-upload.md).

## <a name="publish-your-app-to-your-org"></a>Publicar la aplicación en su organización

Haga que la aplicación esté disponible para los usuarios de la organización. Este tipo de distribución requiere la aprobación del administrador de Teams.

Para obtener más información, consulte [Administrar las aplicaciones en el Centro de administración de Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json).

### <a name="government-community-cloud-gcc-organizations"></a>Organizaciones de Government Community Cloud (GCC)

En entornos de Teams de GCC, las aplicaciones de Microsoft compatibles están habilitadas de forma predeterminada. Sin embargo, antes de publicar una aplicación, asegúrese de que todos los puntos de conexión de la aplicación cumplan los requisitos de la organización de GCC. Para obtener más información, consulte [Government Community Cloud](../app-fundamentals-overview.md#government-community-cloud).

> [!IMPORTANT]
>Si la aplicación incluye un bot o una extensión de mensajería, debe seleccionar la opción **Microsoft Teams para Administración Pública** al configurar un canal entre el bot y Teams en Azure. Para obtener más información, consulte [Conexión de un bot a canales](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).

## <a name="publish-your-app-to-the-teams-store"></a>Publicar la aplicación en la tienda de Teams

Haga que la aplicación esté disponible para todos los usuarios. Este tipo de distribución requiere la aprobación de Microsoft.

Para más información, consulte [cómo publicar en la tienda de Teams](~/concepts/deploy-and-publish/appsource/publish.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configurar las opciones de instalación predeterminadas](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>Consulte también

[Programa de cumplimiento de aplicaciones de Microsoft 365](/microsoft-365-app-certification/overview)
