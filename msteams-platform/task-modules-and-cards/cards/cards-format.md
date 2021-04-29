---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjeta en Microsoft Teams
keywords: formato de tarjetas de bots de teams
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: d2806271f99af53139c76dcbd1090a96adcd0f31
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068825"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="53d9f-104">Dar formato a tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="53d9f-104">Format cards in Teams</span></span>

<span data-ttu-id="53d9f-105">Puede agregar formato de texto enriquecido a las tarjetas mediante Markdown o HTML, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="53d9f-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="53d9f-106">Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.</span><span class="sxs-lookup"><span data-stu-id="53d9f-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="53d9f-107">El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="53d9f-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="53d9f-108">Se recomienda usar el formato Markdown para el desarrollo actual y futuro de tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="53d9f-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="53d9f-109">La compatibilidad con el formato difiere entre los distintos tipos de tarjeta y la representación de la tarjeta puede diferir ligeramente entre los clientes de teams móviles y de escritorio, así como teams en el explorador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="53d9f-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="53d9f-110">Puedes incluir una imagen en línea con cualquier tarjeta de Teams.</span><span class="sxs-lookup"><span data-stu-id="53d9f-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="53d9f-111">Las imágenes con formato como , o archivos y no deben superar  `.png` `.jpg` los `.gif` 1024 ×1024 px o 1 MB.</span><span class="sxs-lookup"><span data-stu-id="53d9f-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="53d9f-112">Gif animado no es compatible oficialmente.</span><span class="sxs-lookup"><span data-stu-id="53d9f-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="53d9f-113">*Consulta Referencia* [de tarjetas](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="53d9f-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="53d9f-114">Formato de tarjetas con Markdown</span><span class="sxs-lookup"><span data-stu-id="53d9f-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="53d9f-115">Hay dos tipos de tarjeta que admiten Markdown en Teams:</span><span class="sxs-lookup"><span data-stu-id="53d9f-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53d9f-116">**Tarjetas adaptables:** Markdown se admite en el campo Tarjeta `Textblock` adaptable, así como `Fact.Title` y `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="53d9f-117">Html no se admite en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="53d9f-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="53d9f-118">**Tarjetas de conector de O365:** Markdown y HTML limitado se admiten en las tarjetas de Conector de Office 365 en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="53d9f-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="53d9f-119">**Formato markdown: tarjetas adaptables**</span><span class="sxs-lookup"><span data-stu-id="53d9f-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="53d9f-120">Los estilos admitidos `Textblock` para , `Fact.Title` y `Fact.Value` son:</span><span class="sxs-lookup"><span data-stu-id="53d9f-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="53d9f-121">Estilo</span><span class="sxs-lookup"><span data-stu-id="53d9f-121">Style</span></span> | <span data-ttu-id="53d9f-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="53d9f-122">Example</span></span> | <span data-ttu-id="53d9f-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="53d9f-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53d9f-124">bold</span><span class="sxs-lookup"><span data-stu-id="53d9f-124">bold</span></span> | <span data-ttu-id="53d9f-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="53d9f-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="53d9f-126">italic</span><span class="sxs-lookup"><span data-stu-id="53d9f-126">italic</span></span> | <span data-ttu-id="53d9f-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="53d9f-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="53d9f-128">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="53d9f-128">unordered list</span></span> | <ul><li><span data-ttu-id="53d9f-129">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-129">text</span></span></li><li><span data-ttu-id="53d9f-130">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="53d9f-131">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="53d9f-131">ordered list</span></span> | <ol><li><span data-ttu-id="53d9f-132">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-132">text</span></span></li><li><span data-ttu-id="53d9f-133">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="53d9f-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="53d9f-134">Hyperlinks</span></span> |[<span data-ttu-id="53d9f-135">Bing</span><span class="sxs-lookup"><span data-stu-id="53d9f-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="53d9f-136">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="53d9f-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="53d9f-137">Encabezados</span><span class="sxs-lookup"><span data-stu-id="53d9f-137">Headers</span></span>
* <span data-ttu-id="53d9f-138">Tablas</span><span class="sxs-lookup"><span data-stu-id="53d9f-138">Tables</span></span>
* <span data-ttu-id="53d9f-139">Imágenes</span><span class="sxs-lookup"><span data-stu-id="53d9f-139">Images</span></span>
* <span data-ttu-id="53d9f-140">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="53d9f-140">Preformatted text</span></span>
* <span data-ttu-id="53d9f-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="53d9f-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53d9f-142">Las tarjetas adaptables no admiten formato HTML.</span><span class="sxs-lookup"><span data-stu-id="53d9f-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="53d9f-143">Líneas nuevas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="53d9f-144">En las listas puede usar las `\r` `\n` secuencias de escape o para las líneas nuevas.</span><span class="sxs-lookup"><span data-stu-id="53d9f-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="53d9f-145">Si se usa en una lista, se aplica sangría al siguiente elemento `\n\n` de la lista.</span><span class="sxs-lookup"><span data-stu-id="53d9f-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="53d9f-146">Si necesita líneas nuevas en otra parte del bloque de texto, use `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="53d9f-147">Diferencias de dispositivos móviles y de escritorio para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="53d9f-148">El formato es ligeramente diferente entre el escritorio y las versiones móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="53d9f-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="53d9f-149">En el escritorio, el formato markdown de tarjeta adaptable aparece de esta forma en los exploradores web y en la aplicación cliente de Teams:</span><span class="sxs-lookup"><span data-stu-id="53d9f-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formato markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="53d9f-151">En iOS, el formato markdown de tarjeta adaptable aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="53d9f-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Formato markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="53d9f-153">En Android, el formato de markdown de tarjeta adaptable aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="53d9f-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Formato markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="53d9f-155">Más información sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-155">More information on Adaptive cards</span></span>

<span data-ttu-id="53d9f-156">[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) Las características de fecha y localización mencionadas en este tema no se admiten en Teams.</span><span class="sxs-lookup"><span data-stu-id="53d9f-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="53d9f-157">Ejemplo de formato para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="53d9f-158">Mencione la compatibilidad con tarjetas adaptables v1.2</span><span class="sxs-lookup"><span data-stu-id="53d9f-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="53d9f-159">Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="53d9f-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="53d9f-160">Puede agregar menciones @ dentro de un cuerpo de tarjeta adaptable para bots y respuestas de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="53d9f-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="53d9f-161">Para agregar menciones @ en tarjetas, siga la misma lógica de notificación y representación que las [menciones basadas](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)en mensajes en conversaciones de chat de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="53d9f-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="53d9f-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span><span class="sxs-lookup"><span data-stu-id="53d9f-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="53d9f-163">[Actualmente,](https://adaptivecards.io/explorer/Media.html) los elementos multimedia no se admiten en las tarjetas adaptables v1.2 en la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="53d9f-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="53d9f-164">Las menciones & equipo de canal no se admiten en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="53d9f-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="53d9f-165">Menciones de construcción</span><span class="sxs-lookup"><span data-stu-id="53d9f-165">Constructing mentions</span></span>

<span data-ttu-id="53d9f-166">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="53d9f-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="53d9f-167">`<at>username</at>` en los elementos de tarjeta adaptable compatibles.</span><span class="sxs-lookup"><span data-stu-id="53d9f-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="53d9f-168">El objeto dentro de una propiedad en el contenido de la tarjeta, que incluye el identificador de usuario `mention` de Teams del usuario `msteams` mencionado.</span><span class="sxs-lookup"><span data-stu-id="53d9f-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="53d9f-169">El `userId` es único para el identificador del bot y un usuario en particular.</span><span class="sxs-lookup"><span data-stu-id="53d9f-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="53d9f-170">Se puede usar para @mention un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="53d9f-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="53d9f-171">Se `userId` puede recuperar mediante una de las opciones mencionadas en obtener el identificador de [usuario](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="53d9f-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="53d9f-172">Tarjeta adaptable de ejemplo con una mención</span><span class="sxs-lookup"><span data-stu-id="53d9f-172">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="53d9f-173">Enmascaramiento de información en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="53d9f-174">Use la propiedad information masking para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada de [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="53d9f-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="53d9f-175">La característica solo admite el enmascaramiento de información del lado [cliente,](../../build-your-first-app/build-bot.md)el texto de entrada enmascarado se envía como texto sin formato a la dirección del extremo https que se especificó durante la configuración del bot .</span><span class="sxs-lookup"><span data-stu-id="53d9f-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="53d9f-176">La propiedad de enmascaramiento de información está disponible actualmente solo en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="53d9f-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="53d9f-177">Para enmascarar la información en tarjetas adaptables, agregue la `isMasked` propiedad **al tipo** y establezca su valor `Input.Text` en *true*.</span><span class="sxs-lookup"><span data-stu-id="53d9f-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="53d9f-178">Tarjeta adaptable de ejemplo con la propiedad masking</span><span class="sxs-lookup"><span data-stu-id="53d9f-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="53d9f-179">La siguiente imagen es un ejemplo de enmascaramiento de información en tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="53d9f-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Imagen de información de enmascaramiento](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="53d9f-181">Tarjeta adaptable de ancho completo</span><span class="sxs-lookup"><span data-stu-id="53d9f-181">Full width Adaptive card</span></span>
<span data-ttu-id="53d9f-182">Puede usar la propiedad para expandir el ancho de una tarjeta adaptable y `msteams` usar espacio de lienzo adicional.</span><span class="sxs-lookup"><span data-stu-id="53d9f-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="53d9f-183">Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53d9f-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="53d9f-184">Construcción de tarjetas de ancho completo</span><span class="sxs-lookup"><span data-stu-id="53d9f-184">Constructing full width cards</span></span>
<span data-ttu-id="53d9f-185">Para que una tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la `width` `msteams` tarjeta debe establecerse en `Full` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="53d9f-186">Además, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="53d9f-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="53d9f-187">Tarjeta adaptable de ejemplo con ancho completo</span><span class="sxs-lookup"><span data-stu-id="53d9f-187">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="53d9f-188">Una tarjeta adaptable de ancho completo aparece de la siguiente manera: ![ Vista de tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="53d9f-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="53d9f-189">Si no ha establecido la propiedad en Full , la vista predeterminada de la tarjeta adaptable es la siguiente: Vista de tarjeta adaptable `width` de ancho  ![ pequeño](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="53d9f-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="53d9f-190">Compatibilidad con Typeahead</span><span class="sxs-lookup"><span data-stu-id="53d9f-190">Typeahead support</span></span>

<span data-ttu-id="53d9f-191">Dentro del elemento de esquema, pedir a los usuarios que filtren y seleccionen a través de un número considerable de opciones puede ralentizar significativamente la finalización [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de tareas.</span><span class="sxs-lookup"><span data-stu-id="53d9f-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="53d9f-192">La compatibilidad con la punta de tipo dentro de las tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada cuando un usuario escribe la entrada.</span><span class="sxs-lookup"><span data-stu-id="53d9f-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="53d9f-193">Habilitar el cabezal de tipo en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="53d9f-194">Para habilitar typeahead dentro del `Input.Choiceset` conjunto en y asegurarse de que está establecido en `style` `filtered` `isMultiSelect` `false` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="53d9f-195">Tarjeta adaptable de ejemplo con compatibilidad con membrete</span><span class="sxs-lookup"><span data-stu-id="53d9f-195">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="53d9f-196">Vista de fase para imágenes en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="53d9f-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="53d9f-197">Esta característica está disponible actualmente solo en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="53d9f-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="53d9f-198">En una tarjeta adaptable, puedes usar la propiedad para agregar la capacidad de mostrar imágenes en la vista de fase `msteams` de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="53d9f-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="53d9f-199">Cuando los usuarios mantienen el mouse sobre las imágenes, verían un icono de expansión, para el que `allowExpand` el atributo está establecido en `true` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="53d9f-200">Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53d9f-200">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="53d9f-201">Cuando los usuarios mantienen el mouse sobre la imagen, aparece un icono expandir en la esquina superior derecha de la imagen: ![ tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="53d9f-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="53d9f-202">La imagen aparece en la vista de fase cuando el usuario selecciona el botón expandir: ![ Imagen expandida a vista de fase](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="53d9f-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="53d9f-203">En la vista de fase, los usuarios pueden acercar y alejar la imagen.</span><span class="sxs-lookup"><span data-stu-id="53d9f-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="53d9f-204">Puedes seleccionar qué imágenes de la tarjeta adaptable deben tener esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="53d9f-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="53d9f-205">La funcionalidad acercar y alejar solo se aplica a los elementos de imagen (tipo Image) de una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="53d9f-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="53d9f-206">En el caso de las aplicaciones móviles de Teams, la funcionalidad de vista de fase para imágenes en tarjetas adaptables está disponible de forma predeterminada y los usuarios podrán ver imágenes de tarjeta adaptables en la vista de fase simplemente pulsando en la imagen, independientemente de si el atributo está presente o `allowExpand` no.</span><span class="sxs-lookup"><span data-stu-id="53d9f-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="53d9f-207">**Formato markdown: tarjetas de conector de O365**</span><span class="sxs-lookup"><span data-stu-id="53d9f-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="53d9f-208">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="53d9f-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="53d9f-209">La compatibilidad con HTML se describe en la última sección.</span><span class="sxs-lookup"><span data-stu-id="53d9f-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="53d9f-210">Estilo</span><span class="sxs-lookup"><span data-stu-id="53d9f-210">Style</span></span> | <span data-ttu-id="53d9f-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="53d9f-211">Example</span></span> | <span data-ttu-id="53d9f-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="53d9f-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53d9f-213">bold</span><span class="sxs-lookup"><span data-stu-id="53d9f-213">bold</span></span> | <span data-ttu-id="53d9f-214">**text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="53d9f-215">italic</span><span class="sxs-lookup"><span data-stu-id="53d9f-215">italic</span></span> | <span data-ttu-id="53d9f-216">*text*</span><span class="sxs-lookup"><span data-stu-id="53d9f-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="53d9f-217">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="53d9f-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="53d9f-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="53d9f-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="53d9f-219">strikethrough</span></span> | <span data-ttu-id="53d9f-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="53d9f-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="53d9f-221">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="53d9f-221">unordered list</span></span> | <ul><li><span data-ttu-id="53d9f-222">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-222">text</span></span></li><li><span data-ttu-id="53d9f-223">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="53d9f-224">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="53d9f-224">ordered list</span></span> | <ol><li><span data-ttu-id="53d9f-225">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-225">text</span></span></li><li><span data-ttu-id="53d9f-226">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="53d9f-227">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="53d9f-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="53d9f-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="53d9f-228">blockquote</span></span> | <span data-ttu-id="53d9f-229">>texto de bloques</span><span class="sxs-lookup"><span data-stu-id="53d9f-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="53d9f-230">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="53d9f-230">hyperlink</span></span> | [<span data-ttu-id="53d9f-231">Bing</span><span class="sxs-lookup"><span data-stu-id="53d9f-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="53d9f-232">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="53d9f-232">image link</span></span> |![Agacharse en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="53d9f-234">En las tarjetas de conector, las líneas nuevas se representan `\n\n` para , pero no para o `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="53d9f-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="53d9f-235">Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con Markdown</span><span class="sxs-lookup"><span data-stu-id="53d9f-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="53d9f-236">En el escritorio, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="53d9f-238">En iOS, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="53d9f-240">Problemas:</span><span class="sxs-lookup"><span data-stu-id="53d9f-240">Issues:</span></span>

* <span data-ttu-id="53d9f-241">El cliente de iOS para Teams no representa imágenes en línea markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="53d9f-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="53d9f-242">Las comillas bloques se representan como sangría pero sin un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="53d9f-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="53d9f-243">En Android, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="53d9f-245">Ejemplo de formato para tarjetas de conector de Markdown</span><span class="sxs-lookup"><span data-stu-id="53d9f-245">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="53d9f-246">Formato de tarjetas con HTML</span><span class="sxs-lookup"><span data-stu-id="53d9f-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="53d9f-247">**Formato HTML: tarjetas de conector de O365**</span><span class="sxs-lookup"><span data-stu-id="53d9f-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="53d9f-248">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="53d9f-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="53d9f-249">Markdown se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="53d9f-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="53d9f-250">Estilo</span><span class="sxs-lookup"><span data-stu-id="53d9f-250">Style</span></span> | <span data-ttu-id="53d9f-251">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="53d9f-251">Example</span></span> | <span data-ttu-id="53d9f-252">HTML</span><span class="sxs-lookup"><span data-stu-id="53d9f-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53d9f-253">bold</span><span class="sxs-lookup"><span data-stu-id="53d9f-253">bold</span></span> | <span data-ttu-id="53d9f-254">**text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="53d9f-255">italic</span><span class="sxs-lookup"><span data-stu-id="53d9f-255">italic</span></span> | <span data-ttu-id="53d9f-256">*text*</span><span class="sxs-lookup"><span data-stu-id="53d9f-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="53d9f-257">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="53d9f-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="53d9f-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="53d9f-259">strikethrough</span><span class="sxs-lookup"><span data-stu-id="53d9f-259">strikethrough</span></span> | <span data-ttu-id="53d9f-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="53d9f-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="53d9f-261">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="53d9f-261">unordered list</span></span> | <ul><li><span data-ttu-id="53d9f-262">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-262">text</span></span></li><li><span data-ttu-id="53d9f-263">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="53d9f-264">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="53d9f-264">ordered list</span></span> | <ol><li><span data-ttu-id="53d9f-265">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-265">text</span></span></li><li><span data-ttu-id="53d9f-266">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="53d9f-267">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="53d9f-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="53d9f-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="53d9f-268">blockquote</span></span> | <blockquote><span data-ttu-id="53d9f-269">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="53d9f-270">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="53d9f-270">hyperlink</span></span> | [<span data-ttu-id="53d9f-271">Bing</span><span class="sxs-lookup"><span data-stu-id="53d9f-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="53d9f-272">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="53d9f-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="53d9f-273">En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="53d9f-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="53d9f-274">Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con HTML</span><span class="sxs-lookup"><span data-stu-id="53d9f-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="53d9f-275">En el escritorio, el formato HTML de las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="53d9f-277">En iOS, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-277">On iOS, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="53d9f-279">Problemas:</span><span class="sxs-lookup"><span data-stu-id="53d9f-279">Issues:</span></span>

* <span data-ttu-id="53d9f-280">Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="53d9f-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="53d9f-281">El texto con formato previo se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="53d9f-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="53d9f-282">En Android, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="53d9f-282">On Android, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="53d9f-284">Ejemplo de formato para tarjetas de conector HTML</span><span class="sxs-lookup"><span data-stu-id="53d9f-284">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="53d9f-285">**Formato HTML: tarjetas de miniatura y de héroe**</span><span class="sxs-lookup"><span data-stu-id="53d9f-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="53d9f-286">Las etiquetas HTML son compatibles con tarjetas sencillas, como la tarjeta de miniatura y la de héroe.</span><span class="sxs-lookup"><span data-stu-id="53d9f-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="53d9f-287">Markdown no es compatible.</span><span class="sxs-lookup"><span data-stu-id="53d9f-287">Markdown is not supported.</span></span>

| <span data-ttu-id="53d9f-288">Estilo</span><span class="sxs-lookup"><span data-stu-id="53d9f-288">Style</span></span> | <span data-ttu-id="53d9f-289">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="53d9f-289">Example</span></span> | <span data-ttu-id="53d9f-290">HTML</span><span class="sxs-lookup"><span data-stu-id="53d9f-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53d9f-291">bold</span><span class="sxs-lookup"><span data-stu-id="53d9f-291">bold</span></span> | <span data-ttu-id="53d9f-292">**text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="53d9f-293">italic</span><span class="sxs-lookup"><span data-stu-id="53d9f-293">italic</span></span> | <span data-ttu-id="53d9f-294">*text*</span><span class="sxs-lookup"><span data-stu-id="53d9f-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="53d9f-295">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="53d9f-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="53d9f-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="53d9f-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="53d9f-297">strikethrough</span><span class="sxs-lookup"><span data-stu-id="53d9f-297">strikethrough</span></span> | <span data-ttu-id="53d9f-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="53d9f-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="53d9f-299">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="53d9f-299">unordered list</span></span> | <ul><li><span data-ttu-id="53d9f-300">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-300">text</span></span></li><li><span data-ttu-id="53d9f-301">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="53d9f-302">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="53d9f-302">ordered list</span></span> | <ol><li><span data-ttu-id="53d9f-303">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-303">text</span></span></li><li><span data-ttu-id="53d9f-304">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="53d9f-305">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="53d9f-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="53d9f-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="53d9f-306">blockquote</span></span> | <blockquote><span data-ttu-id="53d9f-307">text</span><span class="sxs-lookup"><span data-stu-id="53d9f-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="53d9f-308">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="53d9f-308">hyperlink</span></span> | [<span data-ttu-id="53d9f-309">Bing</span><span class="sxs-lookup"><span data-stu-id="53d9f-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="53d9f-310">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="53d9f-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="53d9f-311">Diferencias de escritorio y móvil para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="53d9f-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="53d9f-312">Debido a las diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="53d9f-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="53d9f-313">En el escritorio, el formato HTML aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="53d9f-313">On the desktop, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="53d9f-315">En iOS, el formato HTML aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="53d9f-315">On iOS, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="53d9f-317">Problemas:</span><span class="sxs-lookup"><span data-stu-id="53d9f-317">Issues:</span></span>

* <span data-ttu-id="53d9f-318">El formato de caracteres como negrita y cursiva no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="53d9f-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="53d9f-319">En Android, el formato HTML aparece de esta forma:</span><span class="sxs-lookup"><span data-stu-id="53d9f-319">On Android, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="53d9f-321">El formato de caracteres como negrita y cursiva se muestra correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="53d9f-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="53d9f-322">Ejemplo de formato para formato HTML en tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="53d9f-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="53d9f-323">Estas capturas de pantalla se crearon con Teams AppStudio, donde la propiedad de texto de una tarjeta de héroe se estableció en la siguiente cadena.</span><span class="sxs-lookup"><span data-stu-id="53d9f-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="53d9f-324">Puedes probar el formato en tus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="53d9f-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
