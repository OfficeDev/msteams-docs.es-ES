## <a name="update-your-application"></a>Actualizar la aplicación

### <a name="_layoutcshtml"></a>_Layout. cshtml

Para que la pestaña aparezca en Microsoft Teams, debe incluir el **SDK del cliente de JavaScript para Microsoft Teams** e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página. Así es como la pestaña y la aplicación Microsoft Teams se comunican:

- Navegue hasta la carpeta **compartida** , Abra **_Layout. cshtml**y agregue lo siguiente a la `<head>` sección Etiquetas:

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a>PersonalTab. cshtml

Abra **PersonalTab. cshtml** y actualice las etiquetas `<script>` insertadas llamando `microsoftTeams.initialize()`a.

Asegúrese de guardar la *PersonalTab. cshtml*actualizada.