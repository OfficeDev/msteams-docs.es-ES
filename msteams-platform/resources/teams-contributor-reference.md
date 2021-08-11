---
title: Contribuir a este contenido
description: pasos para crear y publicar Teams documentación
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: d09f946926f7377b65910c7bccce7cef8e30ef739afa31b94c83354cffbd7c27
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708059"
---
# <a name="contribute-to-teams-documentation"></a>Contribuir a este contenido

Teams documentación forma parte de la biblioteca de documentación técnica de **Microsoft Docs.** El contenido se organiza en grupos denominados docsets, cada uno que representa un grupo de documentos relacionados administrados como una sola entidad. Los artículos del mismo conjunto de documentos tienen la misma extensión de ruta de acceso url después **de docs.microsoft.com**. Por ejemplo, `/docs.microsoft.com/microsoftteams/...` es el principio de la ruta Teams de archivo docset. Teams artículos se escriben en la sintaxis de Markdown y se hospedan en GitHub.

## <a name="set-up-your-workspace"></a>Configurar el área de trabajo

> [!div class="checklist"]
>
> * Instalar [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Instalar [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Instale [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde VS Code Marketplace.
<br>&emsp;&emsp; o

> [!div class="checklist"]
>
> * Instalar en VS Code:

   1. Seleccione el **icono Extensiones** en la barra de actividad lateral o use el comando Ver = **> Extensiones** o Ctrl+Mayús+X y busque **Microsoft Docs Authoring Pack**.
   1. Seleccione **Instalar**.
   1. Después de la instalación, **el botón Instalar** cambia al botón **Administrar** engranaje.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Revisar la Guía de colaboradores de Microsoft Docs

La guía de colaboradores proporciona instrucciones para crear, publicar y actualizar contenido técnico en la **plataforma de Microsoft Docs.** 

## <a name="microsoft-writing-style-and-content-guides"></a>Guías de contenido, estilo y escritura de Microsoft

* **[Microsoft Writing Style Guide:](/style-guide/welcome)** Microsoft Writing Style Guide es un recurso completo para la escritura técnica y refleja el enfoque moderno de Microsoft para la voz y el estilo. Para obtener una referencia sencilla, agregue esta guía en línea al menú **Favoritos del** explorador.

* **[Escribir contenido para](/style-guide/developer-content/)** desarrolladores: Teams contenido específico está dirigido a una audiencia de desarrolladores con una comprensión fundamental de los conceptos y procesos de programación. Es importante que proporcione información clara y técnicamente precisa de una manera atractiva mientras mantiene el tono y el estilo de Microsoft.

* **[Escribir instrucciones paso a paso:](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Las experiencias aplicadas e interactivas son una excelente manera para que los desarrolladores aprendan sobre los productos y tecnologías de Microsoft. Presentar procedimientos complejos o simples en un formato progresivo es natural y fácil de usar.

## <a name="markdown-reference"></a>Referencia de MarkDown

**Las páginas de Microsoft Docs** se escriben en **la sintaxis de MarkDown** y se analizan a través de un [motor Markdig.](https://github.com/lunet-io/markdig) Para obtener más información sobre etiquetas específicas y convenciones de formato, vea [Docs Markdown reference](/contribute/markdown-reference).

## <a name="file-paths"></a>Rutas de acceso a archivos

Al usar rutas de acceso relativas y crear vínculos a otros conjuntos de documentos, es importante establecer una ruta de acceso de archivo válida para hipervínculos en la documentación. La compilación se ejecuta GitHub solo si la ruta de acceso del archivo es correcta o válida.
 
Para obtener más información sobre hipervínculos y rutas de acceso a archivos, [vea usar vínculos en la documentación](/contribute/how-to-write-links).

> [!IMPORTANT]
> Para hacer referencia a un artículo que **forma parte del** docset Teams plataforma:<br>
> &emsp;&#x2714; use una ruta relativa sin una barra diagonal hacia delante.<br>
> &emsp;&#x2714; incluir la extensión de archivo Markdown.<br>
>Por ejemplo: **directorio primario/directorio/ruta de** acceso a article.md :> [Crear una aplicación para Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Para hacer referencia a un artículo de biblioteca de Microsoft Docs que **no forma** parte del Teams docset de la plataforma:<br>
> &emsp;&#x2714; use una ruta relativa que comience por una barra diagonal.<br>
> &emsp;&#x2714; No incluya la extensión de archivo. <br> Ex: **/docset/address-to-file-location** —> [Use la API](/graph/api/resources/teams-api-overview) de Microsoft Graph para trabajar con Microsoft Teams<br><br>
> Para hacer referencia a una página fuera de la biblioteca de Microsoft Docs, como GitHub, use la ruta de `https` acceso de archivo completa.<br>

## <a name="code-samples-and-snippets"></a>Ejemplos de código y fragmentos de código

Los ejemplos de código desempeñan un papel importante para usar api y SDK de forma eficaz. Los ejemplos de código bien presentados pueden comunicar cómo funcionan las cosas más claramente que el texto descriptivo y la información de instrucciones solo. Los ejemplos de código deben ser precisos, concisos, bien documentados y fáciles de usar para el lector. El código fácil de leer debe ser fácil de comprender, probar, depurar, mantener, modificar y extender. Para obtener más información, [vea cómo incluir código en los documentos](/contribute/code-in-docs).

## <a name="see-also"></a>Vea también

* [Microsoft Docs](/)
* [guía de colaboradores](/contribute)
* [Inicio rápido de voz y estilo de documentos](/contribute/style-quick-start)
* [Cutting Edge : Source Code Readability Sugerencias](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams documentación](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtener actualizaciones de Microsoft Docs y los anuncios más recientes](/teamblog)
