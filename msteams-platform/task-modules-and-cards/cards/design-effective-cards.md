---
title: Diseño de tarjetas eficaces
description: Describe las instrucciones de diseño para crear tarjetas
keywords: Directrices de diseño de Microsoft Teams tarjetas de marco de referencia adaptables ligeras
ms.openlocfilehash: 33ee0b59a3a5a1490d6e2106f8532094ed852598
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41676151"
---
# <a name="designing-effective-cards"></a>Diseño de tarjetas eficaces

Las tarjetas son fragmentos de código accionables que puede Agregar a una conversación a través de un bot, un conector o una aplicación. Mediante el uso de texto, gráficos y botones, las tarjetas le permiten comunicarse con una audiencia.

Nuestro marco de tarjeta elimina la carga de diseñar una experiencia de usuario completamente funcional. Hemos desarrollado varios tipos de tarjetas estándar y cada una se ajusta a las plataformas admitidas. Esto significa que el diseño se ha realizado por completo y que no necesitará desarrollar distintas iteraciones de tarjeta entre plataformas. En su lugar, puede centrarse en marcar el contenido.

---

## <a name="guidelines"></a>Instrucciones

Piense en una tarjeta como una respuesta a una pregunta de un usuario o una configuración. Una tarjeta puede responder a una pregunta directa (como, por ejemplo, "¿cuántos errores abiertos tengo?") o a una condición (como, "enviar una lista de mis errores abiertos en 9 a.m. todos los días").

> [!TIP]
> Usar uno de los tipos de tarjetas estándar significa que ya sabrá que todas las respuestas se representarán de forma agradable en cada plataforma compatible.

Una tarjeta puede incluir cualquiera de los siguientes elementos:<br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. **Texto sobre**: se usa mejor para los mensajes de chat. Por ejemplo, si desea que un bot diga: "Esto es lo que me he encontrado". o "tiempo para el Resumen de noticias de 1:00", el mensaje se muestra mejor en el texto sobre.

   El texto sobre es una excelente forma de inyectar un poco de personalidad en su servicio, simplemente Recuerde que debe mantenerlo relativamente corto.

2. **Título**: el título siempre será el texto más grande de la tarjeta. También sirve como "enlace", por lo que debe intentar mantener el título corto, memorable y fácil de examinar.

3. **Subtítulo**: se usa mejor para la atribución, las consignaciones o como una directiva secundaria. Este componente aparece justo debajo del título.

4. **Imagen**: la escala de las imágenes se ajusta a su contenedor. Las tarjetas de Hero tienen un ancho máximo de 420px, las miniaturas tienen un ancho máximo de 100px y las vistas de lista solo permiten 32 en el modo de escritorio.

5. **Text**: el mejor uso para texto sin formato en el cuerpo de la tarjeta. La longitud máxima depende del tipo de tarjeta que haya seleccionado.

6. **Botones**: se usa mejor para abrir páginas web, pestañas o contenido adicional de chat. Asegúrese de mantener el texto del botón corto y en el punto.

   Puede incluir hasta 6 botones por tarjeta, pero recomendamos seguir una filosofía de "menor es más".

7. **Pulse región**: es la región en la que se hace clic de la tarjeta. La mayoría de los usuarios querrán hacer clic en las imágenes de forma automática, así que pruebe y diseñe el texto para que sepan dónde deben puntear o haga clic.

> [!TIP]
> No es necesario incluir todos los elementos de cada tarjeta que cree. Permita que el contenido dicte sus elementos.

---

## <a name="types-of-cards"></a>Tipos de tarjetas

### <a name="hero"></a>Elemento principal

Nuestra tarjeta más grande. Se usa mejor para artículos, descripciones largas o escenarios en los que la imagen está indicando la mayor parte del artículo.

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a>Thumbnail

Corta y agradable. Estas tarjetas son ideales para respuestas breves o si desea devolver varias tarjetas a la vez para que el usuario pueda elegir entre varias opciones. Creemos que estos son una estupenda manera de crear un vínculo profundo a otra pestaña o un servicio Web.

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a>Iniciar sesión

Algunos servicios requieren que los usuarios inicien sesión independientemente de la autenticación. En ese caso, deberá presentar una tarjeta de inicio de sesión antes de que el usuario pueda conectarse a su servicio.

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> Limite las repeticiones de una tarjeta de inicio de sesión adicional, ya que constituyen una rugosidad de velocidad significativa para los nuevos usuarios.

---

## <a name="card-collections"></a>Colecciones de tarjetas

También tenemos tipos de tarjeta estándar que se usan mejor cuando desea presentar varias partes de contenido a la vez o en una sucesión rápida. Para ello, tenemos un carrusel, un resumen, una lista y lo que llamamos "combinación de burbujas".

### <a name="carousel"></a>Carrusel

Se usa mejor para artículos, compras y examen de tarjetas.

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> El carrusel será el alto máximo de la tarjeta más grande. Se recomienda usar el mismo tipo de tarjeta y los mismos campos de contenido en el mismo.

### <a name="digest"></a>Digest

Se usa mejor para noticias, resúmenes y siempre que quiera que el usuario vea varias tarjetas a la vez. Se recomienda usar tarjetas de miniaturas para los resúmenes.

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a>Listas

Las listas son una buena forma de presentar un conjunto de objetos que se pueden analizar en un escenario "Elija uno de estos". Las listas se usan mejor para los elementos que no necesitan mucha explicación.

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a>Combinación de burbujas

Se pueden obtener efectos interesantes mediante el envío de un héroe y varias miniaturas en una sucesión rápida. Recomendamos este enfoque cuando desee servir un resultado principal, pero incluya algunos elementos más relacionados.

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a>Procedimientos recomendados

### <a name="keep-the-noise-down"></a>Mantener el ruido hacia abajo

Es fácil enviar varias tarjetas a una conversación, pero una vez que las tarjetas se desplazan fuera de la vista, se vuelven menos útiles. Intente limitarse a los conceptos básicos. Esto es especialmente cierto en un canal en el que los usuarios tienen menos tolerancia para lo que perciben como "ruido".

### <a name="test-on-mobile"></a>Probar en dispositivos móviles

Los entornos móviles tienen limitaciones de espacio y ancho de banda, por lo que debe tener cuidado con la inclusión de imágenes de gran tamaño y conjuntos de datos de gran tamaño en listas y carruseles. Además, los anchos de los títulos y las longitudes del texto se truncarán en dispositivos móviles, por lo que es otro aspecto que debe tener en vista.

### <a name="check-your-graphics"></a>Comprobar los gráficos

Los gráficos van a escalarse, así que asegúrese de obtener una vista previa de ellos en todas las plataformas.

### <a name="avoid-including-text-in-a-graphic"></a>Evitar incluir texto en un gráfico

Todo lo que deba leer un usuario debe incluirse en un campo de texto. Una vez que se escala dinámicamente una imagen, cualquier texto que agregue a un gráfico puede volverse ininteligible.

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a>Use menciones si desea la atención de usuarios específicos

> [!NOTE]
> Mencione que la compatibilidad en tarjetas solo se admite actualmente en [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) .

Las menciones son una excelente manera de notificar a usuarios específicos en un equipo o un chat en grupo. Puede incluir una mención en tarjeta en escenarios como, una tarea que está asignada a un usuario o conceder prestigio a un compañero. Obtenga información sobre cómo incluir menciones en tarjetas en la [Página formato de tarjeta](~/task-modules-and-cards/cards/cards-format.md). 
