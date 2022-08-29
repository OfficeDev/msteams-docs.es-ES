---
title: Uso del servicio Azure Fluid Relay personalizado
author: surbhigupta
description: En este módulo, aprenderá a usar un servicio de Azure Fluid Relay personalizado con Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 07/21/2022
ms.openlocfilehash: baa192bf82e059b1cfe7a9fc8979874710f266b1
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425637"
---
---

# <a name="custom-azure-fluid-relay-service"></a>Servicio de Azure Fluid Relay personalizado

Aunque es probable que prefiera usar nuestro servicio hospedado gratuito, hay situaciones en las que es beneficioso usar su propio servicio de Azure Fluid Relay para la aplicación Live Share.

## <a name="pre-requisites"></a>Requisitos previos

1. Cree un panel lateral de la reunión y una extensión de reunión de la aplicación de fase, como se muestra en el [tutorial de rodillos de dados](../teams-live-share-tutorial.md).
2. Actualice el manifiesto de la aplicación para incluir todos los [permisos necesarios](../teams-live-share-capabilities.md#register-rsc-permissions).
3. Aprovisione un servicio de Azure Fluid Relay como se describe en este [tutorial](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal).

## <a name="connect-to-azure-fluid-relay-service"></a>Conexión al servicio Azure Fluid Relay

Al construir la clase `TeamsFluidClient`, puede definir su propio `AzureConnectionConfig`. Live Share asocia los contenedores que crea con reuniones, pero deberá implementar la `ITokenProvider` interfaz para firmar tokens para los contenedores. En este ejemplo se explica el de `AzureFunctionTokenProvider`Azure, que usa una función en la nube de Azure para solicitar un token de acceso desde un servidor.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_SERVICE_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, ITeamsFluidClientOptions } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps: ITeamsFluidClientOptions = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_FUNCTION_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

## <a name="why-use-a-custom-azure-fluid-relay-service"></a>¿Por qué usar un servicio de Azure Fluid Relay personalizado?

Considere la posibilidad de usar una conexión de servicio AFR personalizada si:

* Requerir almacenamiento de datos en contenedores Fluid más allá de la duración de una reunión.
* Transmitir datos confidenciales a través del servicio que requiere una directiva de seguridad personalizada.
* Desarrolle características a través de Fluid Framework para su aplicación fuera de Teams.

## <a name="why-use-live-share-with-your-custom-service"></a>¿Por qué usar Live Share con el servicio personalizado?

Azure Fluid Relay está diseñado para trabajar con cualquier aplicación basada en web, lo que significa que funciona con Microsoft Teams o sin él. Esto plantea una pregunta importante: si creo mi propio servicio de Azure Fluid Relay, ¿todavía necesito Live Share?

Live Share tiene características que son beneficiosas para escenarios comunes de reuniones que aumentan otras características de la aplicación, como:

* [Asignación de contenedores](#container-mapping)
* [Comprobación de roles y objetos efímeros](#ephemeral-objects-and-role-verification)
* [Sincronización de medios](#media-synchronization)

### <a name="container-mapping"></a>Asignación de contenedores

La clase de `TeamsFluidClient` Live Share es responsable de asignar un identificador de reunión único a los contenedores de Fluid, lo que garantiza que todos los participantes de la reunión se unan al mismo contenedor. Como parte de este proceso, el cliente intenta conectarse a un `containerId` asignado a la reunión que ya existe. Si no existe, se usa para crear un contenedor mediante `AzureConnectionConfig` y, a continuación, `AzureClient` retransmitirlo a otros participantes de la `containerId` reunión.

Si la aplicación ya tiene un mecanismo para crear contenedores de Fluid y compartirlos con otros miembros, como insertando en la `containerId` dirección URL compartida en la fase de reunión, puede que no sea necesario para la aplicación.

### <a name="ephemeral-objects-and-role-verification"></a>Comprobación de roles y objetos efímeros

Las estructuras de datos efímeras de Live Share como `EphemeralPresence`, `EphemeralState`y `EphemeralEvent` están adaptadas a la colaboración en reuniones y, por tanto, no se admiten en contenedores Fluid que se usan fuera de Microsoft Teams. Características como la verificación de roles ayudan a la aplicación a alinearse con las expectativas de nuestros usuarios.

> [!NOTE]
> Como ventaja adicional, los objetos efímeros también presentan latencias de mensajes más rápidas en comparación con las estructuras de datos fluid tradicionales.

Para obtener más información, consulte [la página de funcionalidades principales](../teams-live-share-capabilities.md) .

### <a name="media-synchronization"></a>Sincronización de medios

Los paquetes de `@microsoft/live-share-media` no se admiten en contenedores Fluid que se usan fuera de Microsoft Teams.

Para obtener más información, consulte la página [funcionalidades multimedia](../teams-live-share-media-capabilities.md) .

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Capacidades de Live Share](../teams-live-share-capabilities.md)
* [Funcionalidades de medios de Live Share](../teams-live-share-media-capabilities.md)
* [Preguntas más frecuentes sobre Live Share](../teams-live-share-faq.md)
* [Aplicaciones de Teams en las reuniones](../teams-apps-in-meetings.md)
