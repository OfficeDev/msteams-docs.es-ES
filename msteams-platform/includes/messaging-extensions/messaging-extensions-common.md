## <a name="add-a-message-extension-to-your-app"></a>Agregar una extensión de mensaje a la aplicación

Una extensión de mensaje es un servicio hospedado en la nube que escucha las solicitudes del usuario y responde con datos estructurados, como una [tarjeta](~/task-modules-and-cards/what-are-cards.md). Integre el servicio con Microsoft Teams a través de objetos de Bot Framework `Activity` . Nuestras extensiones .NET y Node.js del SDK de Bot Builder pueden ayudarle a agregar la funcionalidad de extensión de mensaje a la aplicación.

![Diagrama del flujo de mensajes para extensiones de mensaje](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Registro en Bot Framework

Si aún no lo ha hecho, primero debe registrar un bot con Microsoft Bot Framework. Los puntos de conexión de devolución de llamada y el identificador de la aplicación de Microsoft para el bot, tal como se define allí, se usarán en la extensión de mensaje para recibir y responder a las solicitudes del usuario. No olvide habilitar el canal de Microsoft Teams para el bot.

Registre el identificador de la aplicación de bot y la contraseña de la aplicación; deberá proporcionar el identificador de la aplicación en el manifiesto de la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Al igual que con los bots y las pestañas, se actualiza el [manifiesto](~/resources/schema/manifest-schema.md#composeextensions) de la aplicación para incluir las propiedades de la extensión de mensaje. Estas propiedades rigen cómo aparece y se comporta la extensión de mensaje en el cliente de Microsoft Teams. Las extensiones de mensaje se admiten a partir de la versión 1.0 del manifiesto.

#### <a name="declare-your-message-extension"></a>Declaración de la extensión de mensaje

Para agregar una extensión de mensaje, incluya una nueva estructura JSON de nivel superior en el manifiesto con la `composeExtensions` propiedad . Actualmente, está limitado a crear una sola extensión de mensaje para la aplicación.

> [!NOTE]
> El manifiesto hace referencia a las extensiones de mensaje como `composeExtensions`. Esto es para mantener la compatibilidad con versiones anteriores.

La definición de extensión es un objeto que tiene la estructura siguiente:

| Nombre de propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Normalmente, debe ser el mismo que el identificador de la aplicación general de Teams. | Sí |
| `scopes` | Matriz que declara si esta extensión se puede agregar a `personal` o `team` ámbitos (o ambos). | Sí |
| `canUpdateConfiguration` | Habilita **el elemento de menú Configuración** . | No |
| `commands` | Matriz de comandos que admite esta extensión de mensaje. Está limitado a 10 comandos. | Sí |

#### <a name="define-commands"></a>Definición de comandos

La extensión de mensaje debe declarar un comando, que aparece cuando el usuario selecciona la aplicación en el botón **Más opciones** (**&#8943;**) del cuadro de redacción.

![Captura de pantalla de la lista de extensiones de mensaje en Teams](~/assets/images/compose-extensions/compose-extension-list.png)

En el manifiesto de la aplicación, el elemento de comando es un objeto con la siguiente estructura:

| Nombre de propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Identificador único que se asigna a este comando. La solicitud de usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Establezca el tipo de comando. Los valores posibles incluyen `query` y `action`. Si no es así, presente que el valor predeterminado está establecido en `query`. | No | 1.4 |
| `initialRun` | Parámetro opcional, que se usa con `query` comandos. Si se establece en **true**, indica que este comando se debe ejecutar en cuanto el usuario elija este comando en la interfaz de usuario. | No | 1.0 |
| `fetchTask` | Parámetro opcional, que se usa con `action` comandos. Establézcalo en **true** para capturar la tarjeta adaptable o la dirección URL web que se mostrará en el [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md). Esto se usa cuando la entrada al `action` comando es dinámica en lugar de un conjunto estático de parámetros. Tenga en cuenta que si se establece en **true** , se omite la lista de parámetros estáticos para el comando. | No | 1.4 |
| `parameters` | Lista estática de parámetros para el comando. | Sí | 1.0 |
| `parameter.name` | Nombre del parámetro. Esto se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Describe los fines o el ejemplo de este parámetro del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Título o etiqueta de parámetros breves fáciles de usar. | Sí | 1.0 |
| `parameter.inputType` | Establezca en el tipo de entrada necesaria. Entre los valores posibles se incluyen , , , , , `toggle``time`. `date``number``textarea``text` El valor predeterminado está establecido en `text`. | No | 1.4 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción del mensaje. Los valores posibles son `message`, `compose`o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |
