---
title: Desarrollo de extensiones de mensaje
description: Describe cómo empezar a trabajar con extensiones de mensaje en Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: extensiones de mensajería de teams extensiones de mensajería
ms.openlocfilehash: 8d44ea8ffe3c265a5c65ae2e842fe4f55f950e58
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111923"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>Desarrollo de extensiones de mensajes para Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensaje son una manera eficaz de que los usuarios interactúen con la aplicación desde Microsoft Teams. Con esta funcionalidad, los usuarios pueden consultar o publicar información hacia y desde el servicio y publicar esa información, en forma de tarjetas, directamente en un mensaje.

![Ejemplo de tarjeta de extensión de mensaje](~/assets/images/compose-extensions/ceexample.png)

Las extensiones de mensaje aparecen en la parte inferior del cuadro de redacción. Algunos están integrados, como Emoji, Giphy y Sticker. Elija el botón **Más opciones** (**&#8943;**) para ver otras extensiones de mensaje, incluidas las que agregue desde la galería de aplicaciones o cargue usted mismo.

¿Cómo usaría las extensiones de mensaje? Estas son algunas posibilidades:

* Elementos de trabajo y errores
* Incidencias de soporte técnico al cliente
* Gráficos e informes de uso
* Imágenes y contenido multimedia
* Oportunidades de ventas y clientes potenciales

## <a name="types-of-message-extensions"></a>Tipos de extensiones de mensaje

Hay principalmente dos tipos de extensiones de mensaje que puede crear para Teams hoy en día. Los temas siguientes le guiarán a través del proceso de creación de ellos:

* [Extensiones de mensaje basadas en búsquedas](~/resources/messaging-extension-v3/search-extensions.md): consulte el servicio para obtener información e insértelo en un mensaje. Ejemplo: Búsqueda de un elemento de trabajo
* [Extensiones de mensajes basadas en acciones](~/resources/messaging-extension-v3/create-extensions.md): recopile información del usuario y publique en un servicio de terceros. Ejemplo: Creación de un elemento de trabajo
