## <a name="prerequisites"></a>Requisitos previos

- Para completar este tutorial, necesitará un inquilino de Office 365 y un equipo configurado con la *opción permitir la carga de aplicaciones personalizadas* habilitada. Para obtener más información, vea [preparar el inquilino de Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).
  - Si actualmente no tiene una cuenta de Office 365, puede registrarse para obtener una suscripción gratuita a través del [programa de desarrolladores de office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program). La suscripción permanecerá activa siempre que la use para el desarrollo continuado.

- Usará App Studio para importar la aplicación a Microsoft Teams. Para instalar App Studio, **** ![seleccione aplicación](~/assets/images/tab-images/storeApp.png) de la tienda de aplicaciones en la esquina inferior izquierda de la aplicación Teams y busque App Studio. Una vez que encuentre el icono, selecciónelo y elija instalar en el cuadro de diálogo ventana emergente.

Además, este proyecto requiere que tenga instalado lo siguiente en el entorno de desarrollo:

- La versión actual del IDE de Visual Studio con la carga de trabajo **multiplataforma del núcleo de .net** instalada. Si todavía no tiene Visual Studio, puede descargar e instalar la versión más reciente de la [comunidad de Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) de forma gratuita.

- La herramienta de proxy inverso de [ngrok](https://ngrok.com) . Usará ngrok para crear un túnel a los puntos de conexión HTTPS del servidor Web que se ejecutan de forma local. Puede [descargarla aquí](https://ngrok.com/download).
