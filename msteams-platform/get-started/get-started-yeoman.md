---
title: 'Tutorial: crear la primera aplicación con el generador de Yeoman'
description: Obtén información sobre cómo empezar a crear Microsoft Teams aplicaciones con el generador de Yeoman.
keywords: introducción a node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: a3519da1495dc51a811f4e95bc4ada9b11aa8292
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254358"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Crear la primera aplicación Microsoft Teams con el generador de Yeoman

> [!Note]
> Este tutorial proviene del generador [de Yeoman para Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).

En este tutorial, aprenderás a crear la primera aplicación Microsoft Teams con el generador de Yeoman Microsoft Teams de Yeoman. También le guiará a través del proceso de actualización de su Teams mediante el generador de Yeoman. Antes de comenzar, debes tener una cuenta Teams que permita la [instalación local de la aplicación](~/concepts/build-and-test/prepare-your-o365-tenant.md).

![git generador de yeoman](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtener requisitos previos

Debe instalar lo siguiente en el equipo antes de empezar a usar el generador de Yeoman:

* Node.js

   Debe tener Node.js instalado en el equipo. Debe usar la versión [lts más reciente](https://nodejs.org).

* Un editor de código

   Necesita un editor de código. La mayoría de esta documentación e imágenes hacen referencia al [uso de Visual Studio Code](https://code.visualstudio.com). Sin embargo, no dude en usar el editor de texto que prefiera.

* CLI de Yeoman y Gulp

   Para scaffolding de proyectos con el generador, debe instalar la herramienta Yeoman y el administrador de tareas de la CLI de Gulp.

   Abra un símbolo del sistema y escriba lo siguiente:

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a>Instalar el generador

Instale el Teams Yeoman con el siguiente comando:

```bash
npm init yo teams
```

Instale la versión preliminar del generador con el siguiente comando:

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a>Generar el proyecto

Esta sección le guiará por los pasos para generar el proyecto.

**Para generar el proyecto**

1. Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto.
1. Vaya al directorio y ejecute el comando `yo teams` . Se inicia el generador.
1. Responda al conjunto de preguntas que le pida el generador:

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. Escriba un nombre para el proyecto. Puede dejarla tal como está presionando Entrar.
   1. Escriba una ruta de acceso para el nuevo directorio si desea crear un directorio nuevo. Como ya está en el directorio que desea, simplemente presione ENTRAR.
   1. Escriba el título del proyecto. Este título se usará en el manifiesto y la descripción de la aplicación. 
   1. Escriba un nombre de empresa que también se usará en el manifiesto.
   1. Escriba la versión del manifiesto que desea usar. Para este tutorial, `v1.5` seleccione , que es el esquema disponible general actual.
   1. Seleccione los elementos que desea agregar al proyecto. Puede seleccionar una sola o cualquier combinación de elementos. Para estos tutoriales, solo tienes *que seleccionar una pestaña*:

    ![selección de elementos](~/assets/yeoman-images/teams-first-app-2.png)

1. Responda al siguiente conjunto de preguntas de seguimiento que aparecen en función de los elementos seleccionados en el paso 2.
1. Escriba una dirección URL para la ubicación donde hospedará la solución. 

   > [!NOTE]
   > La dirección URL puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL de sitio web de Azure.

1. Confirme si desea incluir pruebas unitarias para la solución. La respuesta predeterminada es **Sí**. Si opta por incluir pruebas unitarias, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding. 
   > [!NOTE]
   > * Para este tutorial, elija no incluir un marco de prueba.
   > * El generador tiene una gran cantidad de características avanzadas integradas de las que puede participar o no participar.

1. Para facilitar el inicio de sesión, también se le preguntará si desea usar Azure Application Ideas para iniciar sesión. Si selecciona **Sí**, tendrá que proporcionar una clave de Ideas Azure Application. 

   > [!NOTE]
   > En este tutorial no se puede usar application Ideas.

   El siguiente conjunto de preguntas se basará en los elementos seleccionados anteriormente. Para una pestaña solo tienes que proporcionar un nombre y, opcionalmente, elegir si quieres poder usar esta aplicación como un elemento web SharePoint Online. Después de proporcionar el nombre, el generador generará el proyecto e instalará todas las dependencias. Esto llevará uno o dos minutos.

## <a name="add-code-to-your-tab"></a>Agregar código a la pestaña

Una vez terminado el generador, puede abrir la solución en el editor de código favorito. Tómese uno o dos minutos y familiarícese con cómo se organiza el código. Para obtener más información, [vea Project structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)

La pestaña está en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo. Esta es la clase basada React TypeScript para la pestaña. 

1. Busque el `render()` método y agregue una línea de código dentro del control para que se vea `<PanelBody>` así:

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. Guarde el archivo y vuelva al símbolo del sistema.

## <a name="build-your-app"></a>Crear una aplicación

Ahora puede crear el proyecto. Esto se realiza en dos pasos.

1. Crea el Teams de manifiesto de la aplicación para la aplicación que has cargado en Microsoft Teams. Esto se realiza mediante la tarea Gulp `gulp manifest` . Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.
1. Ejecute el `gulp build` comando para compilar la solución. Esto transpilará la solución en la `./dist` carpeta. 

## <a name="run-your-app"></a>Ejecutar la aplicación

Para ejecutar la aplicación, usa el `gulp serve` comando. Esto compilará e iniciará un servidor web local para que pruebe la aplicación. El comando también reconstruirá la aplicación siempre que guarde un archivo en el proyecto. 

Ahora debe ir a y `http://localhost:3007/myFirstAppTab/` asegurarse de que la pestaña se está representando. Sin embargo, aún no está Microsoft Teams. 

**Para representar la pestaña en Microsoft Teams**

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a>Ejecute la aplicación en Microsoft Teams

Microsoft Teams no te permite tener la aplicación hospedada en localhost, por lo que debes publicarla en una dirección URL pública o usar un proxy como ngrok. Una buena noticia es que el proyecto scaffolded tiene este proyecto integrado. 

**Para ejecutar la aplicación en Teams**

1. Ejecutar `gulp ngrok-serve` en terminal. Cuando ejecute el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp ngrok-serve` `gulp serve` .
1. Cree un nuevo Microsoft Teams equipo.
1. Seleccione el nombre del equipo > Teams Configuración > Aplicaciones.
1. En la esquina inferior derecha, **selecciona Upload una aplicación personalizada.**
1. Vaya a la `package` carpeta de la carpeta del proyecto. 
1. Seleccione el archivo zip de esa carpeta y seleccione Abrir. 
   La aplicación ahora se ha descargado localmente en Microsoft Teams:

   ![aplicación de sideloaded](~/assets/yeoman-images/teams-first-app-4.png)
1. Vuelva al canal **General** y seleccione **+** agregar una nueva pestaña. Debería ver la pestaña en la lista de pestañas: ![ configurar ficha](~/assets/yeoman-images/teams-first-app-5.png)
1. Seleccione la pestaña y siga las instrucciones para agregarla. Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizado para el que puede editar el origen. Seleccione *Guardar* para agregar la pestaña al canal. La pestaña se carga ahora dentro de Microsoft Teams!

   ![ejecutar pestaña en teams](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a>Actualizar Microsoft Teams

También puede actualizar la versión Microsoft Teams actual a la versión más reciente mediante el generador de Yeoman Microsoft Teams de Yeoman.

**Para actualizar Microsoft Teams**

1. Obtenga la versión actual de Teams con el siguiente comando:

   ```PowerShell
    yo teams --version
   ```
2. Use el siguiente comando para seleccionar y actualizar el generador:

   ```PowerShell
    yo
   ```
3. Use las teclas de flecha para **seleccionar Actualizar los generadores:**

   ![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. Seleccione el generador que desee de la lista de generadores:
   > [!NOTE]
   > Use la barra espaciador para seleccionar o borrar una versión Teams seleccionada de las opciones disponibles.

    ![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > Se tardan unos segundos y minutos en completarse Teams instalación.

5. Una vez completada la instalación, use el siguiente comando para comprobar la versión instalada:

   ```PowerShell
    yo teams --version
   ```
   ¡Felicidades! Has creado e implementado la primera Microsoft Teams aplicación. También ha actualizado Microsoft Teams.

 ## <a name="see-also"></a>Vea también

* [Introducción a tutoriales](code-samples.md)
* [Crear una aplicación de bots de conversación](first-app-bot.md)
* [Crear una extensión de mensajería](first-message-extension.md)
* [Muestras de código](https://github.com/OfficeDev/Microsoft-Teams-Samples)