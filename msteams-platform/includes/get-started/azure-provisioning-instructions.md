## <a name="deploy-your-app-to-azure"></a>Implementar la aplicación en Azure

La implementación consta de dos pasos.  En primer lugar, se crean los recursos en la nube necesarios (también conocidos como aprovisionamiento) y, a continuación, el código que forma la aplicación se copia en los recursos de nube creados.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Abrir Visual Studio Code.
1. Seleccione el Teams Toolkit de la barra lateral seleccionando el Teams.
1. Seleccione **Aprovisionar en la nube**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="Captura de pantalla que muestra los comandos de aprovisionamiento":::

1. Si es necesario, seleccione una suscripción para usar para los recursos de Azure.

   > [!NOTE]
   > Siempre hay algunos recursos de Azure usados para hospedar la aplicación.

1. Un cuadro de diálogo le advierte de que pueden producirse costos al ejecutar recursos en Azure.  Presione **Aprovisionar**.

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="Captura de pantalla del cuadro de diálogo de aprovisionamiento.":::

   El proceso de aprovisionamiento creará recursos en la nube de Azure.  Esto llevará algún tiempo.  Puede supervisar el progreso viendo los cuadros de diálogo en la esquina inferior derecha.  Después de unos minutos, verá el siguiente aviso:

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="Captura de pantalla que muestra el cuadro de diálogo completado de aprovisionamiento.":::

1. Una vez completado el aprovisionamiento, seleccione **Implementar en la nube.**  Al igual que con el aprovisionamiento, este proceso tarda algún tiempo.  Puede supervisar el proceso viendo los cuadros de diálogo en la esquina inferior derecha. Después de unos minutos, verá un aviso de finalización.

# <a name="command-line"></a>[Línea de comandos](#tab/cli)

En la ventana de terminal:

1. Ejecute `teamsfx provision`.

   ``` bash
   teamsfx provision
   ```

   Es posible que se le pida que inicie sesión en su suscripción de Azure.  Si es necesario, se le pedirá que seleccione una suscripción de Azure que se usará para los recursos de Azure.

   > [!NOTE]
   > Siempre hay algunos recursos de Azure usados para hospedar la aplicación.

1. Ejecute `teamsfx deploy`.

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> **¿Cuál es la diferencia entre Aprovisionar e Implementar?**
>
> El **paso Aprovisionar** creará recursos en Azure y M365 para la aplicación, pero no se copia ningún código (HTML, CSS, JavaScript, etc.) en los recursos.  El **paso** Implementar copiará el código de la aplicación en los recursos que creaste durante el paso de aprovisionamiento.  Es común implementar varias veces sin aprovisionar nuevos recursos. Dado que el paso de aprovisionamiento puede tardar algún tiempo en completarse, es independiente del paso de implementación.

Una vez finalizados los pasos de aprovisionamiento e implementación:

1. Desde Visual Studio Code, abra el panel de depuración (**Ctrl+Mayús+D**  /  **.⇧-D** o **Ver > Ejecutar**)
1. Seleccione **Iniciar remoto (perimetral)** en la lista desplegable configuración de inicio.
1. Presione el botón Reproducir para iniciar la aplicación: ahora se ejecuta de forma remota desde Azure.
