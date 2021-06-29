### <a name="_layoutcshtml"></a>_Layout.cshtml

Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página. Así se comunican la pestaña y Teams cliente:

Vaya a la **carpeta Shared,** abra **_Layout.cshtml** y agregue lo siguiente a la `<head>` etiqueta:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> No copie ni pegue las direcciones URL de esta página, ya que es posible que `<script src="...">` no representen la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre [a Microsoft Teams API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).

### <a name="tabcshtml"></a>Tab.cshtml

**Para actualizar el script incrustado**

1. En Visual Studio, abra **Tab.cshtml** para actualizar el `<script>` .

1. En la parte superior del script, llame `microsoftTeams.initialize()` a .

1. Actualice los `websiteUrl` valores y de cada función con la dirección URL de https `contentUrl` ngrok a la pestaña.

    El código ahora debería tener el siguiente aspecto con **y8rCgT2b** reemplazado por la dirección URL de ngrok:

    ```javascript
        microsoftTeams.initialize();
    
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. Asegúrese de guardar el **tab.cshtml actualizado.**

## <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

En Visual Studio, presione **F5** o **elija Iniciar depuración** en el **menú** Depurar. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

> [!TIP]
> Debe tener la aplicación en ejecución Visual Studio y ngrok. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en **ella, mantenga ngrok en ejecución**. Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio. Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.

## <a name="upload-your-tab"></a>Upload la pestaña

>[!Note]
> App Studio se puede usar para editar el **archivomanifest.jsarchivo** y cargar el paquete completado en Teams. También puede editar manualmente el **archivomanifest.jsen** si lo prefiere. Si lo hace, asegúrese de compilar la solución de nuevo para crear el **archivotab.zip** que se va a cargar.

**Para cargar la pestaña**

1. Vaya a Microsoft Teams. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)

1. Ve a **App Studio** y selecciona la pestaña Editor **de manifiestos.**

1. Selecciona **Importar una aplicación existente en** el editor de manifiestos para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo. El nombre del paquete de la **aplicación estab.zip**. Está disponible aquí:

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. Upload **tab.zip** a App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualizar el paquete de la aplicación con el editor de manifiestos

Después de cargar el paquete de la aplicación en App Studio, debes terminar de configurarlo.

Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.

Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que deben tener valores para cada uno de esos pasos. El usuario ha proporcionado gran parte de la **informaciónmanifest.js,** pero hay algunos campos que debe actualizar:

#### <a name="details-app-details"></a>Detalles: Detalles de la aplicación

En la **sección Detalles de la** aplicación:

1. En **Identificación**, seleccione **Generar** para reemplazar el identificador de marcador de posición con el GUID necesario para la pestaña.

1. En **Información para desarrolladores,** actualice **el** sitio web con la dirección URL HTTPS de **ngrok.**

1. En **Direcciones URL de la** aplicación, actualice la declaración **privacidad** y `https://<yourngrokurl>/privacy` los **Términos** de uso `https://<yourngrokurl>/tou` para>.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la **sección Pestañas:**

1. En **la pestaña Equipo,** **seleccione Agregar**.

1. En la **ventana emergente de la pestaña** Equipo, actualice la dirección URL de **configuración** a `https://<yourngrokurl>/tab` .

1. Asegúrese de **que las casillas ¿Puede** actualizar la configuración? , **Equipo** y **Chat** de grupo están seleccionadas y **seleccione Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la **sección Dominios y permisos,** los dominios de las **pestañas** deben contener la dirección URL de ngrok sin el prefijo HTTPS `<yourngrokurl>.ngrok.io/` .

#### <a name="finish-test-and-distribute"></a>Finalizar: probar y distribuir

>[!IMPORTANT]
> A la derecha, en **Descripción,** verá la siguiente advertencia:
>
> &#9888; "**La matriz 'validDomains' no puede contener un sitio de túnel...**"
>
> Esta advertencia puede omitirse mientras se prueba la pestaña.

1. En la **sección Probar y distribuir,** seleccione **Instalar**.

1. En el cuadro de diálogo emergente, seleccione **Agregar a un** equipo o en la lista desplegable, seleccione Agregar a un **chat.**

1. Elija el equipo o el chat donde desea que se muestre la pestaña y seleccione **Configurar una pestaña**.

1. En el siguiente cuadro de diálogo emergente, elija **Seleccionar gris** o **Seleccionar** rojo y seleccione **Guardar**.

1. Para ver la pestaña, vaya al equipo donde instaló la pestaña y selecciónelo en la barra de pestañas. Se muestra la página que eligió durante la configuración.

    ![Pestaña canal ASPNETMVC cargada](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

