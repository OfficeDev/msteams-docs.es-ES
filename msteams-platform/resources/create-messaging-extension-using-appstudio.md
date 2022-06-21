---
title: Crear una extensión de mensajería usando App Studio
author: surbhigupta
description: Obtenga información sobre cómo crear una extensión de mensajería de Microsoft Teams mediante App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 9f222f52a4eea3b59e6caf15e77b006a58a426d2
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190023"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Crear una extensión de mensajería usando App Studio

> [!TIP]
> ¿Busca una manera más rápida de empezar? Cree una [extensión de mensajería](../build-your-first-app/build-messaging-extension.md) mediante el Microsoft Teams Toolkit.

En un nivel alto, deberá completar los pasos siguientes para crear una extensión de mensajería.

1. Preparar el entorno de desarrollo.
2. Cree e implemente el servicio web (mientras desarrolla usa un servicio de tunelización como ngrok para ejecutarlo localmente).
3. Registre el servicio web con Bot Framework.
4. Cree el paquete de la aplicación.
5. Upload el paquete a Teams.

La creación del servicio web, la creación del paquete de la aplicación y el registro del servicio web con Bot Framework se pueden realizar en cualquier orden. Dado que esas tres piezas están tan entrelazadas, independientemente del orden en el que las hagas, tendrás que volver a actualizar las demás. El registro necesita el punto de conexión de mensajería del servicio web implementado y el servicio web necesita el identificador y la contraseña creados a partir del registro. El manifiesto de la aplicación también necesita ese identificador para conectar Teams al servicio web.

A medida que va a compilar la extensión de mensajería, se moverá periódicamente entre cambiar el manifiesto de la aplicación e implementar código en el servicio web. Al trabajar con el manifiesto de aplicación, asegúrese de que puede modificar manualmente el archivo JSON o realizar cambios a través de App Studio. En cualquier caso, tendrá que volver a implementar (cargar) la aplicación en Teams al realizar un cambio en el manifiesto, pero no es necesario hacerlo al implementar los cambios en el servicio web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Crear su servicio web

El corazón de la extensión de mensajería es el servicio web. Definirá una única ruta, normalmente `/api/messages`, para recibir todas las solicitudes. Si va a empezar desde cero, tiene algunas opciones entre las que elegir.

