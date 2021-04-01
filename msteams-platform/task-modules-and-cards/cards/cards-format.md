---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjeta en Microsoft Teams
keywords: formato de tarjetas de bots de teams
ms.date: 03/29/2018
ms.openlocfilehash: d7016f8b954e885221c55bd6c29309fd90a1dcfc
ms.sourcegitcommit: d41da0b608327829b902aded6bc85c0d0016d068
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475002"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="7fe79-104">Dar formato a tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="7fe79-104">Format cards in Teams</span></span>

<span data-ttu-id="7fe79-105">Puede agregar formato de texto enriquecido a las tarjetas mediante Markdown o HTML, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="7fe79-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="7fe79-106">Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.</span><span class="sxs-lookup"><span data-stu-id="7fe79-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="7fe79-107">El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="7fe79-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="7fe79-108">Se recomienda usar el formato Markdown para el desarrollo actual y futuro de tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="7fe79-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="7fe79-109">La compatibilidad con el formato difiere entre los distintos tipos de tarjeta y la representación de la tarjeta puede diferir ligeramente entre los clientes de teams móviles y de escritorio, así como teams en el explorador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="7fe79-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="7fe79-110">Puedes incluir una imagen en línea con cualquier tarjeta de Teams.</span><span class="sxs-lookup"><span data-stu-id="7fe79-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="7fe79-111">Las imágenes con formato como , o archivos y no deben superar  `.png` `.jpg` los `.gif` 1024 ×1024 px o 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7fe79-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="7fe79-112">Gif animado no es compatible oficialmente.</span><span class="sxs-lookup"><span data-stu-id="7fe79-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="7fe79-113">*Consulta Referencia* [de tarjetas](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="7fe79-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="7fe79-114">Formato de tarjetas con Markdown</span><span class="sxs-lookup"><span data-stu-id="7fe79-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="7fe79-115">Hay dos tipos de tarjeta que admiten Markdown en Teams:</span><span class="sxs-lookup"><span data-stu-id="7fe79-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fe79-116">**Tarjetas adaptables:** Markdown se admite en el campo Tarjeta `Textblock` adaptable, así como `Fact.Title` y `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="7fe79-117">Html no se admite en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="7fe79-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="7fe79-118">**Tarjetas de conector de O365:** Markdown y HTML limitado se admiten en las tarjetas de Conector de Office 365 en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="7fe79-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="7fe79-119">**Formato markdown: tarjetas adaptables**</span><span class="sxs-lookup"><span data-stu-id="7fe79-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="7fe79-120">Los estilos admitidos `Textblock` para , `Fact.Title` y `Fact.Value` son:</span><span class="sxs-lookup"><span data-stu-id="7fe79-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="7fe79-121">Estilo</span><span class="sxs-lookup"><span data-stu-id="7fe79-121">Style</span></span> | <span data-ttu-id="7fe79-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7fe79-122">Example</span></span> | <span data-ttu-id="7fe79-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="7fe79-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fe79-124">bold</span><span class="sxs-lookup"><span data-stu-id="7fe79-124">bold</span></span> | <span data-ttu-id="7fe79-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="7fe79-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="7fe79-126">italic</span><span class="sxs-lookup"><span data-stu-id="7fe79-126">italic</span></span> | <span data-ttu-id="7fe79-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="7fe79-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="7fe79-128">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="7fe79-128">unordered list</span></span> | <ul><li><span data-ttu-id="7fe79-129">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-129">text</span></span></li><li><span data-ttu-id="7fe79-130">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="7fe79-131">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="7fe79-131">ordered list</span></span> | <ol><li><span data-ttu-id="7fe79-132">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-132">text</span></span></li><li><span data-ttu-id="7fe79-133">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="7fe79-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="7fe79-134">Hyperlinks</span></span> |[<span data-ttu-id="7fe79-135">Bing</span><span class="sxs-lookup"><span data-stu-id="7fe79-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="7fe79-136">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="7fe79-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="7fe79-137">Encabezados</span><span class="sxs-lookup"><span data-stu-id="7fe79-137">Headers</span></span>
* <span data-ttu-id="7fe79-138">Tablas</span><span class="sxs-lookup"><span data-stu-id="7fe79-138">Tables</span></span>
* <span data-ttu-id="7fe79-139">Imágenes</span><span class="sxs-lookup"><span data-stu-id="7fe79-139">Images</span></span>
* <span data-ttu-id="7fe79-140">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="7fe79-140">Preformatted text</span></span>
* <span data-ttu-id="7fe79-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="7fe79-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fe79-142">Las tarjetas adaptables no admiten formato HTML.</span><span class="sxs-lookup"><span data-stu-id="7fe79-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="7fe79-143">Líneas nuevas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="7fe79-144">En las listas puede usar las `\r` `\n` secuencias de escape o para las líneas nuevas.</span><span class="sxs-lookup"><span data-stu-id="7fe79-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="7fe79-145">Si se usa en una lista, se aplica sangría al siguiente elemento `\n\n` de la lista.</span><span class="sxs-lookup"><span data-stu-id="7fe79-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="7fe79-146">Si necesita líneas nuevas en otra parte del bloque de texto, use `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="7fe79-147">Diferencias de dispositivos móviles y de escritorio para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="7fe79-148">El formato es ligeramente diferente entre el escritorio y las versiones móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="7fe79-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="7fe79-149">En el escritorio, el formato markdown de tarjeta adaptable aparece de esta forma en los exploradores web y en la aplicación cliente de Teams:</span><span class="sxs-lookup"><span data-stu-id="7fe79-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formato markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="7fe79-151">En iOS, el formato markdown de tarjeta adaptable aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="7fe79-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Formato markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="7fe79-153">En Android, el formato de markdown de tarjeta adaptable aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="7fe79-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Formato markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="7fe79-155">Más información sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-155">More information on Adaptive cards</span></span>

<span data-ttu-id="7fe79-156">[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) Las características de fecha y localización mencionadas en este tema no se admiten en Teams.</span><span class="sxs-lookup"><span data-stu-id="7fe79-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="7fe79-157">Ejemplo de formato para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="7fe79-158">Mencione la compatibilidad con tarjetas adaptables v1.2</span><span class="sxs-lookup"><span data-stu-id="7fe79-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="7fe79-159">Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="7fe79-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="7fe79-160">Puede agregar menciones @ dentro de un cuerpo de tarjeta adaptable para bots y respuestas de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="7fe79-160">You can add @ mentions within an Adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="7fe79-161">Para agregar menciones @ en tarjetas, siga la misma lógica de notificación y representación que las [menciones basadas](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )en mensajes en conversaciones de chat de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="7fe79-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="7fe79-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span><span class="sxs-lookup"><span data-stu-id="7fe79-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="7fe79-163">[Actualmente,](https://adaptivecards.io/explorer/Media.html) los elementos multimedia no se admiten en las tarjetas adaptables v1.2 en la plataforma de Teams.</span><span class="sxs-lookup"><span data-stu-id="7fe79-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="7fe79-164">Las menciones & equipo de canal no se admiten en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="7fe79-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="7fe79-165">Menciones de construcción</span><span class="sxs-lookup"><span data-stu-id="7fe79-165">Constructing mentions</span></span>

<span data-ttu-id="7fe79-166">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos</span><span class="sxs-lookup"><span data-stu-id="7fe79-166">To include a mention in an Adaptive card your app needs to include the following elements</span></span>

* <span data-ttu-id="7fe79-167">`<at>username</at>` en los elementos de tarjeta adaptable compatibles</span><span class="sxs-lookup"><span data-stu-id="7fe79-167">`<at>username</at>` in the supported Adaptive card elements</span></span>
* <span data-ttu-id="7fe79-168">El objeto dentro de una propiedad en el contenido de la tarjeta, que incluye el identificador de usuario `mention` de Teams del usuario `msteams` mencionado</span><span class="sxs-lookup"><span data-stu-id="7fe79-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="7fe79-169">Tarjeta adaptable de ejemplo con una mención</span><span class="sxs-lookup"><span data-stu-id="7fe79-169">Sample Adaptive card with a mention</span></span>

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


### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="7fe79-170">Enmascaramiento de información en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-170">Information masking in Adaptive cards</span></span>
<span data-ttu-id="7fe79-171">Use la propiedad information masking para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada de [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7fe79-171">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="7fe79-172">La característica solo admite el enmascaramiento de información del lado [cliente,](../../build-your-first-app/build-bot.md#4-configure-your-bot)el texto de entrada enmascarado se envía como texto sin formato a la dirección del extremo https que se especificó durante la configuración del bot .</span><span class="sxs-lookup"><span data-stu-id="7fe79-172">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-configure-your-bot).</span></span> 

> [!NOTE]
> <span data-ttu-id="7fe79-173">La propiedad de enmascaramiento de información está disponible actualmente solo en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="7fe79-173">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="7fe79-174">Para enmascarar la información en tarjetas adaptables, agregue la `isMasked` propiedad **al tipo** y establezca su valor `Input.Text` en *true*.</span><span class="sxs-lookup"><span data-stu-id="7fe79-174">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="7fe79-175">Tarjeta adaptable de ejemplo con la propiedad masking</span><span class="sxs-lookup"><span data-stu-id="7fe79-175">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="7fe79-176">La siguiente imagen es un ejemplo de enmascaramiento de información en tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="7fe79-176">The following image is an example of masking information in Adaptive cards:</span></span>

![Imagen de información de enmascaramiento](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="7fe79-178">Tarjeta adaptable de ancho completo</span><span class="sxs-lookup"><span data-stu-id="7fe79-178">Full width Adaptive card</span></span>
<span data-ttu-id="7fe79-179">Puede usar la propiedad para expandir el ancho de una tarjeta adaptable y `msteams` usar espacio de lienzo adicional.</span><span class="sxs-lookup"><span data-stu-id="7fe79-179">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="7fe79-180">Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7fe79-180">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="7fe79-181">Construcción de tarjetas de ancho completo</span><span class="sxs-lookup"><span data-stu-id="7fe79-181">Constructing full width cards</span></span>
<span data-ttu-id="7fe79-182">Para que una tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la `width` `msteams` tarjeta debe establecerse en `Full` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-182">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="7fe79-183">Además, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7fe79-183">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="7fe79-184">Tarjeta adaptable de ejemplo con ancho completo</span><span class="sxs-lookup"><span data-stu-id="7fe79-184">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="7fe79-185">Una tarjeta adaptable de ancho completo aparece de la siguiente manera: ![ Vista de tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="7fe79-185">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="7fe79-186">Si no ha establecido la propiedad en Full , la vista predeterminada de la tarjeta adaptable es la siguiente: Vista de tarjeta adaptable `width` de ancho  ![ pequeño](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="7fe79-186">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="7fe79-187">Compatibilidad con Typeahead</span><span class="sxs-lookup"><span data-stu-id="7fe79-187">Typeahead support</span></span>

<span data-ttu-id="7fe79-188">Dentro del elemento de esquema, pedir a los usuarios que filtren y seleccionen a través de un número considerable de opciones puede ralentizar significativamente la finalización [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de tareas.</span><span class="sxs-lookup"><span data-stu-id="7fe79-188">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="7fe79-189">La compatibilidad con la punta de tipo dentro de las tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada cuando un usuario escribe la entrada.</span><span class="sxs-lookup"><span data-stu-id="7fe79-189">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="7fe79-190">Habilitar el cabezal de tipo en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-190">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="7fe79-191">Para habilitar typeahead dentro del `Input.Choiceset` conjunto en y asegurarse de que está establecido en `style` `filtered` `isMultiSelect` `false` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-191">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="7fe79-192">Tarjeta adaptable de ejemplo con compatibilidad con membrete</span><span class="sxs-lookup"><span data-stu-id="7fe79-192">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="7fe79-193">Vista de fase para imágenes en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="7fe79-193">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="7fe79-194">Esta característica está disponible actualmente solo en la versión preliminar del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="7fe79-194">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="7fe79-195">En una tarjeta adaptable, puedes usar la propiedad para agregar la capacidad de mostrar imágenes en la vista de fase `msteams` de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="7fe79-195">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="7fe79-196">Cuando los usuarios mantienen el mouse sobre las imágenes, verían un icono de expansión, para el que `allowExpand` el atributo está establecido en `true` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-196">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="7fe79-197">Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7fe79-197">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="7fe79-198">Cuando los usuarios mantienen el mouse sobre la imagen, aparece un icono expandir en la esquina superior derecha de la imagen: ![ tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="7fe79-198">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="7fe79-199">La imagen aparece en la vista de fase cuando el usuario selecciona el botón expandir: ![ Imagen expandida a vista de fase](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="7fe79-199">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="7fe79-200">En la vista de fase, los usuarios pueden acercar y alejar la imagen.</span><span class="sxs-lookup"><span data-stu-id="7fe79-200">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="7fe79-201">Puedes seleccionar qué imágenes de la tarjeta adaptable deben tener esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="7fe79-201">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe79-202">La funcionalidad acercar y alejar solo se aplica a los elementos de imagen (tipo Image) de una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="7fe79-202">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe79-203">En el caso de las aplicaciones móviles de Teams, la funcionalidad de vista de fase para imágenes en tarjetas adaptables está disponible de forma predeterminada y los usuarios podrán ver imágenes de tarjeta adaptables en la vista de fase simplemente pulsando en la imagen, independientemente de si el atributo está presente o `allowExpand` no.</span><span class="sxs-lookup"><span data-stu-id="7fe79-203">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="7fe79-204">**Formato markdown: tarjetas de conector de O365**</span><span class="sxs-lookup"><span data-stu-id="7fe79-204">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="7fe79-205">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="7fe79-205">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="7fe79-206">La compatibilidad con HTML se describe en la última sección.</span><span class="sxs-lookup"><span data-stu-id="7fe79-206">HTML support is described in the last section.</span></span>

| <span data-ttu-id="7fe79-207">Estilo</span><span class="sxs-lookup"><span data-stu-id="7fe79-207">Style</span></span> | <span data-ttu-id="7fe79-208">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7fe79-208">Example</span></span> | <span data-ttu-id="7fe79-209">Markdown</span><span class="sxs-lookup"><span data-stu-id="7fe79-209">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fe79-210">bold</span><span class="sxs-lookup"><span data-stu-id="7fe79-210">bold</span></span> | <span data-ttu-id="7fe79-211">**text**</span><span class="sxs-lookup"><span data-stu-id="7fe79-211">**text**</span></span> | `**text**` |
| <span data-ttu-id="7fe79-212">italic</span><span class="sxs-lookup"><span data-stu-id="7fe79-212">italic</span></span> | <span data-ttu-id="7fe79-213">*text*</span><span class="sxs-lookup"><span data-stu-id="7fe79-213">*text*</span></span> | `*text*` |
| <span data-ttu-id="7fe79-214">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="7fe79-214">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="7fe79-215">**Texto**</span><span class="sxs-lookup"><span data-stu-id="7fe79-215">**Text**</span></span> | `### Text`|
| <span data-ttu-id="7fe79-216">strikethrough</span><span class="sxs-lookup"><span data-stu-id="7fe79-216">strikethrough</span></span> | <span data-ttu-id="7fe79-217">~~text~~</span><span class="sxs-lookup"><span data-stu-id="7fe79-217">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="7fe79-218">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="7fe79-218">unordered list</span></span> | <ul><li><span data-ttu-id="7fe79-219">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-219">text</span></span></li><li><span data-ttu-id="7fe79-220">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-220">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="7fe79-221">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="7fe79-221">ordered list</span></span> | <ol><li><span data-ttu-id="7fe79-222">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-222">text</span></span></li><li><span data-ttu-id="7fe79-223">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-223">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="7fe79-224">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="7fe79-224">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="7fe79-225">blockquote</span><span class="sxs-lookup"><span data-stu-id="7fe79-225">blockquote</span></span> | <span data-ttu-id="7fe79-226">>texto de bloques</span><span class="sxs-lookup"><span data-stu-id="7fe79-226">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="7fe79-227">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="7fe79-227">hyperlink</span></span> | [<span data-ttu-id="7fe79-228">Bing</span><span class="sxs-lookup"><span data-stu-id="7fe79-228">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="7fe79-229">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="7fe79-229">image link</span></span> |![Agacharse en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="7fe79-231">En las tarjetas de conector, las líneas nuevas se representan `\n\n` para , pero no para o `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="7fe79-231">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="7fe79-232">Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con Markdown</span><span class="sxs-lookup"><span data-stu-id="7fe79-232">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="7fe79-233">En el escritorio, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-233">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="7fe79-235">En iOS, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-235">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="7fe79-237">Problemas:</span><span class="sxs-lookup"><span data-stu-id="7fe79-237">Issues:</span></span>

* <span data-ttu-id="7fe79-238">El cliente de iOS para Teams no representa imágenes en línea markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="7fe79-238">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="7fe79-239">Las comillas bloques se representan como sangría pero sin un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="7fe79-239">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="7fe79-240">En Android, el formato markdown para tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-240">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Formato markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="7fe79-242">Ejemplo de formato para tarjetas de conector de Markdown</span><span class="sxs-lookup"><span data-stu-id="7fe79-242">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="7fe79-243">Formato de tarjetas con HTML</span><span class="sxs-lookup"><span data-stu-id="7fe79-243">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="7fe79-244">**Formato HTML: tarjetas de conector de O365**</span><span class="sxs-lookup"><span data-stu-id="7fe79-244">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="7fe79-245">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="7fe79-245">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="7fe79-246">Markdown se describe en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="7fe79-246">Markdown is described in the next section.</span></span>

| <span data-ttu-id="7fe79-247">Estilo</span><span class="sxs-lookup"><span data-stu-id="7fe79-247">Style</span></span> | <span data-ttu-id="7fe79-248">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7fe79-248">Example</span></span> | <span data-ttu-id="7fe79-249">HTML</span><span class="sxs-lookup"><span data-stu-id="7fe79-249">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fe79-250">bold</span><span class="sxs-lookup"><span data-stu-id="7fe79-250">bold</span></span> | <span data-ttu-id="7fe79-251">**text**</span><span class="sxs-lookup"><span data-stu-id="7fe79-251">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="7fe79-252">italic</span><span class="sxs-lookup"><span data-stu-id="7fe79-252">italic</span></span> | <span data-ttu-id="7fe79-253">*text*</span><span class="sxs-lookup"><span data-stu-id="7fe79-253">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="7fe79-254">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="7fe79-254">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="7fe79-255">**Texto**</span><span class="sxs-lookup"><span data-stu-id="7fe79-255">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="7fe79-256">strikethrough</span><span class="sxs-lookup"><span data-stu-id="7fe79-256">strikethrough</span></span> | <span data-ttu-id="7fe79-257">~~text~~</span><span class="sxs-lookup"><span data-stu-id="7fe79-257">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="7fe79-258">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="7fe79-258">unordered list</span></span> | <ul><li><span data-ttu-id="7fe79-259">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-259">text</span></span></li><li><span data-ttu-id="7fe79-260">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-260">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="7fe79-261">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="7fe79-261">ordered list</span></span> | <ol><li><span data-ttu-id="7fe79-262">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-262">text</span></span></li><li><span data-ttu-id="7fe79-263">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-263">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="7fe79-264">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="7fe79-264">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="7fe79-265">blockquote</span><span class="sxs-lookup"><span data-stu-id="7fe79-265">blockquote</span></span> | <blockquote><span data-ttu-id="7fe79-266">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-266">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="7fe79-267">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="7fe79-267">hyperlink</span></span> | [<span data-ttu-id="7fe79-268">Bing</span><span class="sxs-lookup"><span data-stu-id="7fe79-268">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="7fe79-269">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="7fe79-269">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="7fe79-270">En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="7fe79-270">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="7fe79-271">Diferencias de dispositivos móviles y de escritorio para tarjetas de conector con HTML</span><span class="sxs-lookup"><span data-stu-id="7fe79-271">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="7fe79-272">En el escritorio, el formato HTML de las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-272">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="7fe79-274">En iOS, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-274">On iOS, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="7fe79-276">Problemas:</span><span class="sxs-lookup"><span data-stu-id="7fe79-276">Issues:</span></span>

* <span data-ttu-id="7fe79-277">Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="7fe79-277">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="7fe79-278">El texto con formato previo se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="7fe79-278">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="7fe79-279">En Android, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7fe79-279">On Android, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="7fe79-281">Ejemplo de formato para tarjetas de conector HTML</span><span class="sxs-lookup"><span data-stu-id="7fe79-281">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="7fe79-282">**Formato HTML: tarjetas de miniatura y de héroe**</span><span class="sxs-lookup"><span data-stu-id="7fe79-282">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="7fe79-283">Las etiquetas HTML son compatibles con tarjetas sencillas, como la tarjeta de miniatura y la de héroe.</span><span class="sxs-lookup"><span data-stu-id="7fe79-283">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="7fe79-284">Markdown no es compatible.</span><span class="sxs-lookup"><span data-stu-id="7fe79-284">Markdown is not supported.</span></span>

| <span data-ttu-id="7fe79-285">Estilo</span><span class="sxs-lookup"><span data-stu-id="7fe79-285">Style</span></span> | <span data-ttu-id="7fe79-286">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7fe79-286">Example</span></span> | <span data-ttu-id="7fe79-287">HTML</span><span class="sxs-lookup"><span data-stu-id="7fe79-287">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fe79-288">bold</span><span class="sxs-lookup"><span data-stu-id="7fe79-288">bold</span></span> | <span data-ttu-id="7fe79-289">**text**</span><span class="sxs-lookup"><span data-stu-id="7fe79-289">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="7fe79-290">italic</span><span class="sxs-lookup"><span data-stu-id="7fe79-290">italic</span></span> | <span data-ttu-id="7fe79-291">*text*</span><span class="sxs-lookup"><span data-stu-id="7fe79-291">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="7fe79-292">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="7fe79-292">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="7fe79-293">**Texto**</span><span class="sxs-lookup"><span data-stu-id="7fe79-293">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="7fe79-294">strikethrough</span><span class="sxs-lookup"><span data-stu-id="7fe79-294">strikethrough</span></span> | <span data-ttu-id="7fe79-295">~~text~~</span><span class="sxs-lookup"><span data-stu-id="7fe79-295">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="7fe79-296">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="7fe79-296">unordered list</span></span> | <ul><li><span data-ttu-id="7fe79-297">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-297">text</span></span></li><li><span data-ttu-id="7fe79-298">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-298">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="7fe79-299">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="7fe79-299">ordered list</span></span> | <ol><li><span data-ttu-id="7fe79-300">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-300">text</span></span></li><li><span data-ttu-id="7fe79-301">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-301">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="7fe79-302">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="7fe79-302">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="7fe79-303">blockquote</span><span class="sxs-lookup"><span data-stu-id="7fe79-303">blockquote</span></span> | <blockquote><span data-ttu-id="7fe79-304">text</span><span class="sxs-lookup"><span data-stu-id="7fe79-304">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="7fe79-305">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="7fe79-305">hyperlink</span></span> | [<span data-ttu-id="7fe79-306">Bing</span><span class="sxs-lookup"><span data-stu-id="7fe79-306">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="7fe79-307">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="7fe79-307">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="7fe79-308">Diferencias de escritorio y móvil para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="7fe79-308">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="7fe79-309">Debido a las diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="7fe79-309">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="7fe79-310">En el escritorio, el formato HTML aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="7fe79-310">On the desktop, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="7fe79-312">En iOS, el formato HTML aparece de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="7fe79-312">On iOS, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="7fe79-314">Problemas:</span><span class="sxs-lookup"><span data-stu-id="7fe79-314">Issues:</span></span>

* <span data-ttu-id="7fe79-315">El formato de caracteres como negrita y cursiva no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="7fe79-315">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="7fe79-316">En Android, el formato HTML aparece de esta forma:</span><span class="sxs-lookup"><span data-stu-id="7fe79-316">On Android, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="7fe79-318">El formato de caracteres como negrita y cursiva se muestra correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="7fe79-318">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="7fe79-319">Ejemplo de formato para formato HTML en tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="7fe79-319">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="7fe79-320">Estas capturas de pantalla se crearon con Teams AppStudio, donde la propiedad de texto de una tarjeta de héroe se estableció en la siguiente cadena.</span><span class="sxs-lookup"><span data-stu-id="7fe79-320">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="7fe79-321">Puedes probar el formato en tus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="7fe79-321">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
