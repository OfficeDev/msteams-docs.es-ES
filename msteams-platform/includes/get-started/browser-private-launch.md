### <a name="optional-adjust-your-browser-launch-settings"></a><span data-ttu-id="1eda8-101">(Opcional) Ajustar la configuración de inicio del explorador</span><span class="sxs-lookup"><span data-stu-id="1eda8-101">(Optional) Adjust your browser launch settings</span></span>

<span data-ttu-id="1eda8-102">Al desarrollar una aplicación Teams, es común ejecutar la aplicación en un inquilino de desarrollador alternativo o con credenciales alternativas.</span><span class="sxs-lookup"><span data-stu-id="1eda8-102">When developing a Teams app, it is common to run your app in an alternate developer tenant or with alternate credentials.</span></span>  <span data-ttu-id="1eda8-103">Tanto Microsoft Edge como Google Chrome proporcionan facilidades para ajustar la configuración de inicio del explorador.</span><span class="sxs-lookup"><span data-stu-id="1eda8-103">Both Microsoft Edge and Google Chrome provide facilities to adjust the launch settings for your browser.</span></span>  <span data-ttu-id="1eda8-104">Por ejemplo, para actualizar el proyecto para que admita el modo InPrivate (Microsoft Edge), abra el `.vscode/launch.json` archivo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1eda8-104">For example, to update the project to support InPrivate mode (Microsoft Edge), open the `.vscode/launch.json` file in your project.</span></span>  <span data-ttu-id="1eda8-105">Busque la configuración de inicio adecuada y agregue el siguiente bloque a cada uno:</span><span class="sxs-lookup"><span data-stu-id="1eda8-105">Look for the appropriate launch settings, and add the following block to each one:</span></span>

``` json
"runtimeArgs": [ "--inprivate" ]
```

<span data-ttu-id="1eda8-106">Por ejemplo, la configuración de inicio para ejecutarse localmente tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="1eda8-106">For instance, the launch setting for running locally looks like this:</span></span>

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

<span data-ttu-id="1eda8-107">Como alternativa, puede configurar el explorador para que use el último perfil conocido.</span><span class="sxs-lookup"><span data-stu-id="1eda8-107">Alternatively, you can configure your browser to use the last known profile.</span></span> <span data-ttu-id="1eda8-108">[Cree un nuevo perfil en](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="1eda8-108">[Create a new profile](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) in Microsoft Edge.</span></span>  <span data-ttu-id="1eda8-109">A continuación, ajusta la configuración para usar el último perfil conocido para nuevos vínculos:</span><span class="sxs-lookup"><span data-stu-id="1eda8-109">Then adjust the settings to use the last known profile for new links:</span></span>

- <span data-ttu-id="1eda8-110">En Microsoft Edge, abra `edge://settings/profiles/multiProfileSettings` .</span><span class="sxs-lookup"><span data-stu-id="1eda8-110">In Microsoft Edge, open `edge://settings/profiles/multiProfileSettings`.</span></span>
- <span data-ttu-id="1eda8-111">Desactivar La **conmutación automática de perfiles**.</span><span class="sxs-lookup"><span data-stu-id="1eda8-111">Turn off **Automatic profile switching**.</span></span>
- <span data-ttu-id="1eda8-112">Para el **perfil predeterminado para vínculos externos,** seleccione **Last used (default).**</span><span class="sxs-lookup"><span data-stu-id="1eda8-112">For the **Default profile for external links**, select **Last used (default)**.</span></span>

<span data-ttu-id="1eda8-113">Asegúrate de que el explorador está abierto al perfil correcto antes de depurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1eda8-113">Ensure your browser is opened to the correct profile before debugging your app.</span></span>
