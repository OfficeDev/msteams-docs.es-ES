---
title: Novedades
description: Describe todas las nuevas características para desarrolladores de Microsoft Teams
keywords: Teams novedades más recientes
ms.openlocfilehash: eede16c65faa2366b8c0734a39d84b558b1d68ed
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453857"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Novedades para desarrolladores en Microsoft Teams

## <a name="change-log"></a>Registro de cambios

El registro de cambios muestra los cambios en la plataforma de Microsoft Teams y en este conjunto de documentos. A veces, se pueden usar entradas para llamar la atención sobre una nueva característica que sólo es de interés para los desarrolladores de Microsoft Teams.

| **Fecha** | **Notas** | **Temas cambiados** |
| -------- | --------- | ------------------ |
| 05/20/2020 | Los permisos de consentimiento específicos de recursos que usan las API de Microsoft Graph están en Developer Preview. |[Autorización específica de recursos (RSC): vista previa para desarrolladores](graph-api/rsc/resource-specific-consent.md) |
| 03/24/2020 | Se ha agregado compatibilidad para recuperar un solo miembro de una conversación y una compatibilidad adicional para recuperar miembros paginados. | [Obtención del contexto de Teams para un bot](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | El `replyToId` parámetro de las cargas enviadas a un bot ya no está cifrado, lo que le permite usar este valor para crear deeplinks en estos mensajes. Las cargas de mensajes incluyen los valores cifrados en el parámetro. `legacy.replyToId`.  |
| 11/5/2019 | El inicio de sesión único con el SDK de Teams para JavaScript en una página de contenido web se encuentra en Developer Preview. | [Inicio de sesión único](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Los bots de conversación y la documentación de la extensión de mensajería se han actualizado para reflejar el SDK de bot Framework de 4,6. La documentación del SDK de la versión 3 de V3 está disponible en la sección recursos. | Toda la documentación de la extensión de Bot y mensajería. |
| 10/31/2019 | Nueva estructura de documentación y Refactorización de artículo principal. Informa de los vínculos muertos o de los 404 mediante la creación de un problema de GitHub. | Todos ellos. |
| 9/13/2019 | El bot request se instala desde la extensión de mensajería basada en acciones. | [Iniciar acciones con extensiones de mensajería](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Compatibilidad con canales privados en pestañas y conectores. | [Obtener contexto para la pestaña](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Comparta un sitio web externo, desde un sitio web externo, en un canal de Microsoft Teams. | [Compartir con Teams](~/share-to-teams.md) |
| 05/25/2019 | Responder con el mensaje de bot del módulo de tareas. | [Responder con mensaje de bot del módulo de tareas](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Bots en chats de grupo. | [Interactuar con una bot en el canal o el chat de grupo](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Localización del manifiesto de la aplicación. | [Localización de la aplicación](~/publishing/apps-localization.md) |
| 05/20/2019 | Acciones de mensaje. | [Acciones de mensaje](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Link unfurling (vistas previas de direcciones URL personalizadas). | [Apertura de vínculos](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Programa de certificación de aplicaciones para aplicaciones de la tienda. | [Certificación de aplicaciones](~/publishing/application-certification.md) |
| 05/06/2019 | Las plantillas de aplicación ahora están disponibles. | [Plantillas de aplicaciones](~/samples/app-templates.md) |
| 04/23/2019 | Las extensiones de mensajería basadas en acciones ya están disponibles. | [Extensiones de mensajes basadas en acciones](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | La creación de vínculos profundos a un chat privado está fuera de la vista previa para desarrolladores y disponible. | [Vinculación profunda a un chat](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Superficies SKU y licenceType información en el contexto de la pestaña. | [Contexto de la pestaña](~/concepts/tabs/tabs-context.md) |
| 12/11/2018 | Las pestañas de chat en grupo ahora están disponibles en la versión de lanzamiento de Teams y se han sacado de la vista previa para desarrolladores. Como parte de este trabajo, la sección de pestañas se ha reasignado para que sea más claro.| [Pestañas configurables](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | La introducción a node JS y .NET/C# se ha actualizado para usar App Studio en Teams y se ha agregado una nueva sección sobre el hospedaje de aplicaciones de Teams basadas en nodos en Azure. | Introducción a [la plataforma de Microsoft Teams con C#/.net y app Studio](~/get-started/get-started-dotnet-app-studio.md), Introducción [a la plataforma de Microsoft Teams con node JS y app Studio](~/get-started/get-started-nodejs-app-studio.md), [hospedar la aplicación de Teams de nodos en Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Ahora puede crear vínculos profundos a chats privados entre usuarios. | [Vinculación profunda a un chat](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 08/11/2018 | SharePoint Framework 1,7 ha enviado y con una nueva característica para usar la pestaña de Microsoft Teams como un elemento Web de SharePoint Framework. | [Pestañas de SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Se ha lanzado la característica "módulo de tarea". Un módulo de tareas le permite crear experiencias de elemento emergente modal en su aplicación de Teams, desde bots y pestañas. Dentro del elemento emergente, puede ejecutar su propio código HTML/JavaScript personalizado, mostrar un `<iframe>` widget basado en un complemento de YouTube o Microsoft Stream video, o mostrar una [tarjeta adaptable](https://docs.microsoft.com/adaptive-cards/). | [Introducción al módulo](~/concepts/task-modules/task-modules-overview.md)de tareas, [módulo de tareas en pestañas](~/concepts/task-modules/task-modules-tabs.md), [módulo de tareas en bots](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | La información de formato de las tarjetas se ha actualizado y probado en los clientes de escritorio, iOS y Android para Microsoft Teams. | [Tarjetas](~/concepts/cards/cards.md), [formato de tarjeta](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Las llamadas y las API de reuniones en línea para Microsoft Graph se lanzaron a la versión beta, y las aplicaciones de Teams ahora pueden interactuar con los usuarios de formas enriquecidas mediante voz y vídeo. | [Llamadas y reuniones en línea bots](~/concepts/calls-and-meetings/registering-calling-bot.md), [conceptos de medios en tiempo real](~/concepts/calls-and-meetings/real-time-media-concepts.md), [registro de un bot de llamada](~/concepts/calls-and-meetings/registering-calling-bot.md), [depuración y pruebas locales](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md), [medios hospedados por aplicaciones](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), [control de notificaciones de llamadas entrantes](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Las páginas de configuración de pestañas son ahora significativamente más altas. | [Diseño de pestañas](tabs/design/tabs.md) |
| 08/15/2018 | Las tarjetas adaptables ahora se admiten en Microsoft Teams.|[Acciones de tarjeta adaptable en Microsoft Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Se ha documentado la compatibilidad de clientes para DevTools para Developer Preview.| [DevTools para el cliente de escritorio de Microsoft Teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Las extensiones de mensajería ahora admiten varios comandos. Esta característica se encuentra en la versión preliminar para desarrolladores y ahora se ha lanzado a todos los usuarios.| [composeExtensions. Commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | La configuración en línea ahora es compatible con los conectores. La documentación de los conectores también se ha revisado y ampliado para que sea más claro.| [Conectores](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Ahora, el bot puede enviar y recibir archivos.| [Enviar y recibir archivos a través de su bot](~/concepts/bots/bots-files.md)|
| 07/27/2018 | La vista previa para desarrolladores ahora admite varios comandos en las extensiones de mensajería. | [Se han ampliado las extensiones de mensajería](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Se ha agregado información sobre la nueva certificación de la aplicación a la sección publicación. |[Permisos del manifiesto](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | En la vista previa para desarrolladores, se ha asignado más espacio a la página de configuración de la pestaña. | [La página de configuración de la ficha es significativamente más alta](tabs/design/tabs.md#configuration-page-height)|
| 07/12/2018 | Información sobre el acceso de invitado. | [Acceso de invitado en Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Se ha agregado la información de la versión preliminar del catálogo de aplicaciones del espacio empresarial de Microsoft Teams. | [Publicar la aplicación de Microsoft Teams](~/publishing/apps-publish.md)|
| 05/31/2018 | La versión preliminar para desarrolladores de Microsoft Teams (llamada 3,6) se ha actualizado para incluir la capacidad de agregar bots y fichas a un chat en grupo. | [Características de la vista previa para desarrolladores](~/resources/dev-preview/developer-preview-features.md), [Developer Preview Schema](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Las tarjetas adaptables ahora se admiten en Teams en las acciones de la [tarjeta adaptable en Microsoft Teams](task-modules-and-cards/cards/cards-reference.md). |
| 05/29/2018 | Si usa la [vista previa para desarrolladores](~/resources/dev-preview/developer-preview-intro.md), su bot ahora puede enviar y recibir archivos.| [Enviar y recibir archivos a través de su bot](~/concepts/bots/bots-files.md), [características de la versión preliminar para desarrolladores públicos para Microsoft Teams](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | replyToID se ha agregado a la carga de las `Invoke` `MessageBack` acciones de tarjeta y. Esto es especialmente útil si necesita actualizar el mensaje del que proviene la acción de la tarjeta. | [Acciones de tarjeta](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Se agregó este tema para realizar un seguimiento de los cambios en la interfaz de programación de Microsoft Teams y en este conjunto de documentación. | [Novedades](~/whats-new.md)|
| 04/10/2018 | Se cambiaron las direcciones URL de autenticación para usar de forma coherente el identificador de inquilino en la ruta de acceso. | [Flujo de autenticación para pestañas](~/concepts/authentication/auth-flow-tab.md), [autenticación de pestañas AAD](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Se agregaron instrucciones de diseño para usar el cuadro de comando. |[Cuadro de comando](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Uso de bots para enviar notificaciones para la aplicación. |[Bots de solo notificación](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Documentación ampliada para la mensajería proactiva. |[Inicio de una conversación](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Documentación refactorizada para tarjetas. |[Tarjetas](~/concepts/cards/cards.md), [acciones de tarjetas](~/concepts/cards/cards-actions.md), [formato de tarjeta](~/concepts/cards/cards-format.md), [referencia de tarjetas](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Se ha agregado documentación sobre Teams App Studio. |[Desarrollar rápidamente aplicaciones con Teams App Studio](~/get-started/get-started-app-studio.md) [mediante la biblioteca de controles en App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Se ha agregado un código de ejemplo para demostrar el método AsTeamsChannelAccounts (). |[Obtener contexto para el bot](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Se agregaron temas para empezar a usar C#. |[Introducción a la plataforma de Microsoft Teams con C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Envíe sus preguntas, errores, solicitudes de características y contribuciones

Escuchamos a la comunidad de desarrolladores en [varios canales](feedback.md).
