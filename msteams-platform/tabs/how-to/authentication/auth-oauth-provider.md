---
title: Usar proveedores de OAuth externos
description: En este módulo, aprenderá a realizar la autenticación mediante proveedores de OAuth externos y a agregarla al explorador externo.
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 62f056fd852eda320a180fa61cf5693ef0105b8b
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2022
ms.locfileid: "67435072"
---
# <a name="use-external-oauth-providers"></a>Usar proveedores de OAuth externos

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

Puede admitir proveedores de OAuth externos o de terceros (3P), como Google, GitHub, LinkedIn y Facebook mediante la API de `authenticate()` actualizada:

```JavaScript
function authenticate(authenticateParameters: AuthenticatePopUpParameters): Promise<string>
```

Se agregan los siguientes elementos a la API de `authenticate()` para admitir proveedores de OAuth externos:

* parámetro `isExternal`
* Dos valores de marcador de posición en el parámetro `url` existente

En la tabla siguiente se proporciona la lista de parámetros de `authenticate()` API (`AuthenticatePopUpParameters`) y funciones junto con sus descripciones:

| Parámetro| Descripción|
| --- | --- |
|`isExternal` | El tipo de parámetro es booleano, que indica que la ventana de autenticación se abre en un explorador externo.|
|`height` |Alto preferido para el elemento emergente. El valor se puede omitir si está fuera de los límites aceptables.|
|`url`  <br>|Dirección URL del servidor de aplicaciones 3P para el elemento emergente de autenticación, con los dos marcadores de posición de parámetro siguientes:</br> <br> - `oauthRedirectMethod`: Pasar marcador de posición en `{}`. Este marcador de posición se reemplaza por el vínculo profundo o la página web por la plataforma de Teams, que informa al servidor de aplicaciones si la llamada procede de la plataforma móvil.</br> <br> - `authId`: este marcador de posición se reemplaza por UUID. El servidor de aplicaciones lo usa para mantener la sesión.| 
|`width`|Ancho preferido para el elemento emergente. El valor se puede omitir si está fuera de los límites aceptables.|

