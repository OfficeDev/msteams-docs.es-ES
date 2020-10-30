---
title: Crear una extensión de mensajería con App Studio
author: clearab
description: Obtenga información sobre cómo crear una extensión de mensajería de Microsoft Teams con App Studio.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c3437457f7084d2d768af0f0db5208525c368682
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796186"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Crear una extensión de mensajería con App Studio

> [!TIP]
> ¿Busca una forma más rápida de empezar? Cree una [extensión de mensajería](../../build-your-first-app/build-messaging-extension.md) mediante el kit de herramientas de Microsoft Teams.

En un nivel alto, deberá completar los siguientes pasos para crear una extensión de mensajería.

1. Preparar el entorno de desarrollo
2. Cree e implemente el servicio Web (mientras desarrolla un servicio de túnel como ngrok para ejecutarlo localmente)
3. Registrar el servicio web con Bot Framework
4. Creación del paquete de aplicación
5. Cargar el paquete en Microsoft Teams

La creación de un servicio Web, la creación de un paquete de la aplicación y el registro del servicio Web con bot Framework se puede realizar en cualquier orden. Como estas tres piezas están tan entrelazadas, independientemente del orden en que las haga, necesitará volver a actualizar las demás. El registro necesita el punto de conexión de mensajería del servicio Web implementado y el servicio web necesita que se cree el identificador y la contraseña a partir del registro. El manifiesto de la aplicación también necesita ese identificador para conectar Teams a su servicio Web.

Al compilar la extensión de mensajería, trabajará con regularidad entre los cambios en el manifiesto de la aplicación y la implementación del código en el servicio Web. Al trabajar con el manifiesto de la aplicación, tenga en cuenta que puede manipular manualmente el archivo JSON o realizar cambios a través de App Studio. En cualquier caso, tendrá que volver a implementar (cargar) la aplicación en Teams cuando realice un cambio en el manifiesto, pero no tendrá que hacerlo cuando implemente cambios en el servicio Web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Crear su servicio web

El corazón de la extensión de mensajería es su servicio Web. Definirá una única ruta, normalmente, en la `/api/messages` que se recibirán todas las solicitudes de. Si empieza desde cero, tiene algunas opciones entre las que puede elegir.

