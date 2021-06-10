---
title: Modo conferencia en Teams
description: Trabajar con el modo de colaboración
ms.topic: conceptual
ms.openlocfilehash: 1620e01ef1825ec43e94614ff8ea355e764e10e0
ms.sourcegitcommit: 1cc1516e71441f6f3f82b35868e21ba9933333cd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2021
ms.locfileid: "52651743"
---
# <a name="together-mode-in-teams"></a>Modo conferencia en Teams

> [!NOTE]
> Esta característica está disponible actualmente solo en [la versión preliminar del desarrollador](../resources/dev-preview/developer-preview-intro.md) público.

Microsoft Teams El modo juntos proporciona un entorno de reunión envolvente y atractivo que reúne a las personas y les anima a activar su vídeo. Combina digitalmente a los participantes en una sola escena virtual y coloca sus secuencias de vídeo en puestos predefinidos diseñados y fijos por el creador de la escena.

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

Una escena en el modo juntos es un artefacto creado por el desarrollador de la escena mediante el estudio de escena de Microsoft. En una configuración de escena pensada, los participantes han designado puestos con secuencias de vídeo representados en esos puestos.

> [!NOTE]
> Solo se recomiendan las aplicaciones de escena, ya que la experiencia de adquisición de estas aplicaciones es más sencilla.

El siguiente proceso proporciona información general para crear una aplicación de solo escena:

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Crear solo una aplicación de escena" border="false":::

> [!NOTE]
> * Una única aplicación de escena sigue siendo una aplicación en Microsoft Teams. Scene studio controla la creación de paquetes de aplicaciones en segundo plano.
> * Varias escenas de un único paquete de aplicación aparecen como una lista plana de escenas para los usuarios.

## <a name="prerequisites"></a>Requisitos previos

Debe tener una comprensión básica de lo siguiente para usar el modo juntos:

* Definición de escena y puestos en una escena.
* Tenga una cuenta de Microsoft Developer y familiarícese con Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) y App Studio.
* [Concepto de instalación local de la aplicación](../concepts/deploy-and-publish/apps-upload.md).
* Asegúrese de que el administrador ha concedido permiso para **Upload una** aplicación personalizada y para seleccionar todos los filtros como parte de las directivas de configuración y reunión de la aplicación respectivamente.

## <a name="best-practices"></a>Procedimientos recomendados

Antes de crear una escena, tenga en cuenta lo siguiente para tener una experiencia de creación de escena sin problemas:

* Asegúrese de que todas las imágenes están en formato PNG.
* Asegúrese de que el paquete final con todas las imágenes juntas no debe superar la resolución de 1920 x 1080.

    > [!NOTE]
    > La resolución es un número par. Este es un requisito para que las escenas se ilumine correctamente.

* Asegúrese de que el tamaño máximo de la escena es de 10 MB.
* Asegúrese de que el tamaño máximo de cada imagen es de 5 MB.

    > [!NOTE]
    > * Una escena es una colección de varias imágenes. El límite es para cada imagen individual.
    > * La resolución de imagen individual también debe ser un número par.
  
* Asegúrese de que la **casilla Transparente** está activada si la imagen es transparente. Esta casilla está disponible en el panel derecho cuando se selecciona una imagen.

    > [!NOTE]
    > Las imágenes superpuestas deben marcarse como **Transparentes** para indicar que son imágenes superpuestas en la escena.

## <a name="build-a-scene-using-the-scene-studio"></a>Crear una escena con scene studio

Microsoft tiene un estudio de escena que te permite crear escenas. Está disponible en [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).

> [!NOTE]
> Este documento hace referencia a Scene studio en el Microsoft Teams Developer Portal. La interfaz y las funcionalidades son iguales en el Diseñador de escenas de App Studio.

Una escena en el contexto del estudio de escena es un artefacto que contiene lo siguiente:

