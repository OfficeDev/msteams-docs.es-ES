---
title: Contribuir a la documentación de Microsoft Teams
description: pasos para crear y publicar documentación de Teams
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a6742b8b994cc3752df923db75a3d7d77cbebd83
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019674"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Contribuir a la documentación de Microsoft Teams

[La documentación de Teams](/microsoftteams/platform/overview) forma parte de la biblioteca de documentación técnica de [Microsoft Docs.](https://docs.microsoft.com/) El contenido se organiza en grupos denominados docsets, cada uno que representa un grupo de documentos relacionados administrados como una sola entidad. Los artículos del mismo conjunto de documentos tienen la misma extensión de ruta de acceso url después *de docs <span></span> .microsoft.com*.  Por ejemplo,  `/docs.microsoft.com/microsoftteams/...`   es el principio de la ruta de acceso del archivo docset de Teams. Los artículos de Teams se escriben [en la sintaxis de MarkDown](#markdown-reference) y se hospedan en [GitHub.](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)

## <a name="set-up-your-workspace"></a>Configurar el área de trabajo

> [!div class="checklist"]
>
> * Instalar [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Instalar [Visual Studio (código](https://code.visualstudio.com/) VS).
> * Instalar [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde VS Code Marketplace
<br>&emsp;&emsp; o

> [!div class="checklist"]
>
> * Instalar desde vs code:

   1. Seleccione el **icono Extensiones** en la barra de actividad lateral o use el comando Ver = **> Extensiones** (Ctrl+Mayús+X) y busque *docs Authoring Pack* (Microsoft).
   1. Seleccione el **botón Instalar.**
   1. Una vez completada la instalación, **el botón Instalar** cambiará al botón **Administrar** engranaje.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Revisar la Guía de colaboradores de Microsoft Docs

La [guía de colaboradores](/contribute) ofrece instrucciones para crear, publicar y actualizar contenido técnico en la plataforma de Microsoft Docs. *Vea también*, [Estilo docs y inicio rápido de voz.](/contribute/style-quick-start)

## <a name="microsoft-writing-style-and-content-guides"></a>Guías de contenido, estilo y escritura de Microsoft

* **[Guía de estilo de Microsoft Writing](/style-guide/welcome)**. Considera la posibilidad de agregar esta guía en línea al menú **Favoritos del** explorador. Es un recurso completo para la escritura técnica actual y refleja el enfoque moderno de Microsoft para la voz y el estilo.

* **[Escritura de contenido para desarrolladores](/style-guide/developer-content/)**. El contenido específico de Teams está dirigido a una audiencia de desarrolladores con una comprensión fundamental de los conceptos y procesos de programación. Es importante que proporcione información clara y técnicamente precisa de una manera atractiva mientras mantiene el tono y el estilo de Microsoft.

* **[Escribir instrucciones paso a paso](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. Las experiencias aplicadas e interactivas son una excelente manera para que los desarrolladores aprendan sobre los productos y tecnologías de Microsoft. Presentar procedimientos complejos o simples en un formato progresivo es natural y fácil de usar.

## <a name="markdown-reference"></a>Referencia de MarkDown

 Las páginas de Microsoft Docs se escriben en la sintaxis de MarkDown y se analizan a través de un [motor Markdig.](https://github.com/lunet-io/markdig) Consulte *Docs* [Markdown reference for](/contribute/markdown-reference) specific tags and formatting conventions.

## <a name="file-paths"></a>Rutas de acceso a archivos

Establecer una ruta de acceso de archivo válida para hipervínculos en la documentación puede ser un desafío, especialmente cuando se usan rutas relativas y se crean vínculos a otros conjuntos de documentos.  La compilación no se completa correctamente en GitHub si la ruta de acceso del archivo es incorrecta o no es válida.

Para obtener más información sobre hipervínculos y rutas de acceso a archivos, *consulte* [Usar vínculos en la documentación](/contribute/how-to-write-links).

>[!IMPORTANT]
> Para hacer referencia a un artículo que *forma parte del* conjunto de documentos de la plataforma de Teams:<br>
> &emsp;&#x2714; use una ruta relativa sin una barra diagonal hacia delante.<br>
> &emsp;&#x2714; incluir la extensión de archivo Markdown.<br>
>Por ejemplo:  **directorio primario/directorio/ruta de acceso a article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Para hacer referencia a un artículo de biblioteca de Microsoft Docs que *no forma* parte del docset de la plataforma teams:<br>
> &emsp;&#x2714; use una ruta relativa que comience por una barra diagonal.<br>
> &emsp;&#x2714; No incluya la extensión de archivo. <br> Por ejemplo:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Para hacer referencia a una página fuera de la biblioteca de Microsoft Docs, como GitHub, use la ruta de `https` acceso de archivo completa.<br>

## <a name="code-samples-and-snippets"></a>Ejemplos de código y fragmentos de código

Los ejemplos de código desempeñan un papel importante al ayudar a los desarrolladores a usar correctamente API y SDK. Los ejemplos de código bien presentados pueden comunicar cómo funcionan las cosas más claramente que el texto descriptivo y la información de instrucciones solo. Los ejemplos de código deben ser precisos, concisos, bien documentados y, lo más importante, fáciles de usar para el lector. El código fácil de leer también es fácil de comprender, probar, depurar, mantener, modificar y extender. *Consulte* [How to include code in docs](/contribute/code-in-docs). Para obtener sugerencias de legibilidad, vea *también* [Cutting Edge : Source Code Readability Tips](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtener actualizaciones de Microsoft Docs y los anuncios más recientes](/teamblog)
