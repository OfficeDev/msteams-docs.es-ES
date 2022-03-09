---
title: Extensiones de mensajería
author: surbhigupta
description: Información general sobre las extensiones de mensajería en la Microsoft Teams de mensajería
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 696bd7e97cd2588dc62d934c79a9cd2e9310d07d
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355996"
---
# <a name="messaging-extensions"></a>Extensiones de mensajería

Las extensiones de mensajería permiten a los usuarios interactuar con el servicio web a través de botones y formularios en el Microsoft Teams cliente. Pueden buscar o iniciar acciones en un sistema externo desde el área del mensaje de redacción, el cuadro de comandos o directamente desde un mensaje. Puede devolver los resultados de esa interacción al Microsoft Teams en forma de tarjeta con un formato enriquecido. En este documento se proporciona información general sobre la extensión de mensajería, las tareas realizadas en diferentes escenarios, el trabajo de la extensión de mensajería, la acción y los comandos de búsqueda y la desamuesación de vínculos.

La siguiente imagen muestra las ubicaciones desde las que se invocan las extensiones de mensajería:

![ubicaciones de invocación de extensión de mensajería](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning extensiones de mensaje ya no se admiten en el cuadro de redacción.

## <a name="scenarios-where-messaging-extensions-are-used"></a>Escenarios en los que se usan extensiones de mensajería

| Escenario | Ejemplo |
|:-----------------|:-----------------|
|Desea que algún sistema externo realice una acción y que el resultado de la acción se envíe de vuelta a la conversación.|Reserve un recurso y permita que el canal esté al corriente de la franja horaria reservada.|
|Desea encontrar algo en un sistema externo y compartir los resultados con la conversación.|Busque un elemento de trabajo en Azure DevOps y compártelo con el grupo como una tarjeta adaptable.|
|Desea completar una tarea compleja que incluya varios pasos o mucha información en un sistema externo y compartir los resultados con una conversación.|Crea un error en el sistema de seguimiento basado en un mensaje de Teams, asigna ese error a Bob y envía una tarjeta al hilo de conversación con los detalles del error.|

## <a name="understand-how-messaging-extensions-work"></a>Comprender cómo funcionan las extensiones de mensajería

Una extensión de mensajería consta de un servicio web que hospeda y un manifiesto de aplicación, que define desde dónde se invoca el servicio web en el Microsoft Teams cliente. El servicio web aprovecha el esquema de mensajería de Bot Framework y el protocolo de comunicación seguro, por lo que debe registrar el servicio web como bot en Bot Framework.

> [!NOTE]
> Aunque puede crear el servicio web manualmente, use [bot Framework SDK](https://github.com/microsoft/botframework-sdk) para trabajar con el protocolo.

En el manifiesto de la aplicación Microsoft Teams aplicación, se define una sola extensión de mensajería con hasta diez comandos diferentes. Cada comando define un tipo, como acción o búsqueda, y las ubicaciones del cliente desde donde se invoca. Las ubicaciones de invocación son área de mensaje de redacción, barra de comandos y mensaje. Al invocar, el servicio web recibe un mensaje HTTPS con una carga JSON que incluye toda la información relevante. Responda con una carga JSON, lo que permite al Teams cliente conocer la siguiente interacción que se habilitará.

## <a name="types-of-messaging-extension-commands"></a>Tipos de comandos de extensión de mensajería

Hay dos tipos de comandos de extensión de mensajería, comando de acción y comando de búsqueda. El tipo de comando de extensión de mensajería define los elementos de la interfaz de usuario y los flujos de interacción disponibles para el servicio web. Algunas interacciones, como la autenticación y la configuración, están disponibles para ambos tipos de comandos.

### <a name="action-commands"></a>Comandos de acción

Los comandos action se usan para presentar a los usuarios un elemento emergente modal para recopilar o mostrar información. Cuando el usuario envía el formulario, el servicio web responde insertando un mensaje en la conversación directamente o insertando un mensaje en el área del mensaje de redacción. Después, el usuario puede enviar el mensaje. Puede encadenar varios formularios para flujos de trabajo más complejos.

Los comandos de acción se desencadenan desde el área del mensaje de redacción, el cuadro de comandos o desde un mensaje. Cuando se invoca el comando desde un mensaje, la carga JSON inicial enviada al bot incluye todo el mensaje desde el que se invocó. En la siguiente imagen se muestra el módulo de tareas de comando de acción de extensión de mensajería: módulo ![de tareas de comando de acción de extensión de mensajería](~/assets/images/task-module.png)

### <a name="search-commands"></a>Comandos de búsqueda

Los comandos de búsqueda permiten a los usuarios buscar información en un sistema externo manualmente a través de un cuadro de búsqueda o pegando un vínculo a un dominio supervisado en el área del mensaje de redacción e insertar los resultados de la búsqueda en un mensaje. En el flujo de comandos de búsqueda más básico, el mensaje de invocación inicial incluye la cadena de búsqueda que el usuario envió. Responderá con una lista de tarjetas y vistas previas de tarjetas. El Teams representa una lista de vistas previas de tarjeta para el usuario. Cuando el usuario selecciona una tarjeta de la lista, la tarjeta de tamaño completo se inserta en el área del mensaje de redacción.

Las tarjetas se desencadenan desde el área del mensaje de redacción o el cuadro de comando y no se desencadenan desde un mensaje. No se pueden desencadenar desde un mensaje.
En la siguiente imagen se muestra el módulo de tareas de comando de búsqueda de extensión de mensajería:

![comando de búsqueda de extensión de mensajería](~/assets/images/search-extension.png)

> [!NOTE]
> Para obtener más información sobre las tarjetas, [consulta qué son las tarjetas](../task-modules-and-cards/what-are-cards.md).

## <a name="link-unfurling"></a>Apertura de vínculos

Se invoca un servicio web cuando se pega una dirección URL en el área del mensaje de redacción. Esta funcionalidad se conoce como desenlaznado de vínculos. Puede suscribirse para recibir una invocación cuando las direcciones URL que contienen un dominio determinado se pegan en el área del mensaje de redacción. El servicio web puede "desplegar" la dirección URL en una tarjeta detallada, lo que proporciona más información que la tarjeta de vista previa del sitio web estándar. Puede agregar botones para permitir que los usuarios tomen medidas inmediatamente sin salir del Microsoft Teams cliente.
Las siguientes imágenes muestran la característica de desamuestración de vínculos cuando se pega un vínculo en la extensión de mensajería:

![vínculo unfurl](../assets/images/messaging-extension/unfurl-link.png)

![desafusado de vínculos](../assets/images/messaging-extension/link-unfurl.gif)

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

El código siguiente proporciona un ejemplo de búsqueda basada en extensiones de mensajería:

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
| Extensión de mensajería con comandos basados en acciones | En este ejemplo se muestra cómo crear una extensión de mensajería basada en acciones. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| Extensión de mensajería con comandos basados en búsqueda | En este ejemplo se muestra cómo crear una extensión de mensajería basada en búsquedas. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [Ver](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|Acción de extensión de mensajería para la programación de tareas|En este ejemplo se muestra cómo programar una tarea desde el comando de acción de extensión de mensajería y obtener una tarjeta de aviso en una fecha y hora programadas.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Definir comando de extensión de mensajería de acción](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>Vea también

* [Definir comando de extensión de mensajería de búsqueda](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Crear una extensión de mensajería](../build-your-first-app/build-messaging-extension.md)
