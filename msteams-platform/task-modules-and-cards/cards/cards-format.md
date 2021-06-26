---
title: Formato de texto en tarjetas
description: Describe el formato de texto de tarjeta en Microsoft Teams
keywords: formato de tarjetas de bots de teams
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140671"
---
# <a name="format-cards-in-microsoft-teams"></a><span data-ttu-id="c6f3e-104">Dar formato a las tarjetas Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c6f3e-104">Format cards in Microsoft Teams</span></span>

<span data-ttu-id="c6f3e-105">Estas son las dos formas de agregar formato de texto enriquecido a las tarjetas:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-105">Following are the two ways to add rich text formatting to your cards:</span></span>
* [<span data-ttu-id="c6f3e-106">Markdown</span><span class="sxs-lookup"><span data-stu-id="c6f3e-106">Markdown</span></span>](#format-cards-with-markdown)
* [<span data-ttu-id="c6f3e-107">HTML</span><span class="sxs-lookup"><span data-stu-id="c6f3e-107">HTML</span></span>](#format-cards-with-html)

<span data-ttu-id="c6f3e-108">Las tarjetas solo admiten el formato en la propiedad de texto, no en las propiedades de título o subtítulo.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-108">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="c6f3e-109">El formato se puede especificar mediante un subconjunto de formato XML o HTML o Markdown, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-109">Formatting can be specified using a subset of XML or HTML formatting or Markdown, depending on the card type.</span></span> <span data-ttu-id="c6f3e-110">Para el desarrollo actual y futuro de tarjetas adaptables, se recomienda el formato markdown.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-110">For current and future development of Adaptive Cards, Markdown formatting is recommended.</span></span>

<span data-ttu-id="c6f3e-111">La compatibilidad con el formato difiere entre los tipos de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-111">Formatting support differs between card types.</span></span> <span data-ttu-id="c6f3e-112">La representación de la tarjeta puede diferir ligeramente entre el escritorio y los clientes Microsoft Teams móviles, así como Teams en el explorador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-112">Rendering of the card can differ slightly between the desktop and the mobile Microsoft Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="c6f3e-113">Puedes incluir una imagen en línea con cualquier Teams tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-113">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="c6f3e-114">Las imágenes pueden tener formato como , o archivos y no deben superar `.png` `.jpg` los `.gif` 1024 ×1024 px o 1 MB.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-114">Images can be formatted as `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="c6f3e-115">Gif animado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-115">Animated GIF is not supported.</span></span> <span data-ttu-id="c6f3e-116">Para obtener más información, vea [tipos de tarjetas](./cards-reference.md#inline-card-images).</span><span class="sxs-lookup"><span data-stu-id="c6f3e-116">For more information, see [types of cards](./cards-reference.md#inline-card-images).</span></span>

<span data-ttu-id="c6f3e-117">Puedes dar formato a tarjetas adaptables y Office 365 connector con Markdown que incluyan ciertos estilos admitidos.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-117">You can format Adaptive Cards and Office 365 Connector cards with Markdown that include certain supported styles.</span></span>

## <a name="format-cards-with-markdown"></a><span data-ttu-id="c6f3e-118">Dar formato a tarjetas con Markdown</span><span class="sxs-lookup"><span data-stu-id="c6f3e-118">Format cards with Markdown</span></span>

<span data-ttu-id="c6f3e-119">Los siguientes tipos de tarjeta admiten el formato Markdown en Teams:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-119">The following card types support Markdown formatting in Teams:</span></span>

* <span data-ttu-id="c6f3e-120">Tarjetas adaptables: Markdown se admite en el campo Tarjeta `Textblock` adaptable, así como `Fact.Title` en `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-120">Adaptive Cards: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="c6f3e-121">Html no se admite en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-121">HTML is not supported in Adaptive Cards.</span></span>
* <span data-ttu-id="c6f3e-122">Tarjetas de conector de O365: Markdown y HTML limitado se admiten en las tarjetas de conector de O365 en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-122">O365 Connector cards: Markdown and limited HTML is supported in O365 Connector cards in the text fields.</span></span>

<span data-ttu-id="c6f3e-123">Puedes usar líneas nuevas para tarjetas adaptables mediante `\r` o `\n` secuencias de escape para las líneas nuevas de las listas.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-123">You can use newlines for Adaptive Cards using `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="c6f3e-124">El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-124">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards.</span></span> <span data-ttu-id="c6f3e-125">Las menciones basadas en tarjetas se admiten en clientes web, de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-125">Card-based mentions are supported in web, desktop, and mobile clients.</span></span> <span data-ttu-id="c6f3e-126">Puede usar la propiedad de enmascaramiento de información para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada Tarjeta `Input.Text` adaptable.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-126">You can use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card `Input.Text` input element.</span></span> <span data-ttu-id="c6f3e-127">Puede expandir el ancho de una tarjeta adaptable mediante el `width` objeto.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-127">You can expand the width of an Adaptive Card using the `width` object.</span></span> <span data-ttu-id="c6f3e-128">Puede habilitar la compatibilidad con typeahead en tarjetas adaptables y filtrar el conjunto de opciones de entrada a medida que el usuario escribe la entrada.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-128">You can enable typeahead support within Adaptive Cards and filter the set of input choices as the user types the input.</span></span> <span data-ttu-id="c6f3e-129">Puede usar la propiedad `msteams` para agregar la capacidad de mostrar imágenes en la vista de fase de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-129">You can use the `msteams` property to add the ability to display images in stage view selectively.</span></span>

<span data-ttu-id="c6f3e-130">El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas adaptables y tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-130">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards and connector cards.</span></span> <span data-ttu-id="c6f3e-131">En esta sección, puede ir a través del ejemplo de formato Markdown para tarjetas adaptables y tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-131">In this section, you can go through the Markdown format example for Adaptive Cards and connector cards.</span></span>

# <a name="markdown-format-for-adaptive-cards"></a>[<span data-ttu-id="c6f3e-132">Formato markdown para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-132">Markdown format for Adaptive Cards</span></span>](#tab/adaptive-md)

 <span data-ttu-id="c6f3e-133">En la tabla siguiente se proporcionan los estilos admitidos para `Textblock` `Fact.Title` , y `Fact.Value` :</span><span class="sxs-lookup"><span data-stu-id="c6f3e-133">The following table provides the supported styles for `Textblock`, `Fact.Title`, and `Fact.Value`:</span></span>

| <span data-ttu-id="c6f3e-134">Estilo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-134">Style</span></span> | <span data-ttu-id="c6f3e-135">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-135">Example</span></span> | <span data-ttu-id="c6f3e-136">Markdown</span><span class="sxs-lookup"><span data-stu-id="c6f3e-136">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6f3e-137">Negrita</span><span class="sxs-lookup"><span data-stu-id="c6f3e-137">Bold</span></span> | <span data-ttu-id="c6f3e-138">**Bold**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-138">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="c6f3e-139">Italic</span><span class="sxs-lookup"><span data-stu-id="c6f3e-139">Italic</span></span> | <span data-ttu-id="c6f3e-140">_Italic_</span><span class="sxs-lookup"><span data-stu-id="c6f3e-140">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="c6f3e-141">Lista no ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-141">Unordered list</span></span> | <ul><li><span data-ttu-id="c6f3e-142">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-142">text</span></span></li><li><span data-ttu-id="c6f3e-143">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-143">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="c6f3e-144">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-144">Ordered list</span></span> | <ol><li><span data-ttu-id="c6f3e-145">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-145">text</span></span></li><li><span data-ttu-id="c6f3e-146">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-146">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="c6f3e-147">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="c6f3e-147">Hyperlinks</span></span> |[<span data-ttu-id="c6f3e-148">Bing</span><span class="sxs-lookup"><span data-stu-id="c6f3e-148">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="c6f3e-149">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-149">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="c6f3e-150">Encabezados</span><span class="sxs-lookup"><span data-stu-id="c6f3e-150">Headers</span></span>
* <span data-ttu-id="c6f3e-151">Tablas</span><span class="sxs-lookup"><span data-stu-id="c6f3e-151">Tables</span></span>
* <span data-ttu-id="c6f3e-152">Imágenes</span><span class="sxs-lookup"><span data-stu-id="c6f3e-152">Images</span></span>
* <span data-ttu-id="c6f3e-153">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-153">Preformatted text</span></span>
* <span data-ttu-id="c6f3e-154">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="c6f3e-154">Blockquotes</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="c6f3e-155">Nuevas líneas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-155">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="c6f3e-156">Puede usar las `\r` secuencias de `\n` escape o para las líneas nuevas de las listas.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-156">You can use the `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="c6f3e-157">El uso en listas hace que se aplique sangría al siguiente elemento `\n\n` de la lista.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-157">Using `\n\n` in lists causes the next element in the list to be indented.</span></span> <span data-ttu-id="c6f3e-158">Si necesita nuevas líneas en otra parte del TextBlock, use `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-158">If you require newlines elsewhere in the TextBlock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="c6f3e-159">Diferencias de dispositivos móviles y de escritorio para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-159">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="c6f3e-160">En el escritorio, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen en los exploradores web y en la Teams cliente:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-160">On the desktop, Adaptive Card Markdown formatting appears as shown in the following image in both web browsers and in the Teams client application:</span></span>

![Formato de markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="c6f3e-162">En iOS, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-162">On iOS, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Formato de markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="c6f3e-164">En Android, el formato de markdown de tarjeta adaptable aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-164">On Android, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Formato de markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

<span data-ttu-id="c6f3e-166">Para obtener más información, vea [características de texto en Tarjetas adaptables](/adaptive-cards/create/textfeatures).</span><span class="sxs-lookup"><span data-stu-id="c6f3e-166">For more information, see [text features in Adaptive Cards](/adaptive-cards/create/textfeatures).</span></span>

> [!NOTE]
> <span data-ttu-id="c6f3e-167">Las características de fecha y localización mencionadas en esta sección no se admiten en Teams.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-167">The date and localization features mentioned in this section are not supported in Teams.</span></span>

### <a name="adaptive-cards-format-sample"></a><span data-ttu-id="c6f3e-168">Muestra de formato de tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-168">Adaptive Cards format sample</span></span>

<span data-ttu-id="c6f3e-169">El siguiente código muestra un ejemplo de formato de tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-169">The following code shows an example of Adaptive Cards formatting:</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="c6f3e-170">Mencione la compatibilidad con tarjetas adaptables v1.2</span><span class="sxs-lookup"><span data-stu-id="c6f3e-170">Mention support within Adaptive Cards v1.2</span></span>

<span data-ttu-id="c6f3e-171">Puedes agregar @mentions cuerpo de una tarjeta adaptable para bots y respuestas de extensión de mensajería.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-171">You can add @mentions within an Adaptive Card body for bots and messaging extension responses.</span></span> <span data-ttu-id="c6f3e-172">Para agregar @mentions tarjetas, siga la misma lógica de notificación y representación que las [menciones basadas](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)en mensajes en conversaciones de chat de canal y grupo.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-172">To add @mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="c6f3e-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="c6f3e-174">[Actualmente,](https://adaptivecards.io/explorer/Media.html) los elementos multimedia no se admiten en Adaptive Cards v1.2 en la Teams plataforma.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-174">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive Cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="c6f3e-175">Las menciones de canal y equipo no se admiten en los mensajes de bot.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-175">Channel and team mentions are not supported in bot messages.</span></span>

<span data-ttu-id="c6f3e-176">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-176">To include a mention in an Adaptive Card, your app needs to include the following elements:</span></span>

* <span data-ttu-id="c6f3e-177">`<at>username</at>` en los elementos de tarjeta adaptable compatibles.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-177">`<at>username</at>` in the supported Adaptive Card elements.</span></span>
* <span data-ttu-id="c6f3e-178">El objeto dentro de una propiedad en el contenido de la tarjeta `mention` incluye el Teams de usuario del usuario `msteams` mencionado.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-178">The `mention` object inside of an `msteams` property in the card content includes the Teams user ID of the user being mentioned.</span></span>
* <span data-ttu-id="c6f3e-179">El `userId` es único para el identificador del bot y un usuario en particular.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-179">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="c6f3e-180">Se puede usar para @mention un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-180">It can be used to @mention a particular user.</span></span> <span data-ttu-id="c6f3e-181">Se `userId` puede recuperar mediante una de las opciones mencionadas en obtener el identificador de [usuario](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span><span class="sxs-lookup"><span data-stu-id="c6f3e-181">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="c6f3e-182">Tarjeta adaptable de ejemplo con una mención</span><span class="sxs-lookup"><span data-stu-id="c6f3e-182">Sample Adaptive Card with a mention</span></span>

<span data-ttu-id="c6f3e-183">El siguiente código muestra un ejemplo de tarjeta adaptable con una mención:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-183">The following code shows an example of Adaptive Card with a mention:</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="c6f3e-184">Enmascaramiento de información en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-184">Information masking in Adaptive Cards</span></span>

<span data-ttu-id="c6f3e-185">Use la propiedad de enmascaramiento de información para enmascarar información específica, como contraseña o información confidencial de los usuarios dentro del elemento de entrada Tarjeta [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) adaptable.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-185">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span>

> [!NOTE]
> <span data-ttu-id="c6f3e-186">La característica solo admite el enmascaramiento de información del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-186">The feature only supports client side information masking.</span></span> <span data-ttu-id="c6f3e-187">El texto de entrada enmascarado se envía como texto sin formato a la dirección del extremo HTTPS que se especificó durante la [configuración del bot](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span><span class="sxs-lookup"><span data-stu-id="c6f3e-187">The masked input text is sent as clear text to the HTTPS endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span></span>

<span data-ttu-id="c6f3e-188">Para enmascarar la información en tarjetas adaptables, agregue la propiedad `isMasked` **al tipo** y establezca su valor `Input.Text` en **true**.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-188">To mask information in Adaptive Cards, add the `isMasked` property to **type** `Input.Text`, and set its value to **true**.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="c6f3e-189">Tarjeta adaptable de ejemplo con la propiedad masking</span><span class="sxs-lookup"><span data-stu-id="c6f3e-189">Sample Adaptive Card with masking property</span></span>

<span data-ttu-id="c6f3e-190">El siguiente código muestra un ejemplo de la propiedad Adaptive Card with masking:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-190">The following code shows an example of Adaptive Card with masking property:</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="c6f3e-191">La siguiente imagen es un ejemplo de enmascaramiento de información en tarjetas adaptables:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-191">The following image is an example of masking information in Adaptive Cards:</span></span>

![Imagen de información de enmascaramiento](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="c6f3e-193">Tarjeta adaptable de ancho completo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-193">Full width Adaptive Card</span></span>

<span data-ttu-id="c6f3e-194">Puede usar la propiedad para expandir el ancho de una tarjeta adaptable y `msteams` usar espacio de lienzo adicional.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-194">You can use the `msteams` property to expand the width of an Adaptive Card and make use of additional canvas space.</span></span> <span data-ttu-id="c6f3e-195">En la siguiente sección se proporciona información sobre cómo usar la propiedad.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-195">The next section provides information on how to use the property.</span></span>

#### <a name="construct-full-width-cards"></a><span data-ttu-id="c6f3e-196">Construir tarjetas de ancho completo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-196">Construct full width cards</span></span>

<span data-ttu-id="c6f3e-197">Para crear una tarjeta adaptable de ancho completo, el objeto de la propiedad en el contenido de la tarjeta `width` `msteams` debe establecerse en `Full` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-197">To make a full width Adaptive Card, the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="c6f3e-198">Tarjeta adaptable de ejemplo con ancho completo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-198">Sample Adaptive Card with full width</span></span>

<span data-ttu-id="c6f3e-199">Para crear una tarjeta adaptable de ancho completo, la aplicación debe incluir los elementos del siguiente ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-199">To make a full width Adaptive Card, your app must include the elements from the following code sample:</span></span>

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

<span data-ttu-id="c6f3e-200">La siguiente imagen muestra una tarjeta adaptable de ancho completo:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-200">The following image shows a full width Adaptive Card:</span></span>

![Vista de tarjeta adaptable de ancho completo](../../assets/images/cards/full-width-adaptive-card.png)

<span data-ttu-id="c6f3e-202">La siguiente imagen muestra la vista predeterminada de la tarjeta adaptable cuando no se ha establecido la `width` propiedad en **Full**:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-202">The following image shows the default view of the Adaptive Card when you have not set the `width` property to **Full**:</span></span>

![Vista de tarjeta adaptable de ancho pequeño](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a><span data-ttu-id="c6f3e-204">Compatibilidad con Typeahead</span><span class="sxs-lookup"><span data-stu-id="c6f3e-204">Typeahead support</span></span>

<span data-ttu-id="c6f3e-205">Dentro del elemento de esquema, pedir a los usuarios que filtren y seleccionen un número considerable de opciones puede ralentizar considerablemente la finalización [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) de las tareas.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-205">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter and select a sizeable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="c6f3e-206">La compatibilidad con la punta de tipo dentro de las tarjetas adaptables puede simplificar la selección de entrada limitando o filtrando el conjunto de opciones de entrada a medida que el usuario escribe la entrada.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-206">Typeahead support within Adaptive Cards can simplify input selection by narrowing or filtering the set of input choices as the user types the input.</span></span>

<span data-ttu-id="c6f3e-207">Para habilitar typeahead dentro del `Input.Choiceset` , establecido en y asegúrese está establecido en `style` `filtered` `isMultiSelect` `false` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-207">To enable typeahead within the `Input.Choiceset`, set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span>

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="c6f3e-208">Tarjeta adaptable de ejemplo con compatibilidad con membrete</span><span class="sxs-lookup"><span data-stu-id="c6f3e-208">Sample Adaptive Card with typeahead support</span></span>

<span data-ttu-id="c6f3e-209">En el siguiente código se muestra un ejemplo de tarjeta adaptable con compatibilidad con punta de tipo:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-209">The following code shows an example of Adaptive Card with typeahead support:</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="c6f3e-210">Vista de fase para imágenes en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="c6f3e-210">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="c6f3e-211">En una tarjeta adaptable, puedes usar la propiedad para agregar la capacidad de mostrar imágenes en la vista de fase `msteams` de forma selectiva.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-211">In an Adaptive Card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="c6f3e-212">Cuando los usuarios mantienen el mouse sobre las imágenes, pueden ver un icono de expansión, para el que `allowExpand` el atributo está establecido en `true` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-212">When users hover over the images, they can see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="c6f3e-213">Para obtener información sobre cómo usar la propiedad, vea el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-213">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="c6f3e-214">Cuando los usuarios mantienen el mouse sobre la imagen, aparece un icono expandir en la esquina superior derecha, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-214">When users hover over the image, an expand icon appears at the top right corner as shown in the following image:</span></span>

![Tarjeta adaptable con imagen expandible](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

<span data-ttu-id="c6f3e-216">La imagen aparece en la vista de fase cuando el usuario selecciona el icono expandir como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-216">The image appears in stage view when the user selects the expand icon as shown in the following image:</span></span>

![Imagen expandida a vista de fase](../../assets/images/cards/adaptivecard-expand-image.png)

<span data-ttu-id="c6f3e-218">En la vista de fase, los usuarios pueden acercar y alejar la imagen.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-218">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="c6f3e-219">Puedes seleccionar las imágenes de la tarjeta adaptable que deben tener esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-219">You can select the images in your Adaptive Card that must have this capability.</span></span>

> [!NOTE]
> * <span data-ttu-id="c6f3e-220">La funcionalidad acercar y alejar solo se aplica a los elementos de imagen que son tipo de imagen en una tarjeta adaptable.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-220">Zoom in and zoom out capability applies only to the image elements that is image type in an Adaptive Card.</span></span>
> * <span data-ttu-id="c6f3e-221">Para Teams móviles, la funcionalidad de vista de fase para imágenes en tarjetas adaptables está disponible de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-221">For Teams mobile apps, stage view functionality for images in Adaptive Cards is available by default.</span></span> <span data-ttu-id="c6f3e-222">Los usuarios pueden ver imágenes de tarjeta adaptable en la vista de fase simplemente pulsando en la imagen, independientemente de si el `allowExpand` atributo está presente o no.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-222">Users can view Adaptive Card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-format-for-o365-connector-cards"></a>[<span data-ttu-id="c6f3e-223">Formato markdown para tarjetas de conector de O365</span><span class="sxs-lookup"><span data-stu-id="c6f3e-223">Markdown format for O365 Connector cards</span></span>](#tab/connector-md)

<span data-ttu-id="c6f3e-224">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-224">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="c6f3e-225">Estilo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-225">Style</span></span> | <span data-ttu-id="c6f3e-226">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-226">Example</span></span> | <span data-ttu-id="c6f3e-227">Markdown</span><span class="sxs-lookup"><span data-stu-id="c6f3e-227">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6f3e-228">Negrita</span><span class="sxs-lookup"><span data-stu-id="c6f3e-228">Bold</span></span> | <span data-ttu-id="c6f3e-229">**text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-229">**text**</span></span> | `**text**` |
| <span data-ttu-id="c6f3e-230">Italic</span><span class="sxs-lookup"><span data-stu-id="c6f3e-230">Italic</span></span> | <span data-ttu-id="c6f3e-231">*text*</span><span class="sxs-lookup"><span data-stu-id="c6f3e-231">*text*</span></span> | `*text*` |
| <span data-ttu-id="c6f3e-232">Encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="c6f3e-232">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c6f3e-233">**Text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-233">**Text**</span></span> | `### Text`|
| <span data-ttu-id="c6f3e-234">Tachado</span><span class="sxs-lookup"><span data-stu-id="c6f3e-234">Strikethrough</span></span> | <span data-ttu-id="c6f3e-235">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c6f3e-235">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="c6f3e-236">Lista no ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-236">Unordered list</span></span> | <ul><li><span data-ttu-id="c6f3e-237">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-237">text</span></span></li><li><span data-ttu-id="c6f3e-238">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-238">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="c6f3e-239">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-239">Ordered list</span></span> | <ol><li><span data-ttu-id="c6f3e-240">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-240">text</span></span></li><li><span data-ttu-id="c6f3e-241">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-241">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="c6f3e-242">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-242">Preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="c6f3e-243">Blockquote</span><span class="sxs-lookup"><span data-stu-id="c6f3e-243">Blockquote</span></span> | <span data-ttu-id="c6f3e-244">>texto de bloques</span><span class="sxs-lookup"><span data-stu-id="c6f3e-244">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="c6f3e-245">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="c6f3e-245">Hyperlink</span></span> | [<span data-ttu-id="c6f3e-246">Bing</span><span class="sxs-lookup"><span data-stu-id="c6f3e-246">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="c6f3e-247">Vínculo imagen</span><span class="sxs-lookup"><span data-stu-id="c6f3e-247">Image link</span></span> |![Agacharse en una roca](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="c6f3e-249">En las tarjetas de conector, las líneas nuevas se representan `\n\n` para , pero no para o `\n` `\r` .</span><span class="sxs-lookup"><span data-stu-id="c6f3e-249">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="c6f3e-250">Diferencias de escritorio y móvil para tarjetas de conector</span><span class="sxs-lookup"><span data-stu-id="c6f3e-250">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="c6f3e-251">En el escritorio, el formato markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-251">On the desktop, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Formato markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="c6f3e-253">En iOS, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-253">On iOS, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Formato markdown para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="c6f3e-255">Las tarjetas de conector que usan Markdown para iOS incluyen los siguientes problemas:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-255">Connector cards using Markdown for iOS include the following issues:</span></span>

* <span data-ttu-id="c6f3e-256">El cliente de iOS para Teams no representa imágenes en línea markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-256">The iOS client for Teams does not render Markdown or HTML inline images in connector cards.</span></span>
* <span data-ttu-id="c6f3e-257">Las comillas bloques se representan como sangría pero sin un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-257">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="c6f3e-258">En Android, el formato Markdown para tarjetas de conector aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-258">On Android, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Formato markdown para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a><span data-ttu-id="c6f3e-260">Ejemplo de formato para tarjetas de conector de Markdown</span><span class="sxs-lookup"><span data-stu-id="c6f3e-260">Format example for Markdown connector cards</span></span>

<span data-ttu-id="c6f3e-261">El siguiente código muestra un ejemplo de formato para tarjetas de conector markdown:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-261">The following code shows an example of formatting for Markdown connector cards:</span></span>

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

## <a name="format-cards-with-html"></a><span data-ttu-id="c6f3e-262">Dar formato a tarjetas con HTML</span><span class="sxs-lookup"><span data-stu-id="c6f3e-262">Format cards with HTML</span></span>

<span data-ttu-id="c6f3e-263">Los siguientes tipos de tarjeta admiten el formato HTML en Teams:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-263">The following card types support HTML formatting in Teams:</span></span>

* <span data-ttu-id="c6f3e-264">Tarjetas de conector de O365: El markdown limitado y el formato HTML se admiten en Office 365 connector.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-264">O365 Connector cards: Limited Markdown and HTML formatting is supported in Office 365 Connector cards.</span></span>
* <span data-ttu-id="c6f3e-265">Tarjetas de miniatura y de héroe: las etiquetas HTML son compatibles con tarjetas sencillas, como las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-265">Hero and thumbnail cards: HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span>

<span data-ttu-id="c6f3e-266">El formato es diferente entre el escritorio y las versiones móviles de Teams para tarjetas de conector de O365 y tarjetas sencillas.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-266">Formatting is different between the desktop and the mobile versions of Teams for O365 Connector cards and simple cards.</span></span> <span data-ttu-id="c6f3e-267">En esta sección, puede ir a través del ejemplo de formato HTML para tarjetas de conector y tarjetas sencillas.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-267">In this section, you can go through the HTML format example for connector cards and simple cards.</span></span>

# <a name="html-format-for-o365-connector-cards"></a>[<span data-ttu-id="c6f3e-268">Formato HTML para tarjetas de conector de O365</span><span class="sxs-lookup"><span data-stu-id="c6f3e-268">HTML format for O365 Connector cards</span></span>](#tab/connector-html)

<span data-ttu-id="c6f3e-269">Las tarjetas de conector admiten markdown limitado y formato HTML.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-269">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="c6f3e-270">Estilo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-270">Style</span></span> | <span data-ttu-id="c6f3e-271">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-271">Example</span></span> | <span data-ttu-id="c6f3e-272">HTML</span><span class="sxs-lookup"><span data-stu-id="c6f3e-272">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6f3e-273">Negrita</span><span class="sxs-lookup"><span data-stu-id="c6f3e-273">Bold</span></span> | <span data-ttu-id="c6f3e-274">**text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-274">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="c6f3e-275">Italic</span><span class="sxs-lookup"><span data-stu-id="c6f3e-275">Italic</span></span> | <span data-ttu-id="c6f3e-276">*text*</span><span class="sxs-lookup"><span data-stu-id="c6f3e-276">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="c6f3e-277">Encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="c6f3e-277">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c6f3e-278">**Text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-278">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="c6f3e-279">Tachado</span><span class="sxs-lookup"><span data-stu-id="c6f3e-279">Strikethrough</span></span> | <span data-ttu-id="c6f3e-280">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c6f3e-280">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="c6f3e-281">Lista no ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-281">Unordered list</span></span> | <ul><li><span data-ttu-id="c6f3e-282">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-282">text</span></span></li><li><span data-ttu-id="c6f3e-283">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-283">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="c6f3e-284">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-284">Ordered list</span></span> | <ol><li><span data-ttu-id="c6f3e-285">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-285">text</span></span></li><li><span data-ttu-id="c6f3e-286">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-286">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="c6f3e-287">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-287">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="c6f3e-288">Blockquote</span><span class="sxs-lookup"><span data-stu-id="c6f3e-288">Blockquote</span></span> | <blockquote><span data-ttu-id="c6f3e-289">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-289">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="c6f3e-290">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="c6f3e-290">Hyperlink</span></span> | [<span data-ttu-id="c6f3e-291">Bing</span><span class="sxs-lookup"><span data-stu-id="c6f3e-291">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="c6f3e-292">Vínculo imagen</span><span class="sxs-lookup"><span data-stu-id="c6f3e-292">Image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="c6f3e-293">En las tarjetas de conector, las líneas nuevas se representan en HTML mediante la `<p>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-293">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="c6f3e-294">Diferencias de escritorio y móvil para tarjetas de conector</span><span class="sxs-lookup"><span data-stu-id="c6f3e-294">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="c6f3e-295">En el escritorio, el formato HTML para tarjetas de conector aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-295">On the desktop, HTML formatting for connector cards appears as shown in the following image:</span></span>

![Formato HTML para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="c6f3e-297">En iOS, el formato HTML aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-297">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Formato HTML para tarjetas de conector en el cliente de iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="c6f3e-299">Las tarjetas de conector que usan HTML para iOS incluyen los siguientes problemas:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-299">Connector cards using HTML for iOS include the following issues:</span></span>

* <span data-ttu-id="c6f3e-300">Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-300">Inline images are not rendered on iOS using either Markdown or HTML in connector cards.</span></span>
* <span data-ttu-id="c6f3e-301">El texto con formato previo se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-301">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="c6f3e-302">En Android, el formato HTML aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-302">On Android, HTML formatting appears as shown in the following image:</span></span>

![Formato HTML para tarjetas de conector en el cliente Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a><span data-ttu-id="c6f3e-304">Ejemplo de formato para tarjetas de conector HTML</span><span class="sxs-lookup"><span data-stu-id="c6f3e-304">Format sample for HTML connector cards</span></span>

<span data-ttu-id="c6f3e-305">El siguiente código muestra un ejemplo de formato para tarjetas de conector HTML:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-305">The following code shows an example of formatting for HTML connector cards:</span></span>

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[<span data-ttu-id="c6f3e-306">Formato HTML para tarjetas de miniatura y de héroe</span><span class="sxs-lookup"><span data-stu-id="c6f3e-306">HTML format for hero and thumbnail cards</span></span>](#tab/simple-html)

<span data-ttu-id="c6f3e-307">Las etiquetas HTML son compatibles con tarjetas sencillas, como las tarjetas de miniatura y de héroe.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-307">HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span> <span data-ttu-id="c6f3e-308">Markdown no es compatible.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-308">Markdown is not supported.</span></span>

| <span data-ttu-id="c6f3e-309">Estilo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-309">Style</span></span> | <span data-ttu-id="c6f3e-310">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-310">Example</span></span> | <span data-ttu-id="c6f3e-311">HTML</span><span class="sxs-lookup"><span data-stu-id="c6f3e-311">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6f3e-312">Negrita</span><span class="sxs-lookup"><span data-stu-id="c6f3e-312">Bold</span></span> | <span data-ttu-id="c6f3e-313">**text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-313">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="c6f3e-314">Italic</span><span class="sxs-lookup"><span data-stu-id="c6f3e-314">Italic</span></span> | <span data-ttu-id="c6f3e-315">*text*</span><span class="sxs-lookup"><span data-stu-id="c6f3e-315">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="c6f3e-316">Encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="c6f3e-316">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c6f3e-317">**Text**</span><span class="sxs-lookup"><span data-stu-id="c6f3e-317">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="c6f3e-318">Tachado</span><span class="sxs-lookup"><span data-stu-id="c6f3e-318">Strikethrough</span></span> | <span data-ttu-id="c6f3e-319">~~text~~</span><span class="sxs-lookup"><span data-stu-id="c6f3e-319">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="c6f3e-320">Lista no ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-320">Unordered list</span></span> | <ul><li><span data-ttu-id="c6f3e-321">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-321">text</span></span></li><li><span data-ttu-id="c6f3e-322">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-322">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="c6f3e-323">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="c6f3e-323">Ordered list</span></span> | <ol><li><span data-ttu-id="c6f3e-324">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-324">text</span></span></li><li><span data-ttu-id="c6f3e-325">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-325">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="c6f3e-326">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="c6f3e-326">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="c6f3e-327">Blockquote</span><span class="sxs-lookup"><span data-stu-id="c6f3e-327">Blockquote</span></span> | <blockquote><span data-ttu-id="c6f3e-328">text</span><span class="sxs-lookup"><span data-stu-id="c6f3e-328">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="c6f3e-329">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="c6f3e-329">Hyperlink</span></span> | [<span data-ttu-id="c6f3e-330">Bing</span><span class="sxs-lookup"><span data-stu-id="c6f3e-330">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="c6f3e-331">Vínculo imagen</span><span class="sxs-lookup"><span data-stu-id="c6f3e-331">Image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="c6f3e-332">Diferencias de escritorio y móvil para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="c6f3e-332">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="c6f3e-333">Como hay diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-333">As there are resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="c6f3e-334">En el escritorio, el formato HTML aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-334">On the desktop, HTML formatting appears as shown in the following image:</span></span>

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="c6f3e-336">En iOS, el formato HTML aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-336">On iOS, HTML formatting appears as shown in the following image:</span></span>

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="c6f3e-338">El formato de caracteres, como negrita y cursiva, no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-338">Character formatting, such as bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="c6f3e-339">En Android, el formato HTML aparece como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-339">On Android, HTML formatting appears as shown in the following image:</span></span>

![Formato HTML en el cliente Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="c6f3e-341">El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-341">Character formatting, such as bold and italic display correctly on Android.</span></span>

### <a name="format-example-for-simple-cards"></a><span data-ttu-id="c6f3e-342">Ejemplo de formato para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="c6f3e-342">Format example for simple cards</span></span>

<span data-ttu-id="c6f3e-343">Las imágenes de la sección anterior se crearon con Teams **App Studio**, donde la propiedad de texto de una tarjeta principal se establece en la siguiente cadena:</span><span class="sxs-lookup"><span data-stu-id="c6f3e-343">The images in the previous section were created using Teams **App Studio**, where the text property of a hero card is set to the following string:</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

<span data-ttu-id="c6f3e-344">Puedes probar el formato en tus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="c6f3e-344">You can test formatting in your own cards by modifying this code.</span></span>

---

## <a name="see-also"></a><span data-ttu-id="c6f3e-345">Vea también</span><span class="sxs-lookup"><span data-stu-id="c6f3e-345">See also</span></span>

* [<span data-ttu-id="c6f3e-346">Acciones de tarjeta</span><span class="sxs-lookup"><span data-stu-id="c6f3e-346">Card actions</span></span>](./cards-actions.md)
* [<span data-ttu-id="c6f3e-347">Módulos de tareas</span><span class="sxs-lookup"><span data-stu-id="c6f3e-347">Task modules</span></span>](~/task-modules-and-cards/cards/cards-format.md)
