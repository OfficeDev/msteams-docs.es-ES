## <a name="upload-your-tab-to-teams-with-app-studio"></a>Upload la pestaña a Teams con App Studio

>[!NOTE]
> Usamos App Studio para editar el **archivomanifest.jsy** cargar el paquete completado en Teams. También puedes editar manualmentemanifest.js **si** lo prefieres. Si lo hace, asegúrese de compilar la solución de nuevo para crear el **archivoTab.zip** que se va a cargar.

- Abra el Microsoft Teams cliente. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)

- Abre App studio y selecciona la **pestaña Editor de manifiestos.**

- Selecciona el **icono Importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo. El nombre del paquete de la **aplicación estab.zip**. Debe encontrarse aquí:

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- Upload **Tab.zip** a App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualizar el paquete de la aplicación con el editor de manifiestos

Una vez que hayas cargado el paquete de la aplicación en App Studio, tendrás que terminar de configurarlo.

- Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.

Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que necesitan tener valores para cada uno de esos pasos. Gran parte de la información ha sido proporcionada por su *manifest.js,* pero hay algunos campos que necesitará actualizar:

#### <a name="details-app-details"></a>Detalles: Detalles de la aplicación

En la **sección Detalles de la** aplicación:

- En **Identificación,** **selecciona Generar** para generar un nuevo identificador de aplicación para la aplicación.

- En **Información del desarrollador,** actualice **la dirección URL del sitio** web con la dirección URL HTTPS de **ngrok.**

- En **Direcciones URL de la aplicación** se actualiza la declaración de **privacidad** y los `https://<yourngrokurl>/privacy` **Términos** de uso `https://<yourngrokurl>/tou` para>.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la *sección Pestañas:*

- En **Agregar una pestaña personal,** seleccione **Agregar**. Se le mostrará una ventana de diálogo emergente.

- Complete el **campo** Nombre.

- Complete el **campo Id. de** entidad.

- Actualice el **campo Dirección URL** de contenido con `https://<yourngrokurl>/personalTab` .

- Deje el **campo Dirección URL** del sitio web en blanco.

- Seleccione **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la **sección Dominios y permisos,** el campo Dominios de las **pestañas** debe contener la dirección URL de ngrok sin el prefijo HTTPS - `<yourngrokurl>.ngrok.io/` .

##### <a name="finish-test-and-distribute"></a>Finalizar: probar y distribuir

>[!IMPORTANT]
>En el **campo** Descripción de la derecha verá la siguiente advertencia:
>
>&#9888; "**La matriz 'validDomains' no puede contener un sitio de túnel...**"
>
>Esta advertencia puede omitirse mientras se prueba la pestaña.

En la **sección Probar y** distribuir:

- Seleccione **Instalar**.

- En la ventana emergente asegúrese de que **Add for you** está establecido en **Sí** y **Agregar a** un equipo o chat está establecido en **No**.

- Seleccione **Instalar**.

- En la siguiente ventana emergente, seleccione **Abrir** y se mostrará la pestaña.

## <a name="view-your-personal-tab"></a>Ver la pestaña personal

- En la barra de navegación situada en el extremo izquierdo de la aplicación Teams, seleccione el `...` menú. Se te mostrará una lista de aplicaciones personales.

- Seleccione la pestaña de la lista que desea ver.
