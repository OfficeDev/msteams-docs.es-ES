---
title: Desarrollar extensiones de mensajería
description: Describe cómo empezar a usar extensiones de mensajería en Microsoft Teams
ms.topic: overview
keywords: extensiones de mensajería de teams
ms.openlocfilehash: 1eb75371b1a8adbeadbcbdbc0d06c7d88f2f1ccc
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696552"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Desarrollar extensiones de mensajería para Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Las extensiones de mensajería son una forma eficaz de que los usuarios puedan interactuar con la aplicación desde Microsoft Teams. Con esta funcionalidad, los usuarios pueden consultar o publicar información desde y hacia el servicio y publicar esa información, en forma de tarjetas, directamente en un mensaje.

![Ejemplo de tarjeta de extensión de mensajería](~/assets/images/compose-extensions/ceexample.png)

Las extensiones de mensajería aparecen en la parte inferior del cuadro de redacción. Algunos están integrados, como Emoji, Giphy y Sticker. Elige el **botón Más opciones** (**&#8943;**) para ver otras extensiones de mensajería, incluidas las que agregues desde la galería de aplicaciones o cargues tú mismo.

¿Cómo usaría las extensiones de mensajería? Estas son algunas posibilidades:

* Elementos de trabajo y errores
* Vales de soporte al cliente
* Gráficos e informes de uso
* Imágenes y contenido multimedia
* Oportunidades de ventas y clientes potenciales

## <a name="types-of-messaging-extensions"></a>Tipos de extensiones de mensajería

Hay principalmente dos tipos de extensiones de mensajería que puede crear para Teams hoy en día. Los siguientes temas le guiarán a través del proceso de creación:

* [Extensiones de mensajería basadas en búsquedas:](~/resources/messaging-extension-v3/search-extensions.md)consulte su servicio para obtener información e insertarla en un mensaje. Ejemplo: buscar un elemento de trabajo
* [Extensiones de mensajería basadas en acciones:](~/resources/messaging-extension-v3/create-extensions.md)recopilar información del usuario y publicarla en un servicio de terceros. Ejemplo: Crear un elemento de trabajo
