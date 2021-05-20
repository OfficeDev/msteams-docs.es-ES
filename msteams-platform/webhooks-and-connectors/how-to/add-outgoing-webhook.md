---
title: Agregue bots personalizados a Microsoft Teams con webhooks salientes
description: describe cómo agregar un webhook saliente
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: los equipos pestañas saliente webhook mensaje procesable verificar webhook
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566533"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>Agregue bots personalizados a Teams con webhooks salientes

## <a name="outgoing-webhooks-in-teams"></a>Webhooks salientes en Teams

Los webhooks son una forma eminente de Teams integrarse con aplicaciones externas. Un webhook es esencialmente una solicitud POST enviada a una dirección URL de devolución de llamada. Los webhooks salientes permiten a los usuarios enviar mensajes a su servicio web sin pasar por todo el proceso de creación de bots a través de [la Microsoft Bot Framework](https://dev.botframework.com/).

Webhook saliente envía datos de Teams a cualquier servicio elegido capaz de aceptar una carga JSON. Después de agregar los webhooks salientes a un equipo, actúa como un bot y busca mensajes en canales mediante **\@ mención.** Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes.

## <a name="outgoing-webhook-key-features"></a>Características salientes de la clave webhook

| Característica | Descripción |
| ------- | ----------- |
| Configuración con ámbito| Los webhooks tienen ámbito a nivel de equipo. Debe pasar por el proceso de configuración de cada equipo en el que desee agregar el webhook saliente. |
| Mensajería reactiva| Los usuarios deben usar @mention para que el webhook reciba mensajes. Actualmente, los usuarios solo pueden enviar mensajes a un webhook saliente en canales públicos y no dentro del ámbito personal o privado. |
|Intercambio de mensajes HTTP estándar|Las respuestas aparecen en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier contenido de mensaje de marco de trabajo de bots, por ejemplo, texto enriquecido, imágenes, tarjetas y emojis. Aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto `openURL` para .|
| Teams Compatibilidad con métodos API|Webhook saliente envía un HTTP POST a un servicio web y procesa una respuesta. No pueden acceder a otras API como recuperar la lista o la lista de canales de un equipo.|

## <a name="creating-actionable-messages"></a>Creación de mensajes que requieren acción

Las tarjetas del conector incluyen tres botones visibles en la tarjeta. Cada botón se define en la `potentialAction` propiedad del mensaje mediante `ActionCard` acciones. Cada `ActionCard` uno contiene un tipo de entrada; un campo de texto, un selector de fecha o una lista de varias opciones. Cada `ActionCard` acción tiene una acción asociada, por ejemplo, `HttpPOST` .

Las tarjetas de conector admiten tres tipos de acciones:

| Acción | Descripción |
| ------- | ----------- |
| `ActionCard` |Presenta uno o varios tipos de entrada y acciones asociadas.|
| `HttpPOST` | Envía una solicitud POST a una dirección URL. |
| `OpenUri` |  Abre un URI en un explorador o aplicación independiente, opcionalmente tiene como destino diferentes URI en función de los sistemas operativos.|

La acción `ActionCard` admite tres tipos de entrada:

| Tipo de entrada | Descripción |
| ------- | ----------- |
| `TextInput` | Un campo de texto de una sola línea o multilínea con un límite de longitud opcional. |
| `DateInput` | Un selector de fechas con un selector de hora opcional. |
| `MultichoiceInput` | Una lista especificada de opciones, que ofrece una sola selección o varias selecciones.|

`MultichoiceInput` admite una `style` propiedad que controla la visualización de una lista completamente expandida. El valor predeterminado depende `style` del `isMultiSelect` valor.

| `isMultiSelect` valor  | `style` valor predeterminado  |
| --- | --- |
| `false` o no especificado | El estilo predeterminado es `compact`|
| `true` | El estilo predeterminado es `expanded` |

> [!NOTE]
> * Introduzca ambos `"isMultiSelect": true` `"style": true` y, si desea que la lista de selección múltiple se muestre en un estilo compacto.
> * La selección de `compact` la propiedad en Teams es lo mismo que seleccionar para la propiedad en Microsoft `style` `normal` `style` Outlook.
> * Los webhooks solo admiten Office 365 tarjetas de devolución de mensajes y tarjetas adaptables.

Para obtener todos los demás detalles sobre las acciones de la tarjeta del conector, consulte **[Acciones](/outlook/actionable-messages/card-reference#actions)** en la referencia de la tarjeta de mensaje procesable.

## <a name="adding-outgoing-webhooks-to-your-app"></a>Agregar webhooks salientes a la aplicación

**Escenario:** inserte notificaciones de estado de cambio en un servidor de base de datos de canal Teams a la aplicación.  
**Ejemplo:** Tiene una aplicación de línea de negocio que realiza un seguimiento de todas las operaciones CRUD realizadas a los registros de empleados por Teams usuarios de recursos humanos de canal a través de una tenencia Office 365.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. Cree una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON

El servicio recibe mensajes en un esquema de mensajería de servicio de bots de Azure estándar. El conector del marco de trabajo de bots es un servicio RESTful que permite al servicio procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS documentados en la [API de Azure Bot Service](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Como alternativa, puede seguir el [SDK de Microsoft Bot Framework] para procesar y analizar mensajes. Consulte también [Acerca de Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).


Los webhooks salientes se limitan al `team` nivel y son visibles para todos los miembros del equipo. Al igual que un bot, los usuarios deben **\@ mencionar** el nombre del webhook saliente para invocarlo en el canal.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. Cree un método para verificar el token HMAC de webhook saliente

#### <a name="hmac-signature-for-testing-with-code-example"></a>Firma HMAC para pruebas con ejemplo de código

Ejemplo de mensaje de entrada e identificador: "contoso" de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Utilice el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" en la autorización del encabezado de solicitud.

Para asegurarse de que el servicio solo recibe llamadas de clientes Teams reales, Teams proporciona un código HMAC en el `hmac` encabezado HTTP. Siempre incluido el código en el protocolo de autenticación.

El código siempre debe validar la firma HMAC incluida en la solicitud:

* Genere el token HMAC a partir del cuerpo de la solicitud del mensaje. Hay bibliotecas estándar para hacer esto en la mayoría de las plataformas (consulte [Cripto](https://nodejs.org/api/crypto.html#crypto_crypto) para obtener Node.js o vea [Teams Ejemplo de Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) para C \# ). Microsoft Teams utiliza criptografía HMAC SHA256 estándar. Debe convertir el cuerpo en una matriz de bytes en UTF8.
* Calcule el hash desde la matriz de bytes del token de seguridad **proporcionado por Teams** cuando registró el webhook saliente en el cliente Teams]. Consulte [Crear un webhook saliente](#create-an-outgoing-webhook).
* Convierta el hash en una cadena mediante codificación UTF-8.
* Compare el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. Crear un método para enviar una respuesta de éxito o fracaso

Las respuestas de los webhooks salientes aparecen en la misma cadena de respuesta que el mensaje original. Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio y el código obtiene cinco segundos para responder al mensaje antes de que se agote el tiempo de finalización y finalice la conexión.

### <a name="example-response"></a>Ejemplo de respuesta

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Creación de un webhook saliente

1. Seleccione el equipo adecuado y elija **Administrar equipo** en el menú desplegable (&#8226;&#8226;&#8226;).
1. Elija la pestaña **Aplicaciones** en la barra de navegación.
1. En la esquina inferior derecha de la ventana, seleccione **Crear un webhook saliente.**
1. En la ventana emergente resultante complete los campos obligatorios:

>* **Nombre**: El título del webhook y @mention toque
>* **URL de devolución de llamada:** el punto de conexión HTTPS que acepta cargas JSON y recibe solicitudes POST de Teams
>* **Descripción**: Una cadena detallada que aparece en la tarjeta de perfil y el panel de aplicaciones de nivel de equipo
>* **Imagen de perfil**: Un icono de aplicación opcional para tu webhook
>* Seleccione el botón **Crear** en la esquina inferior derecha de la ventana emergente y el webhook saliente se agrega a los canales del equipo actual.
>* La siguiente ventana de diálogo muestra un token de seguridad [de código de autenticación de mensajes (HMAC) basado en hash](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) que se usa para autenticar llamadas entre Teams y el servicio externo designado.
>* El webhook saliente está disponible para los usuarios del equipo, solo si la dirección URL es válida y los tokens de autenticación de servidor y cliente son iguales, por ejemplo, un protocolo de enlace HMAC.

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de la muestra** | **Descripción** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks salientes | Ejemplos para crear **bots personalizados** que se usarán en Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

