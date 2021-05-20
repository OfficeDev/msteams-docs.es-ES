---
title: Formato de texto en tarjetas
description: Describe el formato de texto de la tarjeta en Microsoft Teams
keywords: equipos bots formato de tarjetas
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 848656097f2c865705cc0d91dece93049d8c6790
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566588"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="a828c-104">Formatee las tarjetas en Teams</span><span class="sxs-lookup"><span data-stu-id="a828c-104">Format cards in Teams</span></span>

<span data-ttu-id="a828c-105">Puede agregar formato de texto enriquecido a sus tarjetas mediante Markdown o HTML, dependiendo del tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a828c-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="a828c-106">Las tarjetas admiten el formato solo en la propiedad text, no en las propiedades title o subtitle.</span><span class="sxs-lookup"><span data-stu-id="a828c-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="a828c-107">El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown en función del tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="a828c-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="a828c-108">Para el desarrollo actual y futuro se recomienda tarjetas adaptables mediante el formato De reducción.</span><span class="sxs-lookup"><span data-stu-id="a828c-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="a828c-109">El soporte de formato difiere entre diferentes tipos de tarjetas, y la representación de la tarjeta puede diferir ligeramente entre el escritorio y los clientes de Teams móviles, así como Teams en el navegador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="a828c-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="a828c-110">Puede incluir una imagen en línea con cualquier tarjeta de Teams.</span><span class="sxs-lookup"><span data-stu-id="a828c-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="a828c-111">Las imágenes se formatean como  `.png` , o archivos y no deben `.jpg` `.gif` exceder 1024 ×1024 px o 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a828c-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="a828c-112">Gif animado no es oficialmente compatible.</span><span class="sxs-lookup"><span data-stu-id="a828c-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="a828c-113">Para obtener más información, consulte [Referencia de tarjetas](./cards-reference.md#inline-card-images).</span><span class="sxs-lookup"><span data-stu-id="a828c-113">For more information, see [Cards reference](./cards-reference.md#inline-card-images).</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="a828c-114">Formato de tarjetas con Markdown</span><span class="sxs-lookup"><span data-stu-id="a828c-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="a828c-115">Hay dos tipos de tarjetas que admiten Markdown en Teams:</span><span class="sxs-lookup"><span data-stu-id="a828c-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a828c-116">**Tarjetas adaptables:** Markdown es compatible con el campo de la tarjeta `Textblock` adaptativa, así como y `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="a828c-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="a828c-117">HTML no es compatible con tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="a828c-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="a828c-118">**Tarjetas de conector O365:** Markdown y HTML limitado se admiten en Office 365 tarjetas connector en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="a828c-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="a828c-119">**Formato de reducción: tarjetas adaptables**</span><span class="sxs-lookup"><span data-stu-id="a828c-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="a828c-120">Los estilos `Textblock` admitidos para , `Fact.Title` y `Fact.Value` son:</span><span class="sxs-lookup"><span data-stu-id="a828c-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="a828c-121">Estilo</span><span class="sxs-lookup"><span data-stu-id="a828c-121">Style</span></span> | <span data-ttu-id="a828c-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828c-122">Example</span></span> | <span data-ttu-id="a828c-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="a828c-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a828c-124">bold</span><span class="sxs-lookup"><span data-stu-id="a828c-124">bold</span></span> | <span data-ttu-id="a828c-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="a828c-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="a828c-126">italic</span><span class="sxs-lookup"><span data-stu-id="a828c-126">italic</span></span> | <span data-ttu-id="a828c-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="a828c-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="a828c-128">lista desordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-128">unordered list</span></span> | <ul><li><span data-ttu-id="a828c-129">text</span><span class="sxs-lookup"><span data-stu-id="a828c-129">text</span></span></li><li><span data-ttu-id="a828c-130">text</span><span class="sxs-lookup"><span data-stu-id="a828c-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a828c-131">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-131">ordered list</span></span> | <ol><li><span data-ttu-id="a828c-132">text</span><span class="sxs-lookup"><span data-stu-id="a828c-132">text</span></span></li><li><span data-ttu-id="a828c-133">text</span><span class="sxs-lookup"><span data-stu-id="a828c-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a828c-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="a828c-134">Hyperlinks</span></span> |[<span data-ttu-id="a828c-135">Bing</span><span class="sxs-lookup"><span data-stu-id="a828c-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="a828c-136">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="a828c-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="a828c-137">Encabezados</span><span class="sxs-lookup"><span data-stu-id="a828c-137">Headers</span></span>
* <span data-ttu-id="a828c-138">Tablas</span><span class="sxs-lookup"><span data-stu-id="a828c-138">Tables</span></span>
* <span data-ttu-id="a828c-139">Imágenes</span><span class="sxs-lookup"><span data-stu-id="a828c-139">Images</span></span>
* <span data-ttu-id="a828c-140">Texto preformateado</span><span class="sxs-lookup"><span data-stu-id="a828c-140">Preformatted text</span></span>
* <span data-ttu-id="a828c-141">Bloques</span><span class="sxs-lookup"><span data-stu-id="a828c-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a828c-142">Las tarjetas adaptables no admiten el formato HTML.</span><span class="sxs-lookup"><span data-stu-id="a828c-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="a828c-143">Nuevas líneas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="a828c-144">En las listas puede utilizar las `\r` secuencias o `\n` secuencias de escape para las nuevas líneas.</span><span class="sxs-lookup"><span data-stu-id="a828c-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="a828c-145">El uso `\n\n` en una lista hará que el siguiente elemento de la lista tenga sangría.</span><span class="sxs-lookup"><span data-stu-id="a828c-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="a828c-146">Si necesita nuevas líneas en otra parte del bloque de texto, utilice `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="a828c-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="a828c-147">Diferencias móviles y de escritorio para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="a828c-148">El formato es ligeramente diferente entre el escritorio y las versiones móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="a828c-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="a828c-149">En el escritorio, el formato de reducción de tarjeta adaptable aparece así tanto en los navegadores web como en la aplicación cliente Teams:</span><span class="sxs-lookup"><span data-stu-id="a828c-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formato de markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="a828c-151">En iOS, el formato de reducción de tarjeta adaptable aparece así:</span><span class="sxs-lookup"><span data-stu-id="a828c-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![Formato de markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="a828c-153">En Android, el formato de reducción de tarjeta adaptable aparece así:</span><span class="sxs-lookup"><span data-stu-id="a828c-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Formato de markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="a828c-155">Más información sobre las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-155">More information on Adaptive cards</span></span>

<span data-ttu-id="a828c-156">[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) Las características de fecha y localización mencionadas en este tema no se admiten en Teams.</span><span class="sxs-lookup"><span data-stu-id="a828c-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="a828c-157">Ejemplo de formato para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="a828c-158">Mencionar soporte dentro de tarjetas adaptables v1.2</span><span class="sxs-lookup"><span data-stu-id="a828c-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="a828c-159">Las menciones basadas en tarjetas son compatibles con clientes web, de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="a828c-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="a828c-160">Puede agregar menciones @ dentro de un cuerpo de tarjeta adaptable para bots y respuestas de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="a828c-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="a828c-161">Para agregar @ menciones en las tarjetas, siga la misma lógica de notificación y representación que la de las menciones basadas en mensajes en conversaciones de [chat de canal y grupo.](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)</span><span class="sxs-lookup"><span data-stu-id="a828c-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="a828c-162">Los bots y las extensiones de mensajería pueden incluir menciones dentro del contenido de la tarjeta en los elementos [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) y [FactSet.](https://adaptivecards.io/explorer/FactSet.html)</span><span class="sxs-lookup"><span data-stu-id="a828c-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="a828c-163">[Actualmente, los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten en tarjetas adaptables v1.2 en la plataforma Teams.</span><span class="sxs-lookup"><span data-stu-id="a828c-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="a828c-164">Las menciones de equipo de & de canal no se admiten en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="a828c-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="a828c-165">Construcción de menciones</span><span class="sxs-lookup"><span data-stu-id="a828c-165">Constructing mentions</span></span>

<span data-ttu-id="a828c-166">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a828c-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="a828c-167">`<at>username</at>` en los elementos de tarjeta adaptable compatibles.</span><span class="sxs-lookup"><span data-stu-id="a828c-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="a828c-168">Objeto `mention` dentro de una propiedad en el contenido de la `msteams` tarjeta, que incluye el identificador de usuario Teams del usuario mencionado.</span><span class="sxs-lookup"><span data-stu-id="a828c-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="a828c-169">Es `userId` único para su ID de bot y un usuario en particular.</span><span class="sxs-lookup"><span data-stu-id="a828c-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="a828c-170">Se puede utilizar para @mention un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="a828c-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="a828c-171">Se `userId` puede recuperar mediante una de las opciones mencionadas para obtener el ID de [usuario](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="a828c-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="a828c-172">Tarjeta adaptativa de muestra con una mención</span><span class="sxs-lookup"><span data-stu-id="a828c-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="a828c-173">Enmascaramiento de información en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="a828c-174">Utilice la propiedad information masking para enmascarar información específica, como la contraseña o la información confidencial de los usuarios dentro del elemento de entrada de tarjeta [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) adaptable.</span><span class="sxs-lookup"><span data-stu-id="a828c-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="a828c-175">La característica solo admite el enmascaramiento de información del lado cliente, el texto de entrada enmascarado se envía como texto sin cifrar a la dirección de punto de conexión https especificada durante la [configuración del bot.](../../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="a828c-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="a828c-176">La propiedad information masking solo está disponible actualmente en la vista previa del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a828c-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="a828c-177">Para enmascarar la información en tarjetas adaptables, agregue la `isMasked` propiedad a **type** y establezca su valor `Input.Text` en *true*.</span><span class="sxs-lookup"><span data-stu-id="a828c-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="a828c-178">Tarjeta adaptativa de muestra con propiedad de enmascaramiento</span><span class="sxs-lookup"><span data-stu-id="a828c-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="a828c-179">La siguiente imagen es un ejemplo de enmascaramiento de información en tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="a828c-179">The following image is an example of masking information in Adaptive cards:</span></span>

![Imagen de información de enmascaramiento](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="a828c-181">Tarjeta adaptativa de ancho completo</span><span class="sxs-lookup"><span data-stu-id="a828c-181">Full width Adaptive card</span></span>
<span data-ttu-id="a828c-182">Puede utilizar la `msteams` propiedad para expandir el ancho de una tarjeta adaptable y hacer uso de espacio de lienzo adicional.</span><span class="sxs-lookup"><span data-stu-id="a828c-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="a828c-183">Para obtener información sobre cómo utilizar la propiedad, consulte el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a828c-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="a828c-184">Construcción de tarjetas de ancho completo</span><span class="sxs-lookup"><span data-stu-id="a828c-184">Constructing full width cards</span></span>
<span data-ttu-id="a828c-185">Para que una tarjeta adaptable de ancho completo sea el `width` objeto de la propiedad en el contenido de la tarjeta debe `msteams` establecerse en `Full` .</span><span class="sxs-lookup"><span data-stu-id="a828c-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="a828c-186">Además, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a828c-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="a828c-187">Tarjeta adaptativa de muestra con ancho completo</span><span class="sxs-lookup"><span data-stu-id="a828c-187">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="a828c-188">Una tarjeta adaptable de ancho completo aparece de la siguiente manera: ![ Vista de tarjeta adaptativa de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="a828c-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="a828c-189">Si no ha establecido la `width` propiedad en *Full*, la vista predeterminada de la tarjeta adaptable es la siguiente: Vista de tarjeta adaptable de ![ ancho pequeño](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="a828c-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="a828c-190">Soporte de Typeahead</span><span class="sxs-lookup"><span data-stu-id="a828c-190">Typeahead support</span></span>

<span data-ttu-id="a828c-191">Dentro del [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) elemento de esquema, pedir a los usuarios que filtren y seleccionen a través de un número considerable de opciones puede ralentizar significativamente la finalización de tareas.</span><span class="sxs-lookup"><span data-stu-id="a828c-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="a828c-192">La compatibilidad con typeahead dentro de las tarjetas adaptables puede simplificar la selección de entrada al restringir o filtrar el conjunto de opciones de entrada mientras un usuario escribe la entrada.</span><span class="sxs-lookup"><span data-stu-id="a828c-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="a828c-193">Habilitar cabezal tipoa en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="a828c-194">Para habilitar typeahead dentro del `Input.Choiceset` conjunto y asegúrese de que está establecido en `style` `filtered` `isMultiSelect` `false` .</span><span class="sxs-lookup"><span data-stu-id="a828c-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="a828c-195">Tarjeta adaptativa de muestra con soporte de cabezal tipo</span><span class="sxs-lookup"><span data-stu-id="a828c-195">Sample adaptive card with typeahead support</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="a828c-196">Vista de escenario para imágenes en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="a828c-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="a828c-197">Esta característica solo está disponible actualmente en la vista previa del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="a828c-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="a828c-198">En una tarjeta adaptable, puede utilizar la `msteams` propiedad para agregar la capacidad de mostrar imágenes en la vista de escenario de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="a828c-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="a828c-199">Cuando los usuarios pasan el cursor sobre las imágenes, verían un icono de expansión, para el que el `allowExpand` atributo está establecido en `true` .</span><span class="sxs-lookup"><span data-stu-id="a828c-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="a828c-200">Para obtener información sobre cómo utilizar la propiedad, consulte el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a828c-200">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="a828c-201">Cuando los usuarios se desplazan sobre la imagen, aparece un icono de expansión en la esquina superior derecha de la imagen: ![ tarjeta adaptable con imagen ampliable](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="a828c-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="a828c-202">La imagen aparece en la vista de escenario cuando el usuario selecciona el botón expandir: ![ Imagen expandida a vista de escenario](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="a828c-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="a828c-203">En la vista de escenario, los usuarios pueden acercar y alejar la imagen.</span><span class="sxs-lookup"><span data-stu-id="a828c-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="a828c-204">Puede seleccionar qué imágenes de su tarjeta adaptable deben tener esta capacidad.</span><span class="sxs-lookup"><span data-stu-id="a828c-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="a828c-205">La capacidad acercar y alejar solo se aplica a los elementos de imagen (tipo imagen) de una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="a828c-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="a828c-206">Para Teams aplicaciones móviles, la funcionalidad de vista de etapa para imágenes en tarjetas adaptables está disponible de forma predeterminada y los usuarios podrán ver imágenes de tarjetas adaptables en la vista de escenario simplemente tocando la imagen, independientemente de si el `allowExpand` atributo está presente o no.</span><span class="sxs-lookup"><span data-stu-id="a828c-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="a828c-207">**Formato de reducción: tarjetas de conector O365**</span><span class="sxs-lookup"><span data-stu-id="a828c-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="a828c-208">Las tarjetas de conector admiten el formato limitado de Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="a828c-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a828c-209">La compatibilidad con HTML se describe en la última sección.</span><span class="sxs-lookup"><span data-stu-id="a828c-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="a828c-210">Estilo</span><span class="sxs-lookup"><span data-stu-id="a828c-210">Style</span></span> | <span data-ttu-id="a828c-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828c-211">Example</span></span> | <span data-ttu-id="a828c-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="a828c-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a828c-213">bold</span><span class="sxs-lookup"><span data-stu-id="a828c-213">bold</span></span> | <span data-ttu-id="a828c-214">**text**</span><span class="sxs-lookup"><span data-stu-id="a828c-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="a828c-215">italic</span><span class="sxs-lookup"><span data-stu-id="a828c-215">italic</span></span> | <span data-ttu-id="a828c-216">*text*</span><span class="sxs-lookup"><span data-stu-id="a828c-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="a828c-217">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="a828c-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a828c-218">**Texto**</span><span class="sxs-lookup"><span data-stu-id="a828c-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="a828c-219">tachado</span><span class="sxs-lookup"><span data-stu-id="a828c-219">strikethrough</span></span> | <span data-ttu-id="a828c-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a828c-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="a828c-221">lista desordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-221">unordered list</span></span> | <ul><li><span data-ttu-id="a828c-222">text</span><span class="sxs-lookup"><span data-stu-id="a828c-222">text</span></span></li><li><span data-ttu-id="a828c-223">text</span><span class="sxs-lookup"><span data-stu-id="a828c-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a828c-224">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-224">ordered list</span></span> | <ol><li><span data-ttu-id="a828c-225">text</span><span class="sxs-lookup"><span data-stu-id="a828c-225">text</span></span></li><li><span data-ttu-id="a828c-226">text</span><span class="sxs-lookup"><span data-stu-id="a828c-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a828c-227">texto preformateado</span><span class="sxs-lookup"><span data-stu-id="a828c-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="a828c-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="a828c-228">blockquote</span></span> | <span data-ttu-id="a828c-229">>texto en bloque</span><span class="sxs-lookup"><span data-stu-id="a828c-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="a828c-230">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="a828c-230">hyperlink</span></span> | [<span data-ttu-id="a828c-231">Bing</span><span class="sxs-lookup"><span data-stu-id="a828c-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="a828c-232">enlace de imagen</span><span class="sxs-lookup"><span data-stu-id="a828c-232">image link</span></span> |![Pato en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="a828c-234">En las tarjetas de conector, las nuevas líneas se representan para `\n\n` , pero no para o `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="a828c-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="a828c-235">Diferencias móviles y de escritorio para las tarjetas de conector con Markdown</span><span class="sxs-lookup"><span data-stu-id="a828c-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="a828c-236">En el escritorio, el formato de markdown para las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Formato de reducción para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="a828c-238">En iOS, el formato de reducción para las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Formato de reducción para tarjetas de conector en el cliente iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="a828c-240">Problemas:</span><span class="sxs-lookup"><span data-stu-id="a828c-240">Issues:</span></span>

* <span data-ttu-id="a828c-241">El cliente de iOS para Teams no representa imágenes en línea Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="a828c-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="a828c-242">Las comillas de bloque se representan como sangrías pero sin un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="a828c-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="a828c-243">En Android, el formato markdown para las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Formato de reducción para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="a828c-245">Ejemplo de formato para tarjetas de conector markdown</span><span class="sxs-lookup"><span data-stu-id="a828c-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="a828c-246">Formato de tarjetas con HTML</span><span class="sxs-lookup"><span data-stu-id="a828c-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="a828c-247">**Formato HTML: Tarjetas de conector O365**</span><span class="sxs-lookup"><span data-stu-id="a828c-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="a828c-248">Las tarjetas de conector admiten el formato limitado de Markdown y HTML.</span><span class="sxs-lookup"><span data-stu-id="a828c-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a828c-249">La reducción se describe en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="a828c-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="a828c-250">Estilo</span><span class="sxs-lookup"><span data-stu-id="a828c-250">Style</span></span> | <span data-ttu-id="a828c-251">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828c-251">Example</span></span> | <span data-ttu-id="a828c-252">HTML</span><span class="sxs-lookup"><span data-stu-id="a828c-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a828c-253">bold</span><span class="sxs-lookup"><span data-stu-id="a828c-253">bold</span></span> | <span data-ttu-id="a828c-254">**text**</span><span class="sxs-lookup"><span data-stu-id="a828c-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a828c-255">italic</span><span class="sxs-lookup"><span data-stu-id="a828c-255">italic</span></span> | <span data-ttu-id="a828c-256">*text*</span><span class="sxs-lookup"><span data-stu-id="a828c-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a828c-257">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="a828c-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a828c-258">**Texto**</span><span class="sxs-lookup"><span data-stu-id="a828c-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a828c-259">tachado</span><span class="sxs-lookup"><span data-stu-id="a828c-259">strikethrough</span></span> | <span data-ttu-id="a828c-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a828c-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a828c-261">lista desordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-261">unordered list</span></span> | <ul><li><span data-ttu-id="a828c-262">text</span><span class="sxs-lookup"><span data-stu-id="a828c-262">text</span></span></li><li><span data-ttu-id="a828c-263">text</span><span class="sxs-lookup"><span data-stu-id="a828c-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a828c-264">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-264">ordered list</span></span> | <ol><li><span data-ttu-id="a828c-265">text</span><span class="sxs-lookup"><span data-stu-id="a828c-265">text</span></span></li><li><span data-ttu-id="a828c-266">text</span><span class="sxs-lookup"><span data-stu-id="a828c-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a828c-267">texto preformateado</span><span class="sxs-lookup"><span data-stu-id="a828c-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a828c-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="a828c-268">blockquote</span></span> | <blockquote><span data-ttu-id="a828c-269">text</span><span class="sxs-lookup"><span data-stu-id="a828c-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a828c-270">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="a828c-270">hyperlink</span></span> | [<span data-ttu-id="a828c-271">Bing</span><span class="sxs-lookup"><span data-stu-id="a828c-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a828c-272">enlace de imagen</span><span class="sxs-lookup"><span data-stu-id="a828c-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="a828c-273">En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="a828c-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="a828c-274">Diferencias móviles y de escritorio para tarjetas de conectores mediante HTML</span><span class="sxs-lookup"><span data-stu-id="a828c-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="a828c-275">En el escritorio, el formato HTML para las tarjetas de conector tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="a828c-277">En iOS, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-277">On iOS, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="a828c-279">Problemas:</span><span class="sxs-lookup"><span data-stu-id="a828c-279">Issues:</span></span>

* <span data-ttu-id="a828c-280">Las imágenes en línea no se representan en iOS mediante Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="a828c-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="a828c-281">El texto preformateado se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="a828c-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="a828c-282">En Android, el formato HTML tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a828c-282">On Android, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="a828c-284">Ejemplo de formato para tarjetas de conector HTML</span><span class="sxs-lookup"><span data-stu-id="a828c-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="a828c-285">**Formato HTML: tarjetas de héroe y miniatura**</span><span class="sxs-lookup"><span data-stu-id="a828c-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="a828c-286">Las etiquetas HTML son compatibles con tarjetas simples como el héroe y la tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="a828c-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="a828c-287">No se admite la reducción.</span><span class="sxs-lookup"><span data-stu-id="a828c-287">Markdown is not supported.</span></span>

| <span data-ttu-id="a828c-288">Estilo</span><span class="sxs-lookup"><span data-stu-id="a828c-288">Style</span></span> | <span data-ttu-id="a828c-289">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a828c-289">Example</span></span> | <span data-ttu-id="a828c-290">HTML</span><span class="sxs-lookup"><span data-stu-id="a828c-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a828c-291">bold</span><span class="sxs-lookup"><span data-stu-id="a828c-291">bold</span></span> | <span data-ttu-id="a828c-292">**text**</span><span class="sxs-lookup"><span data-stu-id="a828c-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a828c-293">italic</span><span class="sxs-lookup"><span data-stu-id="a828c-293">italic</span></span> | <span data-ttu-id="a828c-294">*text*</span><span class="sxs-lookup"><span data-stu-id="a828c-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a828c-295">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="a828c-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a828c-296">**Texto**</span><span class="sxs-lookup"><span data-stu-id="a828c-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a828c-297">tachado</span><span class="sxs-lookup"><span data-stu-id="a828c-297">strikethrough</span></span> | <span data-ttu-id="a828c-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a828c-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a828c-299">lista desordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-299">unordered list</span></span> | <ul><li><span data-ttu-id="a828c-300">text</span><span class="sxs-lookup"><span data-stu-id="a828c-300">text</span></span></li><li><span data-ttu-id="a828c-301">text</span><span class="sxs-lookup"><span data-stu-id="a828c-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a828c-302">lista ordenada</span><span class="sxs-lookup"><span data-stu-id="a828c-302">ordered list</span></span> | <ol><li><span data-ttu-id="a828c-303">text</span><span class="sxs-lookup"><span data-stu-id="a828c-303">text</span></span></li><li><span data-ttu-id="a828c-304">text</span><span class="sxs-lookup"><span data-stu-id="a828c-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a828c-305">texto preformateado</span><span class="sxs-lookup"><span data-stu-id="a828c-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a828c-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="a828c-306">blockquote</span></span> | <blockquote><span data-ttu-id="a828c-307">text</span><span class="sxs-lookup"><span data-stu-id="a828c-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a828c-308">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="a828c-308">hyperlink</span></span> | [<span data-ttu-id="a828c-309">Bing</span><span class="sxs-lookup"><span data-stu-id="a828c-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a828c-310">enlace de imagen</span><span class="sxs-lookup"><span data-stu-id="a828c-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="a828c-311">Diferencias móviles y de escritorio para tarjetas simples</span><span class="sxs-lookup"><span data-stu-id="a828c-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="a828c-312">Debido a las diferencias de resolución entre el escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="a828c-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="a828c-313">En el escritorio, el formato HTML aparece así:</span><span class="sxs-lookup"><span data-stu-id="a828c-313">On the desktop, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="a828c-315">En iOS, el formato HTML aparece así:</span><span class="sxs-lookup"><span data-stu-id="a828c-315">On iOS, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="a828c-317">Problemas:</span><span class="sxs-lookup"><span data-stu-id="a828c-317">Issues:</span></span>

* <span data-ttu-id="a828c-318">El formato de caracteres como negrita e cursa no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="a828c-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="a828c-319">En Android, el formato HTML aparece así:</span><span class="sxs-lookup"><span data-stu-id="a828c-319">On Android, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="a828c-321">Formato de caracteres como negrita y pantalla cursalica correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="a828c-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="a828c-322">Ejemplo de formato para formato HTML en tarjetas simples</span><span class="sxs-lookup"><span data-stu-id="a828c-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="a828c-323">Estas capturas de pantalla se crearon con Teams AppStudio, donde la propiedad de texto de una tarjeta de héroe se estableció en la siguiente cadena.</span><span class="sxs-lookup"><span data-stu-id="a828c-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="a828c-324">Puede probar el formato en sus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="a828c-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
