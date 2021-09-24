---
title: Crear una extensión de mensajería usando App Studio
author: surbhigupta
description: Obtén información sobre cómo crear una Microsoft Teams de mensajería con App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 61bfed969b981bd5000bdb6eca0bbd77196e8086
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157210"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Crear una extensión de mensajería usando App Studio

> [!TIP]
> ¿Está buscando una forma más rápida de empezar? Cree una [extensión de mensajería](../build-your-first-app/build-messaging-extension.md) mediante el Microsoft Teams Toolkit.

En un nivel alto, deberá completar los siguientes pasos para crear una extensión de mensajería.

1. Preparar el entorno de desarrollo
2. Crear e implementar el servicio web (mientras se desarrolla, use un servicio de túnel como ngrok para ejecutarlo localmente)
3. Registrar el servicio web con Bot Framework
4. Crear el paquete de aplicación
5. Cargar el paquete en Microsoft Teams

La creación del servicio web, la creación del paquete de la aplicación y el registro del servicio web con Bot Framework se pueden realizar en cualquier orden. Dado que estas tres piezas están entrelazadas, independientemente del orden en el que las realice, tendrá que volver a actualizar las otras. El registro necesita el extremo de mensajería del servicio web implementado y el servicio web necesita el identificador y la contraseña creados a partir del registro. El manifiesto de la aplicación también necesita ese identificador para conectarse Teams al servicio web.

Al crear la extensión de mensajería, se mueve regularmente entre cambiar el manifiesto de la aplicación e implementar código en el servicio web. Al trabajar con el manifiesto de la aplicación, ten en cuenta que puedes manipular manualmente el archivo JSON o realizar cambios a través de App Studio. En cualquier caso, tendrás que volver a implementar (cargar) la aplicación en Teams cuando realices un cambio en el manifiesto, pero no es necesario hacerlo al implementar cambios en el servicio web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Crear su servicio web

El corazón de la extensión de mensajería es el servicio web. Definirá una sola ruta, normalmente `/api/messages` , para recibir todas las solicitudes. Si estás empezando desde cero, tienes algunas opciones entre las que elegir.

