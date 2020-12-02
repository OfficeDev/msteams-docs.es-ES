1. En [Azure Portal](https://ms.portal.azure.com/#home), en servicios de Azure, seleccione **Crear un recurso**.
1. Escriba «bot» en el cuadro de búsqueda. Y en la lista desplegable, seleccione **Registro de canales de bot**.
1. Seleccione el botón **Crear**.
1. En la hoja de **Registro de canal de bot**, proporcione la información solicitada sobre el bot.
1. Por ahora, deje en blanco el cuadro de **Punto de conexión de mensajería**. Escribirá la dirección URL requerida después de implementar el bot. La siguiente imagen muestra un ejemplo de la configuración de registro:

    ![registro de canales de aplicaciones de bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Haga clic en **Identificador de aplicación de Microsoft y contraseña** y, a continuación, en **Crear nuevo**.

    ![Crear un identificador de aplicación de Microsoft](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Crear un nuevo identificador de aplicación de Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. Haga clic en el enlace de **Crear un identificador de aplicación en el portal de registro de aplicaciones**.

   ![Registro de aplicaciones](../../assets/images/authentication/AppRegistration.png)
   
1. En la ventana de **Registro de la aplicaciones** que se muestra, haga clic en la pestaña **Nuevo registro** de la parte superior izquierda.
1. Escriba el nombre de la aplicación de bot que está registrando. Hemos usado *BotTeamsAuth* (usted deberá seleccionar su propio nombre único).
1. Para los **Tipos de cuenta admitidos**, seleccione *Cuentas en cualquier directorio organizativo (cualquier directorio de Azure AD - Multiinquilino) y cuentas personales de Microsoft (por ejemplo, Skype o Xbox)*.
1. Haga clic en el botón de **Registro**. Cuando haya finalizado, Azure mostrará la página de *Información general* de la aplicación.
1. Copie y guarde en un archivo el valor del **Id. (cliente) de la aplicación**.
1. En el panel izquierdo, haga clic en **Certificado y secretos**.
    1. En *Secretos de cliente*, haga clic en **Nuevo secreto de cliente**.
    1. Agregue una descripción para identificar este secreto respecto a otros que pueda necesitar crear para esta aplicación.
    1. Establezca la *Caducidad* respecto a la selección.
    1. Haga clic en **Agregar**.
    1. Copie el secreto de cliente y guárdelo en un archivo.
1. Vuelva a la ventana de **Registro de canal de bot** y copie el *Id. de aplicación* y el *Secreto de cliente* en los cuadros **Identificador de aplicación de Microsoft** y **Contraseña**, respectivamente.
1. Haga clic en **Aceptar**.
1. Por último, haga clic en **Crear**.

Cuando Azure haya creado el recurso de registro, se incluirá en la lista de grupos de recursos.  

![grupo de registro de canales de aplicaciones de bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

Una vez que se haya creado el registro de canales de bot, tendrá que habilitar el canal de Teams.

1. En el [Microsoft Azure Portal](https://ms.portal.azure.com/#home), en servicios de Azure, seleccione el **Registro de canal de bot** que acaba de crear.
1. En el panel izquierdo, haga clic en **Canales**.
1. Haga clic en el icono de Microsoft Teams y elija **Guardar**.
