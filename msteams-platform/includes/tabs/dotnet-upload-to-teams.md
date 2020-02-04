## <a name="upload-your-tab-to-teams-with-app-studio"></a>Cargar la pestaña en Teams con App Studio

>[!NOTE]
> Usamos App Studio para editar el archivo **manifest. JSON** y cargar el paquete completado en Teams. También puede editar manualmente el archivo **manifest. JSON** si lo prefiere. Si lo hace, asegúrese de volver a crear la solución para crear el archivo **. zip de pestañas** que se va a cargar.

- Abra el cliente de Microsoft Teams. Si usa la [versión basada en Web](https://teams.microsoft.com) , puede inspeccionar el código Front-end con las [herramientas de desarrollo](~/tabs/how-to/developer-tools.md)de su explorador.

- Abra la aplicación de App Studio y seleccione la pestaña **Editor de manifiestos** .

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

- En *identificación* , seleccione **generar** para generar un nuevo identificador de aplicación para la aplicación.

- En *información para desarrolladores* , actualice el campo **dirección URL del sitio web** con la dirección URL https de *ngrok* .

- En *direcciones URL* de aplicaciones **** `https://<yourngrokurl>/privacy` , actualice la declaración de privacidad y las `https://<yourngrokurl>/tou` **condiciones de uso** para>.

#### <a name="capabilities-tabs"></a>Capacidades: pestañas

En la sección de *tabulaciones* :

- En la *pestaña equipo* , seleccione **Agregar**.

- En la ventana emergente de la pestaña equipo, actualice la *dirección URL de configuración* a `https://<yourngrokurl>/tab`.

- Por último, asegúrese de que la configuración de se *puede actualizar. *Los cuadros equipo y *grupo de chat* están seleccionados y seleccione **Guardar**.

#### <a name="finish-domains-and-permissions"></a>Finalizar: dominios y permisos

En la sección *dominios y permisos* , los *dominios del campo de pestañas* deben contener la dirección URL de ngrok sin el `<yourngrokurl>.ngrok.io/`prefijo https.

#### <a name="finish-test-and-distribute"></a>Finalizar: probar y distribuir

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
