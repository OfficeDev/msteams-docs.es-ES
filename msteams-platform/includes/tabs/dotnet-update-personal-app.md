## <a name="update-your-application"></a>Actualizar la aplicación

### <a name="_layoutcshtml"></a>_Layout.cshtml

Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página. Así se comunican la pestaña y Teams aplicación:

Vaya a la **carpeta Shared,** abra **_Layout.cshtml** y agregue lo siguiente a la sección `<head>` etiquetas:

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Abra **PersonalTab.cshtml** y actualice las etiquetas `<script>` incrustadas llamando a `microsoftTeams.initialize()` .

Asegúrese de guardar el archivo **PersonalTab.cshtml** actualizado.