## <a name="deploy-your-app-to-azure"></a>Implementar la aplicación en Azure

La implementación consta de dos pasos.  En primer lugar, se crean los recursos de nube necesarios (también conocidos como aprovisionamiento). A continuación, el código de la aplicación se copia en los recursos de nube creados. Para este tutorial, implementará la aplicación de pestaña.

> <details>
> <summary>¿Cuál es la diferencia entre Aprovisionar e Implementar?</summary>
>
> El **paso Aprovisionar** crea recursos en Azure y Microsoft 365 para la aplicación, pero no se copia ningún código (HTML, CSS, JavaScript, etc.) en los recursos. El **paso Implementar** copia el código de la aplicación en los recursos que creaste durante el paso de aprovisionamiento. Es común implementar varias veces sin aprovisionar nuevos recursos. Dado que el paso de aprovisionamiento puede tardar algún tiempo en completarse, es independiente del paso de implementación.
</details>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Selecciona el Teams Toolkit :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: en la barra lateral Visual Studio Code barra lateral.

1. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento" border="false":::

1. Seleccione una suscripción para usar para los recursos de Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Captura de pantalla que muestra recursos para el aprovisionamiento" border="false":::

   > [!NOTE]
   > Siempre hay algunos recursos de Azure usados para hospedar la aplicación.

    Un cuadro de diálogo le advierte de que pueden producirse costos al ejecutar recursos en Azure.

1. Seleccione **Aprovisionar**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="Captura de pantalla del cuadro de diálogo de aprovisionamiento." border="false":::

   El proceso de aprovisionamiento crea recursos en la nube de Azure. Puede tardar algo de tiempo. Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha. Después de unos minutos, verá el siguiente aviso:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-success.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento." border="false":::

    Si lo desea, puede ver los recursos aprovisionados. Para este tutorial, no es necesario ver recursos.

    El recurso aprovisionado aparece en la **sección** Entorno.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento." border="false":::

1. Seleccione **Implementar en la nube** en el panel **Implementación** una vez completado el aprovisionamiento.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Captura de pantalla que muestra dónde hacer clic para implementar en la nube." border="false":::

   Al igual que con el aprovisionamiento, la implementación tarda algún tiempo. Puede supervisar el proceso viendo los cuadros de diálogo en la esquina inferior derecha. Después de unos minutos, verá un aviso de finalización.

Ahora, puedes usar el mismo proceso para implementar las aplicaciones Bot y Message Extension en Azure.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

En la ventana de terminal:

1. Ejecute `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Cuando se le pida, seleccione una suscripción de Azure para usar recursos de Azure.

   > [!NOTE]
   > Siempre hay algunos recursos de Azure usados para hospedar la aplicación.

1. Ejecute `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Ejecutar la aplicación implementada

Una vez completados los pasos de aprovisionamiento e implementación:

1. Abra el panel de depuración (**Ctrl+Mayús+D** / **,⇧-D** o **Ver > ejecutar**) desde Visual Studio Code.
1. Seleccione **Iniciar remoto (perimetral)** en la lista desplegable configuración de inicio.
1. Selecciona el botón Reproducir para iniciar la aplicación desde Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Captura de pantalla que muestra la aplicación de inicio de forma remota." border="false":::

1. Seleccione **Agregar**.
   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Captura de pantalla que muestra la aplicación que se está instalando." border="false":::

   La aplicación se carga en el sitio de Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-app.png" alt-text="Captura de pantalla que muestra la aplicación que se está instalando." border="false":::

    ¡Enhorabuena! La aplicación de pestañas se está ejecutando de forma remota desde Azure.
