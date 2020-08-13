---
title: Depurar la aplicación de Teams
description: Describe los pasos que se deben seguir para ejecutar y depurar las aplicaciones de Microsoft Teams
keywords: Teams ejecutar aplicaciones de depuración
ms.topic: conceptual
ms.openlocfilehash: 913306bd24a55797e72396a031d917ec99c43bb9
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652212"
---
# <a name="debugging-your-teams-app"></a>Depurar la aplicación de Teams

Las aplicaciones de Microsoft Teams pueden contener una o más funcionalidades y las formas de ejecutar o incluso hospedarlas pueden ser diferentes. En general, en lo que se refiere a la depuración, tenemos las siguientes formas de ejecutar su aplicación de Microsoft Teams:

* **Puramente local** &emsp; Para los bots, puede probar su experiencia en el emulador de bot. Para otros contenidos, puede ejecutar localmente en el explorador y dirigir el contenido a través de `http://localhost` .
* **Hospedado localmente, en Teams** &emsp; Esto implica la ejecución local con software de tunelización y la [creación de un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Microsoft Teams. Esto le permite ejecutar y depurar fácilmente la aplicación en el cliente de Microsoft Teams.
* **Hospedado en la nube, en Teams** Esto simula realmente (o es) la compatibilidad de nivel de producción para una aplicación de Microsoft Teams. Implica cargar la solución en el servidor de accesible desde el exterior o en la nube que elija (recomendamos Azure, naturalmente) y [crea un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Microsoft Teams.

Para las pruebas puramente locales o locales de Teams, la experiencia se ejecuta desde su propio equipo. Esto le permite compilar y ejecutar en su IDE y aprovechar al máximo las técnicas como puntos de interrupción y depuración de pasos. Para realizar pruebas y depuración en el nivel de producción, se recomienda seguir sus propias directrices de la empresa para asegurarse de que puede admitir pruebas, staging e implementación a través de sus propios procesos.

En general, le recomendamos que use varios manifiestos y paquetes para permitirle mantener la separación entre los servicios de producción y desarrollo. Por ejemplo, puede optar por registrar los bots independientes de desarrollo y producción, y crear los paquetes apropiados para cargarlos en el entorno de prueba. También le recomendamos que cargue y pruebe el paquete de producción antes de enviar la aplicación para publicarla en nuestra tienda de aplicaciones o distribuirla a los clientes.

## <a name="purely-local"></a>Puramente local

> [!NOTE]
> La ejecución de esta manera no le da acceso a las funciones de la aplicación Teams o a las funciones de bot específicas de Teams, como las llamadas de la lista y otras funciones específicas del canal. Además, el marco de bot puede permitir algunas capacidades en el emulador de bot? n que podrían no funcionar cuando se ejecutan en Microsoft Teams.

El bot se puede ejecutar en el emulador de bot. Esto le permite probar parte de la lógica principal del bot, ver un diseño aproximado de mensajes y realizar pruebas sencillas. Para ello, siga estos pasos:

* Ejecutar el código de forma local
* Inicie el emulador de Bot y establezca la dirección URL:
  * Node.js:`http://localhost:3978/api/messages`
  * .NET/C#:`http://localhost:3979/api/messages`
* Deje en blanco el identificador de aplicación y la contraseña de Microsoft app para que se ajusten a las variables de entorno predeterminadas.

## <a name="locally-hosted"></a>Hospedado localmente

Debido a que Microsoft Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que tenga acceso estén disponibles públicamente mediante extremos HTTPS. Por lo tanto, para habilitar la aplicación para que funcione en Microsoft Teams, debe publicar el código en la nube que elija o hacer que nuestra instancia local de ejecución sea accesible externamente. Podemos hacer esto último con software de túnel.

Aunque puede usar cualquier herramienta, se usa y se recomienda [ngrok](https://ngrok.com/download), que crea una dirección URL externamente direccionable para un puerto que se abre de forma local en el equipo. Para configurar ngrok en preparación para la ejecución local de la aplicación de Microsoft Teams:

* En una aplicación de terminal, vaya al directorio en el que ha instalado ngrok.exe. Es posible que desee agregarla como variable de ruta de acceso para evitar este paso.
* Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` o reemplace el número de Puerto según sea necesario.

Se inicia ngrok para escuchar en el puerto especificado. A cambio, le proporciona una dirección URL que se puede direccionar externamente, válida durante el tiempo que se ejecute ngrok.

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia.

Para usar ngrok en el proyecto y las capacidades que use, debe reemplazar todas las referencias a direcciones URL en el código, la configuración o el manifest.jsen el archivo para usar este extremo de dirección URL.

Por ejemplo, para bots registrados en Microsoft bot Framework, actualice el punto de conexión de mensajería del bot para que use este nuevo extremo de ngrok. Por ejemplo, `https://2d1224fb.ngrok.io/api/messages`. Puede comprobar que ngrok funciona mediante la prueba de la respuesta de bot en la ventana probar chat del portal de bot Framework. (De nuevo, al igual que el emulador, esta prueba no permite el acceso a funciones específicas de Teams).

> [!NOTE]
> Para actualizar el punto de conexión de mensajería de un bot, debe usar el marco de robots. Haga clic en su bot en [su lista de bots en el marco de bot](https://dev.botframework.com/bots). No es necesario migrar el bot a Microsoft Azure. También puede actualizar el punto de conexión de mensajería a través de [App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="cloud-hosted"></a>Hospedado en la nube

Puede usar cualquier servicio externamente direccionable para hospedar el código de desarrollo y producción y sus extremos HTTPS. No hay expectativa de que sus funciones residan en el mismo servicio. Es necesario que todos los dominios a los que se accede desde las aplicaciones de Microsoft Team aparezcan en el [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objeto de la manifest.jsen el archivo.

> [!NOTE]
> Para garantizar un entorno seguro, debe ser explícito acerca del dominio y los subdominios exactos a los que hace referencia, y esos dominios deben estar en el control. Por ejemplo, `*.azurewebsites.net` no se recomendaría, pero sí? `contoso.azurewebsites.net` .

## <a name="loading-and-running"></a>Carga y ejecución

En general, para cargar y ejecutar la experiencia en Microsoft Teams, debe crear un paquete y cargarlo en Teams con las siguientes instrucciones:

* [Crear el paquete para su aplicación de Microsoft Teams](~/concepts/build-and-test/apps-package.md)
* [Cargar la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md)
