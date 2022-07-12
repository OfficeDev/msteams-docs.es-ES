---
title: Elegir una configuración para probar y depurar la aplicación
description: En este módulo, aprenderá las opciones para probar y depurar aplicaciones de Microsoft Teams en el entorno local y hospedado en la nube.
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 1f8a444a889eec15495272877ea1cca75f313629
ms.sourcegitcommit: 526ad8562d3bacc13141cd7f695aa5f3f3752052
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2022
ms.locfileid: "66737394"
---
# <a name="choose-a-test-setup-and-debug-your-teams-app"></a>Elección de una configuración de prueba y depuración de la aplicación de Teams

Las aplicaciones de Microsoft Teams contienen una o varias funcionalidades y las formas de ejecutarlas o incluso hospedarlas son diferentes. Para la depuración, use una de las siguientes maneras:

* **Puramente local**: en el caso de los bots, puede probar la experiencia con Bot Emulator. Para otro contenido, puede ejecutarlo localmente en el explorador y direccionar el contenido a través de `http://localhost`.
* **Hospedado localmente en Teams**: esto implica ejecutar la aplicación localmente en el software de tunelización y [crear un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Teams. Esto le permite ejecutar y depurar fácilmente la aplicación dentro del cliente de Teams.
* **Hospedado en la nube en Teams**: esto simula realmente la compatibilidad a nivel de producción para una aplicación Teams. Implica cargar la solución en el servidor accesible externamente o en el proveedor de nube que prefiera y [crear un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Teams.

Ejecute la experiencia desde su propio equipo para realizar pruebas de Teams puramente locales o locales. Al hacerlo, puede compilar y ejecutar en el entorno de desarrollo integrado y aprovechar al máximo las técnicas, como depuración con puntos de interrupción y paso a paso.

> [!NOTE]
> Para la depuración y las pruebas a escala de producción, le recomendamos que siga sus propias directrices de empresa para asegurarse de que puede admitir pruebas, ensayos e implementación a través de sus propios procesos.

Use varios manifiestos y paquetes para mantener la separación entre los servicios de producción y desarrollo. Por ejemplo, puede optar por registrar bots de desarrollo y producción independientes y crear los paquetes adecuados para cargarlos en el entorno de pruebas. También se recomienda cargar y probar el paquete de producción antes de enviar la aplicación para publicarla en nuestra tienda de aplicaciones o distribuirla a los clientes.

## <a name="purely-local"></a>Puramente local

> [!NOTE]
> La ejecución del bot localmente no le proporciona acceso a la funcionalidad de la aplicación de Teams ni a funciones del bot específicas de Teams, como llamadas a lista de participantes y otras funcionalidades específicas del canal. Además, bot Framework permite algunas funcionalidades en Bot Emulator que podrían no funcionar al ejecutarse en Teams.

El bot puede ejecutarse en Bot Emulator. Esto le permite probar parte de la lógica principal del bot, ver un diseño aproximado de los mensajes y realizar pruebas sencillas. Estos son los pasos:

1. Ejecute el código localmente.
2. Inicie Bot Emulator y establezca la dirección URL:
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. Deje el identificador de aplicación de Microsoft y la contraseña de la aplicación de Microsoft en blanco para que coincidan con las variables de entorno predeterminadas.

## <a name="locally-hosted"></a>Hospedado localmente

Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que accede estén disponibles públicamente mediante puntos de conexión HTTPS. Por lo tanto, para permitir que la aplicación funcione dentro de Teams, debe publicar el código en la nube que prefiera o hacer que nuestra instancia de ejecución local sea accesible externamente. Esto último se puede hacer con el software de tunelización.

Aunque puede usar cualquier herramienta que elija, usamos y recomendamos [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que se abre localmente en el equipo.

Para configurar ngrok como preparación para ejecutar la aplicación de Teams localmente, siga estos pasos:

1. Vaya al directorio donde tiene ngrok.exe instalado en una aplicación de terminal. Es posible que desee agregarla como una variable de ruta de acceso para evitar este paso.
2. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` o reemplace el número de puerto según sea necesario.
   Esto inicia ngrok para aparecer en el puerto especificado. A cambio, proporciona una dirección URL direccionable externamente válida durante el tiempo que ngrok se esté ejecutando.

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia.

Para usar ngrok en el proyecto en función de las funcionalidades que esté usando, debe reemplazar todas las referencias url del código, la configuración y el archivo manifest.json para usar este punto de conexión de dirección URL.

Para los bots registrados en Microsoft Bot Framework, actualice el punto de conexión de mensajería del bot para usar este nuevo punto de conexión de ngrok. Por ejemplo, `https://2d1224fb.ngrok.io/api/messages`. Puede validar que ngrok funciona probando respuesta del bot en la ventana del chat de prueba del portal de Bot Framework. Una vez más, al igual que el emulador, esta prueba no le permite acceder a la funcionalidad específica de Teams.

> [!NOTE]
>
> * Para actualizar el punto de conexión de mensajería de un bot, debe usar Bot Framework. Seleccione el bot en [la lista de bots de Bot Framework](https://dev.botframework.com/bots). No es necesario migrar el bot a Microsoft Azure. También puede actualizar el punto de conexión de mensajería a través de [App Studio](~/concepts/build-and-test/app-studio-overview.md).

> [!WARNING]
>
> * Si ha estado usando App Studio, le recomendamos que pruebe el Portal para desarrolladores para configurar, distribuir y administrar las aplicaciones de Teams. App Studio estará en desuso el 01 de agosto de 2022.

## <a name="cloud-hosted"></a>Hospedado en la nube

Puede usar cualquier servicio direccionable externamente para hospedar el código de desarrollo y producción y sus puntos de conexión HTTPS. No hay ninguna expectativa de que las funcionalidades residan en el mismo servicio. Necesitamos que se acceda a todos los dominios desde las aplicaciones de Teams que aparecen en el [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objeto del `manifest.json` archivo.

> [!NOTE]
> Para garantizar un entorno seguro, sea explícito sobre el dominio y los subdominios exactos a los que hace referencia y esos dominios deben estar en su control. Por ejemplo, no se recomienda `*.azurewebsites.net`, pero se recomienda `contoso.azurewebsites.net`.

## <a name="load-and-run-your-experience"></a>Cargar y ejecutar la experiencia

Para cargar y ejecutar su experiencia en Teams, debe crear un paquete y cargarlo en Teams. Para más información, vea:

* [Crear un paquete de aplicación para la aplicación de Microsoft Teams](~/concepts/build-and-test/apps-package.md).
* [Cargar la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Añadir datos de prueba al entorno](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>Consulte también

[Probar y depurar el bot localmente con el IDE](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally-with-ide)
