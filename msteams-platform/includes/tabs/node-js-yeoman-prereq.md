## <a name="prerequisites"></a>Requisitos previos

- Para completar esta iniciación rápida necesitará un inquilino Office 365 y un equipo configurado con *Permitir cargar aplicaciones personalizadas* habilitadas. Para obtener más información, consulte [Preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

  - Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción gratuita a través del Programa de desarrollador Office 365. La suscripción permanecerá activa mientras la use para el desarrollo continuo. Consulte [Bienvenido al Programa para desarrolladores de Office 365](/office/developer-program/microsoft-365-developer-program).

Además, este proyecto requiere que tenga instalado lo siguiente en el entorno de desarrollo:

- Cualquier editor de texto o IDE. Puede instalar y utilizar [Visual Studio Code](https://code.visualstudio.com/download) de forma gratuita.

- [Node.js/npm](https://nodejs.org/en/). Debe utilizar la versión lts más reciente. El nodo Administrador de paquetes (npm) se instalará en el sistema con la instalación de Node.js.

- Después de instalar correctamente Node.js, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:

    ```bash
    npm install yo gulp-cli --global
    ```

- Instale el generador de aplicaciones de Microsoft Teams escribiendo lo siguiente en el símbolo del sistema:

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a>Generar su proyecto

- Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.

- Para iniciar el generador, vaya al nuevo directorio y escriba el siguiente comando:

    ```bash
    yo teams
    ```

- A continuación, proporcionará una serie de valores que se usarán en **lamanifest.js** de archivo de la aplicación:

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **¿Cómo se llama su solución?**

    Este es el nombre del proyecto. Puede aceptar el nombre sugerido pulsando Intro.

    **¿Dónde desea ubicar los archivos?**

    Actualmente se encuentra en el directorio del proyecto. Pulse Intro.

    **¿El título del proyecto de la aplicación Microsoft Teams?**

    Este es el nombre del paquete de la aplicación y se usará en el manifiesto y la descripción de la aplicación.

    **¿Su nombre (de la compañía)? (máximo 32 caracteres)**

    El nombre de su empresa se usará en el manifiesto de la aplicación.

    **¿Qué versión de manifiesto le gustaría usar?**

    Seleccione el esquema predeterminado.

    **¿Andamios rápidos? (Y/n)**

    El valor predeterminado es sí; **escriba n** para introducir el Identificador de socio de Microsoft.

    **Escriba su Id de socio de Microsoft, si tiene uno? (Deje en blanco para omitir)**

    Este campo no es obligatorio y solo se debe usar si ya forma parte de [Microsoft Partner Network.](https://partner.microsoft.com)

    **¿Qué desea agregar a su proyecto?**

    Seleccione ( &ast; ) Una pestaña.

    **¿La dirección URL donde hospedará esta solución?**

    De forma predeterminada, el generador sugiere una dirección URL de sitios Web de Azure. Solo probará la aplicación localmente, por lo tanto, no es necesaria una dirección URL válida para completar esta guía de inicio rápido.

    **¿Desea incluir el marco de trabajo de prueba y las pruebas iniciales? (y/N)**

    Elija **no** incluir un marco de trabajo de prueba para este proyecto. El valor predeterminado es sí; entrar **n**.

    **¿Desea usar Azure Applications Insights para telemetría? (y/N)**

    Elija **no** incluir [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md). El valor predeterminado es no; entrar **n**.

    **¿Nombre de tabulación predeterminado (máx. 16 caracteres)?**

    Nombra tu pestaña. Este nombre de pestaña se utilizará en todo el proyecto como un componente de ruta de acceso de archivo/URL.
