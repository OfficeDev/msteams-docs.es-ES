---
title: 'Documentación para desarrolladores de Microsoft Teams: glosario'
description: Obtenga información sobre los términos usados en la documentación para desarrolladores de Microsoft Teams
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: f5a8979e9f49fa73430ea9c1d547f462fe8d4e65
ms.sourcegitcommit: 526ad8562d3bacc13141cd7f695aa5f3f3752052
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2022
ms.locfileid: "66737387"
---
# <a name="glossary"></a>Glosario

Términos y definiciones comunes que se usan en la documentación para desarrolladores de Teams.

## <a name="a"></a>A

| Término | Definición |
| --- | --- |
| [Comando de acción](../messaging-extensions/how-to/action-commands/define-action-command.md) | Tipo de aplicación de extensión de mensajería que usa un elemento emergente para recopilar o mostrar información. <br>**Vea también**: [Extensión de mensajería](#m); [Comandos de búsqueda](#s) |
| [Tarjetas adaptables](../task-modules-and-cards/what-are-cards.md) | Fragmento de código de contenido accionable agregado a una conversación por un bot o extensión de mensajería. Use texto, gráficos y botones con estas tarjetas para una comunicación fluida. |
| [Usuario anónimo](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Un tipo de participante en una reunión de Teams que no tiene una identidad de Azure AD y no está federado con un inquilino. Son como usuarios externos en una reunión.<br>**Vea también**: [Usuario federado](#f) |
| [Catálogo de aplicaciones](../toolkit/publish.md) | Un sitio que almacena aplicaciones de SharePoint y Office para el uso interno de una organización. <br>**Vea también**: [SPFx](#s) |
| [Manifiesto de la aplicación](../resources/schema/manifest-schema.md) | El manifiesto de la aplicación de Teams describe cómo se integra la aplicación en el producto de Microsoft Teams. El manifiesto debe cumplir con el [esquema de manifiesto](https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json). |
| [Paquete de la aplicación](../concepts/build-and-test/apps-package.md) | Un paquete de aplicación de Teams es un archivo ZIP que contiene el archivo de manifiesto de la aplicación, el icono de color y el icono de esquema. |
| [Permiso de aplicación](../concepts/device-capabilities/browser-device-permissions.md#enable-apps-device-permissions) | Una opción en una aplicación de Teams para habilitar los permisos del dispositivo. Solo está disponible cuando el archivo de manifiesto de la aplicación declara que la aplicación necesita permisos de dispositivo. <br> **Vea también**: Permisos de dispositivo |
| [Ámbito de la aplicación](../concepts/design/app-structure.md) | Un área de Teams donde los usuarios pueden usar la aplicación. Las aplicaciones pueden tener uno o varios ámbitos, como personales, canales, chats y reuniones. Una aplicación de Teams puede existir entre ámbitos. |
| [App Studio](../concepts/build-and-test/app-studio-overview.md) | Una aplicación para empezar a crear o integrar sus propias aplicaciones de Microsoft Teams. Ahora ha evolucionado a Portal para desarrolladores. <br> > Si ha estado usando App Studio, le recomendamos que pruebe el Portal para desarrolladores para poder configurar, distribuir y administrar las aplicaciones de Teams. App Studio quedará en desuso el 1 de agosto de 2022. <br> **Vea también**: [Portal para desarrolladores](#d) |
| Bandeja de la aplicación | Una bandeja de aplicación ubicada en la barra inferior de una aplicación móvil de Teams. Recopila todas las aplicaciones que están abiertas, pero que no se usan actualmente ni están activas. <br>**Vea también**: [Teams para dispositivos móviles](#t) |
| [Recurso de Azure](../toolkit/provision.md) | Un servicio que está disponible a través de Azure y que la aplicación de Teams puede usar para la implementación de Azure. Podrían ser cuentas de almacenamiento, aplicaciones web, bases de datos y mucho más. |
| [Azure Active Directory](../tabs/how-to/authentication/auth-tab-aad.md) | Servicio de administración de identidades y acceso basado en la nube de Microsoft. Ayuda a los usuarios autenticados a acceder a los recursos internos y externos de Azure. |
| [Autenticación](../concepts/authentication/authentication.md) | Proceso para validar el acceso de usuario para el uso de la aplicación. Se puede realizar mediante la API de Microsoft Graph o la autenticación basada en web. <br> **Vea también**: [Proveedores de identidades](#i); [SSO](#s) |
| [Flujo de autenticación](../concepts/authentication/authentication.md) | En Teams, hay dos flujos de autenticación para autenticar a un usuario para usar una aplicación: la autenticación basada en web y el flujo de OAuthPrompt. |

## <a name="b"></a>N

| Término | Definición |
| --- | --- |
| [Blazor](../get-started/get-started-overview.md) | Marco web gratuito y de código abierto que permite a los desarrolladores crear aplicaciones web con C# y HTML. Lo está desarrollando Microsoft. |
| [Bíceps](../toolkit/provision.md) | Lenguaje declarativo, lo que significa que los elementos pueden aparecer en cualquier orden. A diferencia de los lenguajes imperativos, el orden de los elementos no afecta a cómo se procesa la implementación. |
| [Bot](../bots/what-are-bots.md) | Un bot es una aplicación que ejecuta tareas repetitivas programadas. <br> **Vea también**: [Bot de conversación](#c); [Bot de chat](#c) |
| [Bot emulador](../bots/how-to/debug/locally-with-an-ide.md#use-the-bot-emulator) | Una aplicación de escritorio que le permite probar y depurar bots, ya sea de forma local o remota. |
| [Bot Framework](../bots/bot-features.md) | SDK enriquecido que se usa para crear bots mediante C#, Java, Python y JavaScript. Si tiene un bot basado en el Bot Framework, puede modificarlo para que funcione en Teams. |

## <a name="c"></a>C

| Término | Definición |
| --- | --- |
| [Bot de llamada](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | Un bot que participa en llamadas de audio o vídeo y reuniones en línea. <br> **Vea también**: [Bot de chat](#c); [Bot de reunión](#m) |
| [Funcionalidad](../toolkit/add-capability.md) | Una característica de Teams que puede compilar en la aplicación para interactuar con los usuarios de la aplicación. Una funcionalidad de la aplicación se usa para ampliar Teams para adaptarse a las necesidades de la aplicación. Una aplicación puede tener una o varias funcionalidades principales, como la pestaña, el bot y la extensión de mensajería. <br>**Vea también**: [Funcionalidad del dispositivo](#d); [Funcionalidad multimedia](#m) |
| [Bot de chat](../bots/how-to/conversations/conversation-basics.md) | Un bot también se conoce como bot de chat o bot de conversación. Se trata de una aplicación que ejecuta tareas sencillas y repetitivas por parte de usuarios como el servicio de atención al cliente o el personal de soporte técnico. <br> **Vea también**: [Bot de conversación](#c) |
| Canal | Un único lugar para que un equipo comparta mensajes, herramientas y archivos. Puede usar un canal para el trabajo en equipo y la comunicación. <br>**Vea también**: [Conversación](#c) |
| [Secreto de cliente](../bots/how-to/authentication/add-authentication.md) | El secreto de cliente o contraseña o un par de claves públicas o privadas que sean Certificadas. No es necesario para las aplicaciones nativas. <br> **Vea también**: [Bot](#b) |
| [Recursos en la nube](../toolkit/add-resource.md) | Un servicio que está disponible en la nube a través de Internet que la aplicación de Teams puede usar. Podrían ser cuentas de almacenamiento, aplicaciones web, bases de datos y mucho más. |
| [Aplicación de colaboración](../concepts/extensibility-points.md) | Una aplicación con funcionalidades para que un usuario trabaje en un área de trabajo de colaboración con otros usuarios. <br> **Vea también**: [Aplicación independiente](#s) |
| [Extensión de redacción](../resources/schema/manifest-schema.md#composeextensions) | Propiedad del manifiesto de la aplicación (`composeExtensions`) que hace referencia a la funcionalidad de extensión de mensajería. Se usa cuando la extensión necesita autenticarse o configurarse para continuar. <br>**Vea también**: [Manifiesto de la aplicación](#a); [Extensión de mensajería](#m) |
| [Cuadro de comandos](../resources/schema/manifest-schema.md) | Tipo de contexto en el manifiesto de la aplicación (`commandBox`) que puede configurar para invocar una extensión de mensajería desde el cuadro de comandos de Teams. |
| [Connector](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | Permite a los usuarios suscribirse para recibir notificaciones y mensajes de los servicios web. Los conectores exponen el punto de conexión HTTPS para que el servicio publique mensajes en canales de Teams, normalmente en forma de tarjetas. <br> **Vea también**: [Webhook](#w) |
| Conversación | Una serie de mensajes enviados entre la aplicación de Microsoft Teams (pestaña o bot) y uno o varios usuarios. Una conversación puede tener tres ámbitos: canal, chat personal y grupal. <br>**Vea también**: [Chat uno a uno](#o); [Chat en grupo](#g); [Canal](#c) |
| [Bot de conversación](../bots/how-to/conversations/conversation-messages.md) |  Permite a un usuario interactuar con el servicio web mediante texto, tarjetas interactivas y módulos de tareas. <br>**Vea también**[Bot de chat](#c) |

## <a name="d"></a>D

| Término | Definición |
| --- | --- |
| [Vinculación en profundidad](../concepts/build-and-test/deep-links.md) | En una aplicación de Teams, puede crear vínculos profundos a información y características dentro de Teams o para ayudar al usuario a navegar al contenido de la aplicación. |
| [Portal para desarrolladores de Teams](../concepts/build-and-test/teams-developer-portal.md) | La herramienta principal para configurar, distribuir y administrar las aplicaciones de Microsoft Teams. Con el Portal para desarrolladores, puede colaborar con compañeros en la aplicación, configurar entornos en tiempo de ejecución y mucho más. |
| [Versión preliminar para desarrolladores](../resources/dev-preview/developer-preview-intro.md) | Un programa público para desarrolladores que proporciona acceso anticipado a características no publicadas en Microsoft Teams. Le permite explorar y probar las próximas características para su posible inclusión en la aplicación de Microsoft Teams. |
| Implementar | Proceso para cargar el código de back-end y front-end de la aplicación. En la implementación, el código de la aplicación se copia en los recursos que creó durante el aprovisionamiento. <br>**Vea también**: [Aprovisionar](#p) |
| [Funciones del dispositivo](../concepts/device-capabilities/device-capabilities-overview.md) | Dispositivos integrados, como cámara, micrófono, escáner de código de barras, galería de fotos, en un dispositivo móvil o de escritorio. Puede acceder a las siguientes funcionalidades de dispositivo en dispositivos móviles o de escritorio a través de API dedicadas disponibles en el SDK de cliente de JavaScript de Microsoft Teams. <br>**Vea también**: [Funcionalidad](#c); [Funcionalidad multimedia](#m); [Funcionalidad de ubicación](#l) |
| [Permiso de dispositivo](../concepts/device-capabilities/browser-device-permissions.md) | Una configuración de aplicación de Teams que puede configurar en la aplicación. Se usa para solicitar permiso para que la aplicación acceda a una funcionalidad nativa del dispositivo y la use. Puede administrar los permisos del dispositivo en la configuración de Teams. <br>**Vea también**: [Permisos de aplicación](#a) |
| [Entorno de desarrollo](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Tipo de entorno de desarrollo que el kit de herramientas de Teams crea de forma predeterminada. Representa configuraciones de entorno remoto o en la nube. Un proyecto puede tener varios entornos remotos. Puede agregar más entornos de desarrollo al proyecto mediante el kit de herramientas de Teams. <br>**Vea también** [Entorno](#e); [Entorno local](#l) |
| [DevTools](../tabs/how-to/developer-tools.md) | Las herramientas de desarrollo del explorador se usan para ver registros de consola, ver o modificar solicitudes de red en tiempo de ejecución, agregar puntos de interrupción al código (JavaScript) y realizar la depuración interactiva para una aplicación de Teams. La característica solo está disponible para clientes de escritorio y Android una vez habilitada la versión preliminar para desarrolladores. |
| [Búsqueda dinámica](../task-modules-and-cards/cards/dynamic-search.md#dynamic-typeahead-search) | Característica de búsqueda para tarjetas adaptables que resulta útil para buscar y seleccionar datos de grandes conjuntos de datos. Ayuda a filtrar las opciones a medida que el usuario escribe la cadena de búsqueda. <br>**Vea también**: [Búsqueda estática](#s) |

## <a name="e"></a>E

| Término | Definición |
| --- | --- |
| [Cuenta de desarrollador de E5](../toolkit/accounts.md) | Suscripción de desarrollador de E5 para crear aplicaciones para ampliar Microsoft 365. Incluye 25 licencias de usuario, incluido el administrador, solo con fines de desarrollo.  <br>**Vea también**: [Cuenta de Microsoft 365](#m) |
| [Punto de entrada](../concepts/app-fundamentals-overview.md) | Un punto de acceso, como equipo, canal y chat, para una aplicación de Teams donde los usuarios pueden usar la aplicación. |
| [Entorno](../toolkit/teamsfx-multi-env.md) | Una característica del kit de herramientas de Teams que le permite crear y usar varios entornos de desarrollo para el proyecto de aplicación. Hay dos entornos de desarrollo que el kit de herramientas de Teams crea de forma predeterminada, el entorno local y el entorno de desarrollo. <br>**Vea también**: [Entorno local](#l); [Entorno de desarrollo](#d) |

## <a name="f"></a>F

| Término | Definición |
| --- | --- |
| [Usuario federado](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Un tipo de usuario en una reunión de aplicación de Teams que es externo y está invitado a la reunión. Este usuario tiene credenciales válidas federadas por asociados autorizados de Teams. También se denominan usuarios externos. <br>**Vea también**: [Usuario anónimo](#a) |

## <a name="g"></a>G

| Término | Definición |
| --- | --- |
| [Graph API](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | Una API web RESTful para Microsoft Graph que le permite acceder a los recursos del servicio en la nube de Microsoft. <br>**Vea también**: [Probador de Microsoft Graph](#m) |
| [Chat de grupo](../resources/bot-v3/bot-conversations/bots-conversations.md) | Una característica de chat en la que un usuario puede chatear con un bot en una configuración de grupo mediante @mention para invocar el bot. <br>**Vea también**: [Chat uno a uno](#o); [Bot de chat](#c) |

## <a name="i"></a>I

| Término | Definición |
| --- | --- |
| [Proveedor de identidad](../concepts/authentication/configure-identity-provider.md) | Entidad que almacena y proporciona credenciales al usuario. Los usuarios también pueden registrarse con un proveedor de identidades.  <br>**Vea también**: [Autenticación](#a) |
| [Webhook entrante](../webhooks-and-connectors/how-to/add-incoming-webhook.md) | Permite que una aplicación externa comparta contenido en canales de Teams. Estos webhooks se usan como herramientas de seguimiento y notificación. <br>**Vea también**: [Webhook](#w); [Webhook saliente](#o) |
| [Experiencia de la aplicación durante la reunión](../apps-in-teams-meetings/meeting-app-extensibility.md#in-meeting-app-experience) | Una fase del ciclo de vida de una reunión de Teams. Con la experiencia de la aplicación durante la reunión, puedes interactuar con los participantes durante la reunión mediante las aplicaciones y el cuadro de diálogo durante la reunión.<br>**Vea también**: [Ciclo de vida de la reunión](#m) |

## <a name="l"></a>L

| Término | Definición |
| --- | --- |
| [Apertura de vínculos](../messaging-extensions/how-to/link-unfurling.md) | Característica que se usa con la extensión de mensajería y la reunión para expandir vínculos pegados en un área de redacción de mensajes. Los vínculos se expanden para mostrar información adicional sobre el vínculo en tarjetas adaptables o en la vista de la fase de reunión. |
| [Entorno local](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Un entorno de desarrollo predeterminado creado por el kit de herramientas de Teams.  <br>**Vea también**: [Entorno](#e); [Entorno de desarrollo](#d) |
| [Área de trabajo local](../sbs-gs-spfx.yml) | La opción predeterminada para ejecutar y depurar una aplicación de Teams en Visual Studio Code que se crea con SPFx. <br>**Vea también**: [Workbench](#w); [Teams workbench](#t) |
| [Funcionalidad de ubicación](../concepts/device-capabilities/location-capability.md) | Una funcionalidad de dispositivo que puede integrar con la aplicación para conocer la ubicación geográfica del usuario de la aplicación para obtener una experiencia de colaboración mejorada. Esta funcionalidad actualmente solo está disponible para los clientes de dispositivos móviles de Teams.<br>**Vea también**: [Funcionalidad](#c); [Funcionalidad multimedia](#m); [Funcionalidad del dispositivo](#d); [Teams Móvil](#t) |
| [Aplicaciones de código bajo](../samples/teams-low-code-solutions.md) | Una aplicación personalizada de Teams creada desde cero con Microsoft Power Platform que requiere poca o ninguna codificación, y que se puede desarrollar e implementar rápidamente. |

## <a name="m"></a>M

| Término | Definición |
| --- | --- |
| [Funcionalidad multimedia](../concepts/device-capabilities/media-capabilities.md) | Capacidades nativas del dispositivo, como la cámara y el micrófono, que puede integrar con su aplicación de Teams. <br>**Vea también**: [Funcionalidad](#c); [Funcionalidad del dispositivo](#d) |
| [Bot de reunión](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | Bots que interactúan con llamadas y reuniones de Teams mediante el uso compartido de pantalla, vídeo y voz en tiempo real. <br>**Vea también**: [Bot de llamada](#c); [Bot de chat](#c) |
| [Ciclo de vida de la reunión](../apps-in-teams-meetings/meeting-app-extensibility.md#meeting-lifecycle) | Abarca desde la experiencia de aplicación previa a la reunión, en la reunión y posterior a la reunión. Se pueden integrar pestañas, bots y extensiones de mensajería en cada fase del ciclo de vida de la reunión. <br>**Vea también**: [Experiencia en la reunión](#i) |
| [Fase de reunión](../sbs-meetings-stage-view.yml) | Una característica de la aplicación de extensión de reunión. Es un espacio compartido accesible para todos los participantes durante la reunión. Ayuda a los participantes a interactuar y colaborar con el contenido de la aplicación en tiempo real. <br>**Vea también**: [Vista fase](#s) |
| [Extensión de mensajería](../messaging-extensions/what-are-messaging-extensions.md) | Las extensiones de mensajería son métodos abreviados para insertar contenido de la aplicación o realizar una acción en un mensaje. Puede usar una extensión de mensajería sin salir de la conversación. <br>**Vea también**: [Comandos de búsqueda](#s); [Comandos de acción](#a) |
| [Extensión de reunión](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) | Una aplicación diseñada para usarse durante el ciclo de vida de la reunión para que sea más productiva, como pizarra, panel y mucho más. |
| [Cuenta de Microsoft 365](../toolkit/accounts.md#microsoft-365-developer-account-types) | La cuenta de Microsoft 365 incluye 25 licencias de usuario, incluido el administrador, solo con fines de desarrollo. |
| [Programa de desarrolladores de Microsoft 365](../toolkit/accounts.md)| El programa para desarrolladores de Microsoft 365 le ayuda a crear aplicaciones que amplían Microsoft 365. |
| [Explorador de Microsoft Graph](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | La puerta de enlace a los datos y la inteligencia a Microsoft 365.Proporciona un modelo de programación unificado que puede usar para aprovechar la gran cantidad de datos en Microsoft 365, Enterprise Mobility + Security y Windows 10. |
| [Microsoft Teams](../overview.md) | Microsoft Teams es un software de colaboración en grupo que se puede usar para ayudar a los equipos a trabajar juntos de forma remota. |
| [Plataforma de Microsoft Teams](../concepts/app-fundamentals-overview.md) | La plataforma para desarrolladores de Microsoft Teams facilita a los desarrolladores la integración de sus propias aplicaciones y servicios con Teams. |
| [Microsoft Teams de interfaz de usuario](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | La biblioteca de interfaz de usuario de Microsoft Teams le ayuda a ver y probar plantillas de interfaz de usuario de Teams individuales y componentes relacionados en el explorador. |
| [Kit de herramientas de la interfaz de usuario de Microsoft Teams](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | El kit de interfaz de usuario de Microsoft Teams incluye componentes y patrones diseñados específicamente para crear aplicaciones de Teams. |

## <a name="o"></a>O

| Término | Definición |
| --- | --- |
| [Conector de Office 365](../webhooks-and-connectors/how-to/connectors-creating.md) | Le permite crear una página de configuración personalizada para el webhook entrante y empaquetarla como parte de una aplicación de Teams. Puede enviar mensajes principalmente mediante tarjetas del Conector de Office 365 y tener la capacidad de agregarles un conjunto limitado de acciones de tarjeta. |
| [Webhook saliente](../webhooks-and-connectors/how-to/add-outgoing-webhook.md) | Actúa como un bot y busca mensajes en canales mediante @mention. Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes. <br>**Vea también**: [Webhook](#w); [Webhook entrante](#i) |
| [Canal de Outlook](../m365-apps/extend-m365-teams-message-extension.md#add-an-outlook-channel-for-your-bot) | Una característica de la aplicación de extensión de mensajería de Teams que permite a los usuarios interactuar con esta desde Microsoft Outlook. |
| [Chat uno a uno](../resources/bot-v3/bot-conversations/bots-conv-personal.md) | Un tipo de chat entre una aplicación de bot personal de Teams y un solo usuario. <br>**Vea también**: [Chat en grupo](#g); [Bot de chat](#c) |

## <a name="p"></a>P

| Término | Definición |
| --- | --- |
| [Selector de personas](../task-modules-and-cards/cards/people-picker.md) | Un control nativo en la plataforma de Teams para buscar y seleccionar personas, que se puede integrar en aplicaciones web, tarjetas adaptables y mucho más. |
| [Aplicación personal](../concepts/design/personal-apps.md) | Una aplicación personal es una aplicación de Teams con un ámbito personal. Se centra en las interacciones con un único usuario. Puede ser un bot de conversación para participar en conversaciones uno a uno con un usuario o una pestaña personal que proporcione una experiencia web insertada, o ambas. <br>**Vea también**: [Aplicación compartida](#s) |
| [Power Virtual Agents](../bots/how-to/add-power-virtual-agents-bot-to-teams.md) | Una solución de interfaz gráfica guiada sin código que permite a todos los miembros de su equipo crear bots de chat enriquecidos y conversacionales que se integren fácilmente con la plataforma de Teams. |
| [Mensajes proactivos](../bots/how-to/conversations/send-proactive-messages.md) | Un mensaje enviado por un bot que no está en respuesta a una solicitud de un usuario, como mensajes de bienvenida, notificaciones y mensajes programados. |
| [Aprovisionar](../toolkit/provision.md) | Proceso que crea recursos en Azure y Microsoft 365 para la aplicación, pero no se copia ningún código (HTML, CSS, JavaScript, etc.) en los recursos. Es un requisito previo para la implementación.<br>**Vea también**: [Implementar](#d) |

## <a name="r"></a>R

| Término | Definición |
| --- | --- |
| [Limitación de velocidad](../bots/how-to/rate-limit.md) | Un método para limitar los mensajes a una frecuencia máxima determinada para asegurarse de que el número de mensajes es suficiente y no aparece como correo no deseado. |
| [Vistas basadas en roles](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md) | Una característica de pestañas en las que la experiencia de pestaña puede ser diferente para los usuarios en función de su nivel de permisos. |
| [Permiso de RSC](../graph-api/rsc/resource-specific-consent.md) | Los propietarios del equipo necesitan la característica de permiso de consentimiento específico del recurso (RSC) para permitir que una aplicación de bot reciba mensajes a través de canales de un equipo sin ser @mentioned. |

## <a name="s"></a>S

| Término | Definición |
| --- | --- |
| [Comandos de búsqueda](../messaging-extensions/how-to/search-commands/define-search-command.md) | Tipo de aplicación de extensión de mensajería que permite a los usuarios buscar sistemas externos e incluir el resultado de la búsqueda en un mensaje mediante una tarjeta. <br>**Vea también**: [Extensiones de mensajería](#m); [Comandos de acción](#a) |
| [Flujo de trabajo secuencial](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md) | Flujo de trabajo que permite a un bot llevar a cabo una conversación con un usuario en función de la respuesta del usuario. |
| [Aplicación compartida](../concepts/extensibility-points.md#shared-app-experiences) | Una aplicación que existe en un equipo, canal o chat donde los usuarios pueden colaborar e interactuar. <br>**Vea también:** Aplicación personal |
| [Colección de sitios de SharePoint](../sbs-gs-spfx.yml) | Un sitio de colecciones para las aplicaciones de SharePoint. Debe tener una cuenta de administrador para este sitio para poder implementar la aplicación basada en SPFx en el sitio de SharePoint.<br>**Vea también**: SPFx |
| [Instalación de prueba](../toolkit/publish.md#publish-to-individual-scope-or-sideload-permission) | Proceso en el que se carga una aplicación de Teams al cliente de Teams para probarla en el entorno de Teams antes de distribuirla. |
| [SidePanel](../sbs-meetings-sidepanel.yml) | Característica de la aplicación de reunión de Teams que le permite personalizar experiencias en una reunión que permiten a los organizadores y moderadores tener un conjunto diferente de vistas y acciones. |
| [SPFx](../sbs-gs-spfx.yml) | SharePoint Framework (SPFx) es un modelo de desarrollo para crear soluciones del lado cliente para Microsoft Teams y SharePoint. |
| SSO | Acrónimo de Inicio de sesión único, un método de autenticación en el que un usuario necesita iniciar sesión en un servicio independiente de una plataforma de software (como Microsoft 365) solo una vez. Después, el usuario puede acceder a todos los servicios sin tener que volver a realizar la autenticación. <br>**Vea también**: [Autenticación](#a) |
| [Vista de fase](../sbs-meetings-stage-view.yml) | Un componente de interfaz de usuario que le permite representar el contenido que se abre en pantalla completa en Teams y se ancla como una pestaña. Se invoca para mostrar contenido web dentro de Teams. Tenga en cuenta que *no* es lo mismo que la fase de reunión. <br>**Vea también**: [Fase de reunión](#m) |
| [Aplicación independiente](../samples/integrating-web-apps.md) | Una aplicación de página única o grande y compleja. El usuario puede usar algunos aspectos de él en Teams. <br>**Vea también**: [Colaboración aap](#c) |
| [Búsqueda estática](../task-modules-and-cards/cards/dynamic-search.md) | Método de búsqueda de escritura anticipada que permite a los usuarios buscar desde valores especificados previamente en la carga de tarjetas adaptables. <br>**Vea también**: [Búsqueda dinámica](#d) |
| [Directrices de validación de la tienda](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) | Un conjunto de directrices específicas de Teams para validar una aplicación antes de que se pueda enviar a la tienda de Teams. <br>**Vea también**: [Tienda de Teams](#t) |

## <a name="t"></a>T

| Término | Definición |
| --- | --- |
| [Tab](../tabs/what-are-tabs.md) | Las pestañas son páginas web compatibles con Teams insertadas en Microsoft Teams que apuntan a dominios declarados en el manifiesto. Puede agregarlo dentro de un equipo, chat de grupo o aplicación personal. |
| [Chat de pestaña](../tabs/how-to/conversational-tabs.md) | Tipo de pestaña que permite a un usuario tener una experiencia de conversación centrada en pestañas dinámicas. |
| [Módulos de tareas](../task-modules-and-cards/what-are-task-modules.md) | Una característica de la aplicación de Teams para crear un elemento emergente modal para completar tareas, mostrar vídeos o panel. |
| [Discusión del subproceso](../tabs/design/tabs.md#thread-discussion) | Una conversación publicada en un canal o chat entre usuarios. <br>**Vea también** [Conversación](#c); [Canal](#c) |
| [Teams](../overview.md) | Microsoft Teams es la aplicación más sofisticada de mensajería para su organización. Se trata de un espacio de trabajo pensado para la colaboración en tiempo real y la comunicación, las reuniones y el uso compartido de archivos y aplicaciones. |
| [Kit de herramientas de Teams](../toolkit/teams-toolkit-fundamentals.md) | El kit de herramientas de Microsoft Teams le permite crear aplicaciones personalizadas de Teams directamente desde el entorno de Visual Studio Code.  |
| [TeamsFx](../toolkit/teamsfx-cli.md) | TeamsFx es una interfaz de línea de comandos basada en texto que acelera el desarrollo de aplicaciones de Teams. También se denomina CLI de TeamsFx.|
| [TeamsFx SDK](../toolkit/teamsfx-sdk.md) | El SDK de TeamsFx está preconfigurado en un proyecto con scaffolding mediante el kit de herramientas de TeamsFx o la CLI. |
| [SDK de TeamsJS](../tabs/how-to/using-teams-client-sdk.md) | El SDK de TeamsJS le permite crear experiencias hospedadas en Teams. A partir de TeamsJS v.2.0.0, puede ampliar las aplicaciones de Teams para que se ejecuten en Outlook y Office. |
| [Teams para dispositivos móviles](../concepts/design/plan-responsive-tabs-for-teams-mobile.md) | Microsoft Teams está disponible como una aplicación móvil. |
| [Tienda de Teams](../concepts/deploy-and-publish/appsource/publish.md) | Página de aterrizaje de la tienda que lleva las aplicaciones a los usuarios en un solo lugar. Las aplicaciones se clasifican por uso, sector y mucho más. Una aplicación debe seguir las directrices de validación de la Tienda y obtener una aprobación antes de que esté disponible para los usuarios a través de la tienda de Teams.  <br>**Vea también**: [Directrices de validación de la tienda](#s) |
| [Mesa de trabajo de Teams](../sbs-gs-spfx.yml) | Un área de trabajo en Visual Studio Code usa en la compilación de aplicaciones de Teams creadas con SPFx y el kit de herramientas de Teams. <br>**Vea también**: [Mesa de trabajo](#w); [Mesa de trabajo local](#l) |

## <a name="u"></a>U

| Término | Definición |
| --- | --- |
| [Componentes de la interfaz de usuario](../concepts/design/design-teams-app-basic-ui-components.md) | Para el desarrollo de aplicaciones de Teams, puede usar componentes de la interfaz de usuario de Fluent para compilar la aplicación desde cero. |
| [Plantillas de la interfaz de usuario](../concepts/design/design-teams-app-ui-templates.md) | Para el desarrollo de aplicaciones de Teams, puede usar plantillas de interfaz de usuario de Teams para diseñar sus aplicaciones rápidamente. |
| [Acciones universales para tarjetas adaptables](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) | Una manera de implementar tarjetas adaptables entre plataformas y aplicaciones. Usa un bot como back-end común para controlar las acciones. |

## <a name="v"></a>V

| Término | Definición |
| --- | --- |
| [Virtual Assistant](../samples/virtual-assistant.md) | Una plantilla de código abierto de Microsoft que le permite crear una solución conversacional sólida. |

## <a name="w"></a>W

| Término | Definición |
| --- | --- |
| [URL del sitio web](../tabs/design/tabs-mobile.md) | Propiedad del archivo de manifiesto de la aplicación (`websiteUrl`) que vincula la aplicación al sitio web de la organización o a la página de aterrizaje del producto correspondiente. Es una configuración obligatoria para el cliente de dispositivos móviles de Teams. <br>**Vea también**: [Manifiesto de la aplicación](#a); [Teams para dispositivos móviles](#t) |
| [Aplicación web](../samples/integrate-web-apps-overview.md) | Una aplicación que se ejecuta en un servidor web. Se puede integrar con la Plataforma de Microsoft Teams. |
| [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | Es una característica de una aplicación de Teams que se usa para integrarla con aplicaciones externas. <br>**Vea también**: Webhook entrante; webhook saliente |
| [Elemento web](../sbs-gs-spfx.yml) | Componente de interfaz de usuario que se usa para crear una página o un sitio en una aplicación de Teams creada con Visual Studio Code y SharePoint Framework. <br>**Vea también**: [SPFx](#s) |
| [Mesa de trabajo](../sbs-gs-spfx.yml) | En general, Visual Studio Code interfaz de usuario que abarca los componentes de la interfaz de usuario, como la barra de título, el panel y mucho más. <br>**Vea también**: [Mesa de trabajo local](#l); [Mesa de trabajo de Teams](#t) |

## <a name="y"></a>v

| Término | Definición |
| --- | --- |
| [YoTeams](../get-started/get-started-overview.md) | Kit de herramientas de desarrollo para compilar aplicaciones de Microsoft Teams basadas en TypeScript y node.js. |
