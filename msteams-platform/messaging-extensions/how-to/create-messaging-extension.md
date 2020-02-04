---
title: Crear una extensión de mensajería
author: clearab
description: Cómo crear una extensión de mensajería para una aplicación de Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5d70ee361bdf32024f3cbdb56505a8aa410e7db0
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676211"
---
# <a name="create-a-messaging-extension-in-microsoft-teams"></a>Crear una extensión de mensajería en Microsoft Teams

En un nivel alto, deberá completar los siguientes pasos para crear una extensión de mensajería.

1. Preparar el entorno de desarrollo
2. Cree e implemente el servicio Web (mientras desarrolla un servicio de túnel como ngrok para ejecutarlo localmente)
3. Registro del servicio Web con bot Framework
4. Crear el paquete de la aplicación
5. Cargar el paquete en Microsoft Teams

La creación de un servicio Web, la creación de un paquete de la aplicación y el registro del servicio Web con bot Framework se puede realizar en cualquier orden. Como estas tres piezas están tan entrelazadas, independientemente del orden en que las haga, necesitará volver a actualizar las demás. El registro necesita el punto de conexión de mensajería del servicio Web implementado y el servicio web necesita que se cree el identificador y la contraseña a partir del registro. El manifiesto de la aplicación también necesita ese identificador para conectar Teams a su servicio Web.

Al compilar la extensión de mensajería, trabajará con regularidad entre los cambios en el manifiesto de la aplicación y la implementación del código en el servicio Web. Al trabajar con el manifiesto de la aplicación, tenga en cuenta que puede manipular manualmente el archivo JSON o realizar cambios a través de App Studio. En cualquier caso, tendrá que volver a implementar (cargar) la aplicación en Teams cuando realice un cambio en el manifiesto, pero no tendrá que hacerlo cuando implemente cambios en el servicio Web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Crear el servicio Web

El corazón de la extensión de mensajería es su servicio Web. Definirá una única ruta, normalmente `/api/messages`, en la que se recibirán todas las solicitudes de. Si empieza desde cero, tiene algunas opciones entre las que puede elegir.

