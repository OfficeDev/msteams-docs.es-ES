## <a name="add-a-messaging-extension-to-your-app"></a>Agregar una extensión de mensajería a la aplicación

Una extensión de mensajería es un servicio hospedado en la nube que escucha las solicitudes de los usuarios y responde con datos estructurados, como una [tarjeta](~/task-modules-and-cards/what-are-cards.md). Integrará el servicio con Microsoft Teams a través `Activity` de los objetos de bot Framework. Nuestras extensiones .NET y node. js para el SDK de bot Builder pueden ayudarle a agregar la funcionalidad de la extensión de mensajería a la aplicación.

![Diagrama del flujo de mensajes para las extensiones de mensajería](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Registrarse en el marco de trabajo de bot

Si aún no lo ha hecho, primero debe registrar un bot con Microsoft bot Framework. El identificador de aplicación y los extremos de devolución de llamada de Microsoft para el bot, tal y como se definieron, se usarán en la extensión de mensajería para recibir y responder a las solicitudes de los usuarios. Recuerde habilitar el canal de Microsoft Teams para el bot.

Registre el identificador de la aplicación de Bot y la contraseña de aplicación, deberá proporcionar el identificador de la aplicación en el manifiesto de la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Al igual que con los bots y las pestañas, se actualiza el [manifiesto](~/resources/schema/manifest-schema.md#composeextensions) de la aplicación para incluir las propiedades de la extensión de mensajería. Estas propiedades rigen el aspecto y el comportamiento de la extensión de mensajería en el cliente de Microsoft Teams. Las extensiones de mensajería son compatibles a partir de la v 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declarar la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto con `composeExtensions` la propiedad. Actualmente, se limita a crear una extensión de mensajería única para la aplicación.

> [!NOTE]
> El manifiesto hace referencia a extensiones de `composeExtensions`mensajería como. Esto es para mantener la compatibilidad con versiones anteriores.

La definición de la extensión es un objeto que tiene la estructura siguiente:

| Nombre de la propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | IDENTIFICADOR único de la aplicación de Microsoft para el bot como se registra con bot Framework. Suele ser el mismo que el identificador de la aplicación general de Microsoft Teams. | Sí |
| `scopes` | Matriz que declara si esta extensión se puede Agregar a `personal` o `team` a ámbitos (o ambos). | Sí |
| `canUpdateConfiguration` | Habilita el elemento de menú **configuración** . | No |
| `commands` | Matriz de comandos compatibles con esta extensión de mensajería. Tiene un límite de 10 comandos. | Sí |

#### <a name="define-commands"></a>Definir comandos

La extensión de mensajería debe declarar un comando, que aparece cuando el usuario selecciona la aplicación desde el botón **más opciones** (**&#8943;**) en el cuadro de redacción.

![Captura de pantalla de la lista de extensiones de mensajería en Microsoft Teams](~/assets/images/compose-extensions/compose-extension-list.png)

En el manifiesto de la aplicación, el elemento de comando es un objeto con la estructura siguiente:

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | IDENTIFICADOR único que asigna a este comando. La solicitud del usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Establezca el tipo de comando. Los valores posibles incluyen `query` y `action`. Si no está presente, el valor predeterminado se establece en`query` | No | 1.4 |
| `initialRun` | Parámetro opcional, usado con `query` comandos. Si se establece en **true**, indica que este comando debe ejecutarse en cuanto el usuario seleccione este comando en la interfaz de usuario. | No | 1.0 |
| `fetchTask` | Parámetro opcional, usado con `action` comandos. Se establece en **true** para recuperar la tarjeta adaptable o la dirección URL web que se mostrará en el [módulo de tareas](~/task-modules-and-cards/what-are-task-modules.md). Se usa cuando las entradas del `action` comando son dinámicas en lugar de un conjunto estático de parámetros. Tenga en cuenta que el si se establece en **true** , se omite la lista de parámetros estáticos del comando. | No | 1.4 |
| `parameters` | Lista estática de parámetros para el comando. | Sí | 1.0 |
| `parameter.name` | Nombre del parámetro. Se envía al servicio en la solicitud del usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Nombre corto o etiqueta del parámetro sencillo para el usuario. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada requerido. Los valores posibles `text`son `textarea`: `number`, `date`, `time`, `toggle`,. El valor predeterminado está establecido en`text` | No | 1.4 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción del mensaje. Los valores posibles `message`son `compose`, o `commandBox`. El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |
