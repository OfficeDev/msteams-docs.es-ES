---
title: 'Información general: distribuir la aplicación'
description: Describe las opciones para publicar la aplicación Microsoft Teams, cargar la aplicación y GCC.
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: none
keywords: implementar la carga de aplicaciones de publicación gcc
ms.openlocfilehash: 567abdb058f3618236840c993a0ab1a4d638c016
ms.sourcegitcommit: 660273bc6833ab84ba7550e6b374ea6e3780459d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2021
ms.locfileid: "61233501"
---
# <a name="distribute-your-microsoft-teams-app"></a>Distribuir la aplicación Microsoft Teams aplicación

Puedes proporcionar la aplicación Microsoft Teams a una persona, equipo, organización o cualquier persona que quiera usarla. La forma de distribuir depende de varios factores, como las necesidades de los usuarios, la empresa, los requisitos técnicos y los objetivos de la aplicación.

## <a name="configure-default-install-options"></a>Configurar las opciones de instalación predeterminadas

Configure las opciones de instalación predeterminadas. Por ejemplo, si la funcionalidad principal de la aplicación es un bot, también puedes convertir el bot en la funcionalidad predeterminada cuando un usuario instala la aplicación en un equipo.

## <a name="create-your-app-package"></a>Crear el paquete de aplicación

Para distribuir la Microsoft Teams, debes tener un paquete de aplicación válido.  Un paquete de la aplicación es un archivo zip que contiene un **manifiesto de la aplicación y** los iconos de la **aplicación.**

## <a name="upload-your-app-in-teams"></a>Upload la aplicación en Teams

Descarga local de una aplicación para uso personal, colaboración con el equipo o pruebas y depuración. Este tipo de distribución no requiere un proceso de revisión formal.

> [!IMPORTANT]
> Actualmente, las aplicaciones de instalación local están disponibles en Government Community Cloud (GCC), pero no están disponibles para GCC-High y departamento de defensa (DOD).

Para obtener más información, [consulta cargar la aplicación en Teams](apps-upload.md).

## <a name="publish-your-app-to-your-org"></a>Publicar la aplicación en su organización

Haz que la aplicación esté disponible para los usuarios de tu organización. Este tipo de distribución requiere la Teams del administrador.

Para obtener más información, consulta [Administrar tus aplicaciones en el centro Teams administración.](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)

### <a name="government-community-cloud-gcc-organizations"></a>Government Community Cloud (GCC)

En GCC Teams, las aplicaciones de Microsoft compatibles están habilitadas de forma predeterminada. Sin embargo, antes de publicar una aplicación, asegúrate de que todos los puntos de conexión de la aplicación cumplan con los requisitos de tu GCC organización.

> [!IMPORTANT]
>Si la aplicación incluye un bot o una extensión de mensajería, debes seleccionar la opción **Microsoft Teams para Gobierno** al configurar un canal entre el bot y Teams en Azure. Para obtener más información, vea [Conectar un bot a canales](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true).

## <a name="publish-your-app-to-the-teams-store"></a>Publicar la aplicación en la tienda Teams aplicaciones

Haz que la aplicación esté disponible para todos los usuarios. Este tipo de distribución requiere la aprobación de Microsoft.

Para obtener más información, [vea publish to the Teams store](~/concepts/deploy-and-publish/appsource/publish.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Configurar las opciones de instalación predeterminadas de la aplicación](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>Consulte también

[Programa de cumplimiento de aplicaciones de Microsoft 365](/microsoft-365-app-certification/overview)
