## <a name="upload-your-tab-to-teams-with-app-studio"></a>Upload la pestaña para Teams con App Studio

>[!NOTE]
> Usamos App Studio para editar su **manifest.jsen el** archivo y cargar el paquete completado en Teams. También puede editar manualmente **manifest.jsen** si lo prefiere. Si lo hace, asegúrese de volver a compilar la solución para crear el archivo **Tab.zip** que se va a cargar.

- Abra el cliente Microsoft Teams. Si utiliza la [versión basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end utilizando las herramientas para [desarrolladores](~/tabs/how-to/developer-tools.md)de su navegador.

- Abra App Studio y seleccione la pestaña **Editor de manifiestos.**

- Seleccione el icono **Importar una aplicación existente** en el editor de manifiestos para comenzar a actualizar el paquete de aplicación de la pestaña. El código fuente viene con su propio manifiesto parcialmente completo. El nombre del paquete de la aplicación es **tab.zip**. Debe encontrarse aquí:

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- Upload **Tab.zip** a App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualiza tu paquete de aplicaciones con el editor de manifiestos

Una vez que haya cargado el paquete de la aplicación en App Studio, deberá terminar de configurarlo.

- Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.

Hay una lista de pasos en el lado izquierdo del editor de manifiestos y, a la derecha, una lista de propiedades que necesitan tener valores para cada uno de esos pasos. Gran parte de la información ha sido proporcionada por su *manifest.js,* pero hay algunos campos que tendrá que actualizar:

#### <a name="details-app-details"></a>Detalles: Detalles de la aplicación

En la sección Detalles de la **aplicación:**

- En **Identificación,** seleccione **Generar** para generar un nuevo identificador de aplicación para la aplicación.

- En **Información del desarrollador,** actualice la **URL del sitio web** con su URL HTTPS **de ngrok.**

- En **URL de aplicación,** actualice la **declaración de privacidad** y los Términos `https://<yourngrokurl>/privacy` de **uso** a `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Capacidades: Pestañas

En la sección *Pestañas:*

- En **Agregar una pestaña personal,** seleccione **Agregar**. Se le presentará una ventana de diálogo emergente.

- Complete el campo **Nombre.**

- Complete el campo **Entity Id.**

- Actualice el campo **Dirección URL de contenido** con to `https://<yourngrokurl>/personalTab` .

- Deje el campo URL del **sitio web** en blanco.

- Seleccione **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: Dominios y permisos

En la sección **Dominios y permisos,** el campo **Dominios de las pestañas** debe contener la dirección URL de ngrok sin el prefijo HTTPS - `<yourngrokurl>.ngrok.io/` .

##### <a name="finish-test-and-distribute"></a>Finalizar: Probar y distribuir

>[!IMPORTANT]
>En el campo **Descripción** de la derecha verá la siguiente advertencia:
>
>&#9888; "**La matriz 'validDomains' no puede contener un sitio de tunelización...**"
>
>Esta advertencia se puede omitir al probar la pestaña.

En la sección **Prueba y distribución:**

- Seleccione **Instalar**.

- En la ventana emergente asegúrese de que **Agregar para usted** está establecido en **Sí** y **Agregar a un equipo o chat** está establecido en **No**.

- Seleccione **Instalar**.

- En la siguiente ventana emergente, seleccione **Abrir** y se mostrará la pestaña.

## <a name="view-your-personal-tab"></a>Ver su pestaña personal

- En la barra de navegación situada a la izquierda de la aplicación Teams, seleccione el `...` menú. Se te presentará una lista de aplicaciones personales.

- Seleccione la pestaña de la lista que desea ver.
