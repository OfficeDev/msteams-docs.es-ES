---
title: Extensiones de mensajes
author: surbhigupta
description: En este módulo, aprenderá las extensiones de mensajería y los escenarios en los que se usan extensiones de mensaje en la plataforma de Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c93e55bbbbf9bc135afeef3c9b5787cbefe3ce80
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2022
ms.locfileid: "67786958"
---
# <a name="message-extensions"></a>Extensiones de mensajes

Las extensiones de mensajería permiten a los usuarios interactuar con su servicio web mediante botones y formularios en el cliente de Microsoft Teams. Pueden buscar o iniciar acciones en un sistema externo del área de redactar mensajes, el cuadro de comandos o directamente desde un mensaje. Puede devolver los resultados de esa interacción al cliente de Teams en forma de una tarjeta con formato enriquecido.

> [!IMPORTANT]
> Las extensiones de mensaje están disponibles en los entornos de nube de la comunidad de Government (GCC) y GCC-High, pero no en el entorno del Departamento de Defensa (DoD).

En este documento se proporciona información general sobre la extensión del mensaje, las tareas realizadas en diferentes escenarios, el trabajo de la extensión de mensaje, los comandos de acción y búsqueda, y la apertura de vínculos.

La siguiente imagen muestra las ubicaciones desde las que se invocan las extensiones de mensaje:

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="Ubicaciones de invocación de extensión de mensaje":::

> [!NOTE]
> las @menciones en extensiones de mensajería ya no se admiten en el cuadro de redacción.

## <a name="scenarios-where-message-extensions-are-used"></a>Escenarios en los que se usan extensiones de mensajería

| Escenario | Ejemplo |
|:-----------------|:-----------------|
|Quiere que algún sistema externo realice una acción y que el resultado de la acción se envíe a la conversación.|Reserve un recurso y permita que el canal esté al corriente de la franja horaria reservada.|
|Quiere encontrar algo en un sistema externo y compartir los resultados con la conversación.|Busque un elemento de trabajo en Azure DevOps y compártalo con el grupo como tarjeta adaptable.|
|Quiere completar una tarea compleja que implica varios pasos o una gran cantidad de información en un sistema externo y compartir los resultados en una conversación.|Cree un error en su sistema de seguimiento basado en un mensaje de Teams, asigne ese error a un usuario y envíe una tarjeta al hilo de conversación con los detalles del error.|

## <a name="understand-how-message-extensions-work"></a>Descripción del funcionamiento de las extensiones de mensajería

Una extensión de mensaje consta de un servicio web que hospeda y un manifiesto de aplicación, que define desde dónde se invoca el servicio web en el cliente de Teams. El servicio web aprovecha el esquema de mensajería de Bot Framework y el protocolo de comunicación segura de modo que deberá registrar su servicio web como bot en Bot Framework.

> [!NOTE]
> Aunque puede crear el servicio web manualmente, use [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) para trabajar con el protocolo.

En el manifiesto de la aplicación para la aplicación Teams, se define una sola extensión de mensaje con hasta 10 comandos diferentes. Cada comando define un tipo, como acción o búsqueda y las ubicaciones del cliente desde donde se invoca. Las ubicaciones de invocación son el área de redacción de mensajes, la barra de comandos y el mensaje. Al invocar, el servicio web recibe un mensaje HTTPS con una carga JSON que incluye toda la información pertinente. Responda con una carga JSON, lo que permite al cliente de Teams conocer la siguiente interacción que se va a habilitar.

## <a name="types-of-message-extension-commands"></a>Tipos de comandos de extensión de mensajería

Hay dos tipos de comandos de extensión de mensajería: comando de acción y comando de búsqueda. El tipo de comando de extensión de mensaje define los elementos de la interfaz de usuario y los flujos de interacción disponibles para su servicio web. Algunas interacciones, como la autenticación y la configuración, están disponibles para ambos tipos de comandos.

### <a name="action-commands"></a>Comandos de acción

Los comandos de acción se usan para presentar a los usuarios un elemento emergente modal para recopilar o mostrar información. Cuando un usuario envía el formulario, su servicio web puede responder insertando un mensaje directamente en la conversación o insertando un mensaje en el área de redacción de mensajes. Después, el usuario puede enviar el mensaje. Puede encadenar varios formularios para flujos de trabajo más complejos.

Los comandos de acción se pueden desencadenar desde el área de redacción de mensajes, el cuadro de comandos o desde un mensaje. Cuando el comando se invoca desde un mensaje, la carga inicial de JSON enviada a su servicio web incluirá el mensaje completo desde el cual se invocó. La siguiente imagen muestra el módulo de tareas de comandos de acción de extensión de mensajería:

:::image type="content" source="~/assets/images/task-module.png" alt-text="Módulo de tarea de comandos de acción de extensión de mensaje":::

### <a name="search-commands"></a>Comandos de búsqueda

Los comandos de búsqueda permiten a los usuarios buscar información en un sistema externo manualmente a través de un cuadro de búsqueda o pegando un vínculo a un dominio supervisado en el área de redacción de mensajes y, después, insertar los resultados de la búsqueda en un mensaje. En el flujo de comandos de búsqueda más básico, el mensaje de invocación inicial incluirá la cadena de búsqueda que envió el usuario. Responderá con una lista de tarjetas y vistas previas de tarjetas. El cliente Teams provee una lista de vistas previas de tarjetas para el usuario. Cuando el usuario seleccione una tarjeta, la tarjeta a tamaño completo se insertará en el área de redacción del mensajes.

