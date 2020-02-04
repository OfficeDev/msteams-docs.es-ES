### <a name="_layoutcshtml"></a>_Layout. cshtml

Para que la pestaña aparezca en Microsoft Teams, debe incluir el **SDK del cliente de JavaScript para Microsoft Teams** e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página. Así es cómo se comunican la pestaña y el cliente de Microsoft Teams:

- Navegue hasta la carpeta **compartida** , Abra **_Layout. cshtml**y agregue lo siguiente a la `<head>` etiqueta:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
>No copie ni pegue las `<script src="...">` direcciones URL de esta página, ya que es posible que no representen la versión más reciente. Para obtener la versión más reciente del SDK, vaya siempre a: [API de JavaScript de Microsoft Teams](https://www.npmjs.com/package/@microsoft/teams-js.com).

### <a name="tabcshtml"></a>TAB. cshtml

Abra el **. cshtml** y actualice el insertado `<script>` de la siguiente manera:

- En la parte superior del script, llame `microsoftTeams.initialize()`a.

- Actualice los `websiteUrl` valores `contentUrl` y en cada función con la dirección URL https ngrok a su ficha.

El código ahora debería ser similar al siguiente con **y8rCgT2b** reemplazado por su dirección URL de ngrok:

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

Asegúrese de guardar la **pestaña. cshtml**actualizada.

## <a name="build-and-run-your-application"></a>Compilar y ejecutar la aplicación

- En Visual Studio, presione **F5**o elija **iniciar depuración** en el menú **depurar** . Compruebe que **ngrok** se está ejecutando y que funciona correctamente abriendo el explorador y yendo a la página de contenido a través de la dirección URL https ngrok que se proporcionó en la ventana del símbolo del sistema.

>[!TIP]
>Debe tener la aplicación en Visual Studio y ngrok en ejecución para completar este inicio rápido. Si necesita detener la ejecución de la aplicación en Visual Studio para trabajar en ella, **mantenga ngrok en ejecución**. Seguirá escuchando y reanudará el enrutamiento de la solicitud de la aplicación cuando se reinicie en Visual Studio. Si tiene que reiniciar el servicio ngrok, devolverá una nueva dirección URL y tendrá que actualizar la aplicación con la nueva dirección URL.

## <a name="upload-your-tab-to-teams-with-app-studio"></a>Cargar la pestaña en Teams con App Studio

>[!Note]
> Usamos App Studio para editar el archivo **manifest. JSON** y cargar el paquete completado en Teams. También puede editar manualmente el archivo **manifest. JSON** si lo prefiere. Si lo hace, asegúrese de volver a crear la solución para crear el archivo **. zip de pestañas** que se va a cargar.

- Abra el cliente de Microsoft Teams. Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.

- Abra App Studio y seleccione la pestaña **Editor de manifiestos** .

- Seleccione el icono **importar una aplicación existente** en el editor de manifiestos para empezar a actualizar el paquete de la aplicación de la pestaña. El código fuente incluye su propio manifiesto parcialmente completado. El nombre del paquete de la aplicación es **Tab. zip**. Se debe encontrar aquí:

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- Cargue la **ficha. zip** en App Studio.

### <a name="update-your-app-package-with-manifest-editor"></a>Actualizar el paquete de la aplicación con el editor de manifiestos

Una vez que haya cargado el paquete de la aplicación en App Studio, tendrá que finalizar la configuración.

- Seleccione el icono de la pestaña recién importada en el panel derecho de la página de bienvenida del editor de manifiestos.

Hay una lista de pasos en la parte izquierda del editor de manifiestos y, a la derecha, una lista de propiedades que deben tener valores para cada uno de estos pasos. La gran parte de la información se ha proporcionado en *manifest. JSON* , pero hay algunos campos que debe actualizar:

#### <a name="details-app-details"></a>Detalles: detalles de la aplicación

- En *identificación* , seleccione ***generar*** para reemplazar el identificador del marcador de posición por el GUID necesario para la pestaña.

- En *información para desarrolladores* , actualice el campo **dirección URL del sitio web** con la dirección URL https de *ngrok* .

- En *direcciones URL de aplicaciones* , actualice los campos **declaración de privacidad** y **condiciones de uso** URL con la dirección URL https de *ngrok* . Recuerde que debe incluir las rutas de */privacy* y */tou* al final de las direcciones URL.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la sección de *tabulaciones* :

- En la *pestaña equipo* , seleccione **Agregar**.

- En la ventana emergente de la pestaña equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab`.

- Por último, asegúrese de que la configuración de se *puede actualizar. *Los cuadros equipo y *grupo de chat* están seleccionados y seleccione **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de ngrok sin el `<yourngrokurl>.ngrok.io/`prefijo https.

#### <a name="test-and-distribute-test-and-distribute"></a>Pruebas y distribución: probar y distribuir

>[!IMPORTANT]
>En el campo **Descripción** de la derecha, verá la siguiente ADVERTENCIA:
>
>&#9888; "**la matriz ' validDomains ' no puede contener un sitio de túnel...**"
>
>Esta advertencia puede omitirse mientras se prueba la pestaña.

En la sección *probar y distribuir* :

- Haga clic en **Instalar**.

- En el campo *Agregar a un equipo o chat* de la ventana emergente, especifique el equipo y seleccione **instalar**.

- En la siguiente ventana emergente, elija el canal de equipo en el que desea que se muestre la pestaña y seleccione **configurar**.

- En la última ventana emergente, seleccione un valor para la página de ficha (bien un icono rojo o gris) y seleccione **Guardar**.

Para ver la pestaña, navegue hasta el equipo en el que se instaló y selecciónela en la barra de pestañas. Debe mostrarse la página elegida durante la configuración.
