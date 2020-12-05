---
title: Solicitar permisos de dispositivo para la pestaña de Microsoft Teams
description: Cómo actualizar el manifiesto de la aplicación para solicitar acceso a características nativas que suelen requerir el consentimiento del usuario
keywords: desarrollo de pestañas de Microsoft Teams
ms.openlocfilehash: d6c66525ab0e81f0632df5e2c323926279e38a8e
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576896"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>Solicitar permisos de dispositivo para la pestaña de Microsoft Teams

Es posible que quiera enriquecer su pestaña con características que requieran la funcionalidad de dispositivo nativo de Access como:

> [!div class="checklist"]
>
> * Digital
> * Micro
> * Ubicación
> * Notificaciones

> [!IMPORTANT]
>
> * Actualmente, el cliente móvil de Microsoft Teams solo admite `camera` y `location`  a través de capacidades de dispositivo nativas y está disponible en todas las construcciones de aplicaciones, incluidas las pestañas. </br>
> * `camera`La [**API captureImage**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)habilita la compatibilidad con la captura de imágenes.
> * Actualmente, la [**API de ubicación geográfica**](../../resources/schema/manifest-schema.md#devicepermissions) no es totalmente compatible con todos los clientes de escritorio.

## <a name="device-permissions"></a>Permisos de dispositivo

El acceso a los permisos de dispositivo de un usuario le permite crear experiencias mucho más enriquecidas, por ejemplo:

* Grabar y compartir vídeos breves
* Grabe memorandos de audio cortos y guárdelos para más tarde
* Usar la información de ubicación del usuario para mostrar información relevante

Aunque el acceso a estas características es estándar en la mayoría de los exploradores Web modernos, es necesario que los equipos sepan qué características desea usar al actualizar el manifiesto de la aplicación. Esto le permitirá solicitar permisos, de la misma manera que lo haría en un explorador, mientras la aplicación se ejecuta en el cliente de escritorio de Microsoft Teams.

## <a name="manage-permissions"></a>Administrar permisos

# <a name="desktop"></a>[Escritorio](#tab/desktop)

1. Abra Microsoft Teams.
1. En la esquina superior derecha de la ventana, seleccione el icono de su perfil.
1. Seleccione **Settings**  ->  **Permissions** en el menú desplegable.
1. Elija la configuración que desee.

![Pantalla Configuración del escritorio de permisos de dispositivo](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[Móvil](#tab/mobile)

1. Abra Microsoft Teams.
1. En la esquina superior izquierda de la pantalla, seleccione el icono del menú &#9776;.
1. Seleccione **configuración** de  ->  **dispositivos**.
1. Elija la configuración que desee.

![Pantalla de configuración móvil de permisos de dispositivo](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a>Propiedades

Actualice la aplicación `manifest.json` agregando `devicePermissions` y especificando cuál de las cinco propiedades desea usar en la aplicación:

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> Los medios también se usan para los permisos de cámara en dispositivos móviles.

Cada propiedad le permitirá pedir al usuario que pida su consentimiento

| Propiedad      | Descripción   |
| --- | --- |
| Elementos multimedia         | permiso para usar la cámara, el micrófono y los altavoces |
| geolocalización   | permiso para devolver la ubicación del usuario      |
| notificaciones | permiso para enviar notificaciones de usuario      |
| MIDI          | permiso para enviar y recibir información MIDI de un instrumento musical digital   |
| openExternal  | permiso para abrir vínculos en aplicaciones externas  |

## <a name="checking-permissions-from-your-tab"></a>Comprobación de permisos en la pestaña

Una vez que haya agregado `devicePermissions` al manifiesto de la aplicación, puede comprobar los permisos mediante la API de "permisos" de HTML5 sin que se le pida confirmación.

``` Javascript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="prompting-the-user"></a>Preguntar al usuario

Para mostrar una solicitud para obtener consentimiento para obtener acceso a los permisos de dispositivo necesita aprovechar la API de HTML5 o Teams adecuada. Por ejemplo, para pedir al usuario que tenga acceso a su cámara, debe llamar a `getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

Para usar la cámara en el escritorio o en la web, Microsoft Teams mostrará una solicitud de permiso cuando llame a getUserMedia

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

Para capturar la imagen en dispositivos móviles, Teams Mobile le pedirá permiso cuando se lo denomine captureImage ().

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

Las notificaciones le preguntarán al usuario cuando llame a `requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![Pestañas del mensaje de permisos de dispositivo](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a>Comportamiento de permisos en sesiones de inicio de sesión

Los permisos de dispositivos nativos se almacenan por sesión de inicio de sesión. Esto significa que si inicia sesión en otra instancia de Teams (por ejemplo: en otro equipo), los permisos de dispositivo de las sesiones anteriores no estarán disponibles. En su lugar, tendrá que volver a dar su consentimiento a los permisos de dispositivo para la nueva sesión de inicio de sesión. Esto también significa que, si sale de la sesión de Teams (o de los inquilinos de conmutador dentro de los equipos), los permisos de dispositivo se eliminarán para la sesión de inicio anterior. Tenga esto en cuenta cuando desarrolle permisos de dispositivos nativos: las funciones nativas con las que da su consentimiento están solo para su sesión de inicio _actual_ .