Las tarjetas se desencadenan desde el área de redacción de mensajes o del cuadro de comandos y no se desencadenan desde un mensaje. No se pueden desencadenar desde un mensaje.
La siguiente imagen muestra el módulo de tareas de comandos de búsqueda de extensión de mensajería:

:::image type="content" source="~/assets/images/search-extension.png" alt-text="comando de búsqueda de extensión de mensajería":::

> [!NOTE]
> Para obtener más información sobre las tarjetas, consulte [qué son las tarjetas](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Apertura de vínculos

Se invoca un servicio web cuando se pega una dirección URL en el área de redacción de mensajes. Esta funcionalidad se conoce como apertura de vínculos. Con la apertura de vínculos su aplicación puede registrarse para recibir una invocación cuando se pegan direcciones URL con un dominio en particular en el área de redacción de mensajes. El servicio web puede "abrir" la dirección URL en una tarjeta detallada, lo que proporciona más información que la tarjeta de vista previa del sitio web estándar. Puede agregar botones para permitir que los usuarios realicen acciones inmediatamente sin salir del cliente de Teams.
Las siguientes imágenes muestran la característica de apertura de vínculos cuando se pega un vínculo en la extensión de mensaje:

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="abrir vínculo":::

![apertura de vínculos](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>Fragmentos de código

El siguiente código proporciona un ejemplo de acción basada en extensiones de mensajería:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

 protected override Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
        {
            // Handle different actions using switch
            switch (action.CommandId)
            {
                case "HTML":
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Height = 200,
                                Width = 400,
                                Title = "Task Module HTML Page",
                                Url = baseUrl + "/htmlpage.html",
                            },
                        },
                    };
                // return TaskModuleHTMLPage(turnContext, action);
                default:
                    string memberName = "";
                    var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
                    memberName = member.Name;
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Card = <<AdaptiveAction card json>>,
                                Height = 200,
                                Width = 400,
                                Title = $"Welcome {memberName}",
                            },
                        },
                    };
            }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

    async handleTeamsMessagingExtensionFetchTask(context, action) {
        switch (action.commandId) {
            case 'Static HTML':
                return staticHtmlPage();
        }
    }

    staticHtmlPage(){
        return {
            task: {
                type: 'continue',
                value: {
                    width: 450,
                    height: 125,
                    title: 'Task module Static HTML',
                    url: `${baseurl}/StaticPage.html`
                }
            }
        };
    }

```

---

El código siguiente proporciona un ejemplo para la extensión de mensajería basado en búsquedas:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
        {
            var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

            var packages = new[] {
            new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
            new { title = "Fluent UI Library", value = "FluentUI" }};

            // We take every row of the results and wrap them in cards wrapped in MessagingExtensionAttachment objects.
            // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
            var attachments = packages.Select(package =>
            {
                var previewCard = new ThumbnailCard { Title = package.title, Tap = new CardAction { Type = "invoke", Value = package } };
                if (!string.IsNullOrEmpty(package.title))
                {
                    previewCard.Images = new List<CardImage>() { new CardImage(package.title, "Icon") };
                }

                var attachment = new MessagingExtensionAttachment
                {
                    ContentType = HeroCard.ContentType,
                    Content = new HeroCard { Title = package.title },
                    Preview = previewCard.ToAttachment()
                };

                return attachment;
            }).ToList();

            // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
            return new MessagingExtensionResponse
            {
                ComposeExtension = new MessagingExtensionResult
                {
                    Type = "result",
                    AttachmentLayout = "list",
                    Attachments = attachments
                }
            };
        }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;     
        const attachments = [];
                const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);
                
                response.data.objects.forEach(obj => {
                        const heroCard = CardFactory.heroCard(obj.package.name);
                        const preview = CardFactory.heroCard(obj.package.name);
                        preview.content.tap = { type: 'invoke', value: { description: obj.package.description } };
                        const attachment = { ...heroCard, preview };
                        attachments.push(attachment);
                });
    
                return {
                    composeExtension:  {
                           type: 'result',
                           attachmentLayout: 'list',
                           attachments: attachments
                    }
                };
            }       
        }
```

---

## <a name="code-sample"></a>Ejemplo de código

| **Ejemplo de nombre** | **Descripción** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|------------|
| Extensión de mensajería con comandos basados en acciones | Este ejemplo muestra cómo crear una extensión de mensajería basada en acciones. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensión de mensajería con comandos basados en búsquedas | Este ejemplo muestra cómo crear una Extensión de mensajería Basada en búsquedas. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Acción de extensión de mensajería para la programación de tareas|Este ejemplo muestra cómo programar una tarea a partir del comando de acción de extensión de mensajería y obtener una tarjeta de recordatorio en una fecha y hora programadas.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definición del comando de extensión de mensajería de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>Consulte también

* [Definición del comando de extensión de mensajería de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)
* [Acciones universales para extensiones de mensajería basadas en búsqueda](how-to/search-commands/universal-actions-for-search-based-message-extensions.md)
