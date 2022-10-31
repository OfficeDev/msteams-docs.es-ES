---
title: Ampliar las aplicaciones de Teams en Microsoft 365 (versión preliminar)
description: Obtenga información sobre cómo ampliar las aplicaciones de Teams en Microsoft 365 (que se ejecutan en Teams, Outlook y Office como hosts de aplicaciones).
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 91586eefe21836118ed2f0a0071070ac2034bf76
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789880"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Ampliar las aplicaciones de Teams en Microsoft 365

Con las versiones más recientes del [SDK de cliente de JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) (versión 2.0.0 y posteriores), [el manifiesto](../resources/schema/manifest-schema.md) de aplicación de Teams (versión 1.13 y posteriores) y [el kit](../toolkit/visual-studio-code-overview.md) de herramientas de Teams, puede compilar y actualizar aplicaciones de Teams para que se ejecuten en otros productos de Microsoft 365 de uso alto y publicarlas en el marketplace comercial de Microsoft ([Microsoft AppSource](https://appsource.microsoft.com/)) o en la tienda de aplicaciones privadas de su organización.

La ampliación de la aplicación de Teams en Microsoft 365 proporciona una manera simplificada de ofrecer aplicaciones multiplataforma a un público de usuario expandido: desde un único código base, puede crear experiencias de aplicación adaptadas a los entornos de Teams, Outlook y Office. Los usuarios finales no tendrán que abandonar el contexto de su trabajo para usar la aplicación y los administradores se benefician de un flujo de trabajo consolidado de administración e implementación.

La plataforma de aplicaciones de Teams continúa evolucionando y expandiéndose holísticamente en el ecosistema de Microsoft 365. Este es el soporte técnico actual de los elementos de la plataforma de aplicaciones de Teams en Microsoft 365 (Teams, Outlook y Office como hosts de aplicaciones):

| Características de la aplicación de Teams| Elemento de manifiesto de aplicación | Soporte técnico de Teams |Compatibilidad con Outlook* | Soporte técnico de Office* | Notas |
|--|--|--|--|--|--|
| [**Ámbito personal de pestañas**](../tabs/what-are-tabs.md)    |`staticTabs`  | Web, Escritorio, Móvil | Web (versión dirigida), escritorio (canal beta) | Web (versión dirigida), escritorio (canal beta), móvil (Android)| El ámbito de canal y grupo aún no se admite para Microsoft 365. Consulte [las notas](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Extensiones de mensaje basadas**](../messaging-extensions/what-are-messaging-extensions.md) en búsqueda| `composeExtensions` | Web, Escritorio, Móvil| Web (versión dirigida), escritorio (canal beta)| - |Todavía no se admite la acción basada en Microsoft 365. Consulte [las notas](extend-m365-teams-message-extension.md#troubleshooting). |
| apertura de vínculos | `composeExtensions.messageHandlers` | Web, Escritorio | Web (versión dirigida), escritorio (canal beta) | - | Ver [notas](extend-m365-teams-message-extension.md#link-unfurling) |
| [**Complementos de Office**](/office/dev/add-ins/develop/json-manifest-overview) (versión preliminar) | `extensions` | - | Web, Escritorio | - | Solo está disponible en [la versión del manifiesto devPreview](../resources/schema/manifest-schema-dev-preview.md) . Consulte [las notas](#office-add-ins-preview).|

\*La opción de [versión de destino de Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) y Aplicaciones Microsoft 365 inscripción del [canal de actualización](/deployoffice/change-update-channels) requieren la participación del administrador para toda la organización o los usuarios seleccionados. Los canales de actualización son específicos del dispositivo y solo se aplican a las instalaciones de Office que se ejecutan en Windows.

Para obtener instrucciones sobre el manifiesto de la aplicación de Teams y la guía de control de versiones del SDK, y más detalles sobre la compatibilidad actual de la plataforma teams en Microsoft 365, consulte la [introducción al SDK de cliente de JavaScript de Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Agradecemos sus comentarios y los informes de problemas a medida que expande las aplicaciones de Teams para que se ejecuten en el ecosistema de Microsoft 365. Use los [canales habituales de la comunidad de desarrolladores de Microsoft Teams](/microsoftteams/platform/feedback) para enviar comentarios.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Pestañas personales y extensiones de mensajería en Outlook y Office

Para llegar a los usuarios donde se encuentran, justo en el contexto de su trabajo, amplíe la aplicación web como una aplicación de [pestaña personal de Teams](extend-m365-teams-personal-tab.md) que también se ejecuta en Outlook y Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="La captura de pantalla es un ejemplo que muestra la pestaña Personal que se ejecuta en Outlook, Office y Teams.":::

En el móvil, puede probar y depurar la pestaña personal de Teams que se ejecuta en la [aplicación de Office para Android](extend-m365-teams-personal-tab.md#office-app-for-android).

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="La captura de pantalla es un ejemplo que muestra la pestaña personal que se ejecuta en Office.":::

También puede ampliar [las extensiones de mensajes de Teams basadas](extend-m365-teams-message-extension.md) en búsqueda a Outlook en la Web y escritorio de Windows, lo que permite a los clientes buscar y compartir resultados a través del área de redacción de mensajes de Outlook, además de los clientes de Microsoft Teams.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="La captura de pantalla es un ejemplo que muestra la extensión de mensaje que se ejecuta en Outlook y Teams.":::

[La desplegamiento de vínculos](extend-m365-teams-message-extension.md#link-unfurling)  funciona en los entornos web de Outlook y Windows de la misma manera que lo hace en Microsoft Teams sin ningún otro trabajo que el uso del manifiesto de aplicación de Teams versión 1.13 o posterior.

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="La captura de pantalla es un ejemplo que muestra la desplegamiento de vínculos que se ejecuta en Outlook y Teams.":::

Compile la aplicación con el [manifiesto de aplicación de Teams](../resources/schema/manifest-schema.md) más reciente y el SDK de [cliente de JavaScript de Teams](../tabs/how-to/using-teams-client-sdk.md) para beneficiarse del proceso de desarrollo de aplicaciones consolidado más reciente de Microsoft 365. A continuación, ofrezca una experiencia simplificada de implementación, instalación y administración para los clientes que expanda el alcance y el uso de la aplicación.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Uso del manifiesto de aplicación de Teams en Microsoft 365

Con el objetivo de simplificar y simplificar el ecosistema de desarrolladores de Microsoft 365, seguimos expandiendo el manifiesto de aplicación de Teams en otras áreas de Microsoft 365 con lo siguiente.

### <a name="office-add-ins-preview"></a>Complementos de Office (versión preliminar)

Ahora puede definir e implementar complementos de Office en la [versión preliminar para desarrolladores](../resources/schema/manifest-schema-dev-preview.md) del manifiesto de aplicación de Microsoft Teams. Actualmente, esta versión preliminar se limita a los complementos de Outlook que se ejecutan en la suscripción de Office para Windows.

Para obtener más información, vea [Manifiesto de Teams para complementos de Office (versión preliminar)](/office/dev/add-ins/develop/json-manifest-overview).

## <a name="microsoft-commercial-marketplace-submission"></a>Envío de Marketplace comercial de Microsoft

Únase al creciente número de aplicaciones de Teams de producción en la tienda de [Marketplace comercial de Microsoft](https://appsource.microsoft.com/) (Microsoft AppSource) con compatibilidad ampliada con las audiencias de outlook y versión preliminar de Office (versión de destino). El proceso de envío de aplicaciones [para las aplicaciones de Teams habilitadas para Outlook y Office](../concepts/deploy-and-publish/appsource/publish.md) es el mismo que para las aplicaciones tradicionales de Teams. La única diferencia es que usará la [versión 1.13](../tabs/how-to/using-teams-client-sdk.md) del manifiesto de aplicación de Teams en el paquete de la aplicación, lo que introduce compatibilidad con las aplicaciones de Teams que se ejecutan en Microsoft 365.

Una vez que la aplicación se publica como una aplicación de Teams habilitada para Microsoft 365, la aplicación se podrá detectar como una aplicación instalable en las tiendas de aplicaciones de Outlook y Office, además de la tienda teams. Cuando se ejecuta en Outlook y Office, la aplicación usa los mismos permisos concedidos en Teams. Los administradores de Teams pueden [administrar el acceso a las aplicaciones de Teams en Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) para los usuarios de su organización.

Para obtener más información, consulte [Publicación de aplicaciones de Teams para Microsoft 365](publish.md).

## <a name="next-step"></a>Paso siguiente

Configure el entorno de desarrollo para compilar aplicaciones de Teams para Microsoft 365:

> [!div class="nextstepaction"]
> [Requisitos previos para la instalación](prerequisites.md)
