---
title: Contribuir a la Teams documentación
description: pasos para crear y publicar Teams documentación
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a567b0462397780650d6173df9dae1b340a06f97
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140519"
---
# <a name="contribute-to-teams-documentation"></a><span data-ttu-id="1c7ae-103">Contribuir a la Teams documentación</span><span class="sxs-lookup"><span data-stu-id="1c7ae-103">Contribute to Teams documentation</span></span>

<span data-ttu-id="1c7ae-104">Teams documentación forma parte de la biblioteca de documentación técnica de **Microsoft Docs.**</span><span class="sxs-lookup"><span data-stu-id="1c7ae-104">Teams documentation is part of the **Microsoft Docs** technical documentation library.</span></span> <span data-ttu-id="1c7ae-105">El contenido se organiza en grupos denominados docsets, cada uno que representa un grupo de documentos relacionados administrados como una sola entidad.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="1c7ae-106">Los artículos del mismo conjunto de documentos tienen la misma extensión de ruta de acceso url después **de docs.microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-106">Articles in the same docset have the same URL path extension after **docs.microsoft.com**.</span></span> <span data-ttu-id="1c7ae-107">Por ejemplo, `/docs.microsoft.com/microsoftteams/...` es el principio de la ruta Teams de archivo docset.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-107">For example, `/docs.microsoft.com/microsoftteams/...` is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="1c7ae-108">Teams artículos se escriben en la sintaxis de Markdown y se hospedan en GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-108">Teams articles are written in Markdown syntax and hosted on GitHub.</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="1c7ae-109">Configurar el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="1c7ae-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1c7ae-110">Instalar [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="1c7ae-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="1c7ae-111">Instalar [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span><span class="sxs-lookup"><span data-stu-id="1c7ae-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="1c7ae-112">Instale [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde VS Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="1c7ae-113">&emsp;&emsp; o</span><span class="sxs-lookup"><span data-stu-id="1c7ae-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1c7ae-114">Instalar en VS Code:</span><span class="sxs-lookup"><span data-stu-id="1c7ae-114">Install within VS Code:</span></span>

   1. <span data-ttu-id="1c7ae-115">Seleccione el **icono Extensiones** en la barra de actividad lateral o use el comando Ver = **> Extensiones** o Ctrl+Mayús+X y busque **Microsoft Docs Authoring Pack**.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command or Ctrl+Shift+X and, search for **Microsoft Docs Authoring Pack**.</span></span>
   1. <span data-ttu-id="1c7ae-116">Seleccione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-116">Select **Install**.</span></span>
   1. <span data-ttu-id="1c7ae-117">Después de la instalación, **el botón Instalar** cambia al botón **Administrar** engranaje.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-117">After installation, the **Install** changes to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="1c7ae-118">Revisar la Guía de colaboradores de Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="1c7ae-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="1c7ae-119">La guía de colaboradores proporciona instrucciones para crear, publicar y actualizar contenido técnico en la **plataforma de Microsoft Docs.**</span><span class="sxs-lookup"><span data-stu-id="1c7ae-119">The contributors guide provides direction to create, publish, and update technical content on the **Microsoft Docs** platform.</span></span> 

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="1c7ae-120">Guías de contenido, estilo y escritura de Microsoft</span><span class="sxs-lookup"><span data-stu-id="1c7ae-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="1c7ae-121">**[Microsoft Writing Style Guide:](/style-guide/welcome)** Microsoft Writing Style Guide es un recurso completo para la escritura técnica y refleja el enfoque moderno de Microsoft para la voz y el estilo.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide is a comprehensive resource for technical writing and reflects Microsoft's modern approach to voice and style.</span></span> <span data-ttu-id="1c7ae-122">Para obtener una referencia sencilla, agregue esta guía en línea al menú **Favoritos del** explorador.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-122">For easy reference, add this online guide to your browser's **Favorites** menu.</span></span>

* <span data-ttu-id="1c7ae-123">**[Escribir contenido para](/style-guide/developer-content/)** desarrolladores: Teams contenido específico está dirigido a una audiencia de desarrolladores con una comprensión fundamental de los conceptos y procesos de programación.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-123">**[Writing developer content](/style-guide/developer-content/)**: Teams specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="1c7ae-124">Es importante que proporcione información clara y técnicamente precisa de una manera atractiva mientras mantiene el tono y el estilo de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-124">It is important that you must provide clear, technically accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="1c7ae-125">**[Escribir instrucciones paso a paso:](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Las experiencias aplicadas e interactivas son una excelente manera para que los desarrolladores aprendan sobre los productos y tecnologías de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-125">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="1c7ae-126">Presentar procedimientos complejos o simples en un formato progresivo es natural y fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-126">Presenting complex or simple procedures in a progressive format is natural and user friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="1c7ae-127">Referencia de MarkDown</span><span class="sxs-lookup"><span data-stu-id="1c7ae-127">MarkDown reference</span></span>

<span data-ttu-id="1c7ae-128">**Las páginas de Microsoft Docs** se escriben en **la sintaxis de MarkDown** y se analizan a través de un [motor Markdig.](https://github.com/lunet-io/markdig)</span><span class="sxs-lookup"><span data-stu-id="1c7ae-128">**Microsoft Docs** pages are written in **MarkDown** syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="1c7ae-129">Para obtener más información sobre etiquetas específicas y convenciones de formato, vea [Docs Markdown reference](/contribute/markdown-reference).</span><span class="sxs-lookup"><span data-stu-id="1c7ae-129">For more information on specific tags and formatting conventions, see [Docs Markdown reference](/contribute/markdown-reference).</span></span>

## <a name="file-paths"></a><span data-ttu-id="1c7ae-130">Rutas de acceso a archivos</span><span class="sxs-lookup"><span data-stu-id="1c7ae-130">File Paths</span></span>

<span data-ttu-id="1c7ae-131">Al usar rutas de acceso relativas y crear vínculos a otros conjuntos de documentos, es importante establecer una ruta de acceso de archivo válida para hipervínculos en la documentación.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-131">When using relative paths and creating links to other docsets, it is important to set a valid file path for hyperlinks in your documentation.</span></span> <span data-ttu-id="1c7ae-132">La compilación se ejecuta GitHub solo si la ruta de acceso del archivo es correcta o válida.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-132">Your build succeeds on GitHub only if the file path is correct or valid.</span></span>
 
<span data-ttu-id="1c7ae-133">Para obtener más información sobre hipervínculos y rutas de acceso a archivos, [vea usar vínculos en la documentación](/contribute/how-to-write-links).</span><span class="sxs-lookup"><span data-stu-id="1c7ae-133">For more information on hyperlinks and file paths, see [use links in documentation](/contribute/how-to-write-links).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c7ae-134">Para hacer referencia a un artículo que **forma parte del** docset Teams plataforma:</span><span class="sxs-lookup"><span data-stu-id="1c7ae-134">To reference an article that is **part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="1c7ae-135">&emsp;&#x2714; use una ruta relativa sin una barra diagonal hacia delante.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-135">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="1c7ae-136">&emsp;&#x2714; incluir la extensión de archivo Markdown.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-136">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="1c7ae-137">Por ejemplo: **directorio primario/directorio/ruta de** acceso a article.md :> [Crear una aplicación para Microsoft Teams](../concepts/building-an-app.md)</span><span class="sxs-lookup"><span data-stu-id="1c7ae-137">Ex:  **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span></span> <br><br>
> <span data-ttu-id="1c7ae-138">Para hacer referencia a un artículo de biblioteca de Microsoft Docs que **no forma** parte del Teams docset de la plataforma:</span><span class="sxs-lookup"><span data-stu-id="1c7ae-138">To reference a Microsoft Docs library article that **is not part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="1c7ae-139">&emsp;&#x2714; use una ruta relativa que comience por una barra diagonal.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-139">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="1c7ae-140">&emsp;&#x2714; No incluya la extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-140">&emsp;&#x2714; Do not include the file extension.</span></span> <br> <span data-ttu-id="1c7ae-141">Ex: **/docset/address-to-file-location** —> [Use la API](/graph/api/resources/teams-api-overview) de Microsoft Graph para trabajar con Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1c7ae-141">Ex:  **/docset/address-to-file-location** —> [Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)</span></span><br><br>
> <span data-ttu-id="1c7ae-142">Para hacer referencia a una página fuera de la biblioteca de Microsoft Docs, como GitHub, use la ruta de `https` acceso de archivo completa.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-142">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="1c7ae-143">Ejemplos de código y fragmentos de código</span><span class="sxs-lookup"><span data-stu-id="1c7ae-143">Code Samples and Snippets</span></span>

<span data-ttu-id="1c7ae-144">Los ejemplos de código desempeñan un papel importante para usar api y SDK de forma eficaz.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-144">Code samples play an important role to use APIs and SDKs effectively.</span></span> <span data-ttu-id="1c7ae-145">Los ejemplos de código bien presentados pueden comunicar cómo funcionan las cosas más claramente que el texto descriptivo y la información de instrucciones solo.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-145">Well presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="1c7ae-146">Los ejemplos de código deben ser precisos, concisos, bien documentados y fáciles de usar para el lector.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-146">Your code samples must be accurate, concise, well documented, and reader friendly.</span></span> <span data-ttu-id="1c7ae-147">El código fácil de leer debe ser fácil de comprender, probar, depurar, mantener, modificar y extender.</span><span class="sxs-lookup"><span data-stu-id="1c7ae-147">Code that is easy to read must be easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="1c7ae-148">Para obtener más información, [vea cómo incluir código en los documentos](/contribute/code-in-docs).</span><span class="sxs-lookup"><span data-stu-id="1c7ae-148">For more information, see [how to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="1c7ae-149">Vea también</span><span class="sxs-lookup"><span data-stu-id="1c7ae-149">See also</span></span>

* [<span data-ttu-id="1c7ae-150">Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="1c7ae-150">Microsoft Docs</span></span>](/)
* [<span data-ttu-id="1c7ae-151">guía de colaboradores</span><span class="sxs-lookup"><span data-stu-id="1c7ae-151">contributors guide</span></span>](/contribute)
* [<span data-ttu-id="1c7ae-152">Inicio rápido de voz y estilo de documentos</span><span class="sxs-lookup"><span data-stu-id="1c7ae-152">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* [<span data-ttu-id="1c7ae-153">Cutting Edge : Source Code Readability Sugerencias</span><span class="sxs-lookup"><span data-stu-id="1c7ae-153">Cutting Edge : Source Code Readability Tips</span></span>](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [<span data-ttu-id="1c7ae-154">Teams documentación</span><span class="sxs-lookup"><span data-stu-id="1c7ae-154">Teams documentation</span></span>](/microsoftteams/platform/overview)
* [<span data-ttu-id="1c7ae-155">GitHub</span><span class="sxs-lookup"><span data-stu-id="1c7ae-155">GitHub</span></span>](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a><span data-ttu-id="1c7ae-156">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1c7ae-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c7ae-157">Obtener actualizaciones de Microsoft Docs y los anuncios más recientes</span><span class="sxs-lookup"><span data-stu-id="1c7ae-157">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
