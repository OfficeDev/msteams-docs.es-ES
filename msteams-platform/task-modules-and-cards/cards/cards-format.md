---
title: Formato del texto en las tarjetas
description: Describe el formato del texto de las tarjetas en Microsoft Teams
keywords: formato de las tarjetas de bots de Microsoft Teams
ms.date: 03/29/2018
ms.openlocfilehash: 944e6a69c68d284b3a7309063587bd4b75319bc7
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587814"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="0310e-104">Formato de tarjetas en Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0310e-104">Format cards in Teams</span></span>

<span data-ttu-id="0310e-105">Puede Agregar formato de texto enriquecido a las tarjetas con Markdown o HTML, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="0310e-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="0310e-106">Las tarjetas admiten el formato solo en la propiedad de texto, no en las propiedades de título o de subtítulo.</span><span class="sxs-lookup"><span data-stu-id="0310e-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="0310e-107">El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="0310e-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="0310e-108">Para las tarjetas adaptables actuales y futuras del desarrollo, se recomienda usar el formato Markdown.</span><span class="sxs-lookup"><span data-stu-id="0310e-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="0310e-109">La compatibilidad de formato es distinta entre los distintos tipos de tarjetas y la representación de la tarjeta puede variar ligeramente entre el escritorio y los clientes de los equipos móviles, así como los equipos en el explorador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="0310e-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="0310e-110">Puede incluir una imagen incorporada en cualquier tarjeta de Teams.</span><span class="sxs-lookup"><span data-stu-id="0310e-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="0310e-111">Imágenes a las que se les da formato `.png` , `.jpg` o `.gif` archivos y no deben exceder de 1024 × 1024 PX o 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0310e-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="0310e-112">GIF animado no es compatible oficialmente.</span><span class="sxs-lookup"><span data-stu-id="0310e-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="0310e-113">*Consulte* [referencia de tarjetas](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="0310e-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="0310e-114">Tarjetas de formato con Markdown</span><span class="sxs-lookup"><span data-stu-id="0310e-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="0310e-115">Hay dos tipos de tarjetas que admiten Markdown en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="0310e-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0310e-116">**Tarjetas adaptables**: Markdown se admite en el campo tarjeta adaptable `Textblock` , así como en `Fact.Title` y `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="0310e-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="0310e-117">No se admite HTML en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="0310e-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="0310e-118">**Tarjetas de conector de O365**: MARKDOWN y HTML limitado son compatibles con las tarjetas de conector de Office 365 en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="0310e-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="0310e-119">**Formato de Markdown: tarjetas adaptables**</span><span class="sxs-lookup"><span data-stu-id="0310e-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="0310e-120">Los estilos admitidos `Textblock` para `Fact.Title` y `Fact.Value` son:</span><span class="sxs-lookup"><span data-stu-id="0310e-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="0310e-121">Style</span><span class="sxs-lookup"><span data-stu-id="0310e-121">Style</span></span> | <span data-ttu-id="0310e-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0310e-122">Example</span></span> | <span data-ttu-id="0310e-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="0310e-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0310e-124">bold</span><span class="sxs-lookup"><span data-stu-id="0310e-124">bold</span></span> | <span data-ttu-id="0310e-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="0310e-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="0310e-126">italic</span><span class="sxs-lookup"><span data-stu-id="0310e-126">italic</span></span> | <span data-ttu-id="0310e-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="0310e-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="0310e-128">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="0310e-128">unordered list</span></span> | <ul><li><span data-ttu-id="0310e-129">text</span><span class="sxs-lookup"><span data-stu-id="0310e-129">text</span></span></li><li><span data-ttu-id="0310e-130">text</span><span class="sxs-lookup"><span data-stu-id="0310e-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="0310e-131">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="0310e-131">ordered list</span></span> | <ol><li><span data-ttu-id="0310e-132">text</span><span class="sxs-lookup"><span data-stu-id="0310e-132">text</span></span></li><li><span data-ttu-id="0310e-133">text</span><span class="sxs-lookup"><span data-stu-id="0310e-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="0310e-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="0310e-134">Hyperlinks</span></span> |[<span data-ttu-id="0310e-135">Bing</span><span class="sxs-lookup"><span data-stu-id="0310e-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="0310e-136">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="0310e-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="0310e-137">Encabezados</span><span class="sxs-lookup"><span data-stu-id="0310e-137">Headers</span></span>
* <span data-ttu-id="0310e-138">Tablas</span><span class="sxs-lookup"><span data-stu-id="0310e-138">Tables</span></span>
* <span data-ttu-id="0310e-139">Imágenes</span><span class="sxs-lookup"><span data-stu-id="0310e-139">Images</span></span>
* <span data-ttu-id="0310e-140">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="0310e-140">Preformatted text</span></span>
* <span data-ttu-id="0310e-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="0310e-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0310e-142">Las tarjetas adaptables no admiten el formato HTML.</span><span class="sxs-lookup"><span data-stu-id="0310e-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="0310e-143">Nuevas líneas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0310e-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="0310e-144">En las listas puede usar las `\r` `\n` secuencias de escape o de para las nuevas líneas.</span><span class="sxs-lookup"><span data-stu-id="0310e-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="0310e-145">Usar `\n\n` en una lista hará que se aplique sangría al siguiente elemento de la lista.</span><span class="sxs-lookup"><span data-stu-id="0310e-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="0310e-146">Si necesita más líneas en cualquier lugar del TextBlock, use `\n\n` .</span><span class="sxs-lookup"><span data-stu-id="0310e-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="0310e-147">Diferencias de escritorio y móviles para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0310e-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="0310e-148">El formato es ligeramente distinto entre el escritorio y las versiones móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="0310e-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="0310e-149">En el escritorio, el formato de Markdown con tarjeta adaptable aparece como este en los exploradores Web y en la aplicación cliente de Teams:</span><span class="sxs-lookup"><span data-stu-id="0310e-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formato Markdown de tarjeta adaptable en el cliente de escritorio](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="0310e-151">En iOS, el formato de Markdown con tarjeta adaptable tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![Formato Markdown de tarjeta adaptable en iOS](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="0310e-153">En Android, el formato de Markdown con tarjeta adaptable tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Formato Markdown de tarjeta adaptable en Android](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="0310e-155">Más información sobre tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0310e-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="0310e-156">[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) La fecha y las características de localización mencionadas en este tema no se admiten en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0310e-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="0310e-157">Ejemplo de formato para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="0310e-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="0310e-158">Mencione la compatibilidad en las tarjetas adaptables v 1.2</span><span class="sxs-lookup"><span data-stu-id="0310e-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="0310e-159">Las menciones basadas en tarjetas se admiten en clientes Web, de escritorio y móviles.</span><span class="sxs-lookup"><span data-stu-id="0310e-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="0310e-160">Puede Agregar @ menciones en un cuerpo de tarjeta adaptable para bots y respuestas de extensiones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="0310e-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="0310e-161">Para agregar @ menciones en las tarjetas, siga la misma lógica de notificación y representación que la de las [menciones basadas en mensajes en conversaciones de chat en el canal y en el grupo](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span><span class="sxs-lookup"><span data-stu-id="0310e-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="0310e-162">Los bots y las extensiones de mensajería pueden incluir menciones dentro del contenido de la tarjeta en elementos [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) y [FactSet](https://adaptivecards.io/explorer/FactSet.html) .</span><span class="sxs-lookup"><span data-stu-id="0310e-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="0310e-163">Actualmente, [los elementos multimedia](https://adaptivecards.io/explorer/Media.html) no se admiten en las tarjetas adaptables v 1.2 en la plataforma de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0310e-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="0310e-164">Los mensajes de bot no admiten las menciones del equipo & de canal.</span><span class="sxs-lookup"><span data-stu-id="0310e-164">Channel & Team mentions are not supported in bot messages.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="0310e-165">Creación de menciones</span><span class="sxs-lookup"><span data-stu-id="0310e-165">Constructing mentions</span></span>

<span data-ttu-id="0310e-166">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0310e-166">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="0310e-167">`<at>username</at>`en los elementos de tarjeta adaptable admitidos</span><span class="sxs-lookup"><span data-stu-id="0310e-167">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="0310e-168">El `mention` objeto dentro de una `msteams` propiedad en el contenido de la tarjeta, que incluye el identificador de usuario de Teams del usuario que se está mencionando</span><span class="sxs-lookup"><span data-stu-id="0310e-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="0310e-169">Ejemplo de tarjeta adaptable con mención</span><span class="sxs-lookup"><span data-stu-id="0310e-169">Sample Adaptive card with a mention</span></span>

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
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="0310e-170">**Formato de Markdown: tarjetas conector de O365**</span><span class="sxs-lookup"><span data-stu-id="0310e-170">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="0310e-171">Las tarjetas de conector admiten el formato HTML y Markdown limitados.</span><span class="sxs-lookup"><span data-stu-id="0310e-171">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="0310e-172">La compatibilidad con HTML se describe en la última sección.</span><span class="sxs-lookup"><span data-stu-id="0310e-172">HTML support is described in the last section.</span></span>

| <span data-ttu-id="0310e-173">Style</span><span class="sxs-lookup"><span data-stu-id="0310e-173">Style</span></span> | <span data-ttu-id="0310e-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0310e-174">Example</span></span> | <span data-ttu-id="0310e-175">Markdown</span><span class="sxs-lookup"><span data-stu-id="0310e-175">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0310e-176">bold</span><span class="sxs-lookup"><span data-stu-id="0310e-176">bold</span></span> | <span data-ttu-id="0310e-177">**text**</span><span class="sxs-lookup"><span data-stu-id="0310e-177">**text**</span></span> | `**text**` |
| <span data-ttu-id="0310e-178">italic</span><span class="sxs-lookup"><span data-stu-id="0310e-178">italic</span></span> | <span data-ttu-id="0310e-179">*text*</span><span class="sxs-lookup"><span data-stu-id="0310e-179">*text*</span></span> | `*text*` |
| <span data-ttu-id="0310e-180">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="0310e-180">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="0310e-181">**Texto**</span><span class="sxs-lookup"><span data-stu-id="0310e-181">**Text**</span></span> | `### Text`|
| <span data-ttu-id="0310e-182">Aplique</span><span class="sxs-lookup"><span data-stu-id="0310e-182">strikethrough</span></span> | <span data-ttu-id="0310e-183">~~text~~</span><span class="sxs-lookup"><span data-stu-id="0310e-183">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="0310e-184">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="0310e-184">unordered list</span></span> | <ul><li><span data-ttu-id="0310e-185">text</span><span class="sxs-lookup"><span data-stu-id="0310e-185">text</span></span></li><li><span data-ttu-id="0310e-186">text</span><span class="sxs-lookup"><span data-stu-id="0310e-186">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="0310e-187">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="0310e-187">ordered list</span></span> | <ol><li><span data-ttu-id="0310e-188">text</span><span class="sxs-lookup"><span data-stu-id="0310e-188">text</span></span></li><li><span data-ttu-id="0310e-189">text</span><span class="sxs-lookup"><span data-stu-id="0310e-189">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="0310e-190">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="0310e-190">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="0310e-191">blockquote</span><span class="sxs-lookup"><span data-stu-id="0310e-191">blockquote</span></span> | <span data-ttu-id="0310e-192">Texto de >blockquote</span><span class="sxs-lookup"><span data-stu-id="0310e-192">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="0310e-193">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="0310e-193">hyperlink</span></span> | [<span data-ttu-id="0310e-194">Bing</span><span class="sxs-lookup"><span data-stu-id="0310e-194">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="0310e-195">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="0310e-195">image link</span></span> |![Pato en una Rock](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="0310e-197">En las tarjetas conector, las líneas nuevas se representan para `\n\n` , pero no para `\n` o `\r` .</span><span class="sxs-lookup"><span data-stu-id="0310e-197">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="0310e-198">Diferencias de escritorio y móviles para tarjetas de conector con Markdown</span><span class="sxs-lookup"><span data-stu-id="0310e-198">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="0310e-199">En el escritorio, el formato de Markdown para tarjetas de conectores tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-199">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![Formato de Markdown para tarjetas de conector en el cliente de escritorio](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="0310e-201">En iOS, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-201">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![Formato de Markdown para tarjetas conector en el cliente iOS](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="0310e-203">Problemas:</span><span class="sxs-lookup"><span data-stu-id="0310e-203">Issues:</span></span>

* <span data-ttu-id="0310e-204">El cliente iOS para Teams no representa imágenes en línea de Markdown o HTML en tarjetas conectoras.</span><span class="sxs-lookup"><span data-stu-id="0310e-204">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="0310e-205">Blockquotes se representan como con sangría, pero sin fondo gris.</span><span class="sxs-lookup"><span data-stu-id="0310e-205">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="0310e-206">En Android, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-206">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Formato de Markdown para tarjetas conector en el cliente de Android](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="0310e-208">Ejemplo de formato para tarjetas conectoras de Markdown</span><span class="sxs-lookup"><span data-stu-id="0310e-208">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="0310e-209">Tarjetas de formato con HTML</span><span class="sxs-lookup"><span data-stu-id="0310e-209">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="0310e-210">**Formato HTML: tarjetas conector de O365**</span><span class="sxs-lookup"><span data-stu-id="0310e-210">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="0310e-211">Las tarjetas de conector admiten el formato HTML y Markdown limitados.</span><span class="sxs-lookup"><span data-stu-id="0310e-211">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="0310e-212">Markdown se describe en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="0310e-212">Markdown is described in the next section.</span></span>

| <span data-ttu-id="0310e-213">Style</span><span class="sxs-lookup"><span data-stu-id="0310e-213">Style</span></span> | <span data-ttu-id="0310e-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0310e-214">Example</span></span> | <span data-ttu-id="0310e-215">HTML</span><span class="sxs-lookup"><span data-stu-id="0310e-215">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0310e-216">bold</span><span class="sxs-lookup"><span data-stu-id="0310e-216">bold</span></span> | <span data-ttu-id="0310e-217">**text**</span><span class="sxs-lookup"><span data-stu-id="0310e-217">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="0310e-218">italic</span><span class="sxs-lookup"><span data-stu-id="0310e-218">italic</span></span> | <span data-ttu-id="0310e-219">*text*</span><span class="sxs-lookup"><span data-stu-id="0310e-219">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="0310e-220">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="0310e-220">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="0310e-221">**Texto**</span><span class="sxs-lookup"><span data-stu-id="0310e-221">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="0310e-222">Aplique</span><span class="sxs-lookup"><span data-stu-id="0310e-222">strikethrough</span></span> | <span data-ttu-id="0310e-223">~~text~~</span><span class="sxs-lookup"><span data-stu-id="0310e-223">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="0310e-224">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="0310e-224">unordered list</span></span> | <ul><li><span data-ttu-id="0310e-225">text</span><span class="sxs-lookup"><span data-stu-id="0310e-225">text</span></span></li><li><span data-ttu-id="0310e-226">text</span><span class="sxs-lookup"><span data-stu-id="0310e-226">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="0310e-227">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="0310e-227">ordered list</span></span> | <ol><li><span data-ttu-id="0310e-228">text</span><span class="sxs-lookup"><span data-stu-id="0310e-228">text</span></span></li><li><span data-ttu-id="0310e-229">text</span><span class="sxs-lookup"><span data-stu-id="0310e-229">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="0310e-230">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="0310e-230">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="0310e-231">blockquote</span><span class="sxs-lookup"><span data-stu-id="0310e-231">blockquote</span></span> | <blockquote><span data-ttu-id="0310e-232">text</span><span class="sxs-lookup"><span data-stu-id="0310e-232">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="0310e-233">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="0310e-233">hyperlink</span></span> | [<span data-ttu-id="0310e-234">Bing</span><span class="sxs-lookup"><span data-stu-id="0310e-234">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="0310e-235">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="0310e-235">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="0310e-236">En las tarjetas conector, las líneas nuevas se representan en HTML con la `<p>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="0310e-236">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="0310e-237">Diferencias de escritorio y móviles para tarjetas de conector con HTML</span><span class="sxs-lookup"><span data-stu-id="0310e-237">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="0310e-238">En el escritorio, el formato HTML de las tarjetas conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-238">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de escritorio](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="0310e-240">En iOS, el formato HTML tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="0310e-240">On iOS, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente iOS](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="0310e-242">Problemas:</span><span class="sxs-lookup"><span data-stu-id="0310e-242">Issues:</span></span>

* <span data-ttu-id="0310e-243">Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="0310e-243">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="0310e-244">El texto con formato previo se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="0310e-244">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="0310e-245">En Android, el formato HTML es similar a este:</span><span class="sxs-lookup"><span data-stu-id="0310e-245">On Android, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de Android](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="0310e-247">Ejemplo de formato para tarjetas conector de HTML</span><span class="sxs-lookup"><span data-stu-id="0310e-247">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="0310e-248">**Formato HTML: fichas de héroe y miniaturas**</span><span class="sxs-lookup"><span data-stu-id="0310e-248">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="0310e-249">Las etiquetas HTML son compatibles con tarjetas sencillas, como el héroe y la tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="0310e-249">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="0310e-250">No se admite Markdown.</span><span class="sxs-lookup"><span data-stu-id="0310e-250">Markdown is not supported.</span></span>

| <span data-ttu-id="0310e-251">Style</span><span class="sxs-lookup"><span data-stu-id="0310e-251">Style</span></span> | <span data-ttu-id="0310e-252">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="0310e-252">Example</span></span> | <span data-ttu-id="0310e-253">HTML</span><span class="sxs-lookup"><span data-stu-id="0310e-253">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0310e-254">bold</span><span class="sxs-lookup"><span data-stu-id="0310e-254">bold</span></span> | <span data-ttu-id="0310e-255">**text**</span><span class="sxs-lookup"><span data-stu-id="0310e-255">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="0310e-256">italic</span><span class="sxs-lookup"><span data-stu-id="0310e-256">italic</span></span> | <span data-ttu-id="0310e-257">*text*</span><span class="sxs-lookup"><span data-stu-id="0310e-257">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="0310e-258">encabezado (niveles 1 &ndash; 3)</span><span class="sxs-lookup"><span data-stu-id="0310e-258">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="0310e-259">**Texto**</span><span class="sxs-lookup"><span data-stu-id="0310e-259">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="0310e-260">Aplique</span><span class="sxs-lookup"><span data-stu-id="0310e-260">strikethrough</span></span> | <span data-ttu-id="0310e-261">~~text~~</span><span class="sxs-lookup"><span data-stu-id="0310e-261">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="0310e-262">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="0310e-262">unordered list</span></span> | <ul><li><span data-ttu-id="0310e-263">text</span><span class="sxs-lookup"><span data-stu-id="0310e-263">text</span></span></li><li><span data-ttu-id="0310e-264">text</span><span class="sxs-lookup"><span data-stu-id="0310e-264">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="0310e-265">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="0310e-265">ordered list</span></span> | <ol><li><span data-ttu-id="0310e-266">text</span><span class="sxs-lookup"><span data-stu-id="0310e-266">text</span></span></li><li><span data-ttu-id="0310e-267">text</span><span class="sxs-lookup"><span data-stu-id="0310e-267">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="0310e-268">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="0310e-268">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="0310e-269">blockquote</span><span class="sxs-lookup"><span data-stu-id="0310e-269">blockquote</span></span> | <blockquote><span data-ttu-id="0310e-270">text</span><span class="sxs-lookup"><span data-stu-id="0310e-270">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="0310e-271">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="0310e-271">hyperlink</span></span> | [<span data-ttu-id="0310e-272">Bing</span><span class="sxs-lookup"><span data-stu-id="0310e-272">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="0310e-273">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="0310e-273">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="0310e-274">Diferencias entre dispositivos móviles y de escritorio para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="0310e-274">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="0310e-275">Debido a las diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="0310e-275">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="0310e-276">En el escritorio, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="0310e-276">On the desktop, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de escritorio](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="0310e-278">En iOS, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="0310e-278">On iOS, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de iOS](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="0310e-280">Problemas:</span><span class="sxs-lookup"><span data-stu-id="0310e-280">Issues:</span></span>

* <span data-ttu-id="0310e-281">El formato de caracteres, como negrita y cursiva, no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="0310e-281">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="0310e-282">En Android, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="0310e-282">On Android, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de Android](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="0310e-284">El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="0310e-284">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="0310e-285">Ejemplo de formato para el formato HTML en tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="0310e-285">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="0310e-286">Estas capturas de pantallas se crearon con Teams AppStudio, donde la propiedad Text de una tarjeta Hero se estableció en la siguiente cadena.</span><span class="sxs-lookup"><span data-stu-id="0310e-286">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="0310e-287">Puede probar el formato en sus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="0310e-287">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
