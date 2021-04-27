---
title: Agregar bots personalizados a Microsoft Teams con webhooks salientes
description: describe cómo agregar un webhook saliente
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams tabs outgoing webhook actionable message verify webhook
ms.openlocfilehash: cfa8bd550eaf1f198b83cdcc1ee699c75ac1d34d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020214"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>Agregar bots personalizados a Teams con webhooks salientes

## <a name="what-are-outgoing-webhooks-in-teams"></a>¿Qué son los webhooks salientes en Teams?

Los webhooks son una forma eminente de que Teams se integre con aplicaciones externas. Un webhook es esencialmente una solicitud POST enviada a una dirección URL de devolución de llamada. Los webhooks salientes permiten a los usuarios enviar mensajes a su servicio web sin pasar por el proceso completo de creación de bots a través de [Microsoft Bot Framework](https://dev.botframework.com/).

El webhook saliente envía datos de Teams a cualquier servicio elegido que pueda aceptar una carga JSON. Después de agregar los webhooks salientes a un equipo, actúa como bot y busca mensajes en canales mediante **\@ mención**. Envía notificaciones a servicios web externos y responde con mensajes enriquecidos, que incluyen tarjetas e imágenes.

## <a name="outgoing-webhook-key-features"></a>Características clave del webhook saliente

| Característica | Descripción |
| ------- | ----------- |
| Configuración con ámbito| Los webhooks están en el ámbito del nivel de equipo. Debe pasar por el proceso de configuración de cada equipo en el que desee agregar el webhook saliente. |
| Mensajería reactiva| Los usuarios deben usar @mention para que el webhook reciba mensajes. Actualmente, los usuarios solo pueden enviar mensajes a un webhook saliente en canales públicos y no dentro del ámbito personal o privado. |
|Intercambio de mensajes HTTP estándar|Las respuestas aparecen en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier contenido de mensaje de marco de bot, por ejemplo, texto enriquecido, imágenes, tarjetas y emojis. Aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto `openURL` para .|
| Compatibilidad con métodos de la API de Teams|El webhook saliente envía un HTTP POST a un servicio web y procesa una respuesta de nuevo. No pueden tener acceso a otras API como recuperar la lista o lista de canales de un equipo.|

## <a name="creating-actionable-messages"></a>Creación de mensajes que requieren acción

Las tarjetas de conector incluyen tres botones visibles en la tarjeta. Cada botón se define en la `potentialAction` propiedad del mensaje mediante `ActionCard` acciones. Cada uno contiene un tipo de entrada; un campo de texto, un selector `ActionCard` de fechas o una lista de opciones múltiples. Cada `ActionCard` acción tiene una acción asociada, por ejemplo, `HttpPOST` .

Las tarjetas de conector admiten tres tipos de acciones:

| Acción | Descripción |
| ------- | ----------- |
| `ActionCard` |Presenta uno o varios tipos de entrada y acciones asociadas.|
| `HttpPOST` | Envía una solicitud POST a una dirección URL. |
| `OpenUri` |  Abre un URI en un explorador o aplicación independiente, opcionalmente tiene como destino diferentes URI basados en sistemas operativos.|

La acción `ActionCard` admite tres tipos de entrada:

| Tipo de entrada | Descripción |
| ------- | ----------- |
| `TextInput` | Campo de texto de línea única o multilínea con un límite de longitud opcional. |
| `DateInput` | Selector de fecha con un selector de hora opcional. |
| `MultichoiceInput` | Una lista especificada de opciones, que ofrece una selección única o varias selecciones.|

`MultichoiceInput` admite una `style` propiedad que controla la presentación de una lista totalmente expandida. El valor predeterminado de `style` depende del `isMultiSelect` valor.

| `isMultiSelect` value  | `style` valor predeterminado  |
| --- | --- |
| `false` o no especificado | El estilo predeterminado es `compact`|
| `true` | El estilo predeterminado es `expanded` |

> [!NOTE]
> * Escriba ambos y , si desea que la lista de selección múltiple se muestre `"isMultiSelect": true` `"style": true` en un estilo compacto.
> * Seleccionar la `compact` propiedad en Teams es lo mismo que seleccionar la propiedad en Microsoft `style` `normal` `style` Outlook.
> * Los webhooks solo admiten tarjetas de atrás de mensajes de Office 365 y tarjetas adaptables.

Para obtener todos los demás detalles acerca de las acciones de tarjeta de conector, vea **[Acciones](/outlook/actionable-messages/card-reference#actions)** en la referencia de tarjeta de mensaje que se puede realizar.

## <a name="adding-outgoing-webhooks-to-your-app"></a>Agregar webhooks salientes a la aplicación

**Escenario:** insertar notificaciones de estado de cambio en un servidor de base de datos de canal de Teams en la aplicación.  
**Ejemplo:** tiene una aplicación de línea de negocio que realiza un seguimiento de todas las operaciones CRUD realizadas a registros de empleados por los usuarios de recursos humanos del canal de Teams en un arrendamiento de Office 365.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. Crear una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON

El servicio recibe mensajes en un esquema de mensajería de servicio de bots de Azure estándar. El conector de marco de bot es un servicio RESTful que permite al servicio procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS, tal como se documenta en la API de servicio de bots [de Azure.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Como alternativa, puede seguir el [SDK de Microsoft Bot Framework] para procesar y analizar mensajes. Vea también [Acerca del servicio de bots de Azure](/azure/bot-service/bot-service-overview-introduction).


Los webhooks salientes están en el ámbito `team` del nivel y son visibles para todos los miembros del equipo. Al igual que un bot, los usuarios necesitan mencionar el nombre del webhook saliente para invocarlo en el canal. **\@**

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. Crear un método para comprobar el token HMAC de webhook saliente

#### <a name="hmac-signature-for-testing-with-code-example"></a>Firma HMAC para pruebas con código de ejemplo

Usando un ejemplo de mensaje entrante e id: "contoso" de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Use el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" en la autorización del encabezado de solicitud.

Para asegurarse de que el servicio recibe llamadas solo de clientes reales de Teams, Teams proporciona un código HMAC en el encabezado `hmac` HTTP. Siempre se incluyó el código en el protocolo de autenticación.

El código siempre debe validar la firma HMAC incluida en la solicitud:

* Genere el token HMAC desde el cuerpo de la solicitud del mensaje. Hay bibliotecas estándar para hacerlo en la mayoría de las plataformas (vea [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js o vea [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \# ). Microsoft Teams usa criptografía HMAC estándar SHA256. Debe convertir el cuerpo en una matriz de bytes en UTF8.
* Calcule el hash desde la matriz de bytes del token de seguridad proporcionado por **Teams** cuando registró el webhook saliente en el cliente de Teams]. Consulte [Create an outgoing webhook](#create-an-outgoing-webhook).
* Convertir el hash en una cadena mediante codificación UTF-8.
* Compare el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. Crear un método para enviar una respuesta correcta o de error

Las respuestas de los webhooks salientes aparecen en la misma cadena de respuesta que el mensaje original. Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica al servicio y el código obtiene cinco segundos para responder al mensaje antes de que la conexión se alome y finalice.

### <a name="example-response"></a>Ejemplo de respuesta

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Creación de un webhook saliente

1. Seleccione el equipo adecuado y elija **Administrar equipo** en el menú desplegable (&#8226;&#8226;&#8226;).
1. Elija la **pestaña Aplicaciones** en la barra de navegación.
1. En la esquina inferior derecha de la ventana, seleccione **Crear un webhook saliente.**
1. En la ventana emergente resultante, complete los campos necesarios:

>* **Nombre:** el título del webhook y @mention pulsa.
>* **Dirección URL de devolución** de llamada: el extremo HTTPS que acepta cargas JSON y recibe solicitudes POST de Teams.
>* **Descripción:** una cadena detallada que aparece en la tarjeta de perfil y en el panel de aplicaciones de nivel de equipo.
>* **Imagen de** perfil un icono de aplicación opcional para el webhook.
>* Seleccione el **botón** Crear en la esquina inferior derecha de la ventana emergente y el webhook saliente se agregará a los canales del equipo actual.
>* En la siguiente ventana de diálogo se muestra un token de seguridad de código de autenticación de mensajes [(HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basado en hash que se usa para autenticar llamadas entre Teams y el servicio externo designado.
>* El webhook saliente está disponible para los usuarios del equipo, solo si la dirección URL es válida y los tokens de autenticación de servidor y cliente son iguales, por ejemplo, un protocolo de enlace HMAC.

## <a name="code-sample"></a>Ejemplo de código
|**Nombre de ejemplo** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks salientes | Ejemplos para crear **bots personalizados** que se usarán en Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

