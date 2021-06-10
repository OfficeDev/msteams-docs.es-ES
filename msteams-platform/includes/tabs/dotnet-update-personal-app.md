## <a name="update-your-application"></a><span data-ttu-id="9e7be-101">Actualizar la aplicación</span><span class="sxs-lookup"><span data-stu-id="9e7be-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="9e7be-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="9e7be-102">_Layout.cshtml</span></span>

<span data-ttu-id="9e7be-103">Para que la pestaña se muestre en Teams, debe incluir el SDK de cliente Microsoft Teams **JavaScript** e incluir una llamada después de `microsoftTeams.initialize()` que se cargue la página.</span><span class="sxs-lookup"><span data-stu-id="9e7be-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="9e7be-104">Así se comunican la pestaña y Teams aplicación:</span><span class="sxs-lookup"><span data-stu-id="9e7be-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="9e7be-105">Navegue a la **carpeta Shared,** abra **_Layout.cshtml** y agregue lo siguiente a la sección `<head>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="9e7be-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="9e7be-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="9e7be-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="9e7be-107">Abra **PersonalTab.cshtml** y actualice las etiquetas `<script>` incrustadas llamando a `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="9e7be-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="9e7be-108">Asegúrese de guardar el **objeto PersonalTab.cshtml actualizado.**</span><span class="sxs-lookup"><span data-stu-id="9e7be-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>