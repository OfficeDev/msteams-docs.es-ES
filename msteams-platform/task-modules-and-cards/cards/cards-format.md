---
title: Formato del texto en las tarjetas
description: Describe el formato del texto de las tarjetas en Microsoft Teams
keywords: formato de las tarjetas de bots de Microsoft Teams
ms.date: 03/29/2018
ms.openlocfilehash: 4a467c5b0b21cc3c19977bf7caa25e6790904b10
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676152"
---
# <a name="card-formatting"></a><span data-ttu-id="bfcde-104">Formato de tarjeta</span><span class="sxs-lookup"><span data-stu-id="bfcde-104">Card formatting</span></span>

<span data-ttu-id="bfcde-105">Puede Agregar formato de texto enriquecido a las tarjetas con Markdown o HTML, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="bfcde-105">You can add rich text formatting to your cards using either markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="bfcde-106">Las tarjetas admiten el formato solo en la propiedad de texto, no en las propiedades de título o de subtítulo.</span><span class="sxs-lookup"><span data-stu-id="bfcde-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="bfcde-107">El formato se puede especificar mediante un subconjunto de formato XML (HTML) o Markdown, según el tipo de tarjeta.</span><span class="sxs-lookup"><span data-stu-id="bfcde-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="bfcde-108">Para las actuales tarjetas adaptables del desarrollo en el futuro de AMD se recomienda usar el formato Markdown.</span><span class="sxs-lookup"><span data-stu-id="bfcde-108">For current amd future development Adaptive cards using markdown formatting is recommended.</span></span>

<span data-ttu-id="bfcde-109">La compatibilidad de formato es distinta entre los distintos tipos de tarjetas y la representación de la tarjeta puede variar ligeramente entre el escritorio y los clientes de los equipos móviles, así como los equipos en el explorador de escritorio.</span><span class="sxs-lookup"><span data-stu-id="bfcde-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

## <a name="card-types"></a><span data-ttu-id="bfcde-110">Tipos de tarjeta</span><span class="sxs-lookup"><span data-stu-id="bfcde-110">Card types</span></span>

<span data-ttu-id="bfcde-111">Hay tres tipos de tarjetas que admiten Markdown en Microsoft Teams:</span><span class="sxs-lookup"><span data-stu-id="bfcde-111">There are three types of cards that support Markdown in Teams:</span></span>

* <span data-ttu-id="bfcde-112">**Tarjetas adaptables**: Markdown se admite en el `Textblock` campo tarjeta adaptable, `Fact.Title` así `Fact.Value`como en y.</span><span class="sxs-lookup"><span data-stu-id="bfcde-112">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="bfcde-113">No se admite HTML en tarjetas adaptables.</span><span class="sxs-lookup"><span data-stu-id="bfcde-113">HTML is not supported in adaptive cards.</span></span>
* <span data-ttu-id="bfcde-114">**Tarjetas de conector de O365**: MARKDOWN y HTML limitado son compatibles con las tarjetas de conector de Office 365 en los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="bfcde-114">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>
* <span data-ttu-id="bfcde-115">**Tarjetas sencillas**: se admite HTML limitado, pero Markdown no se admite en tarjetas sencillas.</span><span class="sxs-lookup"><span data-stu-id="bfcde-115">**Simple Cards**: Limited HTML is supported, but markdown is not supported in simple cards.</span></span>

## <a name="markdown-formatting-for-adaptive-cards"></a><span data-ttu-id="bfcde-116">Formato de Markdown para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-116">Markdown formatting for Adaptive Cards</span></span>

 <span data-ttu-id="bfcde-117">Los estilos admitidos `Textblock`para `Fact.Title` y `Fact.Value` son:</span><span class="sxs-lookup"><span data-stu-id="bfcde-117">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="bfcde-118">Style</span><span class="sxs-lookup"><span data-stu-id="bfcde-118">Style</span></span> | <span data-ttu-id="bfcde-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfcde-119">Example</span></span> | <span data-ttu-id="bfcde-120">Markdown</span><span class="sxs-lookup"><span data-stu-id="bfcde-120">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfcde-121">bold</span><span class="sxs-lookup"><span data-stu-id="bfcde-121">bold</span></span> | <span data-ttu-id="bfcde-122">**Bold**</span><span class="sxs-lookup"><span data-stu-id="bfcde-122">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="bfcde-123">italic</span><span class="sxs-lookup"><span data-stu-id="bfcde-123">italic</span></span> | <span data-ttu-id="bfcde-124">_Italic_</span><span class="sxs-lookup"><span data-stu-id="bfcde-124">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="bfcde-125">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="bfcde-125">unordered list</span></span> | <ul><li><span data-ttu-id="bfcde-126">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-126">text</span></span></li><li><span data-ttu-id="bfcde-127">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-127">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="bfcde-128">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="bfcde-128">ordered list</span></span> | <ol><li><span data-ttu-id="bfcde-129">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-129">text</span></span></li><li><span data-ttu-id="bfcde-130">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-130">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="bfcde-131">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="bfcde-131">Hyperlinks</span></span> |[<span data-ttu-id="bfcde-132">Bing</span><span class="sxs-lookup"><span data-stu-id="bfcde-132">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="bfcde-133">No se admiten las siguientes etiquetas Markdown:</span><span class="sxs-lookup"><span data-stu-id="bfcde-133">The following markdown tags are not supported:</span></span>

* <span data-ttu-id="bfcde-134">Encabezados</span><span class="sxs-lookup"><span data-stu-id="bfcde-134">Headers</span></span>
* <span data-ttu-id="bfcde-135">Tablas</span><span class="sxs-lookup"><span data-stu-id="bfcde-135">Tables</span></span>
* <span data-ttu-id="bfcde-136">Imágenes</span><span class="sxs-lookup"><span data-stu-id="bfcde-136">Images</span></span>
* <span data-ttu-id="bfcde-137">Texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="bfcde-137">Preformatted text</span></span>
* <span data-ttu-id="bfcde-138">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="bfcde-138">Blockquotes</span></span>

