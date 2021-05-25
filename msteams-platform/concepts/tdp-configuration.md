---
title: Configuración de la aplicación en portal de desarrolladores
description: Obtén información sobre cómo configurar y administrar tus aplicaciones mediante el Portal de desarrolladores para Microsoft Teams
keywords: introducción a los equipos del portal de desarrolladores
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635147"
---
# <a name="app-configuration"></a>Configuración de la aplicación

La parte más significativa de un paquete Microsoft Teams aplicación es su manifest.jsarchivo. Este archivo debe cumplir el esquema [Teams app](~/resources/schema/manifest-schema.md). El manifest.jsen contiene metadatos, lo que Teams para presentar correctamente la aplicación a los usuarios.

Puede realizar las siguientes acciones en la **sección Configurar** del Portal de desarrolladores:

* Crea un paquete de aplicación fácilmente.
* Describe la aplicación.
* Upload los iconos.
* Generar un archivo .zip para facilitar la distribución.

> [!NOTE]
> Portal para desarrolladores no produce código funcional para la aplicación ni hospeda la aplicación. Para que el proceso de carga de la aplicación dé como resultado una aplicación correcta, su aplicación debe estar hospedada y ejecutándose en la dirección URL que aparece en el manifiesto.

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Captura de pantalla que muestra la página Configurar de Teams Developer Portal.":::

## <a name="basic-information-and-branding"></a>Información básica y personal de marca

Las **secciones Información básica** y **Personal** de marca definen la descripción de alto nivel de la aplicación que estás realizando. Esto incluye el nombre, descripción y personal de marca visual de la aplicación. La información de esta sección se usará en la descripción de Teams de la aplicación y en el diálogo de instalación de la aplicación.

## <a name="capabilities"></a>Capacidades

La **sección Funcionalidades** de Configuración contiene los detalles de las capacidades de la aplicación.

> [!NOTE]
> La característica de personalización de la aplicación está disponible actualmente solo en la versión preliminar del desarrollador.
> 
> Como práctica recomendada, debes proporcionar directrices de personalización para que los usuarios de la aplicación y los clientes puedan seguir al personalizar la aplicación. Para obtener más información, consulta [Personalizar aplicaciones en Microsoft Teams](/MicrosoftTeams/customize-apps).

Estas son las funcionalidades:

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Captura de pantalla que muestra la página Configurar de Teams Developer Portal.":::

* **Aplicación personal** 

  Esta sección te permite definir un conjunto de pestañas que se presentan de forma predeterminada en la experiencia de la aplicación personal, es decir, la experiencia que un usuario tiene con la aplicación fuera del contexto de un equipo o canal. En esta sección, proporcione los siguientes detalles:

  * El nombre de la pestaña.
  * Un identificador único.
  * La dirección URL que apunta a la interfaz de usuario que se va a mostrar en Teams.
  * Dirección URL que se usará si un usuario opta por ver la pestaña en un explorador. Esta es una información opcional.
  * Cualquier dominio adicional desde el que la pestaña espera cargarse o vincularse a.

* **Aplicación de grupo y canal**

  Una Teams se convierte en parte de un canal y proporciona acceso rápido a la información y los recursos del equipo. Por ejemplo, la pestaña Planner de un canal contiene un solo plan, Power BI pestaña se asigna a un informe específico. Los usuarios pueden explorar en profundidad el contexto correspondiente, pero no deberían poder navegar fuera de la pestaña. La pestaña Power BI, por ejemplo, no habilita la navegación a otros informes de Power BI, aunque habilita el botón **Ir al sitio web**, que inicia el informe en el sitio web principal de Power BI.

    > [!NOTE]
    > Para las pestañas de equipo, debe proporcionar una dirección URL de configuración para presentar opciones y recopilar información, lo que le ayudará a personalizar el contenido y la experiencia de la pestaña. Esta página HTML iframed se muestra cuando un usuario agrega la pestaña por primera vez a un canal.
    > También debe proporcionar los dominios adicionales desde los que la pestaña espera cargarse o con los que se vincula.

* **Bot**

  Esta sección le permite agregar un [bot de conversación](~/bots/what-are-bots.md) a la aplicación. Si ya tiene un bot registrado con Bot Framework, puede agregarlo haciendo clic en **Configurar** y suministrando el nombre del bot, el id. de Bot Framework y definiendo los ámbitos en los que funcionará el bot.

  Si aún no ha registrado el bot con Bot Framework, haga clic **en Registrar** para crear uno nuevo. Después de registrar el bot, vuelve a esta sección del Editor de manifiestos para escribir su nombre y el id. de Bot Framework.

  Después de proporcionar la información del bot, ahora puedes definir opcionalmente una lista de comandos que el bot pueda sugerir a los usuarios. Agregue el nombre del comando, una descripción del comando que indique su sintaxis y argumentos, y el ámbito al que debe aplicarse este comando.

  Tenga en cuenta que, si ha definido que el bot solo sea compatible con un ámbito, los comandos especificados para un ámbito no compatible serán ignorados. Puede editar el ámbito con el que admite el bot en cualquier momento.

