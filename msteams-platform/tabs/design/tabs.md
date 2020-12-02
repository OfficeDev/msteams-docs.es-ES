---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de marco de trabajo de configuración ficha estática ficha de canal de diseño de ficha sencillo
ms.openlocfilehash: ad4d79608364cc2d37c5e02bd3c98a03deb886cf
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552552"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>Contenido y conversaciones, todos a la vez mediante pestañas

> [!Important]
> **Pestañas en clientes móviles**
>
> Siga las [instrucciones para las pestañas de dispositivos móviles](./tabs-mobile.md) al crear las pestañas. Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.
>
> **Pestañas de canal o grupo (configurable) en dispositivos móviles:**
>
> * Los clientes móviles solo muestran pestañas configurables que tienen un valor para `websiteUrl` . Si desea que la pestaña aparezca en los clientes móviles de Teams, debe establecer el valor de `websiteUrl` .
> * El comportamiento predeterminado de apertura en dispositivos móviles es abrir fuera del explorador con el `websiteUrl` . En el caso de las aplicaciones publicadas en la tienda de aplicaciones públicas, si desea que la ficha de canal se abra dentro de Teams de forma predeterminada, siga las [instrucciones para las pestañas de Mobile](~/tabs/design/tabs-mobile.md)y póngase en contacto con su representante de soporte técnico para que se le solicite que se le solicite que se le pida que

Las pestañas son lienzos que se pueden usar para compartir contenido, mantener conversaciones y hospedar servicios de terceros, todo ello dentro del flujo de trabajo ecológico de un equipo. Cuando se crea una pestaña en Microsoft Teams, se coloca la aplicación web en su lugar y en el centro a la que se puede acceder fácilmente desde las conversaciones clave.

## <a name="guidelines"></a>Instrucciones

Una buena pestaña debe mostrar las siguientes características:

### <a name="focused-functionality"></a>Funcionalidad centrada

Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica. Céntrese en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para el canal en el que se encuentra la pestaña.

### <a name="reduced-chrome"></a>Cromo reducido

Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña. Es decir, intente no tener pestañas en la pestaña.

### <a name="integration"></a>Integración

Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de [tarjetas adaptables](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) en una conversación.

### <a name="conversational"></a>Conversación

Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.

### <a name="streamlined-access"></a>Acceso simplificado

Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado. Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.

### <a name="responsiveness-to-window-sizing"></a>Capacidad de respuesta al tamaño de la ventana

Los equipos se pueden usar en tamaños de ventana tan pequeños como 720px, por lo que es importante asegurarse de que una pestaña se puede usar en una ventana pequeña tan importante como el uso de resoluciones muy altas.

### <a name="flat-navigation"></a>Navegación plana

Le pedimos a los desarrolladores que no agreguen todo su portal a una pestaña. Mantener la navegación relativamente plana ayuda a mantener un modelo de conversación más sencillo. En otras palabras, la conversación trata sobre una lista de cosas, como los elementos de trabajo clasificados o de un solo elemento, como una especificación.

Hay desafíos de navegación inherentes a la jerarquía de navegación profunda en conversaciones encadenadas. Para obtener la mejor experiencia del usuario, la navegación de la pestaña debe mantenerse al mínimo y diseñarse de la siguiente manera:

> [!div class="checklist"]
>
> * **Abre un módulo de tareas como una entidad o elemento de trabajo individual**. Esto excluye completamente el chat y es la mejor opción para mantener el chat específicamente sobre la ficha y no sobre las subentidades o la experiencia de edición.
>* **Abre un pseudo cuadro de diálogo en un iframe**. Si se usa con un fondo con pantalla, se recomienda usar el color más claro en lugar del oscuro. La `app-gray-10 at 30%` transparencia funciona bien.
>* **Abre una página del explorador**.

### <a name="personality"></a>Personalidad

El lienzo de pestañas ofrece una gran oportunidad para personalizar su experiencia. Su logotipo es una parte importante de su identidad y su conexión con los usuarios de, por lo que debe asegurarse de incluirlo:

> [!div class="checklist"]
>
>* Poner el logotipo en la esquina izquierda o derecha o a lo largo del borde inferior
> * Mantener el logotipo en pequeña y discreta

