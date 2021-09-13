---
title: Elegir una configuración para probar y depurar la aplicación
description: Describe las opciones para probar y depurar Microsoft Teams aplicaciones
keywords: teams ejecutar aplicaciones de depuración
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: c20f10fc0f3fb7265921ded2bf412271695bbcd9
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157058"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>Elige una configuración para probar y depurar tu Microsoft Teams aplicación

Microsoft Teams aplicaciones contienen una o más capacidades y las formas de ejecutarlas o incluso hospedarlas son diferentes. Para la depuración, use una de las siguientes maneras:

* **Puramente local:** para bots, puede probar su experiencia en el bot Emulator. Para otro contenido, puede ejecutar localmente en el explorador y dirigir el contenido a través `http://localhost` de .
* **Locally hosted in Teams:** This involves running the app locally in tunneling software and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams. Esto te permite ejecutar y depurar fácilmente la aplicación en el Teams cliente.
* **Hospedado en la nube en Teams:** esto realmente simula la compatibilidad de nivel de producción para una Teams aplicación. Implica cargar la solución en el servidor accesible externamente [](~/concepts/build-and-test/apps-package.md) o el proveedor de nube de elección y crear un paquete para cargarlo [en](~/concepts/deploy-and-publish/apps-upload.md) Teams.

Ejecute la experiencia desde su propio equipo para realizar pruebas de Teams locales. Al hacerlo, puede compilar y ejecutar en el entorno de desarrollo integrado y aprovechar al máximo técnicas, como puntos de interrupción y depuración de pasos. 

> [!NOTE]
> Para la depuración y las pruebas a escala de producción, se recomienda seguir las directrices de su propia empresa para asegurarse de que puede admitir pruebas, almacenamiento provisional e implementación a través de sus propios procesos.

Use varios manifiestos y paquetes para mantener la separación entre los servicios de producción y desarrollo. Por ejemplo, puede elegir registrar bots de desarrollo y producción independientes y crear paquetes adecuados para cargarlos en el entorno de pruebas. También te recomendamos que cargues y pruebes el paquete de producción antes de enviar la aplicación para publicarla en nuestra tienda de aplicaciones o distribuirla a los clientes.

## <a name="purely-local"></a>Puramente local

> [!NOTE]
> Ejecutar el bot localmente no le da acceso Teams la funcionalidad de la aplicación o Teams funciones de bot específicas, como llamadas de lista y otras funciones específicas del canal. Además, algunas funcionalidades están permitidas por Bot Framework en el bot Emulator que podrían no funcionar al ejecutarse en Microsoft Teams.

El bot puede ejecutarse en el bot Emulator. Esto le permite probar parte de la lógica principal del bot, ver un diseño aproximado de los mensajes y realizar pruebas sencillas. A continuación se indican los pasos:

1. Ejecute el código localmente.
2. Inicie el bot Emulator y establezca la dirección URL:
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#: `http://localhost:3979/api/messages`
3. Deje el id. de la aplicación de Microsoft y la contraseña de la aplicación microsoft en blanco, para que coincidan con las variables de entorno predeterminadas.

## <a name="locally-hosted"></a>Hospedado localmente

Microsoft Teams es un producto totalmente basado en la nube, requiere que todos los servicios a los que tiene acceso estén disponibles públicamente mediante puntos de conexión HTTPS. Por lo tanto, para permitir que tu aplicación funcione dentro de Teams, debes publicar el código en la nube de tu elección o hacer que nuestra instancia de ejecución local sea accesible externamente. Podemos hacerlo con software de túnel.

Aunque puedes usar cualquier herramienta que prefieras, usamos y recomendamos [ngrok](https://ngrok.com/download), que crea una dirección URL direccionable externamente para un puerto que abras localmente en el equipo. 

**Para configurar ngrok en preparación para ejecutar la aplicación Microsoft Teams localmente**

1. Vaya al directorio en el que ngrok.exe instalado en una aplicación terminal. Es posible que desee agregarlo como una variable de ruta de acceso para evitar este paso.
2. Ejecute, por ejemplo, `ngrok http 3978 --host-header=localhost:3978` o reemplace el número de puerto según sea necesario.
   Esto inicia ngrok para enumerar en el puerto especificado. A cambio, le proporciona una dirección URL direccionable externamente válida mientras ngrok se esté ejecutando.

> [!NOTE]
> Si detiene y reinicia ngrok, la dirección URL cambia.

Para usar ngrok en el proyecto en función de las capacidades que está usando, debe reemplazar todas las referencias de dirección URL del código, configuración y manifest.jsarchivo para usar este extremo de dirección URL.

Para los bots registrados en el Microsoft Bot Framework, actualice el extremo de mensajería del bot para usar este nuevo extremo de ngrok. Por ejemplo, `https://2d1224fb.ngrok.io/api/messages`. Puede validar que ngrok está funcionando probando la respuesta del bot en la ventana de chat de prueba del portal de Bot Framework. De nuevo, al igual que el emulador, esta prueba no permite acceder a Teams funcionalidad específica.

> [!NOTE]
> Para actualizar el extremo de mensajería de un bot, debe usar bot Framework. Seleccione el bot en [la lista de bots en Bot Framework](https://dev.botframework.com/bots). No es necesario migrar el bot a Microsoft Azure. También puedes actualizar el punto de conexión de mensajería a través [de App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="cloud-hosted"></a>Hospedado en la nube

Puede usar cualquier servicio direccionable externamente para hospedar el código de desarrollo y producción y sus puntos de conexión HTTPS. No hay ninguna expectativa de que sus capacidades residan en el mismo servicio. Se requiere que se tenga acceso a todos los dominios desde Microsoft Teams aplicaciones enumeradas en el [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) objeto del `manifest.json` archivo.

> [!NOTE]
> Para garantizar un entorno seguro, sea explícito sobre el dominio exacto y los subdominios a los que hace referencia y esos dominios deben estar en su control. Por ejemplo, `*.azurewebsites.net` no se recomienda, pero `contoso.azurewebsites.net` se recomienda.

## <a name="load-and-run-your-experience"></a>Cargar y ejecutar la experiencia

Para cargar y ejecutar la experiencia en Microsoft Teams, debe crear un paquete y cargarlo en Teams. Para más información, vea:

* [Crea el paquete para tu Microsoft Teams aplicación](~/concepts/build-and-test/apps-package.md).
* [Upload la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md).

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"] 
> [Añadir datos de prueba al entorno](~/concepts/build-and-test/test-data.md)