* Use uno de nuestros [tutoriales de inicio rápido](#learn-more) que le guiará a través de la creación de su servicio web.
* Elija uno de los ejemplos de extensión de mensajería disponibles en el repositorio de ejemplo [de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) desde el que empezar.
* Si usa JavaScript, use el generador [de Yeoman](https://github.com/OfficeDev/generator-teams) para Microsoft Teams scaffolding de la aplicación Teams, incluido el servicio web.
* Crear su servicio web desde cero. Puede optar por agregar el SDK de Bot Framework para su idioma, o bien puede trabajar directamente con las cargas JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Registrar el servicio web con Bot Framework

Las extensiones de mensajería aprovechan el esquema de mensajería del Bot Framework y el protocolo de comunicación segura; si aún no tiene uno, deberá registrar el servicio web en Bot Framework. El Id. de aplicación de Microsoft (nos referiremos a esto como el Identificador de bot desde dentro de Teams, para identificarlo desde otros identificadores de aplicación con los que podría estar trabajando) y el extremo de mensajería con el que se registrará con Bot Framework se usará en la extensión de mensajería para recibir y responder a las solicitudes. Si usa un registro existente, asegúrese de habilitar el canal [Microsoft Teams .](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)

Si sigue uno de los inicios rápidos o empieza desde uno de los ejemplos disponibles, se le guiará a través del registro del servicio web. Si desea registrar manualmente el servicio, tiene tres opciones para hacerlo. Si decide registrarse sin usar una suscripción de Azure, no podrá aprovechar el flujo simplificado de autenticación de OAuth proporcionado por Bot Framework. Podrás migrar el registro a Azure después de la creación.

* Si tiene una suscripción de Azure (o desea crear una nueva), puede registrar el servicio web manualmente mediante Azure Portal. Cree un recurso "Registro de canales de bot". Puedes elegir el nivel de precios gratuito, ya que los mensajes de Microsoft Teams no cuentan para el total de mensajes permitidos al mes.
* Si no desea usar una suscripción de Azure, puede usar el [portal de registro heredado](https://dev.botframework.com/bots/new).
* App Studio también puede ayudarte a registrar el servicio web (bot). Los servicios web registrados a través de App Studio no están registrados en Azure. Puede usar el [portal heredado para](https://dev.botframework.com/bots) ver, administrar y migrar los registros.

## <a name="create-your-app-manifest"></a>Crear el manifiesto de la aplicación

Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo de forma manual.

### <a name="create-your-app-manifest-using-app-studio"></a>Crear el manifiesto de la aplicación con App Studio

Puedes usar la aplicación app Studio desde el cliente Microsoft Teams para ayudar a crear el manifiesto de la aplicación.

1. En el cliente de Teams, abra App Studio en el menú de desbordamiento **...** del raíl de navegación izquierdo. Si aún no está instalado, puede hacerlo buscándolo.
2. En la **pestaña Editor de manifiestos,** selecciona **Crear** una nueva aplicación (o si estás agregando una extensión de mensajería a una aplicación existente, puedes importar el paquete de la aplicación)
3. Agregue los detalles de la aplicación (consulte [definición de esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener las descripciones completas de cada campo).
4. En la **pestaña Extensiones de mensajería,** haga clic en **el botón Configurar.**
5. Puede crear un nuevo servicio web (bot) para que la extensión de mensajería lo use, o si ya ha registrado un select/add it aquí.
6. Si es necesario, actualice la dirección del extremo del bot para que apunte a su bot. Debería tener un aspecto similar a `https://someplace.com/api/messages`.
7. El **botón** Agregar de la **sección Comando** le guiará a través de la adición de comandos a la extensión de mensajería. Vea la [sección Más información](#learn-more) para obtener vínculos a más información sobre cómo agregar comandos. Recuerde que puede definir hasta 10 comandos para la extensión de mensajería.
8. La **sección Controladores de mensajes** le permite agregar un dominio en el que se desencadenará la mensajería. Vea [deshacer vínculos para](~/messaging-extensions/how-to/link-unfurling.md) obtener más información.

En la pestaña **Finalizar =>** Probar  y distribuir puedes descargar el paquete de la aplicación (que incluye el manifiesto de la aplicación, así como los iconos de la aplicación) o **Instalar** el paquete.

### <a name="create-your-app-manifest-manually"></a>Crear el manifiesto de la aplicación manualmente

Al igual que con los bots y las pestañas, actualizas [el](~/resources/schema/manifest-schema.md#composeextensions) manifiesto de la aplicación para incluir las propiedades de extensión de mensajería. Estas propiedades rigen cómo aparece y se comporta la extensión de mensajería en el Microsoft Teams cliente. Las extensiones de mensajería se admiten a partir de la versión 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declarar la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto de la aplicación con la `composeExtensions` propiedad. Creas una sola extensión de mensajería para la aplicación, con hasta 10 comandos.

> [!NOTE]
> El manifiesto hace referencia a las extensiones de mensajería como `composeExtensions` . Esto es para mantener la compatibilidad con versiones anteriores.

La definición de extensión es un objeto que tiene la siguiente estructura:

| Nombre de la propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Normalmente, debería ser el mismo que el identificador de la aplicación Teams general. | Sí |
| `canUpdateConfiguration` | Habilita **Configuración** elemento de menú. | No |
| `commands` | Matriz de comandos compatibles con esta extensión de mensajería. Está limitado a 10 comandos. | Sí |

#### <a name="define-your-commands"></a>Definir los comandos

La extensión de mensajería debe declarar uno o varios comandos, que definen dónde los usuarios pueden desencadenar la extensión de mensajería y el tipo de interacción. Vea [más información para](#learn-more) obtener más información sobre los comandos de extensión de mensajería.

#### <a name="simple-manifest-example"></a>Ejemplo de manifiesto simple

El siguiente ejemplo es un objeto de extensión de mensajería simple en el manifiesto de la aplicación con un comando de búsqueda. Este no es el archivo de manifiesto de la aplicación completo, solo la parte específica para las extensiones de mensajería. Consulta [esquema de manifiesto de aplicación](~/resources/schema/manifest-schema.md) para ver un ejemplo completo.

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

#### <a name="complete-app-manifest-example"></a>Ejemplo de manifiesto de aplicación completa

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

## <a name="add-your-invoke-message-handlers"></a>Agregar los controladores de mensajes de invocación

Cuando los usuarios desencadene la extensión de mensajería, deberá controlar el mensaje de invocación inicial, recopilar información del usuario y, a continuación, procesar esa información y responder correctamente. Para ello, primero tendrá que decidir qué tipo de comandos desea agregar a [](~/messaging-extensions/how-to/action-commands/define-action-command.md) la extensión de mensajería y agregar comandos de acción o agregar comandos [de búsqueda.](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="messaging-extensions-in-teams-meetings"></a>Extensiones de mensajería en Teams reuniones

> [!NOTE]
> Si una reunión o un chat de grupo tiene usuarios federados en la lista, Teams elimina el acceso a extensiones de mensajería para todos los usuarios, incluido el organizador.

Una vez que se inicia una reunión, Teams participantes pueden interactuar directamente con la extensión de mensajería durante una llamada en directo. Tenga en cuenta lo siguiente al crear la extensión de mensajería en la reunión:

1. **Location**. La extensión de mensajería se puede invocar desde el área del mensaje de redacción, el cuadro de comandos o @mentioned en el chat de la reunión.

1. **Metadatos**. Cuando se invoca la extensión de mensajería, puede identificar el usuario y el inquilino `userId` desde y `tenantId` . Se puede encontrar `meetingId` como parte del objeto `channelData`. La aplicación puede usar la `userId` solicitud y para la API para recuperar roles de `meetingId` `GetParticipant` usuario.

1. **Tipo de comando**. Si la extensión de mensaje usa [comandos basados](../messaging-extensions/what-are-messaging-extensions.md#action-commands)en acciones, debe seguir la autenticación de inicio [de sesión único de pestañas.](../tabs/how-to/authentication/auth-aad-sso.md)

1. **Experiencia del usuario**. La extensión de mensajería debe tener el mismo aspecto y comportamiento que fuera de una reunión.

## <a name="next-steps"></a>Pasos siguientes

* [Crear comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Crear comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Apertura de vínculos](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Más información

Pruébalo en un inicio rápido:

* Inicios rápidos para C #
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Inicios rápidos para JavaScript
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Obtenga más información sobre Teams de desarrollo:

* [Comprender Teams funcionalidades de la aplicación](../concepts/capabilities-overview.md)
* [¿Qué son las extensiones de mensajería?](../messaging-extensions/what-are-messaging-extensions.md)
