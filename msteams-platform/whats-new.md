---
title: Novedades
description: Describe todas las nuevas características para desarrolladores de Microsoft Teams
ms.topic: reference
keywords: novedades de teams
ms.openlocfilehash: 49603a9e48cd0a9951c6d9f0132a705770322de4
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231655"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Novedades para desarrolladores en Microsoft Teams

>[!TIP]
> Consulte nuestras plantillas preparadas para producción en el catálogo [**de plantillas de aplicación de Teams.**](samples/app-templates.md) El catálogo está alfabético y las adiciones más nuevas se etiquetan con una estrella **&#9734;**.

## <a name="change-log"></a>Registro de cambios

El registro de cambios enumera los cambios en la plataforma de Microsoft Teams y en este conjunto de documentos. En ocasiones, las entradas pueden usarse para llamar la atención sobre una nueva característica que es simplemente de interés para los desarrolladores de Teams.

| **Fecha** | **Notas** | **Temas cambiados** |
| -------- | --------- | ------------------ |
|02/09/2021|Nuevo: Información general sobre las funcionalidades de dispositivo agregadas. <br/> Actualización: la información de funcionalidad del micrófono se agrega en los permisos de dispositivo nativo e integra archivos de funcionalidades multimedia.|[Información general,](concepts/device-capabilities/device-capabilities-overview.md) [Solicitar permisos de dispositivo,](concepts/device-capabilities/native-device-permissions.md) [Integrar funcionalidades multimedia](concepts/device-capabilities/mobile-camera-image-permissions.md)|
|11/30/2020|Nuevo: Integración de la plataforma de identidad con Teams Toolkit y Visual Studio código para pestañas|[Autenticación de inicio de sesión único con Teams Toolkit y Visual Studio código para pestañas](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Manifiesto de la aplicación de Teams actualizado a la versión 1.8|[Referencia: esquema de manifiesto para Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Directrices de diseño de bots de Teams|[Directrices de diseño de bots](bots/design/bots.md)|
|9/30/2020|Ahora se admite el envío y recepción de archivos a bots en dispositivos móviles.|[Enviar y recibir archivos a través del bot](resources/bot-v3/bots-files.md)|
|09/22/2020|Nueva guía "Introducción a Teams"|[Información general sobre la creación de la primera aplicación de Teams](build-your-first-app/build-first-app-overview.md)|
|9/18/2020|Compatibilidad con aplicaciones de Teams en reuniones (versión preliminar)|[Crear aplicaciones para reuniones de Teams y](apps-in-teams-meetings/create-apps-for-teams-meetings.md) aplicaciones en reuniones de [Teams](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|8/19/2020|Importar mensajes de Teams con Microsoft Graph|[Importar mensajes de plataformas de terceros a Teams con Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |Las tarjetas adaptables admiten el webhook entrante movido a GA.|[Enviar tarjetas adaptables con un webhook entrante](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Introducción a la creación de aplicaciones de Teams con Visual Studio Toolkit.|[Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio código](toolkit/visual-studio-overview.md) |
|08/06/2020|Compatibilidad con la autenticación sso de pestañas|[Desarrollar una pestaña sso de Microsoft Teams](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Mensajes y bots proactivos de Graph (versión preliminar pública)|[Habilitar la instalación proactiva de bots y la mensajería proactiva en Teams con Microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |Actualizaciones de funcionalidad de dispositivos móviles.|[Solicitar permisos de dispositivo para la pestaña de Microsoft Teams](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Herramienta de validación de aplicaciones de Teams para envíos de AppSource.|[Herramienta de validación de aplicaciones de Teams](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Crear un asistente virtual para Teams|[Asistente virtual para Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Mostrar la documentación de un indicador de carga nativo|[Mostrar un indicador de carga nativo](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Introducción a la creación de aplicaciones de Teams con Visual Studio Code Toolkit.|[Crear aplicaciones con Microsoft Teams Toolkit y Visual Studio código](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Inicio de sesión único para pestañas GA para clientes web y de escritorio de Teams|[Single Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Esquema de manifiesto actualizado a la versión 1.7| [Referencia: esquema de manifiesto para Microsoft Teams](resources/schema/manifest-schema.md)|
| 05/20/2020 | Los permisos de consentimiento específicos de recursos mediante las API de Microsoft Graph se encuentra en la versión preliminar del desarrollador. |[Consentimiento específico de recursos (RSC): Versión preliminar del desarrollador](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Integrar agentes virtuales de power con Teams|[Integrar un bot de chat de Power Virtual Agents con Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Integrar sistemas WFM con Shifts Connector para Teams|[Microsoft Teams cambia los conectores WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Se ha agregado compatibilidad para recuperar un solo miembro de una conversación y compatibilidad adicional para recuperar miembros paginados. | [Obtención del contexto de Teams para un bot](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | El parámetro de las cargas enviadas a un bot ya no está cifrado, lo que le permite usar este valor para crear `replyToId` vínculos profundos a estos mensajes. Las cargas de mensajes incluyen los valores cifrados en el parámetro. `legacy.replyToId`.  |
| 11/5/2019 | El inicio de sesión único con el SDK de JavaScript de Teams en una página de contenido web está en la versión preliminar del desarrollador. | [Inicio de sesión único](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Bots de conversación y documentación de extensión de mensajería actualizada para reflejar el SDK de Bot Framework 4.6. La documentación del SDK de v3 está disponible en la sección Recursos. | Toda la documentación sobre bots y extensiones de mensajería. |
| 10/31/2019 | Nueva estructura de documentación y refactorización de artículos principales. Informe de los vínculos sin conexión o 404 creando un problema de GitHub. | ¡Todos! |
| 9/13/2019 | El bot de solicitud se instala desde la extensión de mensajería basada en acciones. | [Iniciar acciones con extensiones de mensajería](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Compatibilidad con canales privados en pestañas y conectores. | [Obtención del contexto de Teams para la pestaña](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Compartir un sitio web externo, desde un sitio web externo, en un canal de Teams. | [Compartir con Teams](~/share-to-teams.md) |
| 05/25/2019 | Responder con el mensaje de bot desde el módulo de tareas. | [Responder con mensaje de bot desde el módulo de tareas](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Bots en chats en grupo. | [Interactuar con un bot en un canal o chat en grupo](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Localización del manifiesto de la aplicación. | [Localización de aplicaciones](~/publishing/apps-localization.md) |
| 05/20/2019 | Acciones de mensaje. | [Acciones de mensajes](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Desenlazaje de vínculos (vistas previas de url personalizadas). | [Apertura de vínculos](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Programa de certificación de aplicaciones para aplicaciones de la tienda. | [Certificación de aplicaciones](~/publishing/application-certification.md) |
| 05/06/2019 | Las plantillas de aplicación ya están disponibles. | [Plantillas de aplicación](~/samples/app-templates.md) |
| 04/23/2019 | Las extensiones de mensajería basadas en acciones ya están disponibles. | [Extensiones de mensaje basadas en acciones](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | La creación de vínculos profundos al chat privado está fuera de la versión preliminar del desarrollador y está disponible. | [Vinculación profunda a un chat](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Mostrar información de SKU y licenceType en el contexto de la pestaña. | [Contexto de tabulación](~/concepts/tabs/tabs-context.md) |
| 12/11/2018 | Las pestañas del chat en grupo ahora están disponibles en la versión publicada de Teams y se han movido fuera de la versión preliminar del desarrollador. Como parte de este trabajo, se ha reelajeado la sección de pestañas para mayor claridad.| [Pestañas configurables](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | La introducción a Node JS y .NET/C# se ha actualizado para usar App Studio en Teams y se ha agregado una nueva sección sobre cómo hospedar aplicaciones de Teams basadas en Nodos en Azure. | Introducción a la plataforma de Microsoft Teams con [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)y App Studio, Introducción a la plataforma de Microsoft Teams con Node JS y [App Studio,](~/get-started/get-started-nodejs-app-studio.md)Hospedar la aplicación de [Node Teams en Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Ahora puede crear vínculos profundos a chats privados entre usuarios. | [Vinculación profunda a un chat](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 08/11/2018 | SharePoint Framework 1.7 ha incluido y con ella una nueva característica para usar la pestaña de Microsoft Teams como elemento web de SharePoint Framework. | [Pestañas en SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Se publicó la característica "módulo de tareas". Un módulo de tareas le permite crear experiencias emergentes modales en su aplicación de Teams, tanto desde bots como desde pestañas. Dentro del elemento emergente, puede ejecutar su propio código HTML/JavaScript personalizado, mostrar un widget basado en youtube o un vídeo de Microsoft Stream o mostrar una tarjeta `<iframe>` [adaptable.](https://docs.microsoft.com/adaptive-cards/) | [Información general del módulo de](~/concepts/task-modules/task-modules-overview.md)tareas, módulo de tareas en [pestañas,](~/concepts/task-modules/task-modules-tabs.md)  [módulo de tareas en bots](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | La información de formato de las tarjetas se ha actualizado y probado en los clientes de escritorio, iOS y Android para Teams. | [Tarjetas,](~/concepts/cards/cards.md) [formato de tarjeta](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Las API de llamadas y reuniones en línea para Microsoft Graph se lanzaron a la versión beta y las aplicaciones de Teams ahora pueden interactuar con los usuarios de formas enriquecciones con voz y vídeo. | [Bots de](~/concepts/calls-and-meetings/registering-calling-bot.md)llamadas y reuniones en línea, conceptos multimedia en tiempo [real,](~/concepts/calls-and-meetings/real-time-media-concepts.md)registro de un [bot](~/concepts/calls-and-meetings/registering-calling-bot.md)de llamada, depuración y [pruebas locales,](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)medios hospedados por la [aplicación,](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)control de notificaciones de [llamadas entrantes](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Las páginas de configuración de pestañas son ahora significativamente más altas. | [Diseño de pestañas](tabs/design/tabs.md) |
| 08/15/2018 | Las tarjetas adaptables ahora son compatibles con Teams.|[Acciones de tarjeta adaptable en Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Se ha documentado la compatibilidad de cliente con DevTools para Developer Preview.| [DevTools para el cliente de escritorio de Microsoft Teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Ahora, las extensiones de mensajería admiten varios comandos. Esta característica ha estado en la versión preliminar del desarrollador y ahora se ha publicado para todos los usuarios.| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | La configuración en línea ahora es compatible con conectores. La documentación de Conectores también se ha revisado y ampliado para mayor claridad.| [Conectores](~/concepts/connectors/connectors.md)|
| 08/06/2018 | El bot ahora puede enviar y recibir archivos.| [Enviar y recibir archivos a través del bot](~/concepts/bots/bots-files.md)|
| 07/27/2018 | La vista previa del desarrollador ahora admite varios comandos en extensiones de mensajería. | [Se han ampliado las extensiones de mensajería](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Se ha agregado información sobre la ree certificación de la aplicación a la sección Publicación. |[Permisos de manifiesto](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | En la vista previa del desarrollador, se ha asignado más espacio a la página de configuración de pestañas. | [La página de configuración de pestañas es significativamente más alta](tabs/design/tabs.md)|
| 07/12/2018 | Información sobre el acceso de invitados. | [Acceso de invitado en Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Se ha agregado información de versión previa al Catálogo de aplicaciones de inquilinos de Microsoft Teams. | [Publicar la aplicación de Microsoft Teams](~/publishing/apps-publish.md)|
| 05/31/2018 | La versión preliminar para desarrolladores de Teams (anillo 3.6) se ha actualizado para incluir la capacidad de agregar bots y pestañas al chat en grupo. | [Características de la versión preliminar del desarrollador,](~/resources/dev-preview/developer-preview-features.md) [esquema de vista previa del desarrollador](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Las tarjetas adaptables ahora son compatibles con Teams en las [acciones de tarjeta adaptable en Teams.](task-modules-and-cards/cards/cards-reference.md) |
| 05/29/2018 | Si usa la versión preliminar [del desarrollador,](~/resources/dev-preview/developer-preview-intro.md)el bot ahora puede enviar y recibir archivos.| [Enviar y recibir archivos a través de su bot](~/concepts/bots/bots-files.md), características de la versión preliminar del desarrollador público para Microsoft [Teams](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | replyToID se ha agregado a la carga para las acciones `Invoke` de `MessageBack` tarjeta y. Esto es especialmente útil si necesita actualizar el mensaje del que provenía la acción de la tarjeta. | [Acciones de tarjeta](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Se agregó este tema para realizar un seguimiento de los cambios en la interfaz de programación de Teams y en este conjunto de documentación. | [Novedades](~/whats-new.md)|
| 04/10/2018 | Se cambiaron las direcciones URL de autenticación para usar de forma coherente el identificador de inquilino en la ruta de acceso. | [Flujo de autenticación para pestañas,](~/concepts/authentication/auth-flow-tab.md) [autenticación de pestaña de AAD](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Se agregaron directrices de diseño para usar el cuadro de comandos. |[Cuadro de comando](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Usar bots para enviar notificaciones para la aplicación. |[Bots de solo notificación](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Documentación ampliada para mensajería proactiva. |[Inicio de una conversación](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Documentación refactorizado para tarjetas. |[Tarjetas,](~/concepts/cards/cards.md) [acciones de tarjeta,](~/concepts/cards/cards-actions.md) [formato de tarjeta,](~/concepts/cards/cards-format.md) [referencia de tarjeta](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Se agregó documentación para Teams App Studio. |[Desarrollar rápidamente aplicaciones con Teams App Studio,](~/get-started/get-started-app-studio.md) [mediante la biblioteca de controles en App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Se agregó código de ejemplo para demostrar el método AsTeamsChannelAccounts(). |[Obtener contexto para un bot](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Se agregaron temas para empezar a usar C#. |[Introducción a la plataforma de Microsoft Teams con C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Enviar sus preguntas, errores, solicitudes de características y contribuciones

Escuchamos a la comunidad de desarrolladores en [varios canales.](feedback.md)