<span data-ttu-id="bfcde-139">Las tarjetas adaptables no admiten el formato HTML.</span><span class="sxs-lookup"><span data-stu-id="bfcde-139">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="bfcde-140">Nuevas líneas para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-140">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="bfcde-141">En las listas puede usar las `\r` secuencias `\n` de escape o de para las nuevas líneas.</span><span class="sxs-lookup"><span data-stu-id="bfcde-141">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="bfcde-142">Usar `\n\n` en una lista hará que se aplique sangría al siguiente elemento de la lista.</span><span class="sxs-lookup"><span data-stu-id="bfcde-142">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="bfcde-143">Si necesita más líneas en cualquier lugar del TextBlock, `\n\n`use.</span><span class="sxs-lookup"><span data-stu-id="bfcde-143">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="bfcde-144">Diferencias de escritorio y móviles para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-144">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="bfcde-145">El formato es ligeramente distinto entre el escritorio y las versiones móviles de Teams.</span><span class="sxs-lookup"><span data-stu-id="bfcde-145">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="bfcde-146">En el escritorio, el formato de Markdown con tarjeta adaptable aparece como este en los exploradores Web y en la aplicación cliente de Teams:</span><span class="sxs-lookup"><span data-stu-id="bfcde-146">On the desktop, Adaptive Card markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![Formato Markdown de tarjeta adaptable en el cliente de escritorio](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="bfcde-148">En iOS, el formato de Markdown con tarjeta adaptable tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-148">On iOS, Adaptive Card markdown formatting appears like this:</span></span>

![Formato Markdown de tarjeta adaptable en iOS](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="bfcde-150">En Android, el formato de Markdown con tarjeta adaptable tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-150">On Android, Adaptive Card markdown formatting appears like this:</span></span>

![Formato Markdown de tarjeta adaptable en Android](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="bfcde-152">Para obtener más información sobre las tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-152">For more information on Adaptive Cards</span></span>

<span data-ttu-id="bfcde-153">[Características de texto en tarjetas adaptables](/adaptive-cards/create/textfeatures) La fecha y las características de localización mencionadas en este tema no se admiten en Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bfcde-153">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="bfcde-154">Ejemplo de formato para tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-154">Formatting sample for Adaptive cards</span></span>

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
## <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="bfcde-155">Mencione la compatibilidad en tarjetas adaptables</span><span class="sxs-lookup"><span data-stu-id="bfcde-155">Mention support within Adaptive cards</span></span> 

> [!NOTE]
> <span data-ttu-id="bfcde-156">Mencione que la compatibilidad en tarjetas solo se admite actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro) .</span><span class="sxs-lookup"><span data-stu-id="bfcde-156">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro) only.</span></span>

<span data-ttu-id="bfcde-157">Los bots y las extensiones de mensajería ahora pueden incluir menciones dentro del contenido de la tarjeta en elementos FactSet y bloques de texto.</span><span class="sxs-lookup"><span data-stu-id="bfcde-157">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span> 

### <a name="constructing-mentions"></a><span data-ttu-id="bfcde-158">Creación de menciones</span><span class="sxs-lookup"><span data-stu-id="bfcde-158">Constructing mentions</span></span>
<span data-ttu-id="bfcde-159">Para incluir una mención en una tarjeta adaptable, la aplicación debe incluir los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bfcde-159">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="bfcde-160">`<at>username</at>`en los elementos de tarjeta adaptable admitidos</span><span class="sxs-lookup"><span data-stu-id="bfcde-160">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="bfcde-161">El `mention` objeto dentro de una `msteams` propiedad en el contenido de la tarjeta, que incluye el identificador de usuario de Teams del usuario que se está mencionando</span><span class="sxs-lookup"><span data-stu-id="bfcde-161">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="bfcde-162">Tenga en cuenta que las tarjetas con menciones no se admiten en los clientes móviles por el momento.</span><span class="sxs-lookup"><span data-stu-id="bfcde-162">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="bfcde-163">Ejemplo de tarjeta adaptable con mención</span><span class="sxs-lookup"><span data-stu-id="bfcde-163">Sample Adaptive card with a mention</span></span>
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

## <a name="html-formatting-for-connector-cards"></a><span data-ttu-id="bfcde-164">Formato HTML para tarjetas conectoras</span><span class="sxs-lookup"><span data-stu-id="bfcde-164">HTML formatting for Connector Cards</span></span>

<span data-ttu-id="bfcde-165">Las tarjetas de conector admiten el formato HTML y Markdown limitados.</span><span class="sxs-lookup"><span data-stu-id="bfcde-165">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="bfcde-166">Markdown se describe en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="bfcde-166">Markdown is described in the next section.</span></span>

| <span data-ttu-id="bfcde-167">Style</span><span class="sxs-lookup"><span data-stu-id="bfcde-167">Style</span></span> | <span data-ttu-id="bfcde-168">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfcde-168">Example</span></span> | <span data-ttu-id="bfcde-169">HTML</span><span class="sxs-lookup"><span data-stu-id="bfcde-169">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfcde-170">bold</span><span class="sxs-lookup"><span data-stu-id="bfcde-170">bold</span></span> | <span data-ttu-id="bfcde-171">**text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-171">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="bfcde-172">italic</span><span class="sxs-lookup"><span data-stu-id="bfcde-172">italic</span></span> | <span data-ttu-id="bfcde-173">*text*</span><span class="sxs-lookup"><span data-stu-id="bfcde-173">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="bfcde-174">encabezado (niveles 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="bfcde-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="bfcde-175">**Text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-175">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="bfcde-176">Aplique</span><span class="sxs-lookup"><span data-stu-id="bfcde-176">strikethrough</span></span> | <span data-ttu-id="bfcde-177">~~text~~</span><span class="sxs-lookup"><span data-stu-id="bfcde-177">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="bfcde-178">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="bfcde-178">unordered list</span></span> | <ul><li><span data-ttu-id="bfcde-179">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-179">text</span></span></li><li><span data-ttu-id="bfcde-180">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-180">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="bfcde-181">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="bfcde-181">ordered list</span></span> | <ol><li><span data-ttu-id="bfcde-182">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-182">text</span></span></li><li><span data-ttu-id="bfcde-183">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-183">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="bfcde-184">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="bfcde-184">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="bfcde-185">blockquote</span><span class="sxs-lookup"><span data-stu-id="bfcde-185">blockquote</span></span> | <blockquote><span data-ttu-id="bfcde-186">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-186">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="bfcde-187">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="bfcde-187">hyperlink</span></span> | [<span data-ttu-id="bfcde-188">Bing</span><span class="sxs-lookup"><span data-stu-id="bfcde-188">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="bfcde-189">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="bfcde-189">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="bfcde-190">En las tarjetas conector, las líneas nuevas se representan en HTML `<p>` con la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="bfcde-190">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="bfcde-191">Diferencias de escritorio y móviles para tarjetas de conector con HTML</span><span class="sxs-lookup"><span data-stu-id="bfcde-191">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="bfcde-192">En el escritorio, el formato HTML de las tarjetas conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-192">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de escritorio](~/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="bfcde-194">En iOS, el formato HTML tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-194">On iOS, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente iOS](~/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="bfcde-196">Problemas:</span><span class="sxs-lookup"><span data-stu-id="bfcde-196">Issues:</span></span>

* <span data-ttu-id="bfcde-197">Las imágenes en línea no se representan en iOS con Markdown o HTML en tarjetas de conector.</span><span class="sxs-lookup"><span data-stu-id="bfcde-197">Inline images are not rendered on iOS using either markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="bfcde-198">El texto con formato previo se representa pero no tiene un fondo gris.</span><span class="sxs-lookup"><span data-stu-id="bfcde-198">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="bfcde-199">En Android, el formato HTML es similar a este:</span><span class="sxs-lookup"><span data-stu-id="bfcde-199">On Android, HTML formatting looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de Android](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="bfcde-201">Ejemplo de formato para tarjetas conector de HTML</span><span class="sxs-lookup"><span data-stu-id="bfcde-201">Formatting sample for HTML Connector Cards</span></span>

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

## <a name="markdown-formatting-for-connector-cards"></a><span data-ttu-id="bfcde-202">Formato de Markdown para tarjetas conectoras</span><span class="sxs-lookup"><span data-stu-id="bfcde-202">Markdown formatting for Connector Cards</span></span>

<span data-ttu-id="bfcde-203">Las tarjetas de conector admiten el formato HTML y Markdown limitados.</span><span class="sxs-lookup"><span data-stu-id="bfcde-203">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="bfcde-204">El código HTML se describe en la última sección.</span><span class="sxs-lookup"><span data-stu-id="bfcde-204">HTML is described in the last section.</span></span>

| <span data-ttu-id="bfcde-205">Style</span><span class="sxs-lookup"><span data-stu-id="bfcde-205">Style</span></span> | <span data-ttu-id="bfcde-206">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfcde-206">Example</span></span> | <span data-ttu-id="bfcde-207">Markdown</span><span class="sxs-lookup"><span data-stu-id="bfcde-207">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfcde-208">bold</span><span class="sxs-lookup"><span data-stu-id="bfcde-208">bold</span></span> | <span data-ttu-id="bfcde-209">**text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-209">**text**</span></span> | `**text**` |
| <span data-ttu-id="bfcde-210">italic</span><span class="sxs-lookup"><span data-stu-id="bfcde-210">italic</span></span> | <span data-ttu-id="bfcde-211">*text*</span><span class="sxs-lookup"><span data-stu-id="bfcde-211">*text*</span></span> | `*text*` |
| <span data-ttu-id="bfcde-212">encabezado (niveles 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="bfcde-212">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="bfcde-213">**Text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-213">**Text**</span></span> | `### Text`|
| <span data-ttu-id="bfcde-214">Aplique</span><span class="sxs-lookup"><span data-stu-id="bfcde-214">strikethrough</span></span> | <span data-ttu-id="bfcde-215">~~text~~</span><span class="sxs-lookup"><span data-stu-id="bfcde-215">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="bfcde-216">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="bfcde-216">unordered list</span></span> | <ul><li><span data-ttu-id="bfcde-217">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-217">text</span></span></li><li><span data-ttu-id="bfcde-218">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-218">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="bfcde-219">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="bfcde-219">ordered list</span></span> | <ol><li><span data-ttu-id="bfcde-220">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-220">text</span></span></li><li><span data-ttu-id="bfcde-221">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-221">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="bfcde-222">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="bfcde-222">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="bfcde-223">blockquote</span><span class="sxs-lookup"><span data-stu-id="bfcde-223">blockquote</span></span> | <span data-ttu-id="bfcde-224">Texto de >blockquote</span><span class="sxs-lookup"><span data-stu-id="bfcde-224">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="bfcde-225">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="bfcde-225">hyperlink</span></span> | [<span data-ttu-id="bfcde-226">Bing</span><span class="sxs-lookup"><span data-stu-id="bfcde-226">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="bfcde-227">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="bfcde-227">image link</span></span> |![Pato en una Rock](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="bfcde-229">En las tarjetas conector, las líneas nuevas se `\n\n`representan para, pero `\n` no `\r`para o.</span><span class="sxs-lookup"><span data-stu-id="bfcde-229">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="bfcde-230">Diferencias de escritorio y móviles para tarjetas de conector con Markdown</span><span class="sxs-lookup"><span data-stu-id="bfcde-230">Mobile and desktop differences for connector cards using markdown</span></span>

<span data-ttu-id="bfcde-231">En el escritorio, el formato de Markdown para tarjetas de conectores tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-231">On the desktop, markdown formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de escritorio](~/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="bfcde-233">En iOS, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-233">On iOS, markdown formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente iOS](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="bfcde-235">Problemas:</span><span class="sxs-lookup"><span data-stu-id="bfcde-235">Issues:</span></span>

* <span data-ttu-id="bfcde-236">El cliente iOS para Teams no representa imágenes en línea de Markdown o HTML en tarjetas conectoras.</span><span class="sxs-lookup"><span data-stu-id="bfcde-236">The iOS client for Teams does not render markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="bfcde-237">Blockquotes se representan como con sangría, pero sin fondo gris.</span><span class="sxs-lookup"><span data-stu-id="bfcde-237">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="bfcde-238">En Android, el formato de Markdown para tarjetas de conector tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="bfcde-238">On Android, markdown formatting for connector cards looks like this:</span></span>

![Formato HTML para tarjetas conector en el cliente de Android](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="bfcde-240">Ejemplo de formato para tarjetas conectoras de Markdown</span><span class="sxs-lookup"><span data-stu-id="bfcde-240">Formatting example for markdown Connector Cards</span></span>

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

## <a name="html-formatting-for-simple-cards"></a><span data-ttu-id="bfcde-241">Formato HTML para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="bfcde-241">HTML Formatting for simple cards</span></span>

<span data-ttu-id="bfcde-242">Estas etiquetas HTML son compatibles con tarjetas sencillas, como el héroe y la tarjeta en miniatura.</span><span class="sxs-lookup"><span data-stu-id="bfcde-242">These HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="bfcde-243">No se admite Markdown.</span><span class="sxs-lookup"><span data-stu-id="bfcde-243">Markdown is not supported.</span></span>

| <span data-ttu-id="bfcde-244">Style</span><span class="sxs-lookup"><span data-stu-id="bfcde-244">Style</span></span> | <span data-ttu-id="bfcde-245">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bfcde-245">Example</span></span> | <span data-ttu-id="bfcde-246">HTML</span><span class="sxs-lookup"><span data-stu-id="bfcde-246">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bfcde-247">bold</span><span class="sxs-lookup"><span data-stu-id="bfcde-247">bold</span></span> | <span data-ttu-id="bfcde-248">**text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-248">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="bfcde-249">italic</span><span class="sxs-lookup"><span data-stu-id="bfcde-249">italic</span></span> | <span data-ttu-id="bfcde-250">*text*</span><span class="sxs-lookup"><span data-stu-id="bfcde-250">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="bfcde-251">encabezado (niveles 1&ndash;3)</span><span class="sxs-lookup"><span data-stu-id="bfcde-251">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="bfcde-252">**Text**</span><span class="sxs-lookup"><span data-stu-id="bfcde-252">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="bfcde-253">Aplique</span><span class="sxs-lookup"><span data-stu-id="bfcde-253">strikethrough</span></span> | <span data-ttu-id="bfcde-254">~~text~~</span><span class="sxs-lookup"><span data-stu-id="bfcde-254">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="bfcde-255">lista sin ordenar</span><span class="sxs-lookup"><span data-stu-id="bfcde-255">unordered list</span></span> | <ul><li><span data-ttu-id="bfcde-256">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-256">text</span></span></li><li><span data-ttu-id="bfcde-257">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-257">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="bfcde-258">Lista ordenada</span><span class="sxs-lookup"><span data-stu-id="bfcde-258">ordered list</span></span> | <ol><li><span data-ttu-id="bfcde-259">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-259">text</span></span></li><li><span data-ttu-id="bfcde-260">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-260">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="bfcde-261">texto con formato previo</span><span class="sxs-lookup"><span data-stu-id="bfcde-261">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="bfcde-262">blockquote</span><span class="sxs-lookup"><span data-stu-id="bfcde-262">blockquote</span></span> | <blockquote><span data-ttu-id="bfcde-263">text</span><span class="sxs-lookup"><span data-stu-id="bfcde-263">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="bfcde-264">hipervínculo</span><span class="sxs-lookup"><span data-stu-id="bfcde-264">hyperlink</span></span> | [<span data-ttu-id="bfcde-265">Bing</span><span class="sxs-lookup"><span data-stu-id="bfcde-265">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="bfcde-266">vínculo de imagen</span><span class="sxs-lookup"><span data-stu-id="bfcde-266">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="bfcde-267">Diferencias entre dispositivos móviles y de escritorio para tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="bfcde-267">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="bfcde-268">Debido a las diferencias de resolución entre la plataforma de escritorio y la plataforma móvil, el formato es diferente entre el escritorio y la versión móvil de Teams.</span><span class="sxs-lookup"><span data-stu-id="bfcde-268">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="bfcde-269">En el escritorio, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="bfcde-269">On the desktop, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de escritorio](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="bfcde-271">En iOS, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="bfcde-271">On iOS, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de iOS](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="bfcde-273">Problemas:</span><span class="sxs-lookup"><span data-stu-id="bfcde-273">Issues:</span></span>

* <span data-ttu-id="bfcde-274">El formato de caracteres, como negrita y cursiva, no se representa en iOS.</span><span class="sxs-lookup"><span data-stu-id="bfcde-274">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="bfcde-275">En Android, el formato HTML tiene un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="bfcde-275">On Android, HTML formatting appears like this:</span></span>

![Formato HTML en el cliente de Android](~/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="bfcde-277">El formato de caracteres, como negrita y cursiva, se muestra correctamente en Android.</span><span class="sxs-lookup"><span data-stu-id="bfcde-277">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="bfcde-278">Ejemplo de formato para el formato HTML en tarjetas sencillas</span><span class="sxs-lookup"><span data-stu-id="bfcde-278">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="bfcde-279">Estas capturas de pantallas se crearon con Teams AppStudio, donde la propiedad Text de una tarjeta Hero se estableció en la siguiente cadena.</span><span class="sxs-lookup"><span data-stu-id="bfcde-279">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="bfcde-280">Puede probar el formato en sus propias tarjetas modificando este código.</span><span class="sxs-lookup"><span data-stu-id="bfcde-280">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