La incorporación de sus propios colores y diseños Twill también ayuda para comunicar la personalidad.

> [!TIP]
> Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams. *Consulte*, por ejemplo, [colores de Teams](../../concepts/design/components/color.md)

---

## <a name="tab-layouts"></a>Diseños de pestañas

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a>Tipos de pestañas

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a>Alto de página de configuración

>[!IMPORTANT]
>En septiembre de 2018, se incrementó el alto de la [Página de configuración](~/tabs/how-to/create-tab-pages/configuration-page.md) de pestañas mientras el ancho permaneció sin cambios. Si la aplicación está diseñada para el tamaño anterior, la página de configuración de pestañas tendrá una gran cantidad de espacio en blanco vertical. Las aplicaciones de la tienda heredadas exentas de este cambio tendrán que ponerse en contacto con Microsoft después de la actualización para acomodar las nuevas dimensiones.

Las dimensiones de la página de configuración de pestañas:


<img width="450px" title="Tamaños de las pestañas de configuración" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a>Instrucciones para el formato de página de configuración de pestañas

* Base el alto mínimo del área de contenido de la página de configuración de pestañas en elementos gráficos de altura fija.
* Calcula el espacio vertical disponible (el alto del área de contenido en la página de configuración) mediante `window.innerHeight` . Esto devuelve el tamaño del `<iframe>` en el que reside la página de configuración, lo que puede cambiar en futuras versiones. Al usar este valor, el contenido se ajustará automáticamente a los cambios futuros.
* Asigna espacio vertical a los elementos variable-height menos lo que se necesita para los elementos de altura fija.
* Para el estado de *Inicio de sesión* , centrar vertical y horizontalmente el contenido.
* Si desea una imagen de fondo, necesitará una nueva imagen, ajustada para ajustarse al área (recomendado) o puede conservar la misma imagen y elegir entre:
  * alineación a la esquina superior izquierda.
  * escalar la imagen para ajustarla.

Cuando esté correctamente ajustado, la página de configuración de pestaña debe tener un aspecto similar a este:

<img width="450px" title="Nueva pestaña Configuración" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="always-include-a-default-state"></a>Incluir siempre un estado predeterminado

Incluya un estado predeterminado para que las pestañas se puedan configurar fácilmente incluso si la pestaña se puede configurar.

### <a name="deep-linking"></a>Vinculación profunda

Siempre que sea posible, las tarjetas y los bots deben tener un vínculo profundo a datos enriquecidos en una pestaña hospedada. Por ejemplo, puede que una tarjeta muestre un resumen de los datos de los errores, pero al hacer clic en él se muestra el error completo en una pestaña.

### <a name="naming"></a>Poner

En muchos casos, el nombre de la aplicación tomará un nombre de pestaña excelente. Pero, también considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.

### <a name="multi-window"></a>Varias ventanas

Las pestañas de canal que tienen capacidades de edición complejas deben abrir la vista del editor en varias ventanas en lugar de en una pestaña.

### <a name="no-horizontal-scrolling"></a>Sin desplazamiento horizontal

La pestaña no debe tener desplazamiento horizontal.

### <a name="easy-navigation"></a>Navegación sencilla

La navegación dentro de una aplicación de pestaña debe ser fácil de seguir, es decir, las páginas tienen lo siguiente en caso necesario o aplicable:
* Botones atrás
* Encabezados de página
* Las rutas
* Menús de hamburguesa

### <a name="undo-last-action"></a>Deshacer la última acción

El usuario debe poder deshacer la última acción de la aplicación.

### <a name="share-content"></a>Compartir contenido

Las aplicaciones personales deben permitir a los usuarios compartir contenido de una experiencia de la aplicación personal con otros miembros del equipo. La ficha canal debe proporcionar navegación que complemente la navegación principal de los equipos, en lugar de entrar en conflicto con ella (por ejemplo, barras de navegación de carril izquierda).

### <a name="single-view"></a>Vista única