Para obtener más información sobre los parámetros, vea la función [authenticate(AuthenticatePopUpParameters).](/javascript/api/@microsoft/teams-js/authentication#@microsoft-teams-js-authentication-authenticate)

## <a name="add-authentication-to-external-browsers"></a>Agregar autenticación a exploradores externos

> [!NOTE]
> * Actualmente, puede agregar autenticación a exploradores externos solo para pestañas en dispositivos móviles. 
> * Use la versión beta del SDK de JS para aprovechar la funcionalidad. Las versiones beta están disponibles a través de [NPM](https://www.npmjs.com/package/@microsoft/teams-js/v/1.12.0-beta.2).

La siguiente imagen proporciona el flujo para agregar autenticación a exploradores externos:

 :::image type="content" source="../../../assets/images/tabs/tabs-authenticate-OAuth.PNG" alt-text="authenticate-OAuth":::

**Para agregar autenticación a exploradores externos**

1. Inicie el proceso de inicio de sesión de autenticación externo.

   La aplicación 3P llama a la función SDF `authentication.authenticate` con `isExternal` establecido como true para iniciar el proceso de inicio de sesión de autenticación externo.

   El `url` pasado contiene marcadores de posición para `{authId}` y `{oauthRedirectMethod}`.  


    ```JavaScript
    import { authentication } from "@microsoft/teams-js";
    authentication.authenticate({
       url: 'https://3p.app.server/auth?oauthRedirectMethod={oauthRedirectMethod}&authId={authId}',
       isExternal: true,
       successCallback: function (result) {
       //sucess 
       } failureCallback: function (reason) {
       //failure 
        }
    });
    ```

2. El vínculo de Teams se abre en un explorador externo.

   Los clientes de Teams abren la dirección URL en un explorador externo después de reemplazar los marcadores de posición para `oauthRedirectMethod` y `authId` por valores adecuados.

   #### <a name="example"></a>Ejemplo

   ```http
    https://3p.app.server/auth?oauthRedirectMethod=deeplink&authId=1234567890 
   ```

3. El servidor de aplicaciones 3P responde.

   El servidor de aplicaciones 3P recibe y guarda el `url` con los dos parámetros de consulta siguientes:

   | Parámetro | Descripción|
   | --- | --- |
   | `oauthRedirectMethod` |Indica cómo la aplicación 3P debe enviar la respuesta de la solicitud de autenticación a Teams, con uno de los dos valores: vínculo profundo o página.|
   |`authId` | El id. de solicitud que Teams creó para esta solicitud de autenticación específica que debe enviarse de vuelta a Teams a través del vínculo profundo.|

    > [!TIP]
    > La aplicación 3P puede serializar `authId`, `oauthRedirectMethod` en el parámetro de consulta de OAuth `state` al generar la dirección URL de inicio de sesión para OAuthProvider. El `state` contiene los `authId` pasados y `oauthRedirectMethod`, cuando OAuthProvider redirige de nuevo al servidor 3P y la aplicación 3P usa los valores para devolver la respuesta de autenticación a Teams, como se describe en **6. La respuesta del servidor de aplicaciones 3P a Teams**.

4. El servidor de aplicaciones 3P redirige a `url` que se ha especificado.

   El servidor de aplicaciones 3P redirige a la página de autenticación de proveedores de OAuth en el explorador externo. `redirect_uri` es una ruta dedicada en el servidor de aplicaciones 3P. Puede registrar `redirect_uri` en la consola de desarrollo de proveedores de OAuth como estático; los parámetros deben enviarse a través del objeto de estado.

   #### <a name="example"></a>Ejemplo

    ```http
    https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https://3p.app.server/authredirect&state={"authId":"…","oauthRedirectMethod":"…"}&client_id=…    &response_type=code&access_type=offline&scope= … 
    ```

5. Inicie sesión en el explorador externo.

   El usuario inicia sesión en el explorador externo. Los proveedores de OAuth redirigen de nuevo a `redirect_uri` con el código de autenticación y el objeto de estado.

6. El servidor de aplicaciones 3P comprueba y responde a Teams.

   El servidor de aplicaciones 3P controla la respuesta y comprueba `oauthRedirectMethod`, que se devuelve desde el proveedor de OAuth externo en el objeto de estado para determinar si la respuesta debe devolverse a través del vínculo profundo de autenticación-devolución de llamada o a través de la página web que llama a `notifySuccess()`.

      ```JavaScript
      const state = JSON.parse(req.query.state)
      if (state.oauthRedirectMethod === 'deeplink') {
         return res.redirect('msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&result=${req.query.code}')
      }
      else {
      // continue redirecting to a web-page that will call notifySuccess() – usually this method is used in Teams-Web
      …
      ```

7. La aplicación 3P genera un vínculo profundo.

   La aplicación 3P genera un vínculo profundo para Teams Mobile en el siguiente formato y envía el código de autenticación con el identificador de sesión a Teams.

   ```JavaScript
   return res.redirect(`msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&result=${req.query.code}`)
   ```

 8. Teams llama a la devolución de llamada correcta y envía el resultado.

    Teams llama a la devolución de llamada correcta y envía el resultado (código de autenticación) a la aplicación 3P. La aplicación 3P recibe el código en la devolución de llamada correcta y usa el código para recuperar el token y, a continuación, la información del usuario y actualizar la interfaz de usuario.

      ```JavaScript
      successCallback: function (result) { 
      … 
      } 
      ```

## <a name="see-also"></a>Vea también

* [Configurar proveedores de identidades](../../../concepts/authentication/configure-identity-provider.md)
* [Flujo de autenticación de Microsoft Teams para pestañas](auth-flow-tab.md)
