---
title: Contribuir a este contenido
description: Obtenga información sobre los pasos para crear y publicar documentación de Teams
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 5a9b2f16b23eaa4879062c104a85b223564cc10c
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806764"
---
# <a name="contribute-to-teams-documentation"></a>Contribuir a este contenido

La documentación de Teams forma parte de la biblioteca de documentación técnica **de Microsoft Docs**. El contenido se organiza en grupos denominados docsets, cada uno de los cuales representa un grupo de documentos relacionados administrados como una sola entidad. Los artículos del mismo conjunto de documentos tienen la misma extensión de ruta de acceso de dirección URL después de `learn.microsoft.com`. Por ejemplo, `/learn.microsoft.com/microsoftteams/...` es el principio de la ruta de acceso del archivo docset de Teams. Los artículos de Teams se escriben en la sintaxis de Markdown y se hospedan en GitHub.

## <a name="set-up-your-workspace"></a>Configurar el área de trabajo

> [!div class="checklist"]
>
> * Instale [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Instale [Microsoft Visual Studio](https://code.visualstudio.com/) (VS Code).
> * Instale [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directamente desde VS Code Marketplace.<br>&emsp;&emsp; o
[!div class="checklist"]
>
> * Instale dentro de VS Code:

   1. Seleccione el **icono Extensiones** en la barra de actividad lateral o use el comando **Ver => Extensiones** o Ctrl+Mayús+X y busque **Paquete de creación de Microsoft Docs**.
   1. Haga clic en **Instalar**.
   1. Después de la instalación, el botón **Instalar** cambia al botón de engranaje **Administrar**.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Revise la guía de colaboradores de Microsoft Docs

La guía de colaboradores proporciona instrucciones para crear, publicar y actualizar contenido técnico en la plataforma **Microsoft Docs**.

## <a name="microsoft-writing-style-and-content-guides"></a>Guías de escritura, estilo y contenido de Microsoft

* **[Guía de estilo de escritura de Microsoft](/style-guide/welcome)**: La guía de estilo de escritura de Microsoft es un recurso completo para la escritura técnica y refleja el enfoque moderno de Microsoft para la voz y el estilo. Para facilitar la referencia, agregue esta guía en línea al menú **Favoritos** de su navegador.

* **[Escritura de contenido para desarrolladores](/style-guide/developer-content/)**: el contenido específico de Teams está dirigido a un público desarrollador con una comprensión fundamental de los conceptos y procesos de programación. Es importante que proporcione información clara y técnicamente precisa de una manera atractiva mientras mantiene el tono y el estilo de Microsoft.

* **[Escribir instrucciones paso a paso](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: las experiencias aplicadas e interactivas son una excelente manera de que los desarrolladores obtengan información sobre los productos y las tecnologías de Microsoft. Presentar procedimientos complejos o simples en un formato progresivo es natural y fácil de usar.

## <a name="markdown-reference"></a>Referencia de MarkDown

Las páginas de **Microsoft Docs** se escriben en la sintaxis de **MarkDown** y se analizan a través de un motor de [Markdig](https://github.com/lunet-io/markdig). Para obtener más información sobre etiquetas específicas y convenciones de formato, consulte [Referencia de Docs Markdown](/contribute/markdown-reference).

## <a name="file-paths"></a>Rutas de acceso de archivo

Al usar rutas de acceso relativas y crear vínculos a otros conjuntos de documentos, es importante establecer una ruta de acceso de archivo válida para los hipervínculos de la documentación. La compilación se realiza correctamente en GitHub solo si la ruta de acceso del archivo es correcta o válida.

Para obtener más información sobre los hipervínculos y las rutas de acceso de archivo, consulte [usar vínculos en la documentación](/contribute/how-to-write-links).

> [!IMPORTANT]
> Para hacer referencia a un artículo que forma **parte del** conjunto de documentos de la plataforma Teams:<br>
> &emsp;&#x2714; Use una ruta de acceso relativa sin una barra diagonal inicial.<br>
> &emsp;&#x2714; Incluir la extensión de archivo Markdown.<br>
>Por ejemplo: **parent directory/directory/path-to-article.md** —> [Creación de una aplicación para Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Para hacer referencia a un artículo de biblioteca de Microsoft Docs que **no forma parte del** conjunto de documentos de la plataforma Teams:<br>
> &emsp;&#x2714; Use una ruta de acceso relativa que comience con una barra diagonal.<br>&emsp;&#x2714; No incluya la extensión de archivo.<br>
> Ejemplo:  **/docset/address-to-file-location** —> [Usar la API de Microsoft Graph para trabajar con Microsoft Teams](/graph/api/resources/teams-api-overview)<br><br>
> Para hacer referencia a una página fuera de la biblioteca de Microsoft Docs, como GitHub, use la ruta de acceso completa `https` del archivo.<br>

## <a name="code-samples-and-snippets"></a>Ejemplos de código y fragmentos de código

Los ejemplos de código desempeñan un papel importante para usar las API y los SDK de forma eficaz. Los ejemplos de código bien presentados pueden comunicar cómo funcionan las cosas de forma más clara que el texto descriptivo y la información descriptiva por sí solas. Los ejemplos de código deben ser precisos, concisos, bien documentados y fáciles de usar para el lector. El código que es fácil de leer debe ser fácil de entender, probar, depurar, mantener, modificar y ampliar. Para obtener más información, consulte [cómo incluir código en documentos](/contribute/code-in-docs).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtener actualizaciones de Microsoft Docs y los anuncios más recientes](/teamblog)

## <a name="see-also"></a>Consulte también

* [Microsoft Docs](/)
* [Guía de colaboradores](/contribute)
* [Inicio rápido de estilo y voz de Docs](/contribute/style-quick-start)
* [Vanguardia: sugerencias de legibilidad del código fuente](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Documentación de Teams](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
