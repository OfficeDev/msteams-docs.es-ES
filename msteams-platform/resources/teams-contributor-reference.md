---
title: Contribuir a la documentación de Microsoft Teams
description: pasos para crear y publicar la documentación de Microsoft Teams
author: laujan
ms.author: lajanuar
ms.topic: contributor-guide
ms.openlocfilehash: 80aaf7795a226c0437140fe72e1d74b07fa66775
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995019"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Contribuir a la documentación de Microsoft Teams

La [documentación de Teams](/microsoftteams/platform/overview) forma parte de la biblioteca de documentación técnica de [Microsoft docs](https://docs.microsoft.com/) . El contenido se organiza en grupos denominados docsets, cada uno de los cuales representa un grupo de documentos relacionados que se administran como una entidad única. Los artículos de la misma docset tienen la misma extensión de ruta de dirección URL después de *docs <span></span> . Microsoft.com*.  Por ejemplo,  `/docs.microsoft.com/microsoftteams/...`   es el comienzo de la ruta de acceso del archivo docset de Teams. Los artículos de Microsoft Teams se escriben en la sintaxis de  [MarkDown](#markdown-reference) y se hospedan en [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Configurar el área de trabajo

> [!div class="checklist"]
>
> * Instale [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Instale [Visual Studio Code](https://code.visualstudio.com/) (vs Code).
> * Instalar el [paquete de creación de documentos](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde el Marketplace de código vs
<br>&emsp;&emsp; o

> [!div class="checklist"]
>
> * Instalar desde VS Code:

   1. Seleccione el **icono extensiones** en la barra de actividad lateral o use el comando **View => Extensions** (Ctrl + Mayús + X) y busque el *paquete de creación de documentos* (Microsoft).
   1. Seleccione el botón **instalar** .
   1. Una vez completada la instalación, el botón **instalar** cambiará al botón **administrar** engranaje.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Revisión de la guía de colaboradores de Microsoft docs

La [Guía de colaboradores](/contribute) ofrece dirección para crear, publicar y actualizar contenido técnico en Microsoft/docs. *Consulte también* , [estilo docs y inicio rápido de voz](/contribute/style-quick-start) .

## <a name="microsoft-writing-style-and-content-guides"></a>Guías de escritura, estilo y contenido de Microsoft

* **[Guía de estilo de escritura de Microsoft](/style-guide/welcome)**. Considere la posibilidad de agregar esta guía en línea al menú **Favoritos** de su explorador. Es un recurso exhaustivo para la escritura técnica actual y refleja el enfoque moderno de Microsoft hacia voz y estilo.

* **[Escribir contenido para programadores](/style-guide/developer-content/)**. El contenido específico de Microsoft Teams está dirigido a un público de programadores con una comprensión fundamental de los conceptos y procesos de programación. Es importante que proporcione información clara y técnicamente precisa de manera convincente a la vez que mantiene el tono y el estilo de Microsoft.

* **[Escribir instrucciones paso a paso](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. Las experiencias interactivas y aplicadas son una buena forma de que los programadores obtengan información sobre los productos y tecnologías de Microsoft. Presentar procedimientos complejos o sencillos en un formato progresivo es natural y fácil de tener al usuario.

## <a name="markdown-reference"></a>Referencia de MarkDown

 Las páginas de Microsoft docs se escriben en la sintaxis de MarkDown y se analizan a través de un motor de [Markdig](https://github.com/lunet-io/markdig) . *Vea* la [referencia de docs Markdown](/contribute/markdown-reference) para obtener etiquetas específicas y convenciones de formato.

## <a name="file-paths"></a>Rutas de archivo

Establecer una ruta de acceso de archivo válida para los hipervínculos en la documentación puede ser un reto, especialmente cuando se usan rutas relativas y se crean vínculos a otros docsets.  La compilación no tendrá éxito en GitHub si la ruta de acceso del archivo es incorrecta o no es válida.

Para obtener más información acerca de los hipervínculos y las rutas de archivo, *vea* [usar vínculos en la documentación](/contribute/how-to-write-links).

>[!IMPORTANT]
> Para hacer referencia a un artículo que forma *parte de* la plataforma de Teams docset:<br>
> &emsp;&#x2714; usar una ruta de acceso relativa sin una barra diagonal inicial.<br>
> &emsp;&#x2714; incluir la extensión de archivo de Markdown.<br>
>Por ejemplo:  **directorio principal/directorio/ruta de acceso-a-article. MD** : > `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Para hacer referencia a un artículo de la biblioteca de Microsoft docs ( <https://docs.microsoft.com/> ) que *no forma parte de* la plataforma de Teams docset:<br>
> &emsp;&#x2714; usar una ruta de acceso relativa que comience con una barra diagonal.<br>
> &emsp;&#x2714; no incluya la extensión de archivo. <br> Por ejemplo:  **/docset/Address-to-file-Location** : > `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`
>

## <a name="code-samples-and-snippets"></a>Ejemplos de código y fragmentos de código

Los ejemplos de código desempeñan un papel importante en ayudar a los desarrolladores a usar las API y los SDK correctamente. Los ejemplos de código bien presentados pueden comunicar cómo las cosas funcionan con más claridad que el texto descriptivo y la información de las instrucciones sola. Las muestras de código deben ser precisas, concisas y bien documentadas, y, lo que es más importante, fácil de usar para los lectores. El código que es fácil de leer también es fácil de entender, probar, depurar, mantener, modificar y extender. *Vea* [Cómo incluir código en documentos](/contribute/code-in-docs). Para obtener sugerencias de legibilidad, *Consulte también* [Cutting Edge: sugerencias de legibilidad de código fuente](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtener actualizaciones de Microsoft docs y los últimos anuncios](/teamblog)
