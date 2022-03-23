---
title: Ampliar Teams aplicaciones en Microsoft 365 (versión preliminar)
description: Extender las experiencias Teams aplicación a otras áreas de uso alto de Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 1936e6a660d77855e53257f40925cf54b05de0de
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2022
ms.locfileid: "63727297"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Ampliar las aplicaciones de Teams en Microsoft 365

> [!NOTE]
> Esta versión preliminar de desarrolladores está diseñada para proporcionar Teams los desarrolladores con aplicaciones existentes la oportunidad de probar la nueva funcionalidad [](/microsoftteams/platform/feedback) y proporcionar comentarios sobre esta expansión de la plataforma de desarrolladores de Teams en otras áreas de alto uso del ecosistema Microsoft 365.

Puedes probar las aplicaciones Teams que se ejecutan en Microsoft Office y Outlook actualizando el código para usar el nuevo manifiesto de vista previa del SDK de [cliente de JavaScript de Microsoft Teams v2 Preview](using-teams-client-sdk-preview.md) y Microsoft Teams [Developer preview](../resources/schema/manifest-schema-dev-preview.md).

Con esta vista previa, puede:

- Extender las Teams [pestañas personales existentes](/microsoftteams/platform/tabs/how-to/create-personal-tab) a Outlook para escritorio y en la web, y también Office en la Web (office.com).
- Extienda las Teams [de mensajería basadas en búsquedas existentes](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) a Outlook para escritorio y en la web.

Para obtener comentarios y problemas, siga usando los canales Microsoft Teams [comunidad de desarrolladores relevantes](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teams pestañas personales en Office y Outlook

Con esta vista previa, puede extender una aplicación de pestaña personal Teams para que se ejecute en Outlook en Windows escritorio y la web, y también Office en la Web.

Después de realizar la Teams, la pestaña personal aparece como una de las aplicaciones instaladas en Outlook y Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Pestaña personal que se Outlook, Office y Teams":::

## <a name="teams-messaging-extensions-in-outlook"></a>Teams de mensajería en Outlook

Con esta vista previa, puede extender las extensiones de mensajería de Teams basadas en búsquedas al escritorio de Outlook en la Web y Windows, lo que permite a los clientes buscar y compartir resultados a través del área de mensajes de redacción de Outlook, además de Microsoft Teams clientes.

Después de realizar la Teams, la extensión de mensajería aparece como una de las aplicaciones instaladas dentro del área Outlook redacción de mensajes.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extensión de mensajería que se Outlook y Teams":::

## <a name="next-steps"></a>Pasos siguientes

Configure el entorno de desarrollo para extender las aplicaciones Teams en Microsoft 365:

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)
