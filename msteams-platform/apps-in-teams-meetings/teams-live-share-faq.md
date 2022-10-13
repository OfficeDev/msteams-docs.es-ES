---
title: Preguntas más frecuentes sobre Live Share
author: surbhigupta
description: En este módulo, obtendrá más información sobre las preguntas más frecuentes de Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 857c81a364798efd79256c8cdf609a7d625342ad
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560606"
---
---

# <a name="live-share-sdk-faq"></a>Preguntas más frecuentes sobre el SDK de Live Share

Obtenga respuestas a preguntas comunes al usar Live Share.<br>

<br>

<details>

<summary><b>¿Puedo usar mi propio servicio de Azure Fluid Relay?</b></summary>

Sí. Al inicializar Live Share, puede definir su propio `AzureConnectionConfig`. Live Share asocia los contenedores que crea con reuniones, pero deberá implementar la `ITokenProvider` interfaz para firmar tokens para los contenedores. Por ejemplo, puede usar un elemento proporcionado `AzureFunctionTokenProvider`, que usa una función en la nube de Azure para solicitar un token de acceso desde un servidor.

Aunque a la mayoría le parece beneficioso usar nuestro servicio hospedado gratuito, es posible que todavía haya ocasiones en las que sea beneficioso usar su propio servicio De Azure Fluid Relay para la aplicación Live Share. Considere la posibilidad de usar una conexión de servicio AFR personalizada si:

* Requerir almacenamiento de datos en contenedores Fluid más allá de la duración de una reunión.
* Transmitir datos confidenciales a través del servicio que requiere una directiva de seguridad personalizada.
* Desarrolle características a través de Fluid Framework, por ejemplo, `SharedMap`, para la aplicación fuera de Teams.

Para obtener más información, consulte [cómo guiar](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md) o visitar la [documentación de Azure Fluid Relay](/azure/azure-fluid-relay/).

<br>

</details>

<details>

<summary><b>¿Cuánto tiempo son accesibles los datos almacenados en el servicio hospedado de Live Share?</b></summary>

Los datos enviados o almacenados a través de contenedores de Fluid creados por el servicio Azure Fluid Relay hospedado de Live Share son accesibles durante 24 horas. Si quiere conservar los datos más allá de 24 horas, puede reemplazar nuestro servicio Azure Fluid Relay hospedado por el suyo propio. Como alternativa, puede usar su propio proveedor de almacenamiento en paralelo al servicio hospedado de Live Share.

<br>

</details>

<details>

<summary><b>¿Qué tipos de reuniones admite Live Share?</b></summary>

Se admiten reuniones programadas, llamadas uno a uno, llamadas grupales y reuniones ahora. Las reuniones de canal aún no se admiten.

<br>

</details>

<details>

<summary><b>¿Funcionará el paquete multimedia de Live Share con contenido DRM?</b></summary>

No. Actualmente, Teams no admite medios cifrados para aplicaciones de tabulación en el escritorio. Se admiten clientes de Chrome, Edge y móviles. Para obtener más información, puede [realizar un seguimiento del problema aquí](https://github.com/microsoft/live-share-sdk/issues/14).

<br>

</details>

<details>
<summary><b>¿Cuántas personas pueden asistir a una sesión de Live Share?</b></summary>

Actualmente, Live Share admite un máximo de 100 asistentes por sesión. Si esto es algo que le interesa, puede [iniciar una discusión aquí](https://github.com/microsoft/live-share-sdk/discussions).

<br>

</details>

<details>
<summary><b>¿Puedo usar las estructuras de datos de Live Share fuera de Teams?</b></summary>

Actualmente, los paquetes de Live Share requieren que el SDK de cliente de Teams funcione correctamente. Las características de `@microsoft/live-share` o `@microsoft/live-share-media` no funcionarán fuera de Microsoft Teams. Si esto es algo que le interesa, puede [iniciar una discusión aquí](https://github.com/microsoft/live-share-sdk/discussions).

<br>

</details>

<details>
<summary><b>¿Puedo usar varios contenedores Fluid?</b></summary>

Actualmente, Live Share solo admite tener un contenedor con nuestro servicio Azure Fluid Relay proporcionado. Sin embargo, es posible usar un contenedor de Live Share y un contenedor creado por su propia instancia de Azure Fluid Relay.

<br>

</details>

<details>
<summary><b>¿Puedo cambiar el esquema de contenedor de Fluid después de crear el contenedor?</b></summary>

Actualmente, Live Share no admite la adición de nuevos `initialObjects` elementos a Fluid `ContainerSchema` después de crear o unirse a un contenedor. Dado que las sesiones de Live Share son de corta duración, suele ser un problema durante el desarrollo después de agregar nuevas características a la aplicación.

> [!NOTE]
> Si usa la `dynamicObjectTypes` propiedad en `ContainerSchema`, puede agregar nuevos tipos en cualquier momento. Si más adelante quita tipos del esquema, se producirá un error en las instancias de DDS existentes de esos tipos.

Para corregir los errores resultantes de los cambios en al realizar pruebas localmente en el explorador, quite el identificador de contenedor con hash de la dirección URL y vuelva a `initialObjects` cargar la página. Si va a realizar pruebas en una reunión de Teams, inicie una nueva reunión e inténtelo de nuevo.

Si planea actualizar la aplicación con frecuencia con instancias nuevas o `LiveObject` nuevas`SharedObject`, debe tener en cuenta cómo implementar nuevos cambios de esquema en producción. Aunque el riesgo real es relativamente bajo y de corta duración, puede haber sesiones activas en el momento de implementar el cambio. Los usuarios existentes en la sesión no deben verse afectados, pero los usuarios que se unan a esa sesión después de implementar un cambio importante pueden tener problemas para conectarse a la sesión. Para mitigar esto, puede considerar algunas de las siguientes soluciones:

* Implemente los cambios de esquema para la aplicación web fuera del horario comercial normal.
* Use `dynamicObjectTypes` para los cambios realizados en el esquema, en lugar de cambiar `initialObjects`.

> [!NOTE]
> Live Share no admite actualmente el control de `ContainerSchema`versiones de , ni tiene ninguna API dedicada a las migraciones.

<br>

</details>

<details>
<summary><b>¿Hay límites para cuántos eventos de cambio puedo emitir a través de Live Share?</b></summary>

Mientras Live Share está en versión preliminar, no se aplica ningún límite a los eventos emitidos a través de Live Share. Para obtener un rendimiento óptimo, debe eliminar los cambios emitidos a través `SharedObject` de instancias o `LiveObject` a un mensaje cada 50 milisegundos o más. Esto es especialmente importante al enviar cambios basados en coordenadas táctiles o de mouse, como al sincronizar posiciones de cursor, entrada manuscrita y arrastrar objetos alrededor de una página.

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>¿Tiene preguntas o comentarios?

Envíe problemas y solicitudes de características al repositorio del SDK para [SDK de Live Share](https://github.com/microsoft/live-share-sdk). Use la etiqueta `live-share` y `microsoft-teams` para publicar preguntas de procedimientos sobre el SDK en [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams).

## <a name="see-also"></a>Vea también

* [Repositorio de GitHub](https://github.com/microsoft/live-share-sdk)
* [Documentos de referencia del SDK de Live Share](/javascript/api/@microsoft/live-share/)
* [Documentos de referencia del SDK multimedia de Live Share](/javascript/api/@microsoft/live-share-media/)
* [Aplicaciones de Teams en las reuniones](teams-apps-in-meetings.md)
