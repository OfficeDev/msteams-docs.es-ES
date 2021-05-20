## <a name="add-a-messaging-extension-to-your-app"></a>Añade una extensión de mensajería a tu aplicación

Una extensión de mensajería es un servicio hospedado en la nube que escucha las solicitudes de usuario y responde con datos estructurados, como una [tarjeta.](~/task-modules-and-cards/what-are-cards.md) Integre el servicio con Microsoft Teams a través de objetos de Bot `Activity` Framework. Nuestras extensiones .NET y Node.js para el SDK de Bot Builder pueden ayudarle a agregar funcionalidad de extensión de mensajería a la aplicación.

![Diagrama de flujo de mensajes para extensiones de mensajería](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Regístrese en el Marco del Bot

Si aún no lo ha hecho, primero debe registrar un bot con el Microsoft Bot Framework. El identificador de aplicación de Microsoft y los puntos de conexión de devolución de llamada del bot, tal como se definen allí, se usarán en la extensión de mensajería para recibir y responder a las solicitudes de usuario. Recuerde habilitar el canal de Microsoft Teams para el bot.

Registre el IDENTIFICADOR de la aplicación bot y la contraseña de la aplicación, deberá proporcionar el identificador de aplicación en el manifiesto de la aplicación.

### <a name="update-your-app-manifest"></a>Actualiza el manifiesto de la aplicación

Al igual que con los bots y las pestañas, actualiza el [manifiesto](~/resources/schema/manifest-schema.md#composeextensions) de la aplicación para incluir las propiedades de extensión de mensajería. Estas propiedades rigen cómo aparece y se comporta la extensión de mensajería en el cliente Microsoft Teams. Las extensiones de mensajería se admiten a partir de v1.0 del manifiesto.

#### <a name="declare-your-messaging-extension"></a>Declare su extensión de mensajería

Para agregar una extensión de mensajería, incluya una nueva estructura JSON de nivel superior en el manifiesto con la `composeExtensions` propiedad. Actualmente, está limitado a crear una única extensión de mensajería para la aplicación.

> [!NOTE]
> El manifiesto hace referencia a extensiones de mensajería como `composeExtensions` . Esto es para mantener la compatibilidad con versiones anteriores.

La definición de extensión es un objeto que tiene la siguiente estructura:

| Nombre de propiedad | Objetivo | ¿Necesario? |
|---|---|---|
| `botId` | El ID. de aplicación de Microsoft único para el bot, registrado con Bot Framework. Normalmente, esto debería ser el mismo que el identificador de la aplicación general de Teams. | Sí |
| `scopes` | Matriz que declara si esta extensión se puede agregar `personal` o `team` ámbitos (o ambos). | Sí |
| `canUpdateConfiguration` | Habilita **Configuración** elemento de menú. | No |
| `commands` | Matriz de comandos que admite esta extensión de mensajería. Está limitado a 10 comandos. | Sí |

#### <a name="define-commands"></a>Definir comandos

La extensión de mensajería debe declarar un comando, que aparece cuando el usuario selecciona la aplicación en el botón **Más opciones** (**&#8943;**) del cuadro de composición.

![Captura de pantalla de la lista de extensiones de mensajería en Teams](~/assets/images/compose-extensions/compose-extension-list.png)

En el manifiesto de aplicación, el elemento de comando es un objeto con la siguiente estructura:

| Nombre de propiedad | Objetivo | ¿Necesario? | Versión mínima del manifiesto |
|---|---|---|---|
| `id` | ID único que usted asigna a este comando. La solicitud de usuario incluirá este ID. | Sí | 1.0 |
| `title` | Nombre del comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `description` | Texto de ayuda que indica lo que hace este comando. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `type` | Establezca el tipo de comando. Los valores posibles incluyen `query` y `action`. Si no está presente, el valor predeterminado se establece en `query` . | No | 1.4 |
| `initialRun` | Parámetro opcional, utilizado con `query` comandos. Si se establece en **true**, indica que este comando debe ejecutarse tan pronto como el usuario elija este comando en la interfaz de usuario. | No | 1.0 |
| `fetchTask` | Parámetro opcional, utilizado con `action` comandos. Estabzca en **true** para obtener la tarjeta adaptable o la url web que se mostrarán dentro del [módulo de tareas.](~/task-modules-and-cards/what-are-task-modules.md) Esto se utiliza cuando las entradas al `action` comando son dinámicas en lugar de un conjunto estático de parámetros. Tenga en cuenta que el if establecido en **true** la lista de parámetros estáticos para el comando se omite. | No | 1.4 |
| `parameters` | Lista estática de parámetros para el comando. | Sí | 1.0 |
| `parameter.name` | Nombre del parámetro. Esto se envía a su servicio en la solicitud de usuario. | Sí | 1.0 |
| `parameter.description` | Describe los propósitos de este parámetro o el ejemplo del valor que se debe proporcionar. Este valor aparece en la interfaz de usuario. | Sí | 1.0 |
| `parameter.title` | Título o etiqueta de parámetros cortos fáciles de usar. | Sí | 1.0 |
| `parameter.inputType` | Estad en el tipo de entrada necesaria. Los valores posibles incluyen `text` , , , , `textarea` `number` `date` `time` `toggle` . El valor predeterminado se establece en `text` . | No | 1.4 |
| `context` | Matriz opcional de valores que define el contexto en el que está disponible la acción del mensaje. Los valores posibles son `message` `compose` , o `commandBox` . El valor predeterminado es `["compose", "commandBox"]`. | No | 1,5 |
