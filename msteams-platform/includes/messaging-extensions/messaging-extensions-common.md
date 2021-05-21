## <a name="add-a-messaging-extension-to-your-app"></a>Agregar una extensión de mensajería a la aplicación

Una extensión de mensajería es un servicio hospedado en la nube que escucha las solicitudes de los usuarios y responde con datos estructurados, como una [tarjeta.](~/task-modules-and-cards/what-are-cards.md) Integre el servicio con Microsoft Teams a través de objetos de Bot `Activity` Framework. Nuestras extensiones .NET y Node.js para el SDK de Bot Builder pueden ayudarte a agregar funcionalidad de extensión de mensajería a la aplicación.

![Diagrama de flujo de mensajes para extensiones de mensajería](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Registrarse en bot framework

Si aún no lo ha hecho, primero debe registrar un bot con el Microsoft Bot Framework. Los puntos de conexión de id. de aplicación y de devolución de llamada de Microsoft para el bot, tal como se definen allí, se usarán en la extensión de mensajería para recibir y responder a las solicitudes de los usuarios. Recuerde habilitar el canal Microsoft Teams para el bot.

Registra el id. de la aplicación bot y la contraseña de la aplicación, deberás proporcionar el identificador de la aplicación en el manifiesto de la aplicación.

### <a name="update-your-app-manifest"></a>Actualizar el manifiesto de la aplicación

Al igual que con los bots y las pestañas, actualizas el [manifiesto](~/resources/schema/manifest-schema.md#composeextensions) de la aplicación para incluir las propiedades de extensión de mensajería. Estas propiedades rigen cómo aparece y se comporta la extensión de mensajería en el Microsoft Teams cliente. Las extensiones de mensajería se admiten a partir de la versión 1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declarar la extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto con la `composeExtensions` propiedad. Actualmente, estás limitado a crear una sola extensión de mensajería para tu aplicación.

> [!NOTE]
> El manifiesto hace referencia a las extensiones de mensajería como `composeExtensions` . Esto es para mantener la compatibilidad con versiones anteriores.

La definición de extensión es un objeto que tiene la siguiente estructura:

| Nombre de la propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Normalmente, debería ser el mismo que el identificador de la aplicación Teams general. | Sí |
| `scopes` | Matriz que declara si esta extensión se puede agregar a `personal` o `team` ámbitos (o ambos). | Sí |
| `canUpdateConfiguration` | Habilita **Configuración** elemento de menú. | No |
| `commands` | Matriz de comandos compatibles con esta extensión de mensajería. Está limitado a 10 comandos. | Sí |

#### <a name="define-commands"></a>Definir comandos

La extensión de mensajería debe declarar un comando, que aparece cuando el usuario selecciona la aplicación en el botón Más **opciones** (**&#8943;**) en el cuadro de redacción.

![Captura de pantalla de la lista de extensiones de mensajería en Teams](~/assets/images/compose-extensions/compose-extension-list.png)

En el manifiesto de la aplicación, el elemento de comando es un objeto con la siguiente estructura:

| Nombre de la propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | Identificador único que se asigna a este comando. La solicitud de usuario incluirá este identificador. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Establezca el tipo de comando. Los valores posibles incluyen `query` y `action`. Si no está presente, el valor predeterminado se establece en `query` . | No | 1.4 |
| `initialRun` | Parámetro opcional, usado con `query` comandos. Si se establece en **true,** indica que este comando debe ejecutarse tan pronto como el usuario elija este comando en la interfaz de usuario. | No | 1.0 |
| `fetchTask` | Parámetro opcional, usado con `action` comandos. Se establece **en true** para capturar la tarjeta adaptable o la dirección URL web que se va a mostrar en el módulo [de tareas](~/task-modules-and-cards/what-are-task-modules.md). Esto se usa cuando las entradas al comando son dinámicas en lugar de `action` un conjunto estático de parámetros. Tenga en cuenta que si se establece en **true,** se omite la lista de parámetros estáticos del comando. | No | 1.4 |
| `parameters` | Lista estática de parámetros para el comando. | Sí | 1.0 |
| `parameter.name` | Nombre del parámetro. Esto se envía al servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o un ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Título o etiqueta de parámetros fáciles de usar cortos. | Sí | 1.0 |
| `parameter.inputType` | Se establece en el tipo de entrada necesario. Los valores posibles `text` incluyen , , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado se establece en `text` . | No | 1.4 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción del mensaje. Los valores posibles `message` `compose` son , o `commandBox` . El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |
