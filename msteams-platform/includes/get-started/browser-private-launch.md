### <a name="optional-adjust-your-browser-launch-settings"></a>(Opcional) Ajustar la configuración de inicio del explorador

Al desarrollar una aplicación Teams, es común ejecutar la aplicación en un inquilino de desarrollador alternativo o con credenciales alternativas.  Tanto Microsoft Edge como Google Chrome proporcionan facilidades para ajustar la configuración de inicio del explorador.  Por ejemplo, para actualizar el proyecto para que admita el modo InPrivate (Microsoft Edge), abra el `.vscode/launch.json` archivo en el proyecto.  Busque la configuración de inicio adecuada y agregue el siguiente bloque a cada uno:

``` json
"runtimeArgs": [ "--inprivate" ]
```

Por ejemplo, la configuración de inicio para ejecutarse localmente tiene este aspecto:

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

Como alternativa, puede configurar el explorador para que use el último perfil conocido. [Cree un nuevo perfil en](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) Microsoft Edge.  A continuación, ajusta la configuración para usar el último perfil conocido para nuevos vínculos:

- En Microsoft Edge, abra `edge://settings/profiles/multiProfileSettings` .
- Desactivar La **conmutación automática de perfiles**.
- Para el **perfil predeterminado para vínculos externos,** seleccione **Last used (default).**

Asegúrate de que el explorador está abierto al perfil correcto antes de depurar la aplicación.
