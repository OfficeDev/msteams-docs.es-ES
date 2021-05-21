## <a name="prerequisites"></a>Requisitos previos

- Para completar esta guía de inicio rápido, necesitará un inquilino Office 365 y un equipo configurado con *Permitir cargar aplicaciones personalizadas* habilitadas. Para obtener más información, vea [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).

  - Si actualmente no tiene una cuenta Office 365, puede registrarse para obtener una suscripción gratuita a través del programa Office 365 desarrolladores. La suscripción permanecerá activa mientras la estés usando para el desarrollo continuo. Vea [Welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).

Además, este proyecto requiere que tenga lo siguiente instalado en el entorno de desarrollo:

- Cualquier editor de texto o IDE. Puede instalar y [usar](https://code.visualstudio.com/download) Visual Studio Code de forma gratuita.

- [Node.js/npm](https://nodejs.org/en/). Debe usar la versión lts más reciente. El nodo Administrador de paquetes (npm) se instalará en el sistema con la instalación de Node.js.

- Después de instalar correctamente Node.js, instale los paquetes [Yeoman](https://yeoman.io/) y [gulp-cli](https://www.npmjs.com/package/gulp-cli) escribiendo lo siguiente en el símbolo del sistema:

    ```bash
    npm install yo gulp-cli --global
    ```

- Instale el generador Microsoft Teams aplicaciones escribiendo lo siguiente en el símbolo del sistema:

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a>Generar el proyecto

- Abra un símbolo del sistema y cree un nuevo directorio para el proyecto de pestaña.

- Para iniciar el generador, vaya al nuevo directorio y escriba el siguiente comando:

    ```bash
    yo teams
    ```

- A continuación, proporcionará una serie de valores que se usarán en el archivo demanifest.js **aplicación:**

    ![captura de pantalla de apertura del generador](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **¿Cuál es el nombre de la solución?**

    Este es el nombre del proyecto. Puede aceptar el nombre sugerido presionando entrar.

    **¿Dónde desea ubicar los archivos?**

    Actualmente está en el directorio del proyecto. Presione ENTRAR.

    **¿Título de tu Microsoft Teams de aplicación?**

    Este es el nombre del paquete de la aplicación y se usará en el manifiesto y la descripción de la aplicación.

    **¿Su nombre (empresa)? (máximo 32 caracteres)**

    El nombre de la empresa se usará en el manifiesto de la aplicación.

    **¿Qué versión de manifiesto le gustaría usar?**

    Seleccione el esquema predeterminado.

    **¿Scaffolding rápido? (Y/n)**

    El valor predeterminado es sí; escriba **n** para escribir su Id. de partner de Microsoft.

    **Escriba su id. de partner de Microsoft, si tiene uno. (Dejar en blanco para omitir)**

    Este campo no es obligatorio y solo debe usarse si ya forma parte de [la red de partners de Microsoft](https://partner.microsoft.com).

    **¿Qué desea agregar al proyecto?**

    Seleccione ( &ast; ) Una pestaña.

    **¿La dirección URL donde hospedará esta solución?**

    De forma predeterminada, el generador sugiere una dirección URL de Sitios web de Azure. Solo probarás tu aplicación localmente, por lo tanto, no es necesaria una dirección URL válida para completar esta guía de inicio rápido.

    **¿Desea incluir el marco de pruebas y las pruebas iniciales? (y/N)**

    Elija **no incluir** un marco de prueba para este proyecto. El valor predeterminado es sí; escriba **n**.

    **¿Desea usar Azure Applications Insights para telemetría? (y/N)**

    Elija **no incluir** Azure Application [Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md). El valor predeterminado es no; escriba **n**.

    **Nombre de tabulación predeterminado (máximo 16 caracteres)?**

    Asigne un nombre a la pestaña. Este nombre de pestaña se usará en todo el proyecto como un componente de ruta de acceso de archivo/dirección URL.
