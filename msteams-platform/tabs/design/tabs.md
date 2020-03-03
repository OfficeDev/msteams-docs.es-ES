---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de las fichas de marco de trabajo
ms.openlocfilehash: c718dd897d314ecb5acfbb7cc537b8eead142b0c
ms.sourcegitcommit: 646a8224523be7db96f9686e22d420d62d55d4b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "42365265"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>Contenido y conversaciones, todos a la vez mediante pestañas

> [!Important]
> **Pestañas en clientes móviles**
>
> Siga las [instrucciones para las pestañas de dispositivos móviles](./tabs-mobile.md) al crear las pestañas. Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.
>
> **Pestañas personales (estáticas) en dispositivos móviles:**
>
> * Las pestañas estáticas (aplicación personal) están disponibles en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md).
> * Mientras crea las pestañas estáticas, asegúrese de seguir las [instrucciones para las pestañas de la móvil](~/tabs/design/tabs-mobile.md)
>
> **Pestañas de canal o grupo (configurable) en dispositivos móviles:**
>
> * Los clientes móviles solo muestran las pestañas que tienen `websiteUrl`un valor para. Si desea que la pestaña aparezca en los clientes móviles de Teams, debe establecer el valor de `websiteUrl`.
> * El comportamiento predeterminado de apertura en dispositivos móviles es abrir fuera del explorador `websiteUrl`con el. En el caso de las aplicaciones publicadas en la tienda de aplicaciones públicas, si desea que la ficha de canal se abra dentro de Teams de forma predeterminada, siga las [instrucciones para las pestañas de Mobile](~/tabs/design/tabs-mobile.md)y póngase en contacto con su representante de soporte técnico para que se le solicite que se le solicite que se le pida que

Las pestañas son lienzos que se pueden usar para compartir contenido, mantener conversaciones y hospedar servicios de terceros, todo ello dentro del flujo de trabajo ecológico de un equipo. Cuando se crea una pestaña en Microsoft Teams, se coloca la aplicación web en su lugar y en el centro a la que se puede acceder fácilmente desde las conversaciones clave.

## <a name="guidelines"></a>Instrucciones

Una buena pestaña debe mostrar las siguientes características:

### <a name="focused-functionality"></a>Funcionalidad centrada

Las pestañas funcionan mejor cuando se crean para satisfacer una necesidad específica. Céntrese en un pequeño conjunto de tareas o en un subconjunto de datos que sea relevante para el canal en el que se encuentra la pestaña.

### <a name="reduced-chrome"></a>Cromo reducido

Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña. Es decir, intente no tener pestañas en la pestaña.

### <a name="integration"></a>Integración

Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de tarjetas en una conversación, por ejemplo.

### <a name="conversational"></a>Conversación

Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.

### <a name="streamlined-access"></a>Acceso simplificado

Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado. Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.

### <a name="responsiveness-to-window-sizing"></a>Capacidad de respuesta al tamaño de la ventana

Los equipos se pueden usar en tamaños de ventana tan pequeños como 720px, por lo que es importante asegurarse de que una pestaña se puede usar en una ventana pequeña tan importante como el uso de resoluciones muy altas.

### <a name="flat-navigation"></a>Navegación plana

Se pide a los desarrolladores que no agreguen todo su portal a una pestaña. mantener la navegación relativamente plana ayuda a mantener un modelo de conversación más sencillo. En otras palabras, la conversación trata sobre una lista de cosas, como los elementos de trabajo clasificados o de un solo elemento, como una especificación.

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
> Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams. *Consulte*, por ejemplo, [colores de Microsoft Teams] (/Concepts/Design/Components/Typography.MD

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

<img width="450px" title="Tamaños de las pestañas de configuración" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a>Instrucciones para el formato de página de configuración de pestañas

* Base el alto mínimo del área de contenido de la página de configuración de pestañas en elementos gráficos de altura fija.
* Calcula el espacio vertical disponible (el alto del área de contenido en la página de configuración `window.innerHeight`) mediante. Esto devuelve el tamaño del en `<iframe>` el que reside la página de configuración, lo que puede cambiar en futuras versiones. Al usar este valor, el contenido se ajustará automáticamente a los cambios futuros.
* Asigna espacio vertical a los elementos variable-height menos lo que se necesita para los elementos de altura fija.
* Para el estado de *Inicio de sesión* , centrar vertical y horizontalmente el contenido.
* Si desea una imagen de fondo, necesitará una nueva imagen, ajustada para ajustarse al área (recomendado) o puede conservar la misma imagen y elegir entre:
  * alineación a la esquina superior izquierda.
  * escalar la imagen para ajustarla.

Cuando esté correctamente ajustado, la página de configuración de pestaña debe tener un aspecto similar a este:

<img width="450px" title="Nueva pestaña Configuración" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="always-include-a-default-state"></a>Incluir siempre un estado predeterminado

Incluya un estado predeterminado para que las pestañas se puedan configurar fácilmente incluso si la pestaña se puede configurar.

### <a name="deep-linking"></a>Vinculación profunda

Siempre que sea posible, las tarjetas y los bots deben tener un vínculo profundo a datos enriquecidos en una pestaña hospedada. Por ejemplo, puede que una tarjeta muestre un resumen de los datos de los errores, pero al hacer clic en él se muestra el error completo en una pestaña.

### <a name="naming"></a>Poner

En muchos casos, el nombre de la aplicación tomará un nombre de pestaña excelente. Pero, también considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.

## <a name="notifications-for-tabs"></a>Notificaciones para pestañas

Hay dos modos de notificación para cambios de contenido de pestañas:

> [!div class="checklist"]
>
> * **Use la API de aplicaciones para notificar a los usuarios los cambios**. Este mensaje se mostrará en la fuente de actividad del usuario y un vínculo profundo a la ficha. *consulte*  [Create deep links to Content and features in Microsoft Teams](/concepts/build-and-test/deep-links?view=msteams-client-js-latest)
> * **Usar un bot**. Este método es preferible especialmente si el subproceso de la pestaña es de destino. El resultado será que la conversación encadenada de la pestaña se desplazará a la vista como activa recientemente. Este método también permite una sofisticación en el modo en que se envía la notificación.

  El envío de un mensaje a un subproceso de tabulación aumenta la conciencia de la actividad a todos los usuarios sin notificar explícitamente a todos los usuarios. Se trata de un reconocimiento sin ruido. Además, cuando hay usuarios `@mention` específicos, la misma notificación se colocará en la fuente, lo que hará que se vinculen directamente al hilo de la pestaña.
