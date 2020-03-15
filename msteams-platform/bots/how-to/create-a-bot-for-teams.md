---
title: Crear un bot para Microsoft Teams
author: clearab
description: Cómo crear un bot para Microsoft Teams.
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: b9999fb8fcb39b4cd70789d909fecd9cad13e5d7
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "42635301"
---
# <a name="create-a-bot-for-microsoft-teams"></a>Crear un bot para Microsoft Teams

Debe completar los pasos siguientes para crear un bot de conversación:

1. Preparar el entorno de desarrollo.
1. Crear su servicio web.
1. Registrar el servicio web como un bot con Microsoft Bot Framework.
1. Crear el manifiesto de la aplicación y su paquete de aplicación.
1. Cargar el paquete en Microsoft Teams.

La creación de un servicio web, el registro de un servicio web y la creación de un paquete de aplicación, se pueden realizar en cualquier orden con Bot Framework. Sin embargo, como las tres partes están tan entrelazadas, no importa en qué orden se realicen, tendrá que volver a actualizar las demás. El registro necesita el punto final de la mensajería del servicio web implementado y el servicio web necesita el ID. y la contraseña creados a partir del registro. El manifiesto de la aplicación también necesita el identificador de registro para conectar Teams al servicio web.

Durante la creación de la aplicación, se desplazará de forma periódica entre los cambios en el manifiesto de la aplicación y la implementación del código en el servicio web. Al trabajar con el manifiesto de la aplicación, tenga en cuenta que puede manipular manualmente el archivo JSON o realizar cambios mediante App Studio. En ambos casos, tendrá que volver a implementar (cargar) la aplicación en Teams cuando realice un cambio en el manifiesto. Sin embargo, no hay necesidad de hacerlo al implementar cambios en el servicio web.

Para obtener más información sobre Bot Framework, vea la [Documentación de Bot Framework](/azure/bot-service/).

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Crear su servicio web

El corazón de su bot es su servicio web. Definirá una única ruta, normalmente `/api/messages`, en la que recibir todas las solicitudes. Para empezar, tiene algunas opciones entre las que elegir:

