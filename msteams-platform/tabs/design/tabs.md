---
title: Directrices de diseño para pestañas
description: Describe las instrucciones para crear pestañas de contenido y colaboración
keywords: Directrices de diseño de Microsoft Teams referencia de las fichas de marco de trabajo
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675689"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>Contenido y conversaciones, todos a la vez mediante pestañas

> [!Important]
> **Pestañas en clientes móviles**
>
> Siga las [instrucciones para las pestañas de dispositivos móviles](~/tabs/design/tabs-mobile.md) al crear las pestañas. Si su pestaña usa autenticación, debe actualizar el SDK de JavaScript de Teams a la versión 1.4.1 o posterior, o se producirá un error de autenticación.
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

> [!TIP]
> Evite crear varios paneles en una pestaña, agregar capas de navegación o requerir que los usuarios se desplacen tanto vertical como horizontalmente en una pestaña.

### <a name="integration"></a>Integración

Obtenga información sobre cómo notificar a los usuarios la actividad de pestañas mediante el registro de tarjetas en una conversación, por ejemplo.

### <a name="conversational"></a>Conversación

Buscar una forma de facilitar la conversación alrededor de una pestaña. Esto garantiza que las conversaciones se centran en el contenido, los datos o el proceso a mano.

### <a name="streamlined-access"></a>Acceso simplificado

Asegúrese de que está concediendo acceso a las personas adecuadas en el momento adecuado. Mantener simple el proceso de inicio de sesión evitará la creación de obstáculos a la contribución y la colaboración.

### <a name="personality"></a>Personalidad

Tu lienzo de pestañas ofrece una buena oportunidad para personalizar tu experiencia. Incorpore sus propios logotipos, colores y diseños para comunicar la personalidad.

Su logotipo es una parte importante de su identidad y una conexión con los usuarios. Por lo tanto, asegúrese de incluirla.

* Poner el logotipo en la esquina izquierda o derecha o a lo largo del borde inferior
* Mantener el logotipo en pequeña y discreta

> [!TIP]
> Trabaje con nuestro estilo visual para que su servicio se sienta como parte de Microsoft Teams.

---

## <a name="tab-layouts"></a>Diseños de pestañas

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a>Tipos de pestañas

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a>Alto de página de configuración

>[!NOTE]
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

En muchos casos, el nombre de la aplicación puede crear un nombre de pestaña excelente. Pero considere la posibilidad de asignar un nombre a las pestañas según la funcionalidad que proporcionan.
