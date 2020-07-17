---
title: Directrices de diseño para las extensiones de mensajería
description: Describe las instrucciones para crear extensiones de mensajería.
keywords: Directrices de diseño de Microsoft Teams referencia sugerencias de extensiones de mensajería procedimientos recomendados
author: EmilyyC
ms.author: qinch
ms.openlocfilehash: 5d62646c5757f93cc4f6ae6e089ef3a0918f9eea
ms.sourcegitcommit: 81ac2a1070d16e20ae0e4cb6137dce09b31914af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "45152689"
---
# <a name="start-sharing-with-powerful-messaging-extensions"></a>Empezar a compartir con eficaces extensiones de mensajería

Las extensiones de mensajería están diseñadas para compartir contenido accionable. Esta característica representa el mayor retorno de la inversión (ROI) de nuestra pila. Las extensiones de mensajería funcionan en chats y canales, admiten varios extremos de consulta, permiten la creación de nuevas entidades y trabajan con el vínculo unfurling para crear vistas previas de vínculos personalizadas. El reto es que aunque la característica es muy útil y eficaz, no es fácil de detectar. Esta guía le ayudará a crear extensiones de mensajería que más usuarios encuentren y utilicen fácilmente.

## <a name="design-guidelines"></a>Directrices de diseño

### <a name="show-content-as-a-user-type"></a>Mostrar contenido como tipo de usuario

Las extensiones de mensajería presentan una forma única de usar las búsquedas de palabras clave para encontrar contenido accionable que pueda compartirse con uno o varios usuarios. Esta interacción preferida permite a los usuarios escribir términos de búsqueda con una consulta automática aplazada como el tipo de usuario. Este modelo hace un buen trabajo simulando los resultados sugeridos y requiere que los usuarios escriban caracteres mínimos.

> [!TIP]
>Es posible, pero no deseable, requerir que los usuarios seleccionen `enter` o `search` antes de enviar consultas. Aunque hay menos estrés en el servicio back-end, este modelo no es la norma y puede confundir a los usuarios.

### <a name="consider-zero-term-queries"></a>Considere las consultas a cero términos

Las consultas de cero términos se desencadenan directamente por acción del usuario, en lugar de por los términos de escritura del usuario en un cuadro de búsqueda. Todas las extensiones de mensajería se benefician de las consultas a cero, normalmente basadas en lo que el usuario vio por última vez en el servicio. La ventaja es que la probabilidad de que sea conveniente compartir algo que el usuario vio por última vez es bastante alta. Otras consultas a cero términos podrían estar basadas en el servicio. Por ejemplo, `news` es posible que muestre extensiones de noticias publicadas recientemente de eventos recientes y próximos.

<img width="450px" title="Nueva pestaña Configuración" src="../../assets/images/messaging-extension/zero-term-query.png" />

### <a name="include-link-unfurling"></a>Incluir unfurling de vínculo

Una de las formas más comunes de compartir contenido en Microsoft Teams es a través de un hipervínculo, ya sea una tarea en la que ha estado trabajando o un vídeo que ha encontrado divertido. Cuando un usuario comparte un vínculo en Microsoft Teams, se muestra una vista previa que incluye la imagen, el título o la descripción. Con [unfurling de vínculo](../how-to/link-unfurling.md) ahora puede personalizar estas vistas previas. También se les pedirá a los usuarios que instalen la aplicación después de que decidan usar la vista previa. La adición de funcionalidad de unfurling de vínculos a la aplicación puede aumentar enormemente la capacidad de detección de la aplicación.

### <a name="highlight-your-messaging-extension"></a>Resaltar la extensión de mensajería

Las extensiones de mensajería no siempre son fáciles de encontrar. Incluya capturas de pantalla de aplicaciones en la página de detalles de la aplicación y la documentación de ayuda para obtener una extensión de mensajería. También puede incluir documentación *sobre procedimientos* para la extensión de mensajería en las visitas de bot para resaltar toda la aplicación más allá de las interacciones de bot.

### <a name="add-actions-on-card"></a>Agregar acciones a la tarjeta

No solo mostrar texto a los usuarios. Tener algo con los que puede interactuar y realizar la siguiente acción. Por ejemplo, la aplicación de sitios no sólo inserta un mapa en la tarjeta, sino que también tiene un botón que, cuando se selecciona, muestra las direcciones a la ubicación. Los usuarios pueden realizar más tareas después de obtener la tarjeta.

<img width="450px" title="Nueva pestaña Configuración" src="../../assets/images/messaging-extension/action-on-card.png" />

### <a name="keep-users-in-the-app-context"></a>Mantener a los usuarios en el contexto de la aplicación

Si una tarjeta no es suficiente y necesita proporcionar un vínculo para obtener más información, considere la posibilidad de abrir una pestaña en lugar de abrir un explorador para mejorar la experiencia del usuario. *Consulte* [extender la aplicación Teams con una pestaña personalizada](../../tabs/how-to/add-tab.md)