* Use uno de nuestros tutoriales de [QuickStart](#learn-more) que le guiarán a través de la creación del servicio Web.
* Elija uno de los ejemplos de extensiones de mensajería disponibles en el [repositorio de ejemplo de bot Framework](https://github.com/Microsoft/BotBuilder-Samples) del que se va a empezar.
* Si está usando JavaScript, use el [generador de Yeoman para Microsoft Teams](https://github.com/OfficeDev/generator-teams) para aplicar scaffolding a la aplicación de Teams, incluido el servicio Web.
* Cree el servicio web desde cero. Puede elegir agregar el SDK de bot Framework para su idioma o puede trabajar directamente con las cargas de JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Registro del servicio Web con bot Framework

Las extensiones de mensajería aprovechan el esquema de mensajería y el protocolo de comunicaciones seguro del marco de robots; Si aún no tiene una, deberá registrar el servicio Web en el marco de bot. El identificador de aplicación de Microsoft (nos referiremos a esto como el identificador de su robot desde dentro de Teams, para identificarlo a partir de otros identificadores de aplicaciones con los que pueda estar trabajando) y el extremo de mensajería el registro con el marco de robots se usará en su extensión de mensajería para recibir y responder a la solicitud uests. Si está usando un registro existente, asegúrese [de habilitar el canal de Microsoft Teams](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0).

Si sigue uno de los tutoriales o empieza a partir de uno de los ejemplos disponibles, se le guiará por el registro del servicio Web. Si desea registrar manualmente su servicio, tiene tres opciones para hacerlo. Si elige registrarse sin usar una suscripción de Azure, no podrá aprovechar el flujo de autenticación de OAuth simplificado proporcionado por el marco de robots. Podrá migrar su registro a Azure después de crearlo.

* Si tiene una suscripción a Azure (o desea crear una nueva), puede registrar el servicio Web manualmente con Azure portal. Cree un recurso "registro de canales de bot". Puede elegir el plan de tarifa gratuito, ya que los mensajes de Microsoft Teams no cuentan para el total de mensajes permitidos por mes.
* Si no desea usar una suscripción de Azure, puede usar el [portal de registro heredado](https://dev.botframework.com/bots/new).
* App Studio también puede ayudarle a registrar el servicio Web (bot). Los servicios web registrados a través de App Studio no están registrados en Azure. Puede usar el [portal heredado](https://dev.botframework.com/bots) para ver, administrar y migrar sus registros.

## <a name="create-your-app-manifest"></a>Crear el manifiesto de la aplicación

Puede usar App Studio para ayudarle a crear el manifiesto de la aplicación, o bien crearlo manualmente.

### <a name="create-your-app-manifest-using-app-studio"></a>Crear el manifiesto de la aplicación con App Studio

Puede usar la aplicación de App Studio desde el cliente de Microsoft Teams para ayudar a crear el manifiesto de la aplicación.

1. En el cliente de Microsoft Teams, abra App Studio desde el menú **...** Overflow en el raíl de navegación izquierdo. Si aún no está instalado, puede hacerlo si lo busca.
2. En la pestaña **Editor de manifiesto** , seleccione **crear una nueva aplicación** (o, si va a agregar una extensión de mensajería a una aplicación existente, puede importar el paquete de la aplicación)
3. Agregue los detalles de la aplicación (consulte la [definición del esquema del manifiesto](~/resources/schema/manifest-schema.md) para obtener descripciones completas de cada campo).
4. En la ficha **extensiones de mensajería** , haga clic en el botón **configurar** .
5. Puede crear un nuevo servicio Web (bot) para que lo use la extensión de mensajería, o bien, si ya ha registrado una selección o agregarla aquí.
6. Si es necesario, actualice la dirección del punto de conexión de bot para que apunte a su bot. Debe tener un aspecto similar `https://someplace.com/api/messages`a.
7. El botón **Agregar** de la sección comandos le guiará por el **comando** para agregar comandos a la extensión de mensajería. Vea la [sección más información](#learn-more) para obtener vínculos para obtener más información sobre cómo agregar comandos. Recuerde que puede definir hasta 10 comandos para la extensión de mensajería.
8. La sección de **controladores de mensajes** le permite agregar un dominio en el que se activará su mensajería. Consulte [Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) para obtener más información.

En la pestaña **Finalizar => prueba y distribución** , puede **Descargar** el paquete de la aplicación (que incluye el manifiesto de la aplicación, así como los iconos de la aplicación) o **instalar** el paquete.

### <a name="create-your-app-manifest-manually"></a>Crear el manifiesto de la aplicación manualmente

Al igual que con los bots y las pestañas, se actualiza el manifiesto de la [aplicación](~/resources/schema/manifest-schema.md#composeextensions) para incluir las propiedades de la extensión de mensajería. Estas propiedades rigen el aspecto y el comportamiento de la extensión de mensajería en el cliente de Microsoft Teams. Las extensiones de mensajería son compatibles a partir de la v 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declarar la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto de la `composeExtensions` aplicación con la propiedad. Puede crear una extensión de mensajería única para su aplicación, con hasta 10 comandos.

> [!NOTE]
> El manifiesto hace referencia a extensiones de `composeExtensions`mensajería como. Esto es para mantener la compatibilidad con versiones anteriores.

La definición de la extensión es un objeto que tiene la estructura siguiente:

| Nombre de la propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | IDENTIFICADOR único de la aplicación de Microsoft para el bot como se registra con bot Framework. Suele ser el mismo que el identificador de la aplicación general de Microsoft Teams. | Sí |
| `canUpdateConfiguration` | Habilita el elemento de menú **configuración** . | No |
| `commands` | Matriz de comandos compatibles con esta extensión de mensajería. Tiene un límite de 10 comandos. | Sí |

#### <a name="define-your-commands"></a>Definir los comandos

La extensión de mensajería debe declarar uno o más comandos, que definen dónde los usuarios pueden desencadenar la extensión de mensajería y el tipo de interacción. Vea más información sobre los comandos de la [extensión de mensajería](#learn-more) .

#### <a name="simple-manifest-example"></a>Ejemplo de manifiesto sencillo

El siguiente ejemplo es un objeto simple de extensión de mensajería en el manifiesto de la aplicación con un comando de búsqueda. Este no es el archivo del manifiesto de la aplicación completo, solo la parte específica de las extensiones de mensajería. Consulte el [esquema del manifiesto](~/resources/schema/manifest-schema.md) de la aplicación para obtener un ejemplo completo.

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

## <a name="next-steps"></a>Siguientes pasos

* [Crear comandos de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Crear comandos de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Vincular unfurling](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>Más información

Pruébelo en un inicio rápido:

* Tutoriales rápidos para C #
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Tutoriales rápidos de JavaScript
  * [Extensión de mensajería con comandos basados en acciones](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extensión de mensajería con comandos basados en la búsqueda](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

Obtenga más información acerca de los conceptos de extensiones de mensajería:

* [¿Conoce las funcionalidades de la aplicación Teams?](~/concepts/extensibility-points.md)
* [¿Qué son las extensiones de mensajería?](~/messaging-extensions/what-are-messaging-extensions.md)