Las aplicaciones personales deben presentar contenido de instancias de ámbito de chat de equipo o grupo de esa aplicación en una sola vista, por ejemplo, un usuario de Trello debe poder ver todas las instancias de las placas de Trello en las que participan en el nivel de equipo en su aplicación personal.

### <a name="no-app-bar"></a>Sin barra de aplicaciones

Las pestañas no deben proporcionar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de los equipos.

### <a name="navigation"></a>Navegación

Las pestañas no deben tener más de 3 niveles de navegación dentro de la aplicación.

### <a name="l2l3-view"></a>Vista L2/L3

Las páginas secundarias y terciarias de una ficha deben abrirse en una vista L2/L3 en el área de la pestaña principal que se desplaza a través de la ruta de navegación.

### <a name="no-link-to-external-browser"></a>Sin vínculo al explorador externo

Los destinos de vínculo de las pestañas no deben vincularse a un explorador externo, pero deben vincularse a los elementos div incluidos en Teams. Por ejemplo, dentro de módulos de tareas, pestañas, etc.

## <a name="notifications-for-tabs"></a>Notificaciones para pestañas

Hay dos modos de notificación para cambios de contenido de pestañas:

> [!div class="checklist"]
>
> * **Use la API de aplicaciones para notificar a los usuarios los cambios**. Este mensaje se mostrará en la fuente de actividad del usuario y un vínculo profundo a la ficha. *consulte*  [Create deep links to Content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )

> * **Usar un bot**. Este método es preferible especialmente si el subproceso de la pestaña es de destino. El resultado será que la conversación encadenada de la pestaña se desplazará a la vista como activa recientemente. Este método también permite una sofisticación en el modo en que se envía la notificación.

El envío de un mensaje a un subproceso de tabulación aumenta la conciencia de la actividad a todos los usuarios sin notificar explícitamente a todos los usuarios. Se trata de un reconocimiento sin ruido. Además, cuando `@mention`  hay usuarios específicos, la misma notificación se colocará en la fuente, lo que hará que se vinculen directamente al hilo de la pestaña.

### <a name="tab-design-best-practices"></a>Procedimientos recomendados de diseño de pestañas

* Las pestañas personales/estáticas deben permitir a los usuarios compartir contenido de una experiencia de la aplicación personal con otros miembros del equipo.
* Las pestañas personales/estáticas pueden presentar contenido de instancias de ámbito de chat de equipo o grupo de esa aplicación en una sola vista.
* Los destinos de vínculo de las pestañas no deben vincularse a un explorador externo, sino que deben vincularse a los elementos div incluidos en Teams (ejemplo: en los módulos de tareas, pestañas, etc.).
* Las pestañas deben responder a los temas del equipo. Cuando se cambia el tema de Teams, el tema de la aplicación también debe cambiar para reflejar ese tema.
* Las pestañas deben usar componentes con estilo de equipo siempre que sea posible. Significa adoptar las fuentes de Microsoft Teams, las rampas de tipos, las paletas de colores, el sistema de cuadrícula, el movimiento, el tono de la voz, etc.
* Las pestañas deben usar los comportamientos de interacción de Microsoft Teams para la navegación en las páginas, la posición y el uso de cuadros de diálogo, jerarquías de información, etc.
* Las pestañas deben usar el menú hamburguesa de los equipos estándar o la ruta de navegación para la navegación en la aplicación. Las pestañas no deben proporcionar una barra de aplicaciones con iconos en el carril de la izquierda que entran en conflicto con la navegación principal de los equipos.
* Las pestañas no deben tener más de tres niveles de navegación dentro de la aplicación.
* Las páginas secundarias y terciarias de una ficha deben abrirse en una vista L2/L3 en el área de la pestaña principal que se desplaza a través de la ruta de navegación.
* Las pestañas que tienen capacidades de edición complejas en la aplicación deben abrir la vista del editor en varias ventanas en lugar de en una pestaña (para escritorio y Web).
* Para mejorar la experiencia del usuario se incluye un bot? a personal que envía un mensaje de bienvenida al usuario en el primer proceso y responde a los comandos **HI**, **Help** y **Hello** . Puede consultar la documentación de los [bots de conversación](../../bots/what-are-bots#in-a-one-to-one-chat) para obtener ayuda.
