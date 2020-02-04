## <a name="prerequisites"></a>Requisitos previos

- Para completar este tutorial, necesitará un inquilino de Office 365 y un equipo configurado con la *opción permitir la carga de aplicaciones personalizadas* habilitada. Para obtener más información, vea [preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

  - Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción gratuita a través del programa de desarrolladores de Office 365. La suscripción permanecerá activa siempre que la use para el desarrollo continuado. Vea [Bienvenido al programa de desarrolladores de Office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).

Además, este proyecto requiere que tenga instalado lo siguiente en el entorno de desarrollo:

- Cualquier editor de texto o IDE. Puede instalar y usar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.

- [Node. js/NPM](https://nodejs.org/en/). Debe usar la última versión de LTS. El administrador de paquetes de nodos (NPM) se instalará en el sistema con la instalación de node. js.

- Después de instalar correctamente node. js, instale los paquetes [Yeoman](https://yeoman.io/) y [Gulp-CLI](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:

```bash
npm install yo gulp-cli --global
```

- Para instalar el generador de aplicaciones de Microsoft Teams, escriba lo siguiente en el símbolo del sistema:

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a>Generar el proyecto

- Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestañas.

- Para iniciar el generador, navegue hasta el nuevo directorio y escriba el siguiente comando:

```bash
yo teams
```

- A continuación, deberá proporcionar una serie de valores que se usarán en el archivo **manifest. JSON** de la aplicación:

![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

**¿Cuál es el nombre de la solución?**

Este es el nombre del proyecto. Puede aceptar el nombre sugerido; para ello, presione Entrar.

**¿Dónde desea ubicar los archivos?**

Actualmente está en el directorio del proyecto. Presione entrar.

**¿El título del proyecto de la aplicación de Microsoft Teams?**

Este es el nombre del paquete de la aplicación y se usará en el manifiesto de la aplicación y la descripción.

**El nombre de la (empresa)? (máximo 32 caracteres)**

El nombre de la compañía se usará en el manifiesto de la aplicación.

<br>**¿Qué versión de manifiesto desearía usar?**

Seleccione el esquema predeterminado.

**Escriba su identificador de socio de Microsoft, si tiene uno? (Déjelo en blanco para omitir)**

Este campo no es necesario y solo debe usarse si ya forma parte de la [red de asociados de Microsoft](https://partner.microsoft.com).

**¿Qué desea agregar al proyecto?**

Seleccione ( &ast; ) una tabulación.

**La dirección URL en la que va a hospedar esta solución?**

De forma predeterminada, el generador sugiere una dirección URL de sitios web de Azure. Solo va a probar la aplicación de forma local, por lo tanto, no es necesaria una dirección URL válida para completar este inicio rápido.

**¿Le gustaría incluir el marco de pruebas y las pruebas iniciales? (s/N)**

Elija **no** incluir un marco de pruebas para este proyecto. El valor predeterminado es sí; Escriba **n**.

**¿Desea usar las aplicaciones de Azure Insights para telemetría? (s/N)**

Elija **no** incluir [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md). El valor predeterminado es no; Escriba **n**.

**Nombre de pestaña predeterminado (16 caracteres como máximo)?**

Asigne un nombre a la pestaña. Este nombre de la pestaña se usará en el proyecto como un componente de ruta de acceso de archivo o dirección URL.