* Use uno de nuestros [tutoriales de inicio rápido](#learn-more) que le guiará a través de la creación de su servicio web.
* Elija uno de los ejemplos de extensión de mensajería disponibles en el [repositorio de ejemplo de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) desde el que empezar.
* Si usa JavaScript, use el [generador de Yeoman para Microsoft Teams](https://github.com/OfficeDev/generator-teams) para aplicar scaffolding a la aplicación de Teams, incluido el servicio web.
* Crear su servicio web desde cero. Puede optar por agregar el SDK de Bot Framework para su idioma, o bien puede trabajar directamente con las cargas JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Registrar el servicio web con Bot Framework

Las extensiones de mensajería aprovechan el esquema de mensajería de Bot Framework y el protocolo de comunicación seguro; Si aún no tiene uno, deberá registrar el servicio web en Bot Framework. El identificador de aplicación de Microsoft (haremos referencia a este identificador como su identificador de bot desde dentro de Teams, para identificarlo desde otros identificadores de aplicación con los que podría estar trabajando) y el punto de conexión de mensajería con el que se registrará con Bot Framework se usará en la extensión de mensajería para recibir y responder a las solicitudes. Si usa un registro existente, asegúrese de [habilitar el canal de Microsoft Teams](/azure/bot-service/bot-service-manage-channels?preserve-view=true&view=azure-bot-service-4.0).

Si sigue uno de los inicios rápidos o comienza desde uno de los ejemplos disponibles, se le guiará a través del registro del servicio web. Si desea registrar manualmente el servicio, tiene tres opciones para hacerlo. Si decide registrarse sin usar una suscripción de Azure, no podrá aprovechar el flujo de autenticación simplificado de OAuth proporcionado por Bot Framework. Podrá migrar el registro a Azure después de su creación.

* Si tiene una suscripción de Azure (o quiere crear una nueva), puede registrar el servicio web manualmente mediante el portal de Microsoft Azure. Cree un recurso "Registro de canales de bot". Puede elegir el plan de tarifa gratuito, ya que los mensajes de Microsoft Teams no cuentan para el total de mensajes permitidos al mes.
* Si no desea usar una suscripción de Azure, puede usar el [portal de registro heredado](https://dev.botframework.com/bots/new).
* App Studio también puede ayudarle a registrar el servicio web (bot). Los servicios web registrados a través de App Studio no están registrados en Azure. Puede usar el [portal heredado](https://dev.botframework.com/bots) para ver, administrar y migrar los registros.

## <a name="create-your-app-manifest"></a>Creación del manifiesto de la aplicación

Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo de forma manual.

### <a name="create-your-app-manifest-using-app-studio"></a>Creación de un manifiesto de aplicación mediante App Studio

Puede usar la aplicación app de App Studio desde el cliente de Teams para ayudar a crear el manifiesto de la aplicación.

1. En el cliente de Teams, abra App Studio en el menú de desbordamiento **...** del raíl de navegación izquierdo. Si aún no está instalado, puede hacerlo si lo busca.
2. En la pestaña **Editor de manifiestos** , seleccione **Crear una nueva aplicación** (o si va a agregar una extensión de mensajería a una aplicación existente, puede importar el paquete de la aplicación).
3. Agregue los detalles de la aplicación (consulte [definición de esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener las descripciones completas de cada campo).
4. En la pestaña **Extensiones de mensajería** , seleccione el botón **Configurar** .
5. Puede crear un nuevo servicio web (bot) para que la extensión de mensajería se use, o bien si ya ha registrado una, selecciónela o agréguela aquí.
6. Si es necesario, actualice la dirección del extremo del bot para que apunte a su bot. Debería tener un aspecto similar a `https://someplace.com/api/messages`.
7. El botón **Agregar** de la sección **Comando** le guiará a través de la adición de comandos a la extensión de mensajería. Consulte la sección [Más información](#learn-more) para obtener vínculos a más información sobre cómo agregar comandos. Recuerde que puede definir hasta 10 comandos para la extensión de mensajería.
8. La sección **Controladores de** mensajes le permite agregar un dominio en el que se desencadenará la mensajería. Consulte [desplegamiento de vínculos](~/messaging-extensions/how-to/link-unfurling.md) para obtener más información.

En la pestaña **Finalizar => Probar y distribuir** , puedes **descargar** el paquete de la aplicación (que incluye el manifiesto de la aplicación, así como los iconos de la aplicación) o **instalar** el paquete.

### <a name="create-your-app-manifest-manually"></a>Creación manual del manifiesto de la aplicación

Al igual que con los bots y las pestañas, actualiza el [manifiesto de aplicación](~/resources/schema/manifest-schema.md#composeextensions) de la aplicación para incluir las propiedades de la extensión de mensajería. Estas propiedades rigen cómo aparece y se comporta la extensión de mensajería en el cliente de Teams. Las extensiones de mensajería se admiten a partir de la versión 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declaración de la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto de la aplicación con la `composeExtensions` propiedad . Cree una sola extensión de mensajería para la aplicación, con hasta 10 comandos.

> [!NOTE]
> El manifiesto hace referencia a las extensiones de mensajería como `composeExtensions`. Esto es para mantener la compatibilidad con versiones anteriores.

La definición de extensión es un objeto que tiene la estructura siguiente:

| Nombre de propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Normalmente, debe ser el mismo que el identificador de la aplicación de Teams general. | Sí |
| `canUpdateConfiguration` | Habilita **Configuración** elemento de menú. | No |
| `commands` | Matriz de comandos que admite esta extensión de mensajería. Está limitado a 10 comandos. | Sí |

#### <a name="define-your-commands"></a>Definición de los comandos

La extensión de mensajería debe declarar uno o varios comandos, que definen dónde pueden desencadenar los usuarios la extensión de mensajería y el tipo de interacción. Consulte [más información](#learn-more) para obtener más información sobre los comandos de extensión de mensajería.

#### <a name="simple-manifest-example"></a>Ejemplo de manifiesto simple

El ejemplo siguiente es un objeto de extensión de mensajería simple en el manifiesto de la aplicación con un comando de búsqueda. Este no es el archivo de manifiesto de la aplicación completo, solo la parte específica para las extensiones de mensajería. Consulte [esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md) para obtener un ejemplo completo.

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a>Ejemplo de manifiesto de aplicación completo

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a>Adición de controladores de mensajes de invocación

Cuando los usuarios desencadenen la extensión de mensajería, deberá controlar el mensaje de invocación inicial, recopilar información del usuario y, a continuación, procesar esa información y responder adecuadamente. Para ello, primero tendrá que decidir qué tipo de comandos desea agregar a la extensión de mensajería y [agregar comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md) o [agregar comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md).

## <a name="messaging-extensions-in-teams-meetings"></a>Extensiones de mensajería en reuniones de Teams

> [!NOTE]
> Si un chat de reunión o grupo tiene usuarios federados en la lista, Teams suprime el acceso a las extensiones de mensajería para todos los usuarios, incluido el organizador.

Una vez que comienza una reunión, Teams participantes pueden interactuar directamente con la extensión de mensajería durante una llamada en directo. Tenga en cuenta lo siguiente al compilar la extensión de mensajería en la reunión:

1. **Location**. La extensión de mensajería se puede invocar desde el área del mensaje de redacción, el cuadro de comandos o @mentioned en el chat de reunión.

1. **Metadatos**. Cuando se invoca la extensión de mensajería, puede identificar el usuario y el inquilino de `userId` y `tenantId`. Se puede encontrar `meetingId` como parte del objeto `channelData`. La aplicación puede usar y `userId` `meetingId`  para que la solicitud de `GetParticipant` API recupere roles de usuario.

1. **Tipo de comando**. Si la extensión de mensaje usa [comandos basados en acciones](../messaging-extensions/what-are-messaging-extensions.md#action-commands), debe seguir las pestañas [de autenticación de inicio de sesión único](../tabs/how-to/authentication/tab-sso-overview.md) .

1. **Experiencia del usuario**. La extensión de mensajería debe tener un aspecto y comportarse de la misma manera que lo haría fuera de una reunión.

## <a name="next-steps"></a>Pasos siguientes

* [Crear comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Crear comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Apertura de vínculos](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Más información

Pruébelo en un inicio rápido:

* Inicios rápidos para C #
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Inicios rápidos para JavaScript
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Obtenga más información sobre Teams conceptos de desarrollo:

* [Descripción de las funcionalidades de la aplicación Teams](../concepts/capabilities-overview.md)
* [¿Qué son las extensiones de mensajería?](../messaging-extensions/what-are-messaging-extensions.md)
