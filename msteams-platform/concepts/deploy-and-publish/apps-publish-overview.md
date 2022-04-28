---
title: 'Información general: Distribución de la aplicación'
description: Describe las opciones para publicar la aplicación Microsoft Teams, cargar la aplicación y GCC.
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: none
keywords: implementar gcc de carga de aplicaciones de publicación
ms.openlocfilehash: 5db182f9276865fc98d277f642f7e58fd4a52df5
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104437"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribución de la aplicación Microsoft Teams

Puede proporcionar su aplicación de Microsoft Teams a una persona, equipo, organización o cualquier persona que quiera usarla. La distribución depende de varios factores, como las necesidades de los usuarios, la empresa, los requisitos técnicos y los objetivos de la aplicación.

## <a name="configure-default-install-options"></a>Configurar las opciones de instalación predeterminadas

Configure las opciones de instalación predeterminadas. Por ejemplo, si la funcionalidad principal de la aplicación es un bot, también puede convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.

## <a name="create-your-app-package"></a>Crear el paquete de aplicación

Para distribuir la aplicación Microsoft Teams, debe tener un paquete de aplicación válido.  Un paquete de aplicación es un archivo ZIP que contiene un **manifiesto de aplicación** e **iconos de aplicación**.

## <a name="upload-your-app-in-teams"></a>Upload la aplicación en Teams

Transferir localmente una aplicación para su uso personal, colaborar con su equipo o probar y depurar. Este tipo de distribución no requiere un proceso de revisión formal.

> [!IMPORTANT]
> En este momento, la transferencia local de aplicaciones está disponible en Government Community Cloud (GCC), pero no está disponible para GCC-High ni para el Departamento de Defensa (DOD).

Para obtener más información, consulte [Carga de la aplicación en Teams](apps-upload.md).

## <a name="publish-your-app-to-your-org"></a>Publicar la aplicación en su organización

Haga que la aplicación esté disponible para los usuarios de su organización. Este tipo de distribución requiere la aprobación del administrador de Teams.

Para obtener más información, consulte [Administrar las aplicaciones en el centro de administración de Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json).

### <a name="government-community-cloud-gcc-organizations"></a>organizaciones de Government Community Cloud (GCC)

En GCC Teams entornos, las aplicaciones de Microsoft compatibles están habilitadas de forma predeterminada. Sin embargo, antes de publicar una aplicación, asegúrese de que todos los puntos de conexión de la aplicación cumplen los requisitos de la organización de GCC. Para obtener más información, consulte [Government Community Cloud](../app-fundamentals-overview.md#government-community-cloud).

> [!IMPORTANT]
>Si la aplicación incluye un bot o una extensión de mensaje, debe seleccionar la opción **Microsoft Teams for Government** al configurar un canal entre el bot y Teams en Azure. Para obtener más información, consulte [Conexión de un bot a canales](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).

## <a name="publish-your-app-to-the-teams-store"></a>Publicación de la aplicación en el almacén de Teams

Haga que la aplicación esté disponible para todos los usuarios. Este tipo de distribución requiere la aprobación de Microsoft.

Para obtener más información, vea [Publicar en el almacén de Teams](~/concepts/deploy-and-publish/appsource/publish.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configuración de las opciones de instalación predeterminadas de la aplicación](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>Vea también

[Programa de cumplimiento de aplicaciones de Microsoft 365](/microsoft-365-app-certification/overview)
