---
title: Ampliar las aplicaciones de Teams en Microsoft 365 (versión preliminar)
description: Ampliar las experiencias de la aplicación Teams a otras áreas de uso elevado de Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 66ba17a638fc57b47febef34bea769e39cdea7e3
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111951"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Ampliar las aplicaciones de Teams en Microsoft 365

> [!NOTE]
> Esta versión preliminar para desarrolladores está pensada para proporcionar a los desarrolladores de Teams con aplicaciones existentes la oportunidad de probar la nueva funcionalidad y [enviar comentarios](/microsoftteams/platform/feedback) sobre esta expansión de la plataforma para desarrolladores de Teams en otras áreas de uso elevado del ecosistema de Microsoft 365.

Puede probar las aplicaciones de Teams que se ejecutan en Microsoft Office y Outlook actualizando el código para usar el nuevo [SDK de cliente de JavaScript Microsoft Teams versión preliminar v2](using-teams-client-sdk-preview.md) y el [manifiesto de versión preliminar para desarrolladores](../resources/schema/manifest-schema-dev-preview.md) de Microsoft Teams.

Con esta versión preliminar, podrá:

- Extender [las pestañas personales](/microsoftteams/platform/tabs/how-to/create-personal-tab) existentes de Teams a la versión de escritorio y web de Outlook, y también a Office en la Web (office.com).
- Ampliar [las extensiones de mensajes basadas en búsquedas](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) existentes de Teams a la versión de escritorio y web de Outlook.

Para enviar comentarios y problemas, siga usando los canales pertinentes de la [comunidad de desarrolladores Microsoft Teams](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Pestañas personales de Teams en Office y Outlook

Con esta versión preliminar, puede ampliar una aplicación de pestaña personal de Teams para que se ejecute en Outlook en la versión de escritorio de Windows y en la web, y también en Office en la Web.

Después de transferirla localmente a Teams, la pestaña personal aparece como una de las aplicaciones instaladas en Outlook y Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Pestaña personal que se ejecuta en Outlook, Office y Teams":::

## <a name="teams-message-extensions-in-outlook"></a>Extensiones de mensaje de Teams en Outlook

Con esta versión preliminar, puede ampliar las extensiones de mensajes de Teams basadas en la búsqueda a Outlook en la Web y la versión de escritorio de Windows, lo que permite a los clientes buscar y compartir resultados a través del área de mensajes de redacción de Outlook, además de a los clientes de Microsoft Teams.

Después de realizar la transferencia local a Teams, la extensión de mensaje aparece como una de las aplicaciones instaladas dentro del área Outlook redactar mensaje.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extensión de mensaje que se ejecuta en Outlook y Teams":::

## <a name="next-steps"></a>Pasos siguientes

Configure el entorno de desarrollo para ampliar las aplicaciones de Teams entre Microsoft 365:

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)
