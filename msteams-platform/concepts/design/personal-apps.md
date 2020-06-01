---
title: Referencia de directrices de diseño
description: Describe las instrucciones para diseñar una aplicación personal
keywords: guías de diseño de Microsoft Teams referencia de aplicaciones personales
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455502"
---
# <a name="personal-apps"></a>Aplicaciones personales

> [!NOTE]
> Teams admite completamente la compatibilidad con las pestañas de los clientes móviles. Debe seguir las [instrucciones para las pestañas de dispositivos móviles](../../tabs/design/tabs-mobile.md) al crear pestañas para plataformas móviles.

Una aplicación personal es una aplicación de Microsoft Teams con un ámbito personal.  Como desarrollador de aplicaciones, tiene la opción de proporcionar una versión de la aplicación que se Centre en las interacciones con un único usuario. Puede ser un [Bot de conversación](../../bots/what-are-bots.md) para participar en conversaciones de uno a uno con un usuario o con una [pestaña personal](../../tabs/what-are-tabs.md) que proporciona una experiencia Web integrada. Las aplicaciones personales permiten a los usuarios ver su contenido seleccionado en un solo punto. En la siguiente captura de pantalla, contoso es una aplicación personal en el flotante de la aplicación personal.

![imagen del menú de desbordamiento de la aplicación](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a>Instrucciones

Una aplicación personal suele contener las siguientes pestañas:

### <a name="your-tab"></a>La pestaña

Aquí es donde los usuarios verán todo su contenido. Su espacio personal. La pestaña se puede organizar como una lista, una cuadrícula, columnas o un solo lienzo... lo que mejor se adapte a su aplicación. Para obtener más información sobre el diseño de pestañas efectivas, vea: [diseño de pestañas](../../tabs/design/tabs.md).

Como esta pestaña puede mostrar elementos de varios canales, cada elemento debería mostrar su propio equipo, canal y pestaña para que el usuario pueda ver fácilmente dónde se originó.

![Ficha tareas personales](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a>Posterior

La pestaña **reciente** permite a un usuario examinar todo lo que haya visto recientemente en la aplicación. Aparece en orden cronológico (de mayor a menos reciente). Al hacer clic en un elemento de esta lista, se desplazará al usuario hasta el canal y la ficha del elemento.

![Pestaña reciente](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a>Todo

Esta es una lista de todas las pestañas de la organización de la persona (a las que tienen acceso, en cualquier caso). Es decir, los muestra en todas partes donde se usa la aplicación. Como en la ficha **reciente** , al seleccionar un elemento de la lista, el usuario pasa directamente al canal y a la ficha correspondientes.

### <a name="bot"></a>Bot

Un bot no es necesario, pero es una buena forma de comunicarse directa y privadamente con los usuarios. La notificación es una de las funciones más importantes de una aplicación personal y la mejor forma de notificarla que con la comunicación directa.

Los bots entregan mensajes en forma de tarjetas, que pueden proporcionar información específica (por ejemplo, una alerta de que el contenido nuevo está disponible) o actualizaciones amplias (como una lista de tareas pendientes diaria). Para obtener más información sobre el diseño de bots efectivos, vea: [diseño de bot](../../bots/design/bots.md).

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
