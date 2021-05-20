---
title: Contribuir a Microsoft Teams documentación
description: pasos para crear y publicar documentación Teams
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: 52253bb096857e2cb883295c8ae6b58518506d9a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566232"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Contribuir a Microsoft Teams documentación

[Teams documentación](/microsoftteams/platform/overview) forma parte de la biblioteca de documentación técnica de [Microsoft Docs.](https://docs.microsoft.com/) El contenido se organiza en grupos denominados docsets, cada uno representando un grupo de documentos relacionados administrados como una sola entidad. Los artículos del mismo conjunto de documentos tienen la misma extensión de ruta de acceso de URL después *de docs <span></span> .microsoft.com*.  Por ejemplo, `/docs.microsoft.com/microsoftteams/...` es el principio de la ruta de acceso del archivo docset Teams. Teams artículos se escriben en la sintaxis [MarkDown](#markdown-reference) y se hospedan en [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Configure el espacio de trabajo

> [!div class="checklist"]
>
> * Instalar [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Instale [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Instale [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde el marketplace de VS Code.
<br>&emsp;&emsp; o

> [!div class="checklist"]
>
> * Instalar desde dentro de VS Code:

   1. Seleccione el **icono Extensiones** en la barra de actividades lateral o utilice el comando Ver = **extensiones>** (Ctrl+Mayús+X) y busque el Paquete de creación *de documentos* (Microsoft).
   1. Seleccione el botón **Instalar.**
   1. Una vez completada la instalación, el botón **Instalar** cambiará al botón **Administrar** engranaje.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Revise la Guía de colaboradores de Microsoft Docs

La [guía de colaboradores](/contribute) ofrece instrucciones para crear, publicar y actualizar contenido técnico en la plataforma Microsoft Docs.

## <a name="microsoft-writing-style-and-content-guides"></a>Guías de escritura, estilo y contenido de Microsoft

* **[Guía de estilo de escritura de Microsoft](/style-guide/welcome)**. Considere la posibilidad de agregar esta guía en línea al menú **Favoritos** de su navegador. Es un recurso integral para la escritura técnica actual y refleja el enfoque moderno de Microsoft hacia la voz y el estilo.

* **[Escribir contenido para desarrolladores.](/style-guide/developer-content/)** Teams contenido específico está dirigido a un público desarrollador con una comprensión fundamental de los conceptos y procesos de programación. Es importante que proporcione información clara y técnicamente precisa de una manera convincente mientras mantiene el tono y el estilo de Microsoft.

* **[Escribir instrucciones paso a paso.](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Las experiencias aplicadas e interactivas son una excelente manera para que los desarrolladores aprendan sobre los productos y tecnologías de Microsoft. Presentar procedimientos complejos o sencillos en un formato progresivo es natural y fácil de usar.

## <a name="markdown-reference"></a>Referencia de MarkDown

 Las páginas de Microsoft Docs se escriben en la sintaxis MarkDown y se analizan a través de un motor [Markdig.](https://github.com/lunet-io/markdig) Consulte *Referencia* [de Docs Markdown](/contribute/markdown-reference) para etiquetas específicas y convenciones de formato.

## <a name="file-paths"></a>Rutas de archivo

Establecer una ruta de acceso de archivo válida para hipervínculos en la documentación puede ser un desafío, especialmente cuando se usan rutas relativas y se crean vínculos a otros conjuntos de documentos.  La compilación no se realizará correctamente en GitHub si la ruta de acceso del archivo es incorrecta o no válida.

Para obtener más información sobre hipervínculos y rutas de archivo, consulte [Usar vínculos en la documentación](/contribute/how-to-write-links).

>[!IMPORTANT]
> Para hacer referencia a un artículo que forma *parte del* conjunto de documentos de la plataforma Teams:<br>
> &emsp;&#x2714; Utilice una ruta relativa sin una barra diagonal inicial.<br>
> &emsp;&#x2714; Incluir la extensión de archivo Markdown.<br>
>Por ejemplo:  **directorio principal/directorio/ruta de acceso a article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Para hacer referencia a un artículo de biblioteca de Microsoft Docs que *no forma parte del* conjunto de documentos de plataforma Teams:<br>
> &emsp;&#x2714; Utilice una ruta relativa que comience con una barra diagonal.<br>
> &emsp;&#x2714; No incluya la extensión de archivo. <br> Por ejemplo:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Para hacer referencia a una página fuera de la biblioteca de Microsoft Docs, como GitHub, use la ruta de acceso completa del `https` archivo.<br>

## <a name="code-samples-and-snippets"></a>Muestras de código y fragmentos de código

Los ejemplos de código desempeñan un papel importante para ayudar a los desarrolladores a usar correctamente API y SDK. Las muestras de código bien presentadas pueden comunicar cómo funcionan las cosas con mayor claridad que el texto descriptivo y la información instructiva por sí solas. Sus muestras de código deben ser precisas, concisas, bien documentadas y, lo más importante, amigables con los lectores. El código que es fácil de leer también es fácil de entender, probar, depurar, mantener, modificar y ampliar. Para obtener más información, consulte [Cómo incluir código en documentos](/contribute/code-in-docs).

## <a name="see-also"></a>Vea también

* [Estilo docs y inicio rápido de voz](/contribute/style-quick-start)
* [Vanguardia : Legibilidad del código fuente Sugerencias](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtenga actualizaciones de Microsoft Docs y los últimos anuncios](/teamblog)
