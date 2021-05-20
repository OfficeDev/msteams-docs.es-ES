---
title: Elegir una configuración para probar y depurar la aplicación
description: Describe las opciones para probar y depurar aplicaciones Microsoft Teams
keywords: equipos ejecutan aplicaciones de depuración
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 1f11834ad83e8bea7e4114d25d022df2f62c1700
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565161"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Elija una configuración para probar y depurar la aplicación Microsoft Teams

Microsoft Teams aplicaciones contienen una o más capacidades y las formas de ejecutarlas o incluso alojarlas son diferentes. Para la depuración, utilice una de las siguientes maneras:

* **Puramente local:** para bots, puede probar su experiencia en el emulador de bots. Para otros contenidos, puede ejecutarse localmente en el explorador y dirigir el contenido a través de `http://localhost` .
* **Hospedado localmente en Teams:** esto implica ejecutar la aplicación localmente en el software de tunelización y [crear un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Teams. Esto le permite ejecutar y depurar fácilmente la aplicación dentro del cliente Teams.
* **Alojado en la nube en Teams:** esto simula realmente la compatibilidad con el nivel de producción de una aplicación Teams. Implica cargar la solución en su servidor o proveedor de nube accesible externamente de su elección y [crear un paquete](~/concepts/build-and-test/apps-package.md) para [cargarlo](~/concepts/deploy-and-publish/apps-upload.md) en Teams.

Ejecute la experiencia desde su propio equipo para realizar pruebas de Teams puramente locales o locales. Al hacerlo, puede compilar y ejecutar dentro del entorno de desarrollo integrado y aprovechar al máximo las técnicas, como puntos de interrupción y depuración de pasos. 

> [!NOTE]
> Para la depuración y las pruebas a escala de producción, le recomendamos que siga las directrices de su propia empresa para asegurarse de que puede admitir pruebas, ensayo e implementación a través de sus propios procesos.

Utilice varios manifiestos y paquetes para mantener la separación entre los servicios de producción y desarrollo. Por ejemplo, puede optar por registrar bots de desarrollo y producción independientes y crear paquetes adecuados para cargarlos en el entorno de pruebas. También te recomendamos que cargues y pruebes tu paquete de producción antes de enviar tu aplicación para publicarla en nuestra tienda de aplicaciones o distribuirla a los clientes.

## <a name="purely-local"></a>Puramente local

> [!NOTE]
> La ejecución local del bot no le da acceso a Teams funcionalidad de la aplicación o funciones de bot específicas de Teams, como llamadas a listas y otras funciones específicas del canal. Además, el Bot Framework permite algunas capacidades en el emulador de bots que podrían no funcionar al ejecutarse en Microsoft Teams.

El bot se puede ejecutar en el emulador de bots. Esto le permite probar parte de la lógica principal del bot, ver un diseño aproximado de mensajes y realizar pruebas sencillas. A continuación se indican los pasos:

1. Ejecute el código localmente.
2. Inicie el emulador de bots y establezca la dirección URL:
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. Deje el identificador de aplicación de Microsoft y la contraseña de la aplicación de Microsoft en blanco, para que coincidan con las variables de entorno predeterminadas.

## <a name="locally-hosted"></a>Alojado localmente

Microsoft Teams es un producto completamente basado en la nube, requiere que todos los servicios a los que accede estén disponibles públicamente mediante puntos de conexión HTTPS. Por lo tanto, para permitir que la aplicación funcione dentro de Teams, debe publicar el código en la nube de su elección o hacer que nuestra instancia en ejecución local sea accesible externamente. Podemos hacer esto último con software de tunelización.

Aunque puede utilizar cualquier herramienta de su elección, usamos y recomendamos [ngrok](https://ngrok.com/download), que crea una URL direccionable externamente para un puerto que abre localmente en su máquina. 

**Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente**

1. Vaya al directorio donde tiene ngrok.exe instalado en una aplicación terminal. Es posible que desee agregarlo como una variable de ruta de acceso para evitar este paso.
2. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` o reemplace el número de puerto según sea necesario.
   Esto inicia ngrok para enumerar en el puerto que especifique. A cambio, le proporciona una dirección URL direccionable externamente válida durante el tiempo que ngrok se está ejecutando.

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia.

Para usar ngrok en el proyecto en función de las capacidades que esté utilizando, debe reemplazar todas las referencias de dirección URL del código, la configuración y el manifest.jsen el archivo para usar este punto de conexión de dirección URL.

Para los bots registrados en el Microsoft Bot Framework, actualice el punto de conexión de mensajería del bot para usar este nuevo punto de conexión ngrok. Por ejemplo, `https://2d1224fb.ngrok.io/api/messages`. Puede validar que ngrok está trabajando probando la respuesta del bot en la ventana de chat de prueba del portal de Bot Framework. Una vez más, al igual que el emulador, esta prueba no le permite acceder a Teams funcionalidad específica.

> [!NOTE]
> Para actualizar el punto de conexión de mensajería de un bot, debe usar Bot Framework. Seleccione el bot en [la lista de bots en Bot Framework](https://dev.botframework.com/bots). No es necesario migrar el bot a Microsoft Azure. También puede actualizar el punto de conexión de mensajería a través de [App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="cloud-hosted"></a>Hospedado en la nube

Puede usar cualquier servicio direccionable externamente para hospedar el código de desarrollo y producción y sus puntos de conexión HTTPS. No hay expectativas de que sus capacidades residan en el mismo servicio. Requerimos que se acceda a todos los dominios desde sus Microsoft Teams aplicaciones que aparecen en el [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objeto del `manifest.json` archivo.

> [!NOTE]
> Para garantizar un entorno seguro, sea explícito sobre el dominio exacto y los subdominios a los que hace referencia y esos dominios deben estar en su control. Por ejemplo, `*.azurewebsites.net` no se recomienda, sin embargo `contoso.azurewebsites.net` se recomienda.

## <a name="load-and-run-your-experience"></a>Cargue y ejecute su experiencia

Para cargar y ejecutar su experiencia dentro de Microsoft Teams, debe crear un paquete y cargarlo en Teams. Para más información vea:

* [Cree el paquete para la aplicación Microsoft Teams.](~/concepts/build-and-test/apps-package.md)
* [Upload la aplicación en Microsoft Teams.](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"] 
> [Añadir datos de prueba al entorno](~/concepts/build-and-test/test-data.md)

