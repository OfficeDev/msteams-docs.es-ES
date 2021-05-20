---
title: Tutorial - Crea tu primera aplicación usando el generador Yeoman
description: Obtén información sobre cómo empezar a crear aplicaciones Microsoft Teams con el generador Yeoman.
keywords: comenzando node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566827"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Crea tu primera aplicación Microsoft Teams usando el generador Yeoman

> [!Note]
> Este tutorial proviene del [generador Yeoman para Teams wiki.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

En este tutorial, vamos a caminar a través de la creación de su primera aplicación Microsoft Teams utilizando el generador de Microsoft Teams Yeoman. También le guía a través del proceso de actualización de su Teams utilizando el generador Yeoman. El requisito previo para comenzar con este tutorial es que tiene una cuenta de Teams que permite [la descarga lateral de la aplicación.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

![generador yeoman git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Configure y prepare su máquina

Debe instalar lo siguiente en su máquina antes de empezar a utilizar el generador Yeoman.

### <a name="install-nodejs"></a>Instalar Node.js

Debe tener Node.js instalado en su máquina. Debe utilizar la [versión lts](https://nodejs.org)más reciente .

### <a name="install-a-code-editor"></a>Instalar un editor de código

Necesitas un editor de código. La mayor parte de esta documentación e imágenes hacen referencia al uso [de Visual Studio Code](https://code.visualstudio.com). Sin embargo, siéntase libre de usar cualquier editor de texto que prefiera.

### <a name="install-yeoman-and-gulp-cli"></a>Instalan CLI de Yeoman y Gulp

Para andamios que utilizan el generador, debe instalar la herramienta Yeoman y el administrador de tareas de la CLI de Gulp.

Abra un símbolo del sistema y escriba lo siguiente:

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>Instale el generador

Instale el generador de Teams Yeoman con el siguiente comando:

```bash
npm install generator-teams --global
```

Instale la versión preliminar del generador con el siguiente comando:

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Generar su proyecto

En esta sección se recorren los pasos para generar el proyecto.

**Para generar el proyecto**

1. Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto y en ese directorio ejecute el comando `yo teams` . El generador se inicia.
1. Responda al conjunto de preguntas planteadas por el generador:

   ![yo equipos](~/assets/yeoman-images/teams-first-app-1.png)

   1. La primera pregunta es sobre el nombre del proyecto, puede dejarlo tal cual pulsando Intro.
   1. La siguiente pregunta le pregunta si desea crear un nuevo directorio o utilizar el actual. Como ya está en el directorio que desee, simplemente presione entrar.
   1. En la siguiente pregunta, escriba el título del proyecto. Este título se usará en el manifiesto y la descripción de la aplicación. 
   1. A continuación, se le pedirá un nombre de empresa, que también se utilizará en el manifiesto.
   1. La quinta pregunta le pregunta sobre qué versión del manifiesto desea utilizar. Para este tutorial seleccione `v1.5` , que es el esquema general disponible actual.
   1. A continuación, el generador le preguntará qué elementos desea agregar a su proyecto. Puede seleccionar uno solo o cualquier combinación de elementos. Para estos tutoriales, simplemente seleccione *una pestaña:*

    ![selección de artículos](~/assets/yeoman-images/teams-first-app-2.png)

1. Responda al siguiente conjunto de preguntas de seguimiento que aparecen en función de los elementos seleccionados en el paso 2.
1. Escriba una dirección URL de donde hospedará la solución. 

   > [!NOTE]
   > La dirección URL puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL del sitio web de Azure.

1. En la siguiente pregunta, confirme si desea incluir pruebas unitarias para la solución. La respuesta predeterminada es *sí*. Si decide incluir pruebas unitarias, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se están scaffolded. 
   > [!NOTE]
   > * Para este tutorial, elija no incluir un marco de trabajo de prueba.
   > * El generador tiene una gran cantidad de características avanzadas incorporadas que puede optar por participar o optar por no participar.

1. Para facilitarle la iniciación de sesión, también se le preguntará si desea usar Azure Application Insights para iniciar sesión. Si elige *Sí,* deberá proporcionar una clave de Azure Application Insights. 

   > [!NOTE]
   > Para este tutorial, opte por no usar Application Insights.

El siguiente conjunto de preguntas se basará en los elementos previamente seleccionados. Para una pestaña sólo necesita proporcionar un nombre y opcionalmente elegir si desea poder usar esta aplicación como un elemento web SharePoint en línea. Después de proporcionar el nombre, el generador generará el proyecto e instalará todas las dependencias. Esto tomará uno o dos minutos.

## <a name="add-some-code-to-your-tab"></a>Agregue código a su pestaña

Una vez hecho el generador puede abrir la solución en su editor de código favorito. Tómese uno o dos minutos y familiarícese con cómo se organiza el código. Para obtener más información, consulte [Project documentación de estructura.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)

La pestaña está en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo. Esta es la clase basada en React TypeScript para la pestaña. Busque el `render()` método y agregue una línea de código dentro del control para que tenga este `<PanelBody>` aspecto:

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Guarde el archivo y vuelva al símbolo del sistema.

## <a name="build-your-app"></a>Crear una aplicación

Ahora puede compilar el proyecto. Esto se hace en dos pasos (o un paso, ver abajo).

Primero debe crear el archivo de manifiesto de aplicación Teams, que cargue/descargue lateralmente en Microsoft Teams. Esto es hecho por la tarea `gulp manifest` Gulp. Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.

Para crear la solución, utilice el `gulp build` comando. Esto transpilará la solución en la `./dist` carpeta. 

## <a name="run-your-app"></a>Ejecute la aplicación

Para ejecutar la aplicación se usa el `gulp serve` comando. Esto creará e iniciará un servidor web local para que pruebe la aplicación. El comando también reconstruirá la aplicación cada vez que guarde un archivo en el proyecto. 

Ahora debería poder buscar `http://localhost:3007/myFirstAppTab/` para asegurarse de que la pestaña se está representando. Sin embargo, aún no está en Microsoft Teams:

![ver su sitio en un navegador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Ejecute la aplicación en Microsoft Teams

Microsoft Teams no permite que la aplicación se hospede en localhost, por lo que debe publicarla en una dirección URL pública o usar un proxy como ngrok.

La buena noticia es que el proyecto de andamios tiene este incorporado. Cuando ejecute `gulp ngrok-serve` el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp serve` .

Después de ejecutar `gulp ngrok-serve` , cree un nuevo equipo de Microsoft Teams y cuando se cree haga clic en el nombre del equipo, para ir a la configuración de los equipos y, a continuación, seleccione *Aplicaciones*. En la esquina inferior derecha debería ver un vínculo *Upload una aplicación personalizada,* selecciónelo y, a continuación, vaya a la carpeta del proyecto y a la subcarpeta denominada `package` . Seleccione el archivo zip en esa carpeta y elija abrir. La aplicación ahora está descargada lateralmente en Microsoft Teams:

![aplicación descargada lateralmente](~/assets/yeoman-images/teams-first-app-4.png)

Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debería ver su pestaña en la lista de pestañas:

![configurar la pestaña](~/assets/yeoman-images/teams-first-app-5.png)

Elige tu pestaña y sigue las instrucciones para agregarla. Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizado, para el que puede editar el origen. Seleccione *Guardar* para agregar la pestaña al canal. Una vez hecho su pestaña debe ser cargado dentro de Microsoft Teams!

![correr ficha en equipos](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>Actualizar Microsoft Teams

También puede actualizar su versión actual Microsoft Teams a la última versión utilizando el generador Microsoft Teams Yeoman.

**Para actualizar Microsoft Teams**

1. Obtenga la versión actual de Teams con el siguiente comando:

   ```PowerShell
    yo teams --version
   ```
2. Utilice el siguiente comando para seleccionar actualizar el generador:

   ```PowerShell
    yo
   ```
3. Utilice las teclas de flecha para elegir **Actualizar sus generadores:**

   ![imagen de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. Seleccione el generador que desea de la lista de generadores:
   > [!NOTE]
   > Utilice la barra espaciadora para seleccionar o borrar una versión Teams seleccionada de las opciones disponibles.

    ![imagen de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > La instalación de Teams tarda unos segundos en completarse.

5. Una vez completada la instalación, utilice el siguiente comando para comprobar la versión instalada:

   ```PowerShell
    yo teams --version
   ```
   
**¡Felicidades! Creó e implementó la primera aplicación de Microsoft Teams. También ha actualizado Microsoft Teams.**