* Puestos reservados para organizadores de reuniones y presentadores de reuniones.

    > [!NOTE]
    > El moderador no hace referencia al usuario que está compartiendo activamente. Hace referencia al rol [de reunión](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

* Asiento e imagen para cada participante con un ancho y alto ajustables.

    > [!NOTE]
    > PNG es el único formato compatible.

* Coordenadas XYZ de todos los puestos e imágenes.
* Colección de imágenes camufladas como una imagen.

Las dimensiones del asiento se convierten en el lienzo para representar la secuencia de vídeo del participante. La siguiente imagen muestra cada asiento representado como un avatar para crear escenas:

![Scene studio](../assets/images/apps-in-meetings/scene-design-studio.png)

**Para crear una escena con scene studio**

1. Vaya a [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).

    >[!NOTE]
    > * Para abrir Scene studio, puede navegar a la página principal de [Teams Developer Portal](https://dev.teams.microsoft.com/home) y seleccionar Crear escenas **personalizadas para reuniones.**
    > * Para abrir Scene studio, puedes navegar a la página principal de [Teams Developer Portal, seleccionar](https://dev.teams.microsoft.com/home) **Herramientas** en la sección izquierda y seleccionar **Scene studio** en la sección **Herramientas.**

1. En la **página Editor de** escenas, seleccione Crear una nueva **escena.**

1. En el **cuadro Escena,** escriba un nombre para la escena.

    >[!NOTE]
    > * Puede seleccionar Cerrar **para alternar** entre cerrar o volver a abrir el panel derecho.
    > * Puedes acercar o alejar la escena con la barra de zoom para obtener una mejor vista de la escena.

1. Arrastre y coloque la imagen en el entorno tal como se muestra en la siguiente imagen:

    >[!NOTE]
    > * Puede descargar los archivos [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) [ ySampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) con las imágenes.
    > * Como alternativa, puede agregar imágenes de fondo a la escena mediante **Agregar imágenes**.

    ![Arrastrar a la escena](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. Seleccione la imagen que ha colocado.

1. En el panel derecho, seleccione una alineación para la imagen o use el control deslizante **Cambiar** tamaño para ajustar el tamaño de la imagen.

    ![Alineación de imágenes](../assets/images/apps-in-meetings/image-alignment.png)

1. Seleccione un área fuera de la imagen.

1. En la esquina superior derecha, seleccione **Participantes en** **Capas**.

1. Seleccione el número de participantes para la escena en el cuadro Número de **participantes** y seleccione **Agregar**.

    >[!NOTE]
    > * Después de enviar la escena, las ubicaciones de avatar se reemplazan por secuencias de vídeo del participante real.
    > * Puede arrastrar las imágenes de los participantes alrededor de la escena y colocarlas en la posición necesaria y cambiar su tamaño mediante la flecha de cambio de tamaño.

1. Seleccione cualquier imagen de participante y seleccione la casilla **Asignar mancha** para asignar la mancha al participante.

1. Seleccione **Organizador de reuniones** o Rol de **moderador** para el participante.

    >[!NOTE]
    > En una reunión, se debe asignar a un participante el rol de organizador de la reunión.

    ![Asignar spot](../assets/images/apps-in-meetings/assign-spot.png)

1. Seleccione **Guardar** y **seleccione Ver en Teams** para probar rápidamente la escena en Microsoft Teams.

    >[!NOTE]
    > Para eliminar una escena que creaste, **selecciona Eliminar escena** en la barra superior.

1. En el **cuadro de diálogo Ver en Teams,** seleccione Vista previa en **Teams**.
1. En el cuadro de diálogo que aparece, seleccione **Agregar**.

    Se puede probar o acceder a la escena creando una reunión de prueba y iniciando el modo juntos. Para obtener más información, [vea activate the Together Mode](#activate-the-together-mode).

    ![Iniciar el modo juntos](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * Al seleccionar **Vista** previa, se crea automáticamente Microsoft Teams aplicación  que se puede ver en la página Aplicaciones del portal Teams desarrolladores.
    > * Al seleccionar **Vista** previa, se crea automáticamente un paquete de aplicación appmanifest.jsdetrás de la escena. Como se mencionó anteriormente, esto se abstrae, pero puedes acceder al paquete de la aplicación creado automáticamente navegando a **Aplicaciones** desde el menú.
    > * A continuación, la escena se puede ver en la galería de escenas del Modo conjunto.

1. Opcionalmente, puedes seleccionar **Compartir** en el menú desplegable Guardar para crear un vínculo que se pueda compartir para distribuir fácilmente las escenas para que otras personas las usen.  Al abrir este vínculo, se instala la escena para el usuario y pueden empezar a usarlo.

1. Después de la vista previa, la escena se puede enviar como una aplicación a Teams siguiendo los pasos para el envío de la aplicación.

    >[!NOTE]
    > Este paso requiere el paquete de la aplicación que es diferente del paquete de escena, para la escena que se diseñó. El paquete de la aplicación creado automáticamente se puede encontrar en la **sección Aplicaciones** del Centro Teams desarrolladores.

1. Opcionalmente, el paquete de escena se puede recuperar **seleccionando Exportar** en el **menú** desplegable Guardar. Se .zip un archivo de .zip, es decir, el paquete de escena.

    ![Exportar una escena](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > El paquete de escena consta de un scene.jsactivo y los activos PNG usados para crear una escena. El paquete de escena se puede revisar para incorporar otros cambios como se describe en la sección Ejemplo scene.jssección de este documento.

Una escena más compleja que aprovecha el eje Z se muestra en la muestra de introducción paso a paso.

## <a name="sample-scenejson"></a>Ejemplo scene.jsen

Scene.jsjunto con las imágenes indican la posición exacta de los puestos. Una escena consta de imágenes de mapa de bits, sprites y rectángulos para colocar los vídeos de los participantes. Estos sprites y cuadros de participantes se definen en un sistema de coordenadas mundiales con el eje X apuntando a la derecha y el eje Y apuntando hacia abajo. El modo juntos admite el acercamiento de los participantes actuales. Esto es útil para reuniones pequeñas en una escena grande. Un sprite es una imagen de mapa de bits estática posicionada en el mundo. El valor Z del sprite determina la posición del sprite. La representación comienza con el sprite con el valor Z más bajo, por lo que un valor Z más alto significa que está más cerca de la cámara. Cada participante tiene su propia fuente de vídeo, que se segmenta para que solo se represente el primer plano.

A continuación se muestra scene.jsejemplo:

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

Cada escena tiene un identificador y un nombre únicos. El JSON de la escena también contiene información sobre todos los activos usados para la escena. Cada activo contiene un nombre de archivo, ancho, alto y posición en el eje X e Y. Del mismo modo, cada asiento contiene un identificador de asiento, ancho, alto y posición en los ejes X e Y. El orden de asientos se genera automáticamente y se puede modificar según las preferencias.

> [!NOTE]
> El número de pedido de asientos corresponde al orden de las personas que se unen a la llamada.

ZOrder representa el orden de colocar imágenes y puestos a lo largo del eje Z. En muchos casos, proporciona una sensación de profundidad o partición si es necesario. Para obtener más información, consulte el ejemplo de introducción paso a paso. El ejemplo aprovecha el zOrder.

Ahora que has pasado por el ejemplo scene.jsactivado, puedes activar el modo juntos para participar en escenas.

## <a name="activate-the-together-mode"></a>Activar el modo juntos

Obtenga información de un extremo a otro de cómo un usuario final interactúa con las escenas en el modo juntos.

**Para elegir escenas y activar el modo juntos**

1. Crear una nueva reunión de prueba.

    >[!NOTE]
    > Al seleccionar **Vista previa** en el estudio de escena, la escena se instala como una aplicación en Microsoft Teams. Este es el modelo para que un desarrollador pruebe y pruebe las escenas del estudio scene. Después de que una escena se envíe como una aplicación, los usuarios verán estas escenas en la galería de escenas.

1. En la **lista** desplegable Galería de la esquina superior izquierda, seleccione **Modo conjunto**. Aparece **el cuadro de** diálogo Selector y la escena que se agrega está disponible.

1. Seleccione **Cambiar escena** para cambiar la escena predeterminada.

1. En la **Galería de escenarios,** seleccione la escena que desea usar para la reunión.

1. Opcionalmente, el organizador de la reunión y el moderador pueden elegir Cambiar todos los **participantes** al modo de reunión conjunta en la reunión.

    >[!NOTE]
    > En cualquier momento, solo se puede usar una escena de forma homogénea para la reunión. Si un moderador u organizador cambia una escena, cambia para todos. El cambio de entrada o de salida del modo juntos es una función de los participantes individuales, pero mientras están en el modo juntos, todos los participantes tienen la misma escena.

1. Seleccione **Aplicar**. Teams instala la aplicación para el usuario y aplica la escena.

## <a name="open-a-together-mode-scene-package"></a>Abrir un paquete de escena de modo conjunto

Puedes compartir el paquete de escena que es un archivo .zip recuperado del estudio de escena a otros creadores para mejorar aún más la escena. Se **puede aprovechar la funcionalidad** Importar una escena. Esta herramienta ayuda a desenvolver un paquete de escena para permitir al creador continuar con la creación de la escena.

![Archivo zip de escena](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>Consulte también

[Aplicaciones para Teams reuniones](teams-apps-in-meetings.md)
