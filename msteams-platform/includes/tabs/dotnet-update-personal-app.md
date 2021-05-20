## <a name="update-your-application"></a>Actualice la aplicación

### <a name="_layoutcshtml"></a>_Layout.cshtml

Para que la pestaña se muestre en Teams, debe incluir el **SDK de cliente de JavaScript Microsoft Teams** e incluir una llamada después de cargar la `microsoftTeams.initialize()` página. Así es como se comunican la pestaña y la aplicación Teams:

- Vaya a la carpeta **Shared,** abra **_Layout.cshtml** y agregue lo siguiente a la `<head>` sección tags:

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a>PersonalTab.cshtml

Abra **PersonalTab.cshtml** y actualice las etiquetas incrustadas `<script>` mediante una llamada a `microsoftTeams.initialize()` .

Asegúrese de guardar su **PersonalTab.cshtml** actualizado .