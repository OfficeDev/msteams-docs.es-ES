---
title: Referencia de directrices de diseño
description: Describe las instrucciones para diseñar una aplicación personal
keywords: guías de diseño de Microsoft Teams referencia de aplicaciones personales
ms.openlocfilehash: 6a07b618d78a3ad79850713052c88ef178c1ecc1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675783"
---
# <a name="personal-apps"></a>Aplicaciones personales

> [!Important]
> Pronto estará disponible la compatibilidad completa con las pestañas de los clientes móviles. Para prepararse para este cambio, debe seguir las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas. Las aplicaciones personales (pestañas estáticas) están disponibles actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).
>
> Cuando se publica la compatibilidad completa de pestañas:
>
> * Todas las pestañas estarán siempre disponibles en dispositivos móviles
> * El `contentUrl` **se cargará en el cliente móvil de Microsoft Teams**.
> * En las pestañas canal/grupo, los usuarios pueden abrir la pestaña en un explorador independiente `websiteUrl`a través de `contentUrl` la, pero se cargará primero.

Una aplicación personal es una aplicación con un ámbito personal. Como desarrollador de aplicaciones, tiene la opción de proporcionar una versión de la aplicación que se crea para el usuario individual. En esta versión, la colección de pestañas (y el bot, si ha incluido uno), están diseñados para la persona. De este modo, podrá crear una interacción de uno en uno con los usuarios.

Una aplicación personal es donde alguien puede ver todo lo que es y todos los elementos que ha visto recientemente en la aplicación. Coloca todo en un solo punto. En la siguiente captura de pantalla, contoso es una aplicación personal en el flotante de la aplicación personal.

![imagen del menú de desbordamiento de la aplicación](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a>Instrucciones

Una aplicación personal suele contener las siguientes pestañas:

### <a name="your-tab"></a>La pestaña

Aquí es donde los usuarios verán todo su contenido. Su espacio personal. La pestaña se puede organizar como una lista, una cuadrícula, columnas o un solo lienzo... lo que mejor se adapte a su aplicación. Para obtener más información sobre el diseño de pestañas efectivas, vea: [diseño de pestañas (~/Tabs/Design/Tabs.MD).

Como esta pestaña puede mostrar elementos de varios canales, cada elemento debería mostrar su propio equipo, canal y pestaña para que el usuario pueda ver fácilmente dónde se originó.

![Ficha tareas personales](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a>Posterior

La pestaña **reciente** permite a un usuario examinar todo lo que haya visto recientemente en la aplicación. Aparece en orden cronológico (de mayor a menos reciente). Al hacer clic en un elemento de esta lista, se desplazará al usuario hasta el canal y la ficha del elemento.

![Pestaña reciente](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a>Todo

Esta es una lista de todas las pestañas de la organización de la persona (a las que tienen acceso, en cualquier caso). Es decir, los muestra en todas partes donde se usa la aplicación. Como en la ficha **reciente** , al seleccionar un elemento de la lista, el usuario pasa directamente al canal y a la ficha correspondientes.

### <a name="bot"></a>Bot

Un bot no es necesario, pero es una buena forma de comunicarse directa y privadamente con los usuarios. La notificación es una de las funciones más importantes de una aplicación personal y la mejor forma de notificarla que con la comunicación directa.

Los bots entregan mensajes en forma de tarjetas, que pueden proporcionar información específica (por ejemplo, una alerta de que el contenido nuevo está disponible) o actualizaciones amplias (como una lista de tareas pendientes diaria). Para obtener más información sobre el diseño de bots efectivos, consulte: [diseño de Bot (~/bots/Design/bots.MD).

![Saludo de bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a>Ayuda y configuración

El contenido de la ayuda permite a los usuarios descubrir los matices de la aplicación. Agregue una pestaña de **configuración** para darles la capacidad de personalizarla.

### <a name="about"></a>Acerca de

Incluya una ficha **acerca** de para proporcionar información como el número de versión, las capacidades, la privacidad y los vínculos de permisos.

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="communicate-directly-with-your-users"></a>Comunicarse directamente con los usuarios

Usar un bot para notificar a los usuarios los cambios y las nuevas características.

### <a name="customize-your-tabs"></a>Personalice sus pestañas...

No dude en agregar otras pestañas que ayuden a los usuarios a realizar tareas específicas.

### <a name="and-make-them-relevant-to-every-user"></a>... y hacer que sean relevantes para todos los usuarios

Cada pestaña que declare en el manifiesto de la aplicación será visible para todos los usuarios. Por ejemplo, si la aplicación personal es una herramienta de informes de gastos que usan tanto los administradores como los empleados, una ficha de **aprobación** debe proporcionar contenido que sea significativo para ambas funciones.
