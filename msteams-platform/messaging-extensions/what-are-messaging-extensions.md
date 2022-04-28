---
title: Extensiones de mensaje
author: surbhigupta
description: Introducción a las extensiones de mensaje en la plataforma de Microsoft Teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c81f8ec4b1158275ab796883b268d2c7fa6ecfe8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104115"
---
# <a name="message-extensions"></a>Extensiones de mensaje

Las extensiones de mensaje permiten a los usuarios interactuar con el servicio web a través de botones y formularios en el cliente Microsoft Teams. Pueden buscar o iniciar acciones en un sistema externo desde el área del mensaje de redacción, el cuadro de comandos o directamente desde un mensaje. Puede devolver los resultados de esa interacción al cliente de Microsoft Teams en forma de tarjeta con formato enriquecido. En este documento se proporciona información general sobre la extensión del mensaje, las tareas realizadas en diferentes escenarios, el trabajo de la extensión de mensaje, los comandos de acción y búsqueda y la desplegamiento de vínculos.

En la imagen siguiente se muestran las ubicaciones desde las que se invocan las extensiones de mensaje:

![Ubicaciones de invocación de extensión de mensaje](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning extensiones de mensaje ya no se admite en el cuadro de redacción.

## <a name="scenarios-where-message-extensions-are-used"></a>Escenarios en los que se usan extensiones de mensaje

| Escenario | Ejemplo |
|:-----------------|:-----------------|
|Quiere que algún sistema externo realice una acción y que el resultado de la acción se devuelva a la conversación.|Reserve un recurso y permita que el canal esté al corriente de la franja horaria reservada.|
|Quiere encontrar algo en un sistema externo y compartir los resultados con la conversación.|Busque un elemento de trabajo en Azure DevOps y compárelo con el grupo como una tarjeta adaptable.|
|Quiere completar una tarea compleja que implique varios pasos o una gran cantidad de información en un sistema externo y compartir los resultados con una conversación.|Cree un error en el sistema de seguimiento en función de un mensaje de Teams, asigne ese error a Bob y envíe una tarjeta al subproceso de conversación con los detalles del error.|

## <a name="understand-how-message-extensions-work"></a>Descripción del funcionamiento de las extensiones de mensaje

Una extensión de mensaje consta de un servicio web que se hospeda y un manifiesto de aplicación, que define desde dónde se invoca el servicio web en el cliente Microsoft Teams. El servicio web aprovecha el esquema de mensajería de Bot Framework y el protocolo de comunicación seguro, por lo que debe registrar el servicio web como bot en Bot Framework.

> [!NOTE]
> Aunque puede crear el servicio web manualmente, use [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) para trabajar con el protocolo.

En el manifiesto de la aplicación para Microsoft Teams aplicación, se define una única extensión de mensaje con hasta diez comandos diferentes. Cada comando define un tipo, como acción o búsqueda y las ubicaciones del cliente desde donde se invoca. Las ubicaciones de invocación son área de mensaje de redacción, barra de comandos y mensaje. Al invocar, el servicio web recibe un mensaje HTTPS con una carga JSON que incluye toda la información pertinente. Responda con una carga JSON, lo que permite al cliente de Teams conocer la siguiente interacción que se va a habilitar.

## <a name="types-of-message-extension-commands"></a>Tipos de comandos de extensión de mensaje

Hay dos tipos de comandos de extensión de mensaje, comando de acción y comando de búsqueda. El tipo de comando de extensión de mensaje define los elementos de la interfaz de usuario y los flujos de interacción disponibles para el servicio web. Algunas interacciones, como la autenticación y la configuración, están disponibles para ambos tipos de comandos.

### <a name="action-commands"></a>Comandos de acción

Los comandos de acción se usan para presentar a los usuarios un elemento emergente modal para recopilar o mostrar información. Cuando el usuario envía el formulario, el servicio web responde insertando un mensaje en la conversación directamente o insertando un mensaje en el área de redacción del mensaje. Después, el usuario puede enviar el mensaje. Puede encadenar varios formularios para flujos de trabajo más complejos.

Los comandos de acción se desencadenan desde el área del mensaje de redacción, el cuadro de comandos o desde un mensaje. Cuando se invoca el comando desde un mensaje, la carga JSON inicial enviada al bot incluye todo el mensaje desde el que se invocó. En la imagen siguiente se muestra el módulo de tareas de comandos de acción de extensión de mensaje: ![módulo de tareas de comando de acción de extensión de mensaje](~/assets/images/task-module.png)

### <a name="search-commands"></a>Comandos de búsqueda

Los comandos de búsqueda permiten a los usuarios buscar información en un sistema externo manualmente a través de un cuadro de búsqueda o pegando un vínculo a un dominio supervisado en el área de redacción del mensaje e insertan los resultados de la búsqueda en un mensaje. En el flujo de comandos de búsqueda más básico, el mensaje de invocación inicial incluye la cadena de búsqueda que envió el usuario. Responde con una lista de tarjetas y vistas previas de tarjetas. El cliente Teams representa una lista de vistas previas de tarjetas para el usuario. Cuando el usuario selecciona una tarjeta de la lista, la tarjeta de tamaño completo se inserta en el área del mensaje de redacción.

Las tarjetas se desencadenan desde el área del mensaje de redacción o el cuadro de comandos y no se desencadenan desde un mensaje. No se pueden desencadenar a partir de un mensaje.
En la imagen siguiente se muestra el módulo de tareas de comandos de búsqueda de extensión de mensaje:

![comando de búsqueda de extensión de mensaje](~/assets/images/search-extension.png)

> [!NOTE]
> Para obtener más información sobre las tarjetas, consulte [qué son las tarjetas](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Apertura de vínculos

Se invoca un servicio web cuando se pega una dirección URL en el área del mensaje de redacción. Esta funcionalidad se conoce como desplegamiento de vínculos. Puede suscribirse para recibir una invocación cuando las direcciones URL que contienen un dominio determinado se pegan en el área del mensaje de redacción. El servicio web puede "desplegar" la dirección URL en una tarjeta detallada, lo que proporciona más información que la tarjeta de vista previa del sitio web estándar. Puede agregar botones para permitir que los usuarios realicen acciones inmediatamente sin salir del cliente Microsoft Teams.
Las siguientes imágenes muestran la característica de desplegamiento de vínculos cuando se pega un vínculo en la extensión de mensaje:

![unfurl link](../assets/images/messaging-extension/unfurl-link.png)

![desplegamiento de vínculos](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>Fragmentos de código

El código siguiente proporciona un ejemplo de acción basada en extensiones de mensaje:

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

El código siguiente proporciona un ejemplo de búsqueda basada en extensiones de mensaje:

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
| Extensión de mensaje con comandos basados en acciones | En este ejemplo se muestra cómo crear una extensión de mensaje basada en acciones. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensión de mensaje con comandos basados en búsqueda | En este ejemplo se muestra cómo crear una extensión de mensaje basada en búsqueda. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Acción de extensión de mensaje para la programación de tareas|En este ejemplo se muestra cómo programar una tarea a partir del comando de acción de extensión de mensaje y obtener una tarjeta de recordatorio en una fecha y hora programadas.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definición del comando de extensión de mensaje de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>Vea también

* [Definición del comando de extensión de mensaje de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Creación de una extensión de mensaje](../build-your-first-app/build-messaging-extension.md)
