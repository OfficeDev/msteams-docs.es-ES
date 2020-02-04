---
title: Introducción al generador de Yeoman para Microsoft Teams
description: Empezar a compilar excelentes aplicaciones con el generador de Yeoman para Microsoft Teams
keywords: nodo introducción. js NodeJS Yeoman
ms.openlocfilehash: b0a9ae8d526286790d266e4291ef95d4ed7ce90f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675895"
---
# <a name="build-your-first-microsoft-teams-app"></a>Compilar la primera aplicación de Microsoft Teams

>[!Note]
>Este tutorial proviene del [generador de Yeoman para Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

En este tutorial, veremos cómo crear su primera aplicación de Microsoft Teams con el generador de Yeoman de Microsoft Teams. Se da por hecho que ha [habilitado la carga del lado de las aplicaciones de Microsoft Teams](~/concepts/build-and-test/prepare-your-o365-tenant.md).

![git del generador de Yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Configurar y preparar el equipo

Debe instalar lo siguiente en su equipo antes de empezar a usar el generador de equipos.

### <a name="install-node"></a>Nodo de instalación

Debe tener NodeJS instalado en el equipo. Debe usar la última [versión de lts](https://nodejs.org/dist/latest-v8.x/).

### <a name="install-a-code-editor"></a>Instalar un editor de código

También necesita un editor de código, no dude en usar el editor de texto que prefiera. Sin embargo, la mayoría de esta documentación y capturas de pantallas hacen referencia al uso de [Visual Studio Code](https://code.visualstudio.com).

### <a name="install-yeoman-and-gulp-cli"></a>Instalar Yeoman y CLI de Gulp

Para poder aplicar scaffolding a los proyectos con el generador de Teams, debe instalar la herramienta Yeoman y el administrador de tareas de Gulp CLI.

Abra un símbolo del sistema y escriba lo siguiente:

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a>Instalar el generador de aplicaciones de Microsoft Teams-yo Teams

El generador de Yeoman para las aplicaciones de Microsoft Teams se instala con el siguiente comando:

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a>Instalar versiones preliminares

Si desea instalar versiones preliminares del generador de equipos con este comando:

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Generar el proyecto

Abra un símbolo del sistema y cree un nuevo directorio donde desee crear el proyecto y, en ese directorio, escriba el comando `yo teams`. Se iniciará el generador de aplicaciones de Microsoft Teams y se le preguntará un conjunto de preguntas.

![Yo Teams](~/assets/yeoman-images/teams-first-app-1.png)

La primera pregunta trata sobre el nombre del proyecto, puede dejarlo como está presionando entrar. La siguiente pregunta le preguntará si desea crear un nuevo directorio o usar el actual. Como ya se encuentra en el directorio que queremos, simplemente se presiona la tecla entrar.

En el paso siguiente se solicita un título del proyecto, este título se utilizará en el manifiesto y la descripción de la aplicación. Y, a continuación, se le pedirá el nombre de la compañía, que también se usará en el manifiesto.

La quinta pregunta le pregunta qué versión del manifiesto desea usar. Para este tutorial, `v1.5`seleccione, que es el esquema actual disponible en general.

Después de esto, el generador le pedirá qué elementos desea agregar a su proyecto. Puede seleccionar una sola combinación de elementos o una combinación de ellos. Por ahora, solo tiene que seleccionar *una pestaña*.

![selección de elementos](~/assets/yeoman-images/teams-first-app-2.png)

En función de los elementos que seleccione, se le preguntará un conjunto de preguntas de seguimiento.

Ahora debe escribir una dirección URL donde hospedará la solución. Puede ser cualquier dirección URL, pero, de forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure.

El generador tiene muchas características avanzadas integradas que puede incluir o excluir de ellas. Tras la pregunta de dirección URL se le preguntará si desea incluir pruebas unitarias para su solución, de forma predeterminada es sí. Si elige esta opción, el proyecto generado tendrá un marco de pruebas unitarias y algunas pruebas unitarias predeterminadas para los distintos elementos que se van a scaffolding. Para este tutorial, elija no incluir un marco de prueba.

Para que el registro sea más fácil, también se le preguntará si quiere usar Azure Application Insights para el registro. Si elige sí, tendrá que proporcionar una clave de Azure Application Insights. Para este tutorial, rechace la utilización de Application Insights.

El siguiente conjunto de preguntas se basará en la selección de elementos anteriormente. Para una pestaña solo tiene que proporcionar un nombre y, opcionalmente, elegir si desea poder usar esta aplicación como un elemento Web de SharePoint Online. Una vez que haya proporcionado el nombre, el generador generará el proyecto e instalará todas las dependencias. Esto tardará un minuto o dos.

## <a name="add-some-code-to-your-tab"></a>Agregar código a la pestaña

Una vez que el generador haya finalizado, podrá abrir la solución en su editor de código favorito. Tómese un minuto o dos y familiarícese con cómo se organiza el código: puede obtener más información sobre esto en la documentación sobre la [estructura del proyecto](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) .

La pestaña se ubicará en el `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` archivo. Esta es la clase basada en TypeScript reAct para su pestaña. busque `render()` el método y agregue una línea de código dentro `<PanelBody>` del control para que tenga el siguiente aspecto:

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Guarde el archivo y vuelva a la línea de comandos.

## <a name="build-your-app"></a>Crear una aplicación

Ahora puede compilar el proyecto. Esto se realiza en dos pasos (o un paso, vea a continuación).

En primer lugar, debe crear el archivo de manifiesto de la aplicación Teams, que carga o transferir localmente a Microsoft Teams. Esto se realiza mediante la tarea `gulp manifest`de Gulp. Se validará el manifiesto y se creará un archivo zip `./package` en el directorio.

Para compilar la solución, `gulp build` use el comando. Se transpilará la solución a la `./dist` carpeta. 

## <a name="run-your-app"></a>Ejecutar la aplicación

Para ejecutar la aplicación, use el `gulp serve` comando. Se compilará e iniciará un servidor Web local para que pueda probar la aplicación. El comando también volverá a generar la aplicación cada vez que guarde un archivo en el proyecto. 

Ahora debería poder ir a `http://localhost:3007/myFirstAppTab/` para asegurarse de que la pestaña está en representación. Sin embargo, aún no en Microsoft Teams.

![ver el sitio en un explorador](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Ejecutar la aplicación en Microsoft Teams

Microsoft Teams no le permite hospedar la aplicación en localhost, por lo que debe publicarla en una dirección URL pública o usar un proxy como ngrok.

Una buena noticia es que el proyecto con scaffolding tiene esta integrado. Al ejecutar `gulp ngrok-serve` el servicio ngrok, se iniciará en segundo plano, con un único y una entrada DNS pública, y también empaquetará el manifiesto con esa dirección URL única y, a continuación, hará `gulp serve`exactamente lo mismo que.

Una vez `gulp ngrok-serve`ejecutado, cree un nuevo equipo de Microsoft Teams y, cuando se haya creado, haga clic en el nombre del equipo, vaya a la configuración de Microsoft Teams y seleccione *aplicaciones*. En la esquina inferior derecha, debería ver un vínculo *cargar una aplicación personalizada*, seleccionarla y, a continuación, buscar la carpeta del proyecto y la `package`subcarpeta denominada. Seleccione el archivo zip en esa carpeta y elija Abrir. La aplicación ahora se transferirá a Microsoft Teams.

![aplicación transferida localmente](~/assets/yeoman-images/teams-first-app-4.png)

Vuelva al canal *General* y seleccione *+* agregar una nueva pestaña. Debe ver la ficha en la lista de pestañas.

![pestaña configurar](~/assets/yeoman-images/teams-first-app-5.png)

Elija su pestaña y siga las instrucciones para agregarlo. Tenga en cuenta que tiene un cuadro de diálogo de configuración personalizada, para el que puede editar el origen. Seleccione *Guardar* para agregar su pestaña al canal. Una vez que haya terminado, la pestaña debe estar cargada en Microsoft Teams.

![pestaña en ejecución en Microsoft Teams](~/assets/yeoman-images/teams-first-app-6.png)

**Congrats! Ha compilado e implementado su primera aplicación de Microsoft Teams**