* Use uno de nuestros tutoriales de [QuickStart](#learn-more) que le guiarán a través de la creación del servicio Web.
* Elija uno de los ejemplos de extensiones de mensajería disponibles en el [repositorio de ejemplo de bot Framework](https://github.com/Microsoft/BotBuilder-Samples) del que se va a empezar.
* Si está usando JavaScript, use el [generador de Yeoman para Microsoft Teams](https://github.com/OfficeDev/generator-teams) para aplicar scaffolding a la aplicación de Teams, incluido el servicio Web.
* Crear su servicio web desde cero. Puede optar por agregar el SDK de Bot Framework para su idioma, o bien puede trabajar directamente con las cargas JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Registrar el servicio web con Bot Framework

Las extensiones de mensajería aprovechan el esquema de mensajería y el protocolo de comunicaciones seguro del marco de robots; Si aún no tiene una, deberá registrar el servicio Web en el marco de bot. El identificador de aplicación de Microsoft (nos referiremos a esto como el identificador de su robot desde dentro de Teams, para identificarlo a partir de otros identificadores de aplicaciones con los que pueda estar trabajando) y el extremo de mensajería el registro con el marco de robots se usará en su extensión de mensajería para recibir y responder a las solicitudes. Si está usando un registro existente, asegúrese [de habilitar el canal de Microsoft Teams](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).

Si sigue uno de los tutoriales o empieza a partir de uno de los ejemplos disponibles, se le guiará por el registro del servicio Web. Si desea registrar manualmente su servicio, tiene tres opciones para hacerlo. Si elige registrarse sin usar una suscripción de Azure, no podrá aprovechar el flujo de autenticación de OAuth simplificado proporcionado por el marco de robots. Podrá migrar su registro a Azure después de crearlo.

* Si tiene una suscripción a Azure (o desea crear una nueva), puede registrar el servicio Web manualmente con Azure portal. Cree un recurso "registro de canales de bot". Puede elegir el plan de tarifa gratuito, ya que los mensajes de Microsoft Teams no cuentan para el total de mensajes permitidos por mes.
* Si no desea usar una suscripción de Azure, puede usar el [portal de registro heredado](https://dev.botframework.com/bots/new).
* App Studio también puede ayudarle a registrar el servicio Web (bot). Los servicios web registrados a través de App Studio no están registrados en Azure. Puede usar el [portal heredado](https://dev.botframework.com/bots) para ver, administrar y migrar sus registros.

## <a name="create-your-app-manifest"></a>Crear el manifiesto de la aplicación

Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo de forma manual.

### <a name="create-your-app-manifest-using-app-studio"></a>Crear el manifiesto de la aplicación con App Studio

Puede usar la aplicación de App Studio desde el cliente de Microsoft Teams para ayudar a crear el manifiesto de la aplicación.

1. En el cliente de Teams, abra App Studio en el menú de desbordamiento **...** del raíl de navegación izquierdo. Si aún no está instalado, puede hacerlo si lo busca.
2. En la pestaña **Editor de manifiesto** , seleccione **crear una nueva aplicación** (o, si va a agregar una extensión de mensajería a una aplicación existente, puede importar el paquete de la aplicación)
3. Agregue los detalles de la aplicación (consulte [definición de esquema de manifiesto](~/resources/schema/manifest-schema.md) para obtener las descripciones completas de cada campo).
4. En la ficha **extensiones de mensajería** , haga clic en el botón **configurar** .
5. Puede crear un nuevo servicio Web (bot) para que lo use la extensión de mensajería, o bien, si ya ha registrado una selección o agregarla aquí.
6. Si es necesario, actualice la dirección del extremo del bot para que apunte a su bot. Debería tener un aspecto similar a `https://someplace.com/api/messages`.
7. El botón **Agregar** de la sección comandos le guiará por el **comando** para agregar comandos a la extensión de mensajería. Vea la [sección más información](#learn-more) para obtener vínculos para obtener más información sobre cómo agregar comandos. Recuerde que puede definir hasta 10 comandos para la extensión de mensajería.
8. La sección de **controladores de mensajes** le permite agregar un dominio en el que se activará su mensajería. Consulte [Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) para obtener más información.

En la pestaña **Finalizar => prueba y distribución** , puede **Descargar** el paquete de la aplicación (que incluye el manifiesto de la aplicación, así como los iconos de la aplicación) o **instalar** el paquete.

### <a name="create-your-app-manifest-manually"></a>Crear el manifiesto de la aplicación manualmente

Al igual que con los bots y las pestañas, se actualiza el manifiesto de la [aplicación](~/resources/schema/manifest-schema.md#composeextensions) para incluir las propiedades de la extensión de mensajería. Estas propiedades rigen el aspecto y el comportamiento de la extensión de mensajería en el cliente de Microsoft Teams. Las extensiones de mensajería son compatibles a partir de la v 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declarar la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto de la aplicación con la `composeExtensions` propiedad. Puede crear una extensión de mensajería única para su aplicación, con hasta 10 comandos.

> [!NOTE]
> El manifiesto hace referencia a extensiones de mensajería como `composeExtensions` . Esto es para mantener la compatibilidad con versiones anteriores.

La definición de la extensión es un objeto que tiene la estructura siguiente:

| Nombre de propiedad | Finalidad | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Suele ser el mismo que el identificador de la aplicación general de Microsoft Teams. | Sí |
| `canUpdateConfiguration` | Habilita el elemento de menú **configuración** . | No |
| `commands` | Matriz de comandos compatibles con esta extensión de mensajería. Tiene un límite de 10 comandos. | Sí |

#### <a name="define-your-commands"></a>Definir los comandos

La extensión de mensajería debe declarar uno o más comandos, que definen dónde los usuarios pueden desencadenar la extensión de mensajería y el tipo de interacción. Vea más información sobre los comandos de la [extensión de mensajería](#learn-more) .

#### <a name="simple-manifest-example"></a>Ejemplo de manifiesto simple

El siguiente ejemplo es un objeto simple de extensión de mensajería en el manifiesto de la aplicación con un comando de búsqueda. Este no es el archivo de manifiesto de la aplicación completo, solo la parte específica para las extensiones de mensajería. Consulte el [esquema del manifiesto](~/resources/schema/manifest-schema.md) de la aplicación para obtener un ejemplo completo.

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

## <a name="add-your-invoke-message-handlers"></a>Agregar los controladores de mensajes de invocación

Cuando los usuarios desencadenen la extensión de mensajería, deberá controlar el mensaje de invocación inicial, recopilar información del usuario, procesar la información y responder de manera adecuada. Para ello, primero tendrá que decidir qué tipo de comandos desea agregar a su extensión de mensajería y [Agregar comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md) o [Agregar comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md).

## <a name="messaging-extensions-in-teams-meetings"></a>Extensiones de mensajería en reuniones de Microsoft Teams

Una vez iniciada una reunión, los participantes de Microsoft Teams pueden interactuar directamente con la extensión de mensajería durante una llamada activa. Tenga en cuenta lo siguiente al crear la extensión de mensajería en la reunión:

1. **Location** . La extensión de mensajería se puede invocar desde el área redactar mensaje, el cuadro de comando o @mentioned del chat de reuniones.

1. **Metadatos** . Cuando se llama a la extensión de mensajería, puede identificar el usuario y el inquilino de `userId` y `tenantId` . Se puede encontrar `meetingId` como parte del objeto `channelData`. La aplicación puede usar `userId` y `meetingId`  para la solicitud de la `GetParticipant` API para recuperar roles de usuario.

1. **Tipo de comando** . Si su extensión de mensaje usa [comandos basados en acciones](../../messaging-extensions/what-are-messaging-extensions.md#action-commands), debe seguir la autenticación de [Inicio de sesión único de](../../tabs/how-to/authentication/auth-aad-sso.md) las pestañas.

1. **Experiencia del usuario** . La extensión de mensajería debe tener el mismo aspecto y comportarse de la misma manera que fuera una reunión.

## <a name="next-steps"></a>Siguientes pasos

* [Crear comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Crear comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Apertura de vínculos](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Más información

Pruébelo en un inicio rápido:

* Tutoriales rápidos para C #
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Tutoriales rápidos de JavaScript
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Obtenga más información sobre los conceptos de desarrollo de Microsoft Teams:

* [Descripción de las funcionalidades de la aplicación Teams](../../concepts/capabilities-overview.md)
* [¿Qué son las extensiones de mensajería?](~/messaging-extensions/what-are-messaging-extensions.md)
