## <a name="update-your-application"></a><span data-ttu-id="69e13-101">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="69e13-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="69e13-102">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="69e13-102">_Layout.cshtml</span></span>

<span data-ttu-id="69e13-103">Para que la pestaña aparezca en Microsoft Teams, debe incluir el **SDK del cliente de JavaScript para Microsoft Teams** e incluir una llamada a `microsoftTeams.initialize()` después de que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="69e13-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="69e13-104">Así es como la pestaña y la aplicación Microsoft Teams se comunican:</span><span class="sxs-lookup"><span data-stu-id="69e13-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="69e13-105">Navegue hasta la carpeta **compartida** , Abra **_Layout. cshtml**y agregue lo siguiente a la `<head>` sección Etiquetas:</span><span class="sxs-lookup"><span data-stu-id="69e13-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a><span data-ttu-id="69e13-106">PersonalTab. cshtml</span><span class="sxs-lookup"><span data-stu-id="69e13-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="69e13-107">Abra **PersonalTab. cshtml** y actualice las etiquetas `<script>` insertadas llamando `microsoftTeams.initialize()`a.</span><span class="sxs-lookup"><span data-stu-id="69e13-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="69e13-108">Asegúrese de guardar la *PersonalTab. cshtml*actualizada.</span><span class="sxs-lookup"><span data-stu-id="69e13-108">Make sure to save your updated *PersonalTab.cshtml*.</span></span>