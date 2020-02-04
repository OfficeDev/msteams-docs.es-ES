---
title: Desarrollar extensiones de mensajería
description: Describe cómo empezar a trabajar con extensiones de mensajería en Microsoft Teams
keywords: extensiones de mensajería de extensiones de mensajería de Microsoft Teams
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675737"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Desarrollar extensiones de mensajería para Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensajería son una manera eficaz de que los usuarios participen con la aplicación de Microsoft Teams. Con esta capacidad, los usuarios pueden consultar o publicar información desde y hacia el servicio y publicar la información, en forma de tarjetas, directamente en un mensaje.

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

Las extensiones de mensajería aparecen a lo largo de la parte inferior del cuadro de redacción. Algunos están integrados, como Emoji, Giphy y adhesivo. Elija el botón **más opciones** (**&#8943;**) para ver otras extensiones de mensajería, incluidas las que se agregan desde la galería de aplicaciones o que se cargan.

¿Cómo usaría las extensiones de mensajería? Estas son algunas de las posibilidades:

* Elementos de trabajo y errores
* Vales de soporte al cliente
* Gráficos de uso e informes
* Imágenes y contenido multimedia
* Oportunidades y clientes potenciales de ventas

## <a name="types-of-messaging-extensions"></a>Tipos de extensiones de mensajería

Hay principalmente dos tipos de extensiones de mensajería que puede crear para Microsoft Teams en la actualidad. Los siguientes temas le guiarán por el proceso de creación:

* [Search based Messaging Extensions](~/resources/messaging-extension-v3/search-extensions.md): consultar el servicio para obtener información e insertarlo en un mensaje. Ejemplo: buscar un elemento de trabajo
* [Extensiones de mensajería basadas en acciones](~/resources/messaging-extension-v3/create-extensions.md): recopilan información del usuario y se publican en un servicio de terceros. Ejemplo: crear un elemento de trabajo
