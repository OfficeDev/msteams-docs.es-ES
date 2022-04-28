---
title: Extensión de aplicaciones Teams entre Microsoft 365 (versión preliminar)
description: Ampliar las experiencias de la aplicación Teams a otras áreas de uso elevado de Microsoft 365
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 013bb773897965d51daaa485459eec78478292b3
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104346"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Ampliar las aplicaciones de Teams en Microsoft 365

> [!NOTE]
> Esta versión preliminar para desarrolladores temprana está pensada para proporcionar a los desarrolladores de Teams aplicaciones existentes la oportunidad de probar la nueva funcionalidad y [proporcionar comentarios](/microsoftteams/platform/feedback) sobre esta expansión de la plataforma para desarrolladores de Teams en otras áreas de uso elevado del ecosistema de Microsoft 365.

Puede probar las aplicaciones de Teams que se ejecutan en Microsoft Office y Outlook actualizando el código para usar el nuevo [sdk de cliente de JavaScript Microsoft Teams versión preliminar v2](using-teams-client-sdk-preview.md) y Microsoft Teams [manifiesto de versión preliminar para desarrolladores](../resources/schema/manifest-schema-dev-preview.md).

Con esta versión preliminar, puede hacer lo siguiente:

- Extienda [las pestañas personales](/microsoftteams/platform/tabs/how-to/create-personal-tab) de Teams existentes a Outlook para escritorio y en la web, y también Office en la Web (office.com).
- Amplíe [las extensiones de mensajes basadas en búsquedas](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command) Teams existentes a Outlook para escritorio y en la web.

Para obtener comentarios y problemas, siga usando los canales pertinentes [de la comunidad de desarrolladores Microsoft Teams](/microsoftteams/platform/feedback).

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Teams pestañas personales en Office y Outlook

Con esta versión preliminar, puede ampliar una aplicación de pestaña personal de Teams para que se ejecute en Outlook en Windows escritorio y en la web, y también Office en la Web.

Después de transferir localmente a Teams, la pestaña personal aparece como una de las aplicaciones instaladas en Outlook y Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Pestaña personal que se ejecuta en Outlook, Office y Teams":::

## <a name="teams-message-extensions-in-outlook"></a>extensiones de mensaje de Teams en Outlook

Con esta versión preliminar, puede ampliar las extensiones de mensajes de Teams basadas en búsqueda a Outlook en la Web y Windows escritorio, lo que permite a los clientes buscar y compartir resultados a través del área de mensajes de redacción de Outlook, además de Microsoft Teams clientes.

Después de realizar la transferencia local a Teams, la extensión de mensaje aparece como una de las aplicaciones instaladas dentro del área Outlook redactar mensaje.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extensión de mensaje que se ejecuta en Outlook y Teams":::

## <a name="next-steps"></a>Siguientes pasos

Configure el entorno de desarrollo para ampliar las aplicaciones de Teams entre Microsoft 365:

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)
