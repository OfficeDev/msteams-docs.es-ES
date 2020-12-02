---
title: Agregar bots personalizados a Microsoft Teams con webhooks salientes
author: laujan
description: Cómo agregar un webhook saliente
keywords: webhook saliente de pestañas de Teams *
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 61dc8441795925b53e5c8459f9c6eed5a28856e1
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552468"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a>Agregar bots personalizados a Microsoft Teams con webhooks salientes

## <a name="what-are-outgoing-webhooks-in-teams"></a>¿Qué son los webhooks salientes en Teams?

Los webhooks son una buena forma de que Microsoft Teams se integre con aplicaciones externas. Un webhook es básicamente una solicitud POST enviada a una dirección URL de devolución de llamada. En Teams, los webhooks salientes proporcionan una forma sencilla de permitir que los usuarios envíen mensajes al servicio Web sin tener que pasar por el proceso completo de creación de bots mediante [Microsoft bot Framework](https://dev.botframework.com/). Los webhooks salientes exponen datos de Teams a cualquier servicio seleccionado que pueda aceptar una carga JSON. Una vez que un webhook de salida se agrega a un equipo, actúa como bot, escuchando en los canales los mensajes que usan la **\@ mención**, el envío de notificaciones a servicios web externos y la respuesta con mensajes enriquecidos que pueden incluir tarjetas e imágenes.

## <a name="outgoing-webhook-key-features"></a>Características de la clave de webhook saliente

| Característica | Descripción |
| ------- | ----------- |
| Configuración con ámbito| Los webhooks tienen un ámbito en el nivel de equipo. Deberá pasar por el proceso de configuración para cada equipo al que quiera agregar el webhook saliente. |
| Mensajería reactiva| Los usuarios deben usar @mention para que el webhook reciba mensajes. Actualmente, los usuarios solo pueden hacer un mensaje de un webhook de salida en canales públicos y no dentro del ámbito personal o privado. |
|Intercambio de mensajes HTTP estándar|Las respuestas aparecerán en la misma cadena que el mensaje de solicitud original y pueden incluir cualquier contenido de mensaje del marco de Bot? (texto enriquecido, imágenes, tarjetas y emojis). **Nota**: aunque los webhooks salientes pueden usar tarjetas, no pueden usar ninguna acción de tarjeta excepto para `openURL` .|
| Compatibilidad del método de la API de Microsoft Teams|En Teams, los webhooks salientes envían un HTTP POST a un servicio Web y procesan una respuesta. No pueden tener acceso a ninguna otra API, como recuperar la lista o la lista de canales de un equipo.|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a>Adición de procesamiento de webhook saliente a la aplicación

**Escenario**: inserción de notificaciones de estado del cambio en un servidor de base de datos de canal de Microsoft Teams para la aplicación.  
**Ejemplo**: tiene una aplicación de línea de negocio que realiza un seguimiento de todas las operaciones CRUD realizadas a los registros de empleados por parte de los usuarios de recursos humanos de los equipos de recursos humanos en un arrendamiento de Office 365.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. crear una dirección URL en el servidor de la aplicación para aceptar y procesar una solicitud POST con una carga JSON

El servicio recibirá mensajes en el esquema de mensajería estándar del servicio de robots de Azure. Bot Framework Connector es un servicio RESTful que permite al servicio procesar el intercambio de mensajes con formato JSON a través de protocolos HTTPS, tal como se documenta en la [API del servicio de bot de Azure](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Como alternativa, puede seguir [Microsoft bot Framework SDK] para procesar y analizar mensajes. *Consulte también*  [acerca del servicio de bot de Azure](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).

Los webhooks de salida tienen un ámbito de `team` nivel y son visibles para todos los miembros del equipo. Al igual que un bot, los usuarios deben **\@ mencionar** el nombre del webhook saliente para invocarlo en el canal.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. crear un método para comprobar el token HMAC de webhook saliente

#### <a name="hmac-signature-for-testing-with-code-example"></a>Ejemplo de la firma HMAC para pruebas con código

Uso de un ejemplo de mensaje entrante e identificador: "Contoso" de SigningKeyDictionary de {"Contoso", "vqF0En + Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA ="}.

Use el valor "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs + mO41mPL + R1e1U =" en el encabezado Authorization of request.

Para asegurarse de que el servicio recibe llamadas de clientes de equipos reales, Teams proporciona un código HMAC en el `hmac` encabezado HTTP que siempre debe incluirse en el protocolo de autenticación.

El código siempre debe validar la firma HMAC que se incluye en la solicitud:

* *Generar* el token HMAC desde el cuerpo de la solicitud del mensaje. Hay bibliotecas estándar para hacer esto en la mayoría de las plataformas (*consulte* [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js o  *See* [Team webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \# ). Microsoft Teams usa la criptografía de HMAC estándar SHA256. Tendrá que convertir el cuerpo en una matriz de bytes en UTF8.
* *Calcule* el hash a partir de la matriz de bytes del token de seguridad **proporcionado por Teams** cuando registró el webhook saliente en el cliente de Teams. *Consulte* [crear un webhook saliente](#create-an-outgoing-webhook), a continuación.
* *Convierta* el hash en una cadena con codificación UTF-8.
* *Compare* el valor de cadena del hash generado con el valor proporcionado en la solicitud HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. crear un método para enviar una respuesta correcta o incorrecta

Las respuestas del webhook saliente aparecerán en la misma cadena de respuesta que el mensaje original. Cuando el usuario realiza una consulta, Microsoft Teams emite una solicitud HTTP sincrónica a su servicio y el código tendrá 5 segundos para responder al mensaje antes de que se agote el tiempo de espera de la conexión y finalice.

### <a name="example-response"></a>Ejemplo de respuesta

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Creación de un webhook saliente

1. Seleccione el equipo adecuado y seleccione **administrar equipo** en el menú desplegable (&#8226;&#8226;&#8226;).
1. Elija la pestaña **aplicaciones** de la barra de navegación.
1. En la esquina inferior derecha de la ventana, seleccione **crear un webhook saliente**.
1. En la ventana emergente resultante, complete los campos obligatorios:

>* **Name** : el título del webhook y el @mention TAP.
>* **URL de devolución de llamada** : el extremo https que acepta cargas JSON y recibirá solicitudes post de Teams.
>* **Description** : una cadena detallada que aparecerá en la tarjeta de perfil y en el panel de la aplicación de nivel de equipo.
>* **Imagen de perfil** (opcional) icono de aplicación para el webhook.
>* Seleccione el botón **crear** desde la esquina inferior derecha de la ventana emergente y el webhook de salida se agregará a los canales del equipo actual.
>* La siguiente ventana de diálogo mostrará un token [de seguridad de código de autenticación de mensajes (HMAC) basado en hash](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) que se usará para autenticar las llamadas entre Microsoft Teams y el servicio externo designado.
>* Si la dirección URL es válida y los tokens de autenticación del servidor y del cliente son iguales (es decir, un protocolo de enlace HMAC), el webhook saliente estará disponible para los usuarios del equipo.

## <a name="code-samples"></a>Muestras de código

Puede ver ejemplos de código de webhook salientes en GitHub:

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-samples-outhook-webhook-NodeJS](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>CA\#

[OfficeDev/Microsoft-Teams-Sample-outhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
