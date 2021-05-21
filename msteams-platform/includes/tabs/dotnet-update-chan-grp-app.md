### <a name="_layoutcshtml"></a>_Layout.cshtml

Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página. Así se comunican la pestaña y Teams cliente:

- Navegue a la **carpeta Shared,** **abra _Layout.cshtml** y agregue lo siguiente a la `<head>` etiqueta:

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
>No copie ni pegue las direcciones URL de esta página, ya que es posible que `<script src="...">` no representen la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a: Microsoft Teams [API de JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).

### <a name="tabcshtml"></a>Tab.cshtml

Abra **Tab.cshtml** y actualice el incrustado `<script>` de la siguiente manera:

- En la parte superior del script, llame `microsoftTeams.initialize()` a .

- Actualice los `websiteUrl` valores y de cada función con la dirección URL de https `contentUrl` ngrok a la pestaña.

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

Asegúrese de guardar el **tab.cshtml actualizado.**

## <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

- En Visual Studio presione **F5** o **elija Iniciar depuración** en el **menú** Depurar. Compruebe que **ngrok** se está ejecutando y funcionando correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL HTTPS de ngrok que se proporcionó en la ventana del símbolo del sistema.

>[!TIP]
>Debe tener la aplicación en ejecución Visual Studio y ngrok para completar esta guía de inicio rápido. Si necesita dejar de ejecutar la aplicación en Visual Studio para trabajar en **ella, mantenga ngrok en ejecución**. Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio. Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.

## <a name="upload-your-tab-to-teams"></a>Upload la pestaña a Teams

>[!Note]
> Usamos App Studio para editar el **archivomanifest.jsy** cargar el paquete completado en Teams. También puede editar manualmente el **archivomanifest.jsen** si lo prefiere. Si lo hace, asegúrese de compilar la solución de nuevo para crear el **archivotab.zip** que se va a cargar.

- Abra el Microsoft Teams cliente. Si usa la versión [basada en web,](https://teams.microsoft.com) puede inspeccionar el código front-end con las herramientas de desarrollo [del explorador.](~/tabs/how-to/developer-tools.md)

- Abre App studio y selecciona la **pestaña Editor de manifiestos.**

- Selecciona el **icono Importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación para la pestaña. El código fuente viene con su propio manifiesto parcialmente completo. El nombre del paquete de la **aplicación estab.zip**. Debe encontrarse aquí:

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- Upload **tab.zip** a App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualizar el paquete de la aplicación con el editor de manifiestos

Una vez que hayas cargado el paquete de la aplicación en App Studio, tendrás que terminar de configurarlo.

- Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiesto.

Hay una lista de pasos en el lado izquierdo del editor de manifiesto y, a la derecha, una lista de propiedades que necesitan tener valores para cada uno de esos pasos. Gran parte de la información ha sido proporcionada por su *manifest.js,* pero hay algunos campos que necesitará actualizar:

#### <a name="details-app-details"></a>Detalles: Detalles de la aplicación

En la *sección Detalles de la* aplicación:

- *Identificación:* seleccione **Generar para** reemplazar el identificador de marcador de posición con el GUID necesario para la pestaña.

- *Información del desarrollador:* actualice el campo **Dirección URL** del sitio web con la dirección URL HTTPS de *ngrok.*

- *Direcciones URL de la* aplicación: actualice la **declaración de privacidad a** y `https://<yourngrokurl>/privacy` los **Términos de uso** para `https://<yourngrokurl>/tou`>.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la *sección Pestañas:*

- *Ficha Equipo:* seleccione **Agregar**.

- En la ventana emergente de la pestaña Equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab` .

- Por último, asegúrese de que *puede actualizar la configuración. Los cuadros* de *chat* equipo y grupo están activados y selecciona **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la *sección Dominios y permisos:*

- El *campo Dominios de las pestañas* debe contener la dirección URL de ngrok sin el prefijo HTTPS - `<yourngrokurl>.ngrok.io/` .

#### <a name="finish-test-and-distribute"></a>Finalizar: probar y distribuir

>[!IMPORTANT]
>En el **campo** Descripción de la derecha verá la siguiente advertencia:
>
>&#9888; "**La matriz 'validDomains' no puede contener un sitio de túnel...**"
>
>Esta advertencia puede omitirse mientras se prueba la pestaña.

En la *sección Probar y* distribuir:

- Seleccione **Instalar**.

- En el campo Agregar *a* un equipo o chat de la ventana emergente, escriba el equipo y seleccione **Instalar**.

- En la siguiente ventana emergente, elija el canal de grupo en el que desea que se muestre la pestaña y **seleccione Configurar**.

- En la ventana emergente final, seleccione un valor para la página de pestaña (ya sea un icono rojo o gris) y **seleccione Guardar**.

Para ver la pestaña, vaya al equipo en el que la instaló y selecciónelo en la barra de pestañas. Se debe mostrar la página que eligió durante la configuración.
