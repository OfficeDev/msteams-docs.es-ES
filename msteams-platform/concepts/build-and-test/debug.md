---
title: Elegir una configuración para probar y depurar la aplicación
description: Describe las opciones para probar y depurar aplicaciones de Microsoft Teams
keywords: Los equipos ejecutan aplicaciones de depuración
ms.topic: conceptual
ms.openlocfilehash: ea851a0d3ecf3ec87093bcc095050190a282c25e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797802"
---
# <a name="choosing-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Elegir una configuración para probar y depurar la aplicación de Microsoft Teams

Las aplicaciones de Microsoft Teams pueden contener una o más funcionalidades, y las formas de ejecutarlas o incluso hospedarlas pueden ser diferentes. En lo que respecta a la depuración, en general, tenemos las siguientes formas de ejecutar la aplicación de Microsoft Teams:

* **Puramente local** &emsp; Para los bots, puede probar su experiencia en el emulador de bots. Para otro contenido, puede ejecutar localmente en el explorador y dirigir el contenido a través `http://localhost` de .
* **Hospedado localmente, en Teams** &emsp; Esto implica ejecutarse localmente con software de túnel y [crear un paquete para](~/concepts/build-and-test/apps-package.md) [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Teams. Esto le permite ejecutar y depurar fácilmente la aplicación en el cliente de Teams.
* **Hospedado en la nube, en Teams** Esto realmente simula (o es) compatibilidad de nivel de producción para una aplicación de Teams. Implica cargar la solución en el servidor accesible externamente o el proveedor de [](~/concepts/build-and-test/apps-package.md) nube de su elección (le recomendamos Azure, por supuesto) y crear un paquete para cargarlo [en](~/concepts/deploy-and-publish/apps-upload.md) Teams.

Para las pruebas de Teams puramente locales o locales, puede ejecutar la experiencia desde su propio equipo. Esto le permite compilar y ejecutar realmente en su IDE y aprovechar al máximo técnicas como puntos de interrupción y depuración de pasos. Para las pruebas y depuración a escala de producción, le recomendamos que siga las directrices de su propia empresa para asegurarse de que puede admitir pruebas, almacenamiento provisional e implementación a través de sus propios procesos.

En general, se recomienda usar varios manifiestos y paquetes para permitirle mantener la separación entre los servicios de producción y desarrollo. Por ejemplo, puede elegir registrar bots de desarrollo y producción independientes y crear paquetes adecuados para cargarlos en el entorno de pruebas. También te recomendamos que cargues y pruebes el paquete de producción antes de enviar la aplicación para publicarla en nuestra tienda de aplicaciones o distribuirla a los clientes.

## <a name="purely-local"></a>Puramente local

> [!NOTE]
> Si se ejecuta de esta forma, no se proporciona acceso a la funcionalidad de la aplicación Teams ni a las funciones de bot específicas de Teams, como llamadas de lista y otras funciones específicas del canal. Además, algunas funcionalidades pueden ser permitidas por Bot Framework en el emulador de bots que podrían no funcionar al ejecutarse en Microsoft Teams.

El bot se puede ejecutar en el emulador de bots. Esto le permite probar parte de la lógica principal del bot, ver un diseño aproximado de los mensajes y realizar pruebas sencillas. Para ello, siga estos pasos:

* Ejecutar el código localmente
* Inicie el emulador de bots y establezca la dirección URL:
  * Node.js: `http://localhost:3978/api/messages`
  * .NET/C#: `http://localhost:3979/api/messages`
* Deje en blanco el identificador de aplicación de Microsoft y la contraseña de la aplicación de Microsoft para que coincidan con las variables de entorno predeterminadas.

## <a name="locally-hosted"></a>Hospedado localmente

Dado que Microsoft Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que accede estén disponibles públicamente mediante puntos de conexión HTTPS. Por lo tanto, para permitir que la aplicación funcione en Teams, debe publicar el código en la nube de su elección o hacer que nuestra instancia local en ejecución sea accesible externamente. Podemos hacerlo con software de túnel.

Aunque puedes usar cualquier herramienta que elijas, usamos y recomendamos [ngrok,](https://ngrok.com/download)que crea una dirección URL direccionable externamente para un puerto que abras localmente en tu equipo. Para configurar ngrok en preparación para ejecutar la aplicación de Microsoft Teams localmente:

* En una aplicación de terminal, vaya al directorio donde ngrok.exe instalado. Es posible que desee agregarla como una variable de ruta de acceso para evitar este paso.
* Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` o reemplace el número de puerto según sea necesario.

Esto inicia ngrok para escuchar en el puerto que especifique. A cambio, le proporciona una dirección URL direccionable externamente, válida mientras se ejecute ngrok.

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia.

Para usar ngrok en el proyecto y, en función de las capacidades que use, debe reemplazar todas las referencias de dirección URL en el archivo de código, configuración o manifest.json para usar este punto de conexión de dirección URL.

Por ejemplo, para los bots registrados en Microsoft Bot Framework, actualice el extremo de mensajería del bot para que use este nuevo punto de conexión ngrok. Por ejemplo, `https://2d1224fb.ngrok.io/api/messages`. Puede validar que ngrok funciona probando la respuesta del bot en la ventana de chat de prueba del portal de Bot Framework. (De nuevo, al igual que el emulador, esta prueba no le permite acceder a la funcionalidad específica de Teams).

> [!NOTE]
> Para actualizar el extremo de mensajería de un bot, debe usar bot Framework. Haga clic en el bot [en la lista de bots en Bot Framework.](https://dev.botframework.com/bots) No es necesario migrar el bot a Microsoft Azure. También puede actualizar el punto de conexión de mensajería a [través de App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="cloud-hosted"></a>Hospedado en la nube

Puede usar cualquier servicio direccionable externamente para hospedar el código de desarrollo y producción y sus extremos HTTPS. No hay ninguna expectativa de que sus capacidades residan en el mismo servicio. Sí es necesario que todos los dominios a los que se accede desde las aplicaciones de Microsoft Teams aparezcan en el objeto del [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) manifest.jsarchivo on.

> [!NOTE]
> Para garantizar un entorno seguro, sea explícito sobre el dominio y los subdominios exactos a los que hace referencia, y esos dominios deben estar bajo su control. Por ejemplo, `*.azurewebsites.net` no se recomienda, pero `contoso.azurewebsites.net` sí lo haría.

## <a name="loading-and-running"></a>Carga y ejecución

En general, para cargar y ejecutar su experiencia en Microsoft Teams, debe crear un paquete y cargarlo en Teams, con las siguientes instrucciones:

* [Crear el paquete para la aplicación de Microsoft Teams](~/concepts/build-and-test/apps-package.md)
* [Cargar la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md)
