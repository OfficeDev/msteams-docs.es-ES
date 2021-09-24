## <a name="upload-your-tab-with-app-studio"></a>Upload pestaña con App Studio

>[!NOTE]
> Usamos **App Studio** para editar el archivomanifest.js **y** cargar el paquete completado en Teams. También puede editar manualmentemanifest.js **en**. Si lo hace, asegúrese de volver a crear la solución para crear el **archivoTab.zip** cargar.

**Para cargar la pestaña con App Studio**

1. Vaya a Microsoft Teams. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)

1. Ve a **App Studio** y selecciona la pestaña Editor **de manifiestos.**

1. Selecciona **Importar una aplicación existente en** el editor de **manifiestos** para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo. El nombre del paquete de la **aplicación estab.zip**. Está disponible en la siguiente ruta de acceso:

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Upload **tab.zip** a App **Studio**.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualizar el paquete de la aplicación con el editor de manifiestos

Después de cargar el paquete de la aplicación en App Studio, debes configurarlo.

Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.

Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que deben tener valores para cada uno de esos pasos. El usuario ha proporcionado gran parte de la **informaciónmanifest.js,** pero hay campos que debe actualizar.

#### <a name="details-app-details"></a>Detalles: Detalles de la aplicación

En la **sección Detalles de la** aplicación:

1. En **Identificación,** selecciona **Generar** para generar un nuevo identificador de aplicación para tu aplicación.

1. En **Información del desarrollador,** actualice el **sitio web** con la dirección URL HTTPS de **ngrok.**

1. En **Direcciones URL de la** aplicación, actualice la declaración **privacidad** y `https://<yourngrokurl>/privacy` los **Términos** de uso `https://<yourngrokurl>/tou` para>.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la **sección Pestañas:**

1. En **Agregar una pestaña personal,** seleccione **Agregar**. Aparece un cuadro de diálogo emergente.

1. Escriba un nombre para la ficha personal en **Nombre**.

1. Escriba el **id. de entidad**.

1. Actualizar **dirección URL de contenido** con `https://<yourngrokurl>/personalTab` .

    Deje el **campo Dirección URL** del sitio web en blanco.

1. Seleccione **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la **sección Dominios y permisos,** el campo Dominios de las **pestañas** debe contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io/` .

##### <a name="finish-test-and-distribute"></a>Finalizar: probar y distribuir

>[!IMPORTANT]
> A la derecha, en **Descripción,** verá la siguiente advertencia:
>
> &#9888; La **matriz 'validDomains' no puede contener un sitio de túnel...**
>
>Esta advertencia puede omitirse mientras se prueba la pestaña.

1. En la **sección Probar y distribuir,** seleccione **Instalar**.

1. En el cuadro de diálogo emergente, seleccione **Agregar** y la pestaña se muestra con dos opciones.

1. En las opciones de la pestaña, elija **Seleccionar gris** o **Seleccionar rojo**. La pestaña se muestra según el color seleccionado.
 
    ![Pestaña personal ASPNETMVC cargada](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a>Ver la pestaña personal

1. En la barra de navegación situada en el extremo izquierdo de la Teams, selecciona los puntos suspensivos &#x25CF;&#x25CF;&#x25CF;. Se muestra una lista de aplicaciones personales.

1. Seleccione la pestaña de la lista para verlo.