* **Connector**

  Esta sección le permite agregar un conector a la aplicación. Si ya ha registrado un conector Office 365, **seleccione** Configurar y escriba el nombre y el identificador del conector. Si desea un conector nuevo haga clic en **Registrarse** para ir al Panel del desarrollador de conectores en el explorador.

  > [!NOTE]
  > La personalización de aplicaciones permite a los administradores cambiar la apariencia de las aplicaciones cargadas a través de bots, extensiones de mensajería, pestañas y conectores. Por ejemplo, si el Teams personalizado el nombre de una aplicación de a , la aplicación aparecerá con el nuevo nombre para `Contoso` `Contoso Agent` los `Contoso Agent` usuarios. Sin embargo, mientras se agrega un conector a un chat, en la lista, los conectores seguirán mostrándole el nombre de la aplicación como `Contoso` .

* **Extensiones de mensajería**

  Las [extensiones de mensajería](~/messaging-extensions/what-are-messaging-extensions.md) son una forma eficaz de que los usuarios interactúen con su aplicación en Microsoft Teams. Los usuarios pueden consultar la información desde su servicio y publicar esa información en forma de tarjetas, directamente en el canal o en la conversación del chat.

  Las extensiones de mensajería funcionan con tecnología de los bots de Bot Framework, por lo que requieren de un bot configurado para funcionar. Si tiene el nombre y el id. de Bot Framework del bot al que le gustaría dar el poder de la extensión de mensajería, introdúzcalos. De lo contrario, haga clic en *Registrarse* para crear uno e introduzca la información después. Seleccione si el usuario puede actualizar la configuración de una extensión de mensajería.

  Después de configurar el bot subyacente, defina los comandos y parámetros que la extensión de mensajería puede aceptar.

  Cada comando necesita un título y un id. De manera opcional, el comando puede contener una descripción para el usuario. Cada comando puede admitir hasta cinco parámetros, cada uno de los cuales requiere lo siguiente:

  * Nombre del parámetro tal como aparece en el Teams cliente y se incluye en la solicitud de usuario.
  * Un título fácil de usar.
  * Una descripción opcional.

  > [!NOTE]
  > Para crear una extensión de mensajería con app studio, consulta [crear una extensión de mensajería con app studio](~/resources/create-messaging-extension-using-appstudio.md).

* **Extensión de reunión**

  TODO: Rajesh R.

* **Escena**

  Scenes in Together Mode es un artefacto creado por el desarrollador de la escena con el estudio de escena de Microsoft que reúne a las personas junto con su secuencia de vídeo en un entorno creativo tal como lo concidó el creador de la escena. En una configuración de escena pensada, los participantes han designado puestos con secuencias de vídeo representados en esos puestos. Para obtener más información, [vea Teams Modo juntos](~/apps-in-teams-meetings/teams-together-mode.md).

## <a name="permissions"></a>Permisos

Puedes enriquecer tu aplicación Teams con funcionalidades de dispositivo nativas, como cámara, micrófono y ubicación.

## <a name="languages"></a>Idiomas

Configura o cambia los idiomas compatibles con la aplicación.

## <a name="single-sign-on"></a>Inicio de sesión único

Configure la aplicación para autenticar usuarios con inicio de sesión único (SSO).

## <a name="domains"></a>Dominios

Una lista de dominios válidos para sitios web que la aplicación espera cargar en el Teams cliente. Las listas de dominios pueden incluir caracteres comodín, por ejemplo, `*.example.com` . Esto coincide exactamente con un segmento del dominio; si necesita hacer `a.b.example.com` coincidir, use `*.*.example.com` . Si la interfaz de usuario de contenido o configuración de pestañas necesita navegar a cualquier otro dominio además del uso para la configuración de pestañas, este dominio debe especificarse aquí.

No es necesario incluir los dominios de los proveedores de identidades que quieres admitir en la aplicación. Por ejemplo, para autenticar con un identificador de Google, es necesario redirigir a accounts.google.com, sin embargo, no debe incluir accounts.google.com en `validDomains[]` .

Teams aplicaciones que requieren que sus propias direcciones URL de sharepoint funcionen correctamente, incluye "{teamsitedomain}" en su lista de dominios válida.

> [!IMPORTANT]
> No agregue dominios que estén fuera del control, ya sea directamente o a través de caracteres comodín. Por ejemplo, `yourapp.onmicrosoft.com` es válido, sin embargo, `*.onmicrosoft.com` no es válido.

El objeto es una matriz con todos los elementos del tipo `string` .

## <a name="advanced"></a>Opciones avanzadas
Todo de Karthig

### <a name="app-content"></a>Contenido de la aplicación
Todo de Karthig

### <a name="first-party-settings"></a>Configuración del primer usuario
Todo de Karthig

## <a name="see-also"></a>Vea también

* [Información general sobre Teams Developer Portal](~/concepts/build-and-test/teams-developer-portal.md)
* [Distribuir Teams Developer Portal](~/concepts/tdp-distribute.md)
* [Herramientas en Teams Developer Portal](~/concepts/tdp-tools.md)