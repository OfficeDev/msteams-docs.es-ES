---
title: Escenas personalizadas del modo conjunto
description: Trabajar con escenas personalizadas del modo de colaboración
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 3820a711dfa759e3ad9429efd6b848cbe47e4623
ms.sourcegitcommit: e45742fd2aa2ff5e5c15e8f7c20cc14fbef6d441
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2021
ms.locfileid: "61075461"
---
# <a name="custom-together-mode-scenes-in-teams"></a>Escenas personalizadas en modo conjunto en Teams

Las escenas personalizadas del Modo Microsoft Teams proporcionan un entorno de reunión envolvente y atractivo con las siguientes acciones:

* Reúne a las personas y anímelas a activar su vídeo. 
* Combina los participantes digitalmente en una sola escena virtual. 
* Coloca las secuencias de vídeo de los participantes en puestos predefinidos diseñados y fijos por el creador de la escena.

En las escenas personalizadas del Modo conjunto, la escena es un artefacto. La escena la crea el desarrollador de la escena mediante el estudio de escena de Microsoft. En una configuración de escena pensada, los participantes tienen puestos con secuencias de vídeo. Los vídeos se representan en esos puestos. Solo se recomiendan las aplicaciones de escena, ya que la experiencia de estas aplicaciones es clara.

El siguiente proceso proporciona información general para crear una aplicación de solo escena:

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Crear solo una aplicación de escena" border="false":::

Una única aplicación de escena sigue siendo una aplicación en Microsoft Teams. Scene studio controla la creación de paquetes de aplicaciones en segundo plano. Varias escenas de un único paquete de aplicación aparecen como una lista plana para los usuarios.

> [!NOTE]
> Los usuarios no pueden iniciar el modo junto desde el móvil. Sin embargo, después de que un usuario se una a una reunión a través del móvil y el modo Juntos esté activado desde el escritorio, los usuarios móviles que han activado el vídeo aparecerán en modo conjunto en el escritorio. 

## <a name="prerequisites"></a>Requisitos previos

Debe tener una comprensión básica de lo siguiente para usar escenas personalizadas del Modo conjunto:

* Defina la escena y los puestos de una escena.
* Tenga una cuenta de Microsoft Developer y familiarícese con Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) y App Studio.
* Comprender el [concepto de instalación local de aplicaciones](../concepts/deploy-and-publish/apps-upload.md).
* Asegúrate de que el administrador haya concedido permiso [**para Upload una**](../concepts/deploy-and-publish/apps-upload.md) aplicación personalizada y selecciona todos los filtros como parte de las directivas de configuración y reunión de la aplicación respectivamente.

## <a name="best-practices"></a>Procedimientos recomendados

Tenga en cuenta los siguientes procedimientos para una experiencia de creación de escena:

* Asegúrese de que todas las imágenes están en formato PNG.
* Asegúrese de que el paquete final con todas las imágenes juntas no debe superar la resolución de 1920 x 1080. La resolución es un número par. Esta resolución es un requisito para que las escenas se puedan mostrar correctamente.
* Asegúrese de que el tamaño máximo de la escena es de 10 MB.
* Asegúrese de que el tamaño máximo de cada imagen es de 5 MB. Una escena es una colección de varias imágenes. El límite es para cada imagen individual.
* Asegúrese de seleccionar **Transparente según** sea necesario. Esta casilla está disponible en el panel derecho cuando se selecciona una imagen. Las imágenes superpuestas deben estar marcadas **como Transparentes** para indicar que están superpuestas en la escena.

## <a name="build-a-scene-using-the-scene-studio"></a>Crear una escena con scene studio

Microsoft tiene un estudio de escena que te permite crear escenas. Está disponible en Scenes [Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes). Este documento hace referencia a Scene studio en el Microsoft Teams Developer Portal. La interfaz y las funcionalidades son iguales en el Diseñador de escenas de App Studio.

Una escena en el contexto del estudio de escena es un artefacto que contiene los siguientes elementos:

