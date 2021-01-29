---
title: 'Tutorial: crear la primera aplicación con el generador de Yeoman'
description: Obtenga información sobre cómo empezar a compilar aplicaciones de Microsoft Teams con el generador de Yeoman.
keywords: introducción a node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037007"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Crear la primera aplicación de Microsoft Teams con el generador de Yeoman

>[!Note]
>Este tutorial procede del generador [de Yeoman para la wiki de Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

En este tutorial, le mostraremos cómo crear su primera aplicación de Microsoft Teams con el generador de Yeoman de Microsoft Teams. Se supone que tiene una cuenta de Teams que permite [la instalación de prueba de la aplicación.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

![yeoman generator git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Configurar y preparar el equipo

Debes instalar lo siguiente en el equipo antes de empezar a usar el generador de Yeoman.

### <a name="install-nodejs"></a>Instalar Node.js

Debes tener Node.js instalado en el equipo. Debe usar la versión más reciente [de LTS](https://nodejs.org).

### <a name="install-a-code-editor"></a>Instalar un editor de código

También necesitas un editor de código, no dudes en usar el editor de texto que prefieras. Sin embargo, la mayoría de esta documentación y capturas de pantalla hacen referencia al [uso Visual Studio código.](https://code.visualstudio.com)

### <a name="install-yeoman-and-gulp-cli"></a>Instalar la CLI de Yeoman y Gulp

Para poder realizar scaffolding en proyectos con el generador de Teams, debe instalar la herramienta Yeoman, así como el administrador de tareas de la CLI de Gulp.

Abra un símbolo del sistema y escriba lo siguiente:

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>Instalar el generador

Instale el generador de Yeoman de Teams con el siguiente comando:

```bash
npm install generator-teams --global
```

Para instalar versiones preliminares del generador, ejecute este comando:

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Generar el proyecto

Abra un símbolo del sistema y cree un directorio donde quiera crear el proyecto y, en ese directorio, ejecute el `yo teams` comando.

Esto inicia el generador, que le pedirá un conjunto de preguntas.

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

La primera pregunta es sobre el nombre del proyecto, puede dejarlo tal como está presionando ENTRAR. La siguiente pregunta le pregunta si desea crear un nuevo directorio o usar el actual. Como ya estamos en el directorio que queremos, simplemente presionamos ENTRAR.

En el siguiente paso se pide un título del proyecto, este título se usará en el manifiesto y la descripción de la aplicación. Y, a continuación, se le pedirá un nombre de compañía, que también se usará en el manifiesto.

La quinta pregunta le pregunta qué versión del manifiesto desea usar. Para este tutorial, seleccione `v1.5` , que es el esquema disponible general actual.

Después, el generador le preguntará qué elementos desea agregar a su proyecto. Puede seleccionar una sola o cualquier combinación de elementos. Por ahora, solo tiene que *seleccionar una pestaña*.

![selección de elemento](~/assets/yeoman-images/teams-first-app-2.png)

En función de los elementos que seleccione, se le hará un conjunto de preguntas de seguimiento.

Ahora debe escribir una dirección URL donde hospedará la solución. Puede ser cualquier dirección URL, pero de forma predeterminada el generador sugiere una dirección URL de Sitios web de Azure.

El generador tiene una gran cantidad de características avanzadas integradas que puede optar por participar o no participar. Si sigue la pregunta de dirección URL que se le hará si desea incluir pruebas unitarias para la solución, el valor predeterminado es sí. Si eliges esto, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding. Para este tutorial, elija no incluir un marco de prueba.

Para facilitar el registro, también se le preguntará si desea usar Azure Application Insights para el registro. Si elige Sí, deberá proporcionar una clave de Azure Application Insights. En este tutorial no se puede usar Application Insights.

El siguiente conjunto de preguntas se basará en la selección de elementos previamente. Para una pestaña solo necesita proporcionar un nombre y, opcionalmente, elegir si desea poder usar esta aplicación como un elemento web de SharePoint Online. Una vez que haya proporcionado este nombre, el generador generará el proyecto e instalará todas las dependencias. Esto puede tardar uno o dos minutos.

## <a name="add-some-code-to-your-tab"></a>Agregar código a la pestaña

Una vez que haya terminado el generador, puede abrir la solución en su editor de código favorito. Tómese uno o dos minutos y familiarícese con cómo se organiza el código; puede leer más sobre esto en la documentación de la estructura [del](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) proyecto.

La pestaña se encontrará en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo. Esta es la clase basada en TypeScript React para la pestaña. Busque el método y agregue una línea de código dentro del control para que se vea `render()` `<PanelBody>` así:

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Guarde el archivo y vuelva al símbolo del sistema.

## <a name="build-your-app"></a>Crear una aplicación

Ahora puede compilar el proyecto. Esto se realiza en dos pasos (o un paso, consulta a continuación).

En primer lugar, debe crear el archivo de manifiesto de la aplicación de Teams que cargue o cargue localmente en Microsoft Teams. Esto se realiza mediante la tarea de Gulp `gulp manifest` . Esto validará el manifiesto y creará un archivo zip en el `./package` directorio.

Para crear la solución, use el `gulp build` comando. Esto transpilará la solución en la `./dist` carpeta. 

## <a name="run-your-app"></a>Ejecutar la aplicación

Para ejecutar la aplicación, usas el `gulp serve` comando. Esto compilará e iniciará un servidor web local para que pruebe la aplicación. El comando también volverá a generar la aplicación siempre que guarde un archivo en el proyecto. 

Ahora debería poder explorar para asegurarse de `http://localhost:3007/myFirstAppTab/` que se está representando la pestaña. Sin embargo, aún no está en Microsoft Teams.

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Ejecutar la aplicación en Microsoft Teams

Microsoft Teams no le permite tener la aplicación hospedada en localhost, por lo que necesita publicarla en una dirección URL pública o usar un proxy como ngrok.

Una buena noticia es que el proyecto con scaffolding tiene esto integrado. Cuando ejecute el servicio ngrok se iniciará en segundo plano, con una entrada DNS única y pública, y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará exactamente lo mismo que `gulp ngrok-serve` `gulp serve` .

Después de ejecutar , cree un nuevo equipo de Microsoft Teams y, cuando se cree, haga clic en el nombre del equipo, para ir a la configuración de teams y, `gulp ngrok-serve` a continuación, *seleccione Aplicaciones.* En la esquina inferior derecha debería ver un vínculo Cargar una aplicación personalizada, selecciónelo y, a continuación, vaya *a* la carpeta del proyecto y a la subcarpeta llamada `package` . Seleccione el archivo zip de esa carpeta y elija Abrir. La aplicación ahora se ha instalado localmente en Microsoft Teams.

![aplicación de instalación de local](~/assets/yeoman-images/teams-first-app-4.png)

Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debería ver la pestaña en la lista de pestañas.

![pestaña configurar](~/assets/yeoman-images/teams-first-app-5.png)

Elija la pestaña y siga las instrucciones para agregarla. Observe que tiene un cuadro de diálogo de configuración personalizado para el que puede editar el origen. Seleccione *Guardar* para agregar la pestaña al canal. Una vez que haya terminado, la pestaña debe cargarse dentro de Microsoft Teams.

![ejecutar pestaña en teams](~/assets/yeoman-images/teams-first-app-6.png)

**¡Congraciaciones! Ha creado e implementado su primera aplicación de Microsoft Teams**
