## <a name="deploy-your-app-to-azure"></a>Implementar la aplicación en Azure

La implementación consta de dos pasos.  En primer lugar, se crean los recursos en la nube necesarios (también conocidos como aprovisionamiento). A continuación, el código de la aplicación se copia en los recursos en la nube creados. En este tutorial, implementará la aplicación de pestaña.
<br>
<br>
<details>
<summary>¿Cuál es la diferencia entre Aprovisionar e Implementar?</summary>
<br>
El paso <b>Aprovisionar</b> crea recursos en Azure y Microsoft 365 para la aplicación, pero no se copia ningún código (HTML, CSS, JavaScript, etc.) en los recursos. El paso <b>Implementar</b> copia el código de la aplicación en los recursos que creó durante el paso de aprovisionamiento. Es habitual implementar varias veces sin aprovisionar nuevos recursos. Dado que el paso de aprovisionamiento puede tardar algún tiempo en completarse, es independiente del paso de implementación.
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Seleccione icono del Kit de herramientas de Teams :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: en la barra lateral de Visual Studio Code.

1. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

1. Seleccione cualquiera de la suscripción existente.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/select-subscription.png" alt-text="Seleccionar suscripción":::

1. Seleccione un grupo de recursos que se usará para los recursos de Azure.

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="Captura de pantalla que muestra los recursos para el aprovisionamiento":::

   > [!NOTE]
   > Siempre hay algunos recursos de Azure que se usan para hospedar la aplicación.

    Un cuadro de diálogo le advierte de que se pueden incurrir en costos al ejecutar recursos en Azure.

1. Seleccione **Aprovisionar**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-confirm1.png" alt-text="Seleccionar suscripción":::

   El proceso de aprovisionamiento crea recursos en la nube de Azure. Puede tardar algún tiempo. Puede supervisar el progreso observando los diálogos en la esquina inferior derecha. Después de unos minutos, verá el siguiente aviso:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo de aprovisionamiento completo.":::

    Si lo desea, puede ver los recursos aprovisionados. En este tutorial, no es necesario ver los recursos.

    El recurso aprovisionado aparece en la sección **Entorno** .

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo de aprovisionamiento completo.":::

1. Seleccione **Implementar en la nube** en el panel **Implementación** una vez completado el aprovisionamiento.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="Captura de pantalla que muestra dónde hacer clic para implementar en la nube.":::

   Al igual que con el aprovisionamiento, la implementación tarda algún tiempo. Para supervisar el proceso, vea los diálogos en la esquina inferior derecha. Después de unos minutos, verá un aviso de finalización.

Ahora, puede usar el mismo proceso para implementar las aplicaciones Bot y Message Extension en Azure.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

En la ventana del terminal:

1. Ejecute `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Cuando se le solicite, seleccione una suscripción de Azure para usar los recursos de Azure.

   > [!NOTE]
   > Siempre hay algunos recursos de Azure que se usan para hospedar la aplicación.

1. Ejecute `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>Ejecución de la aplicación implementada

Una vez completados los pasos de aprovisionamiento e implementación:

1. Abra el panel de depuración (**Ctrl+Mayús+D** / **⌘⇧-D** o **Ver > ejecutar**) desde Visual Studio Code.
1. Seleccione **Iniciar remoto (Edge)** en la lista desplegable configuración de inicio.
1. Seleccione **Iniciar depuración (F5)** para iniciar la aplicación desde Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="Captura de pantalla que muestra la aplicación de inicio remoto.":::

1. Seleccione **Agregar** cuando se le pida que transfiera localmente la aplicación a Teams.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="Captura de pantalla que muestra la aplicación que se está instalando.":::

    Enhorabuena, la primera aplicación de pestaña se ejecuta en el entorno de Azure.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="Captura de pantalla que muestra el mensaje para probar la aplicación ahora o posterior":::