* Puestos reservados para organizadores de reuniones y presentadores de reuniones. El moderador no hace referencia al usuario que está compartiendo activamente. Hace referencia al rol [de reunión](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

* Asiento e imagen para cada participante con un ancho y alto ajustables. Solo se admite el formato PNG para la imagen.

* Coordenadas XYZ de todos los puestos e imágenes.

* Colección de imágenes camufladas como una imagen.

La siguiente imagen muestra cada puesto representado como un avatar para crear las escenas:

![Scene studio](../assets/images/apps-in-meetings/scene-design-studio.png)

**Para crear una escena con scene studio**

1. Vaya a [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).

    Como alternativa, para abrir Scene studio, puedes ir a la página principal de [Teams Developer Portal:](https://dev.teams.microsoft.com/home)
    * Seleccione **Crear escenas personalizadas para reuniones**.
    * Selecciona **Herramientas** en la sección izquierda y selecciona **Scene studio** en la **sección** Herramientas.

1. En **el Editor de** escenas, seleccione Crear una nueva **escena**.

1. En **Nombre de escena**, escriba un nombre para la escena.

    * Puede seleccionar Cerrar **para alternar** entre cerrar o volver a abrir el panel derecho.
    * Puedes acercar o alejar la escena con la barra de zoom para obtener una mejor vista de la escena.

1. Seleccione **Agregar imágenes** para agregar la imagen al entorno:

    ![Agregar imágenes al entorno](../assets/images/apps-in-meetings/addimages.png)

    >[!NOTE]
    > * Puede descargar los archivos [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) [ ySampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) con las imágenes.

1. Seleccione la imagen que ha agregado.

1. En el panel derecho, seleccione una alineación para la imagen o use **Resize** para ajustar el tamaño de la imagen:

    ![Alineación de imágenes](../assets/images/apps-in-meetings/image-alignment.png)

1. Seleccione un área fuera de la imagen.

1. En la esquina superior derecha, seleccione **Participantes en** **Capas**.

1. Seleccione el número de participantes para la escena en el cuadro Número de **participantes** y seleccione **Agregar**. Después de enviar la escena, las ubicaciones de avatar se reemplazan por secuencias de vídeo del participante real. Puede arrastrar las imágenes de los participantes alrededor de la escena y colocarlas en la posición necesaria. Puede cambiar su tamaño con la flecha de cambio de tamaño.

1. Selecciona cualquier imagen de participante y selecciona **Asignar mancha** para asignar la mancha al participante.

1. Seleccione **Organizador de reuniones** o Rol de **moderador** para el participante. En una reunión, se debe asignar a un participante el rol de organizador de la reunión:

    ![Asignar spot](../assets/images/apps-in-meetings/assign-spot.png)

1. Seleccione **Guardar** y **seleccione Ver en Teams** para probar rápidamente la escena en Microsoft Teams.

    * Al seleccionar **Ver en Teams** crea automáticamente una aplicación de Microsoft Teams que  se puede ver en la página Aplicaciones del portal Teams desarrolladores.
    * Al seleccionar **Ver en Teams** crea automáticamente un paquete de aplicación que es appmanifest.json detrás de la escena. Puedes ir a  **Aplicaciones desde** el menú y acceder al paquete de aplicaciones creado automáticamente.
    * Para eliminar una escena que creaste, **selecciona Eliminar escena** en la barra superior.

1. En **Vista en Teams**, seleccione Vista previa en **Teams**.
1. En el cuadro de diálogo que aparece, seleccione **Agregar**.

    Se prueba o se accede a la escena mediante la creación de una reunión de prueba y el inicio de escenas personalizadas del modo conjunto. Para obtener más información, vea [Activar escenas personalizadas del modo conjunto:](#activate-custom-together-mode-scenes)

    ![Iniciar escenas personalizadas del modo conjunto](../assets/images/apps-in-meetings/launchtogethermode.png)

    A continuación, la escena se puede ver en la galería de escenas del modo conjunto personalizada.

Opcionalmente, puede seleccionar **Compartir en** el **menú** desplegable Guardar. Puede crear un vínculo que se pueda compartir para distribuir las escenas para que otras personas las usen. El usuario puede abrir el vínculo para instalar la escena y empezar a usarlo.

Después de la vista previa, la escena se envía como una aplicación para Teams siguiendo los pasos para el envío de la aplicación. Este paso requiere el paquete de la aplicación. El paquete de la aplicación es diferente del paquete de escena, para la escena que se diseñó. El paquete de la aplicación creado automáticamente se encuentra en la **sección Aplicaciones** del Centro Teams desarrolladores.

Opcionalmente, el paquete de escena se recupera **seleccionando Exportar** en el **menú** desplegable Guardar. Se **.zip** un archivo de.zip, que es el paquete de escena. El paquete de escena incluye un scene.json y los activos PNG usados para crear una escena. Se revisa el paquete de escena para incorporar otros cambios:

![Exportar una escena](../assets/images/apps-in-meetings/build-a-scene.png)

Una escena compleja que usa el eje Z se muestra en el ejemplo de introducción paso a paso.

## <a name="sample-scenejson"></a>Ejemplo scene.json

Scene.json junto con las imágenes indican la posición exacta de los puestos. Una escena consta de imágenes de mapa de bits, sprites y rectángulos para colocar los vídeos de los participantes. Estos sprites y cuadros de participantes se definen en un sistema de coordenadas mundiales. El eje X apunta a la derecha y el eje Y apunta hacia abajo.

Las escenas del Modo conjunto personalizado admiten acercamiento a los participantes actuales. Esta característica es útil para reuniones pequeñas en una escena grande. Un sprite es una imagen de mapa de bits estática posicionada en el mundo. El valor Z del sprite determina la posición del sprite. La representación comienza con el sprite con el valor Z más bajo, por lo que un valor Z más alto significa que está más cerca de la cámara. Cada participante tiene su propia fuente de vídeo, que se segmenta para que solo se represente el primer plano.

El siguiente código es el ejemplo scene.json:

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

Cada escena tiene un identificador y un nombre únicos. El JSON de la escena también contiene información sobre todos los activos usados para la escena. Cada activo contiene un nombre de archivo, ancho, alto y posición en el eje X e Y. Del mismo modo, cada asiento contiene un identificador de asiento, ancho, alto y posición en los ejes X e Y. El orden de asientos se genera automáticamente y se modifica según las preferencias. El número de orden de asientos corresponde al orden de las personas que se unen a la llamada.

Representa `zOrder` el orden de colocación de imágenes y puestos a lo largo del eje Z. Proporciona una sensación de profundidad o partición si es necesario. Consulta el ejemplo de introducción paso a paso. El ejemplo usa `zOrder` el archivo .

Ahora que has pasado por el ejemplo scene.json, puedes activar las escenas personalizadas del Modo conjunto para participar en escenas.

## <a name="activate-custom-together-mode-scenes"></a>Activar escenas personalizadas del modo conjunto

Obtenga más información sobre cómo un usuario interactúa con las escenas en escenas personalizadas del Modo conjunto.

**Para seleccionar escenas y activar escenas personalizadas del Modo conjunto**

1. Crear una nueva reunión de prueba.

    >[!NOTE]
    > Al seleccionar **Vista previa** en el estudio de escena, la escena se instala como una aplicación en Microsoft Teams. Este es el modelo para que un desarrollador pruebe y pruebe las escenas del estudio scene. Después de que una escena se envíe como una aplicación, los usuarios verán estas escenas en la galería de escenas.

1. En la **lista** desplegable Galería de la esquina superior izquierda, seleccione **Modo conjunto**. Aparece **el cuadro de** diálogo Selector y la escena que se agrega está disponible.

1. Seleccione **Cambiar escena** para cambiar la escena predeterminada.

1. En la **Galería de escenarios,** seleccione la escena que desea usar para la reunión.

    Opcionalmente, el organizador de la reunión y el moderador pueden cambiar la escena de todos los **participantes** de la reunión.

    >[!NOTE]
    > En cualquier momento, solo se usa una escena de forma homogénea para la reunión. Si un moderador u organizador cambia una escena, cambia para todos. El cambio de las escenas personalizadas del Modo conjunto es una función de los participantes individuales, pero mientras que en las escenas personalizadas del Modo conjunto, todos los participantes tienen la misma escena.

1. Seleccione **Aplicar**. Teams instala la aplicación para el usuario y aplica la escena.

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>Abrir un paquete de escenas de escenas de modo conjunto personalizado

Puedes compartir el paquete de escena que es un archivo .zip recuperado del estudio de escena a otros creadores para mejorar aún más la escena. La **funcionalidad Importar una escena** ayuda a desenvolver un paquete de escena para permitir al creador continuar con la creación de la escena.

![Archivo zip de escena](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>Vea también

* [Aplicaciones para Teams reuniones](teams-apps-in-meetings.md)
* [Bots de llamadas y reuniones ](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Llamadas multimedia en tiempo real y reuniones con Microsoft Teams](~/bots/calls-and-meetings/real-time-media-concepts.md)
