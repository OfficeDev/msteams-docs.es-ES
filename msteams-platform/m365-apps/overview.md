---
title: Ampliar las aplicaciones de Teams en Microsoft 365 (versión preliminar)
description: Ampliar las experiencias de la aplicación Teams a otras áreas de uso elevado de Microsoft 365
ms.date: 05/24/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 9cc0d88d5f992aa596509a6206a26baa413bdcf1
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668147"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Ampliar las aplicaciones de Teams en Microsoft 365

Con las versiones más recientes de [Microsoft Teams SDK de cliente de JavaScript](../tabs/how-to/using-teams-client-sdk.md) (versión 2.0.0), [Teams manifiesto de aplicación](../resources/schema/manifest-schema.md) (versión 1.13) y [Teams Toolkit](../toolkit/visual-studio-code-overview.md), puede compilar y actualizar Teams aplicaciones para que se ejecuten en otros Microsoft 365 de uso elevado  productos y publicarlos en el marketplace comercial de [Microsoft (Microsoft AppSource](https://appsource.microsoft.com/)).

La ampliación de la aplicación de Teams entre Microsoft 365 proporciona una manera simplificada de ofrecer aplicaciones multiplataforma a un público de usuario expandido: desde un único código base, puede crear experiencias de aplicación adaptadas a entornos de Teams, Outlook y Office. Los usuarios finales no tendrán que abandonar el contexto de su trabajo para usar la aplicación y los administradores se benefician de un flujo de trabajo consolidado de administración e implementación.

La plataforma de aplicaciones Teams continúa evolucionando y expandiéndose holísticamente en el ecosistema de Microsoft 365. Esta es la compatibilidad actual de Teams elementos de la plataforma de aplicaciones en Microsoft 365 (Teams, Outlook y Office como hosts de aplicaciones):

|          | Elemento de manifiesto de aplicación | compatibilidad con Teams |compatibilidad con Outlook* | compatibilidad con Office* | Notas |
|--|--|--|--|--|--|
| [**Pestañas**](../tabs/what-are-tabs.md) (ámbito personal)    |`staticTabs`  | Web, Escritorio, Móvil | Web (versión dirigida), escritorio (canal beta) | Web (versión dirigida)| El ámbito de canal y grupo aún no se admite para Microsoft 365. Consulte [las notas](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Extensiones de mensaje**](../messaging-extensions/what-are-messaging-extensions.md) (basadas en búsqueda)| `composeExtensions` | Web, Escritorio, Móvil| Web (versión dirigida), escritorio (canal beta)| |Aún no se admite la acción basada en Microsoft 365. Consulte [las notas](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook). |
| [**conectores de Graph**](/microsoftsearch/connectors-overview)| `graphConnector` | Web, Escritorio, Móvil| Web, Escritorio | Web| Ver [notas](#graph-connectors)
| [**complementos de Office**](/office/dev/add-ins/develop/json-manifest-overview) (versión preliminar) | `extensions` | | Web, Escritorio  | | Solo está disponible en [la versión del manifiesto devPreview](../resources/schema/manifest-schema-dev-preview.md) . Consulte [las notas](#office-add-ins-preview).|

\*La opción [de versión dirigida Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) y Aplicaciones Microsoft 365 inscripción del [canal de actualización](/deployoffice/change-update-channels) requieren la participación del administrador para toda la organización o los usuarios seleccionados.

Para obtener instrucciones sobre el manifiesto de Teams aplicación y la guía de control de versiones del SDK, así como más detalles sobre la compatibilidad actual con la plataforma de Teams en Microsoft 365, consulte la [introducción al SDK de cliente de JavaScript Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Agradecemos sus comentarios y los informes de problemas a medida que expande Teams aplicaciones para que se ejecuten en el ecosistema de Microsoft 365. Use los [canales habituales Microsoft Teams comunidad de desarrolladores](/microsoftteams/platform/feedback) para enviar comentarios.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Pestañas personales y extensiones de mensajería en Outlook y Office

Para llegar a los usuarios donde se encuentran, justo en el contexto de su trabajo, amplíe la aplicación web como una aplicación de pestaña personal Teams que también se ejecuta en Outlook y Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Pestaña personal que se ejecuta en Outlook, Office y Teams":::

También puede ampliar las extensiones de mensajes de Teams basadas en búsqueda a Outlook en la Web y Windows escritorio, lo que permite a los clientes buscar y compartir resultados a través del área de mensajes de redacción de Outlook, además de Microsoft Teams clientes.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Extensión de mensaje que se ejecuta en Outlook y Teams":::

La creación de la aplicación con el [manifiesto de aplicación de Teams](../resources/schema/manifest-schema.md) más reciente y [Teams SDK de cliente de JavaScript](../tabs/how-to/using-teams-client-sdk.md) le proporciona un proceso de desarrollo consolidado. Al permitirle ofrecer una experiencia simplificada de implementación, instalación y administración para los clientes, puede expandir el posible alcance y el uso de la aplicación.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Usar Teams manifiesto de aplicación en Microsoft 365

Con el objetivo de simplificar y simplificar el ecosistema de desarrolladores de Microsoft 365, seguimos expandiendo el manifiesto de aplicación Teams en otras áreas de Microsoft 365 con lo siguiente.

### <a name="graph-connectors"></a>conectores de Graph

Con los conectores de Microsoft Graph, su organización puede indexar datos de terceros para que aparezcan como Búsqueda de Microsoft resultados, expandiendo los tipos de orígenes de contenido que se pueden buscar en las aplicaciones de Teams.
Para obtener más información, consulte [Introducción a los conectores de Microsoft Graph para Búsqueda de Microsoft](/microsoftsearch/connectors-overview).

Para empezar a trabajar con conectores de grafos en Teams aplicaciones, consulte el [ejemplo de conectores de Teams Toolkit Graph](https://aka.ms/teamsfx-graph-connector-sample) y Microsoft Teams referencia del [esquema del manifiesto de versión preliminar para desarrolladores](../resources/schema/manifest-schema-dev-preview.md).

### <a name="office-add-ins-preview"></a>complementos de Office (versión preliminar)

Ahora puede definir e implementar Office complementos en la [versión preliminar para desarrolladores](../resources/schema/manifest-schema-dev-preview.md) del manifiesto de la aplicación Microsoft Teams. Actualmente, esta versión preliminar está limitada a Outlook complementos que se ejecutan en Office de suscripción para Windows.

Para obtener más información, vea [Teams manifiesto para complementos de Office (versión preliminar).](/office/dev/add-ins/develop/json-manifest-overview)

## <a name="microsoft-appsource-submission"></a>Envío de Microsoft AppSource

Únase al número creciente de aplicaciones de Teams de producción en la tienda [Microsoft AppSource](https://appsource.microsoft.com/) con compatibilidad ampliada con audiencias de Outlook y Office versión preliminar (versión de destino). El proceso de envío de aplicaciones [para Teams aplicaciones habilitadas para Outlook y Office](../concepts/deploy-and-publish/appsource/publish.md) es el mismo que para las aplicaciones Teams tradicionales; la única diferencia es que usará Teams [versión 1.13](../tabs/how-to/using-teams-client-sdk.md) del manifiesto de la aplicación en el paquete de la aplicación, lo que presenta compatibilidad con Teams aplicaciones que se ejecutan a través de Microsoft 365.

Una vez publicada como una aplicación de Teams habilitada para Microsoft 365, la aplicación se podrá detectar como una aplicación instalable desde las tiendas de Outlook y Aplicación de Office, además de la tienda de Teams. Cuando se ejecuta en Outlook y Office, la aplicación usa los mismos permisos concedidos en Teams. Teams los administradores pueden [administrar el acceso a Teams aplicaciones en Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) para los usuarios de su organización.

Para obtener más información, consulte [Publicar aplicaciones de Teams para Microsoft 365](publish.md).

## <a name="next-step"></a>Paso siguiente

Configure el entorno de desarrollo para compilar aplicaciones Teams para Microsoft 365:

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)
