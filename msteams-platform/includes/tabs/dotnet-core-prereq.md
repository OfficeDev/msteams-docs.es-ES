## <a name="prerequisites"></a>Requisitos previos

- Para completar este inicio rápido, necesitarás un inquilino Microsoft 365 y un equipo configurado con Permitir cargar *aplicaciones personalizadas* habilitadas. Para obtener más información, vea [Prepare your Microsoft 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).
  - Si actualmente no tiene una cuenta Microsoft 365, puede registrarse para obtener una suscripción gratuita a través del Programa [para desarrolladores de Microsoft](https://developer.microsoft.com/en-us/microsoft-365/dev-program). La suscripción permanecerá activa mientras la estés usando para el desarrollo continuo.

- Usarás App Studio para importar la aplicación a Teams. Para instalar App Studio, selecciona **Aplicación** de la Tienda de aplicaciones en la esquina inferior izquierda de la aplicación Teams y busca ![ App ](~/assets/images/tab-images/storeApp.png) Studio. Una vez que encuentre el icono, selecciónelo y elija instalarlo en el cuadro de diálogo de la ventana emergente.

Además, este proyecto requiere que tenga lo siguiente instalado en el entorno de desarrollo:

- La versión actual del Visual Studio IDE con la carga de trabajo de desarrollo **multiplataforma .NET CORE** instalada. Si aún no tienes Visual Studio, puedes descargar e instalar la última [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) versión gratuita.

- La herramienta de proxy [inverso ngrok.](https://ngrok.com) Usará ngrok para crear un túnel para los puntos de conexión HTTPS del servidor web que se ejecuta localmente. Puede [descargarlo aquí](https://ngrok.com/download).