* Comience con la muestra de bot de conversación de Teams en [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) o [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot).
* Si usa JavaScript, use el [generador Yeoman para Microsoft Teams](https://github.com/OfficeDev/generator-teams) para el scaffolding de la aplicación de Teams, incluido el servicio web. Esto es especialmente útil al crear una aplicación de Teams que contiene más de un bot de conversación.
* Crear su servicio web desde cero. Puede optar por agregar el SDK de Bot Framework para su idioma, o bien puede trabajar directamente con las cargas JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Registrar el servicio web con Bot Framework

> [!IMPORTANT]
> Al registrar el servicio web, asegúrese de establecer la **Nombre para mostrar** en el mismo nombre que utilizó para su **Nombre corto** en el manifiesto de la aplicación. Cuando la aplicación se distribuya por carga directa o a través del catálogo de aplicaciones de la organización, los mensajes que su bot envíe a una conversación usarán el **Nombre para mostrar** en lugar del **Nombre abreviado** de la aplicación.

El registro del servicio web con Bot Framework ofrece un canal de comunicación seguro entre el cliente de Teams y el servicio web. El cliente de Teams y el servicio web nunca se comunican directamente. En su lugar, los mensajes se redirigen a través del servicio de Bot Framework (Microsoft Teams usa una instancia distinta de este servicio y que cumple con los estándares de Office 365).

Hay dos opciones al registrar el servicio web con Bot Framework. Puede usar [App Studio](#using-app-studio) o el [portal heredado](#in-the-legacy-portal) para registrar su bot sin usar una suscripción de Azure. O bien, si ya tiene una suscripción a Azure (o no le importa crear una), puede usar [Microsoft Azure Portal](#with-an-azure-subscription) para registrar el servicio web.

### <a name="without-an-azure-subscription"></a>Sin una suscripción de Azure

Si no desea crear el registro de bots en Azure, **debe** usar este vínculo (https://dev.botframework.com/bots/new) o App Studio. Si hace clic en el botón *Crear un bot* en el portal de Bot Framework, se creará el registro de bots en Microsoft Azure y tendrá que proporcionar una suscripción de Azure. Para administrar el registro o migrarlo a una suscripción de Azure tras la creación, vaya a: https://dev.botframework.com/bots.

Al editar las propiedades de un registro de Bot Framework existente que no se registró en Azure, verá una columna "Estado de la migración" y un botón "Migrar" azul que le llevará a Microsoft Azure Portal. No seleccione el botón "Migrar", a menos que sea lo que quiere hacer. En su lugar, seleccione el **nombre** del bot y podrá editar sus propiedades:

   ![Editar propiedades del bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)

Situaciones en las que **debe** tener el registro del bot en Azure (ya sea creándolo en Microsoft Azure Portal o por migración):

* Quiera usar [OAuthPrompt](./authentication/auth-flow-bot.md) de Bot Framework para la autenticación.
* Quiere habilitar canales adicionales como chat web, línea directa o Skype.

#### <a name="using-app-studio"></a>Usar App Studio

*App Studio* es una aplicación de Teams que le ayuda a crear aplicaciones de Teams, incluido el registro de su servicio web como bot, la creación de un manifiesto de la aplicación y el paquete de la aplicación, y la actualización de configuraciones y opciones. También contiene una biblioteca de control React y ejemplos configurables para tarjetas. Consulte [Introducción a Teams App Studio](../../concepts/build-and-test/app-studio-overview.md).

Recuerde que si usa App Studio para registrar el servicio web, tendrá que ir a https://dev.botframework.com/bots para administrar el registro.

#### <a name="in-the-legacy-portal"></a>En el portal heredado

Cree el registro del bot con este vínculo: https://dev.botframework.com/bots/new. **Asegúrese de agregar Microsoft Teams como canal de la lista de canales destacados después de crear el bot.** Puede volver a usar cualquier identificador de aplicación de Microsoft que haya generado si ya ha creado el manifiesto o el paquete de la aplicación.

   ![Página de registro de Bot Framework](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a>Con una suscripción de Azure

También puede registrar el servicio web creando un recurso de registro de canales de bots en Microsoft Azure Portal.

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

El [portal de Bot Framework](https://dev.botframework.com) se ha optimizado para el registro de bots en Microsoft Azure. Estos son algunos aspectos que debe tener en cuenta:

* El canal de Microsoft Teams para bots registrados en Azure es **gratuito**. Los mensajes que se envían a través del canal de Teams no se contabilizarán como mensajes consumidos para el bot.
* Si registra el bot con Microsoft Azure, no es necesario que el código del bot se *hospede* en Microsoft Azure.
* Si registra un bot con Microsoft Azure Portal, debe tener una cuenta de Microsoft Azure. Puede [crear una de forma gratuita](https://azure.microsoft.com/free/). Para comprobar su identidad al crear una cuenta de Azure, debe proporcionar una tarjeta de crédito, pero no se realizará ningún cargo. Siempre es gratuito crear y usar bots con Microsoft Teams.

## <a name="create-your-app-manifest-and-package"></a>Crear un manifiesto y un paquete de aplicación

El [manifiesto de la aplicación](~/resources/schema/manifest-schema.md) define los metadatos de la aplicación, los puntos de extensión que usa la aplicación, y los punteros a los servicios web a los que se conectan los puntos de extensión. Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo de forma manual.

### <a name="add-using-app-studio"></a>Agregar con App Studio

1. En el cliente de Teams, abra App Studio en el menú de desbordamiento **...** del raíl de navegación izquierdo. Si App Studio aún no está instalado, puede instalarlo si lo busca.
2. En la pestaña **Editor de manifiestos**, seleccione **Crear una nueva aplicación** (o bien, si está agregando un bot a una aplicación existente, puede importar el paquete de la aplicación).
3. Agregue los detalles de la aplicación (consulte [definición de esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener las descripciones completas de cada campo).
4. En la pestaña **Bots**, haga clic en el botón **Configuración**.
5. Puede crear un nuevo registro de un servicio web (**Nuevo bot**), o bien, si ya ha registrado uno, seleccione **Bot existente**.
6. Seleccione las funciones y el alcance que necesitará el bot.
7. Si es necesario, actualice la dirección del extremo del bot para que apunte a su bot. Debería tener un aspecto similar a `https://someplace.com/api/messages`.
8. Si quiere, agregue [comandos de bot](~/bots/how-to/create-a-bot-commands-menu.md).
9. De forma opcional, puede descargar el paquete de la aplicación finalizado desde la pestaña **Probar y distribuir**.

### <a name="create-it-manually"></a>Crearlo manualmente

Al igual que con las pestañas y extensiones de mensajería, se actualiza el [manifiesto de la aplicación](~/resources/schema/manifest-schema.md) para definir el bot. Agregue nueva estructura JSON de nivel superior en el manifiesto de la aplicación con la propiedad `bots`.

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`botId`|String|64 caracteres|✔|El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Este puede ser el mismo que el identificador de aplicación general.|
|`needsChannelSelector`|Booleano|||Describe si el bot usa una sugerencia del usuario para agregar el bot a un canal específico. Valor predeterminado: `false`.|
|`isNotificationOnly`|Booleano|||Indica si un bot es un bot unidireccional de solo notificación o un bot de conversación. Valor predeterminado: `false`.|
|`supportsFiles`|Booleano|||Indica si el bot es compatible con la capacidad para cargar y descargar archivos en chat personal. Valor predeterminado: `false`.|
|`scopes`|Matriz de enumeración|3|✔|Especifica si el bot ofrece una experiencia en el contexto de un canal en un `team`, en un chat de grupo (`groupchat`) o una experiencia específica para un solo usuario (`personal`). Estas opciones no son exclusivas.|

De forma opcional, puede definir una o varias listas de comandos que el bot puede recomendar a los usuarios. El objeto es una matriz (con un máximo de 2 elementos) y todos los elementos de tipo `object`. Debe definir una lista de comandos independiente para cada ámbito que sea compatible con el bot. Para obtener más información, *consulte* [Menús de bot](./create-a-bot-commands-menu.md).

|Nombre| Tipo| Tamaño máximo | Necesario | Descripción|
|---|---|---|---|---|
|`items.scopes`|matriz de enumeración|3|✔|Especifica el ámbito para el que la lista de comandos es válida. Las opciones son `team`, `personal` y `groupchat`.|
|`items.commands`|matriz de objetos|10|✔|Una matriz de comandos que el bot admite:<br>`title`: el nombre de comando del bot (cadena, 32)<br>`description`: una descripción o un ejemplo sencillo de la sintaxis del comando y su argumento (cadena, 128).|

#### <a name="simple-manifest-example"></a>Ejemplo de manifiesto simple

El ejemplo siguiente es un objeto de bot simple, con dos listas de comandos definidas. Este no es el archivo de manifiesto de la aplicación completo, solo la parte específica para las extensiones de mensajería.

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a>Crear el paquete de aplicación manualmente

Para crear un paquete de aplicación, debe agregar el manifiesto de la aplicación y, opcionalmente, los iconos de la aplicación a un archivo de almacenamiento .zip. Vea [Crear un paquete de aplicación](~/concepts/build-and-test/apps-package.md) para obtener más detalles. Asegúrese de que el archivo .zip contiene solo los archivos necesarios y de que no tenga ninguna estructura de carpetas adicional en él.

## <a name="upload-your-package-to-microsoft-teams"></a>Cargar el paquete en Microsoft Teams

Si ha estado usando App Studio, puede instalar la aplicación desde la pestaña **Probar y distribuir** en el **Editor de manifiestos**. Como alternativa, puede instalar el paquete de la aplicación haciendo clic en el menú de desbordamiento `...` desde el panel de navegación izquierdo, al hacer clic en **Más aplicaciones** y el vínculo **Cargar una aplicación personalizada**. También puede importar un manifiesto de aplicación o un paquete de aplicación en App Studio para realizar actualizaciones adicionales antes de cargarlas.

## <a name="next-steps"></a>Pasos siguientes

* [Conceptos básicos de las conversaciones de bot](./conversations/conversation-basics.md)
* [Suscribirse a eventos de conversación](./conversations/subscribe-to-conversation-events.md)
