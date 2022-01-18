---
title: Microsoft Teams developer documentation - Glossary
description: Glosario para Microsoft Teams para desarrolladores
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams de desarrollador
ms.openlocfilehash: 0858d0cfb246e99871c02f81c82c1eaa30bb6edf
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059834"
---
# <a name="glossary"></a>Glosario

Términos y definiciones comunes usados en Teams documentación para desarrolladores.
<br>
<br>
<details>
<summary>A</summary>

| Término | Definición |
| --- | --- |
| Comando Action | Los comandos action se usan para presentar a los usuarios un elemento emergente modal para recopilar o mostrar información. <br>**Vea también**: Extensión de mensajería; Comandos de búsqueda |
| Tarjeta adaptable | Una tarjeta adaptable es un fragmento de código de contenido que se puede agregar a una conversación a través de un bot o una extensión de mensajería. Con texto, gráficos y botones, estas tarjetas proporcionan una comunicación enriquecida a la audiencia. |
| Catálogo de aplicaciones | El Catálogo de aplicaciones se usa para almacenar las aplicaciones para SharePoint y office para el uso interno de nuestra organización. |
| Manifiesto de la aplicación | El Teams de la aplicación describe cómo se integra la aplicación en el Microsoft Teams aplicación. El manifiesto debe cumplir con el esquema hospedado en https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json . |
| Paquete de la aplicación | Un Teams de aplicación es un archivo zip que contiene el archivo de manifiesto de la aplicación y los iconos de la aplicación: icono de color e icono de esquema. |
| Permisos de aplicación | La opción Permisos de la aplicación Teams permite habilitar los permisos de dispositivo de la aplicación para la aplicación. Solo está disponible cuando el archivo de manifiesto de la aplicación declara que la aplicación necesita permisos de dispositivo. <br> **Vea también**: Permisos de dispositivo |
| Ámbito de la aplicación | El ámbito de la aplicación determina cómo interactúa la aplicación con los usuarios. Una aplicación puede tener ámbito personal, ámbito de canal o ámbito de equipo. Una Teams aplicación puede existir en todos los ámbitos. |
| App Studio | App Studio es una aplicación para empezar a crear o integrar tus propias Microsoft Teams aplicaciones. Ahora ha evolucionado a Portal de desarrolladores. <br> **Vea también**: Portal de desarrolladores |
| Recurso de Azure | Un servicio que está disponible a través de Azure que la Teams puede usar para la implementación de Azure. Podrían ser cuentas de almacenamiento, aplicaciones web, bases de datos y mucho más. |
| Azure Active Directory | Azure Active Directory (Azure AD) es el servicio de administración de acceso y identidad basado en la nube de Microsoft. Ayuda a los usuarios autenticados a obtener acceso a recursos internos y externos de Azure. |
| Autenticación | La autenticación es un proceso para autorizar el acceso de los usuarios para el uso de la aplicación. se puede hacer con las API Graph Microsoft o la autenticación basada en web. <br> **Vea también**: Proveedores de identidades |
| Flujo de autenticación | En Teams, hay dos flujos de autenticación diferentes para autenticar a un usuario para usar una aplicación: autenticación basada en web y flujo de OAuthPrompt. |
|
</details>
<br>
<details>
<summary>N</summary>

| Término | Definición |
| --- | --- |
| Blazor | Blazor es un marco web gratuito y de código abierto que permite a los desarrolladores crear aplicaciones web con C# y HTML. Le permite crear URI web interactivas con C# en lugar de JavaScript. Las aplicaciones de Blazor se componen de componentes reutilizables de la interfaz de usuario web implementadas C#, HTML y CSS. Microsoft la está desarrollando. |
| Bicep | Bícep es un lenguaje declarativo, lo que significa que los elementos pueden aparecer en cualquier orden. A diferencia de los lenguajes imperativos, el orden de los elementos no afecta a la forma en que se procesa la implementación. |
| Bot | Un bot es una aplicación que realiza tareas repetitivas programadas. <br> **Vea también**: Bot conversacional; Bot de chat |
| Bot Emulator | Bot Framework Emulator es una aplicación de escritorio que permite probar y depurar bots, ya sea de forma local o remota. |
| Bot Framework | Bot Framework es un SDK enriquecido que se usa para crear bots con C#, Java, Python y JavaScript. Si ya tienes un bot basado en Bot Framework, puedes modificarlo fácilmente para que funcione en Teams. |
</details>
<br>
<details>
<summary>C</summary>

| Término | Definición |
| --- | --- |
| Bot de llamada | Bot que participa en llamadas de audio o vídeo y reuniones en línea. <br> **Vea también**: Bot de chat; Bot de reunión |
| Funcionalidad | La característica de una Teams se denomina funcionalidad. Una aplicación puede tener una o más funcionalidades principales, como pestaña, bot, extensiones de mensajería. <br>**Vea también**: Funcionalidad del dispositivo; Funcionalidad multimedia |
| Bot de chat | Un bot también se conoce como bot de chat o bot conversacional. Es una aplicación que ejecuta tareas sencillas y repetitivas por parte de los usuarios, como el servicio de atención al cliente o el personal de soporte técnico. <br> **Vea también**: Bot conversacional. |
| Canal | Un canal es un único lugar para que un equipo comparta mensajes, herramientas y archivos. En Teams, el trabajo en equipo y la comunicación se suceden en canales.  |
| Secreto de cliente | El secreto de cliente/contraseña o un par de claves pública o privada que es Certificate. Esto no es necesario para las aplicaciones nativas. <br> **Vea también**: Bot |
| Recursos en la nube | Un servicio que está disponible en la nube a través de Internet que tu Teams aplicación puede usar. Podrían ser cuentas de almacenamiento, aplicaciones web, bases de datos y mucho más. |
| Aplicación de colaboración |  <br> **Consulta también**: Aplicación independiente |
| Conectores |  <br> **Vea también**: Webhooks |
| Conversación | Una conversación es una serie de mensajes enviados entre el bot Microsoft Teams y uno o más usuarios. Una conversación puede tener tres ámbitos: chat de canal, personal y de grupo. <br>**Vea también**: chat uno a uno; Chat en grupo |
| Bot conversacional |  Los bots conversacionales permiten a los usuarios interactuar con el servicio web mediante texto, tarjetas interactivas y módulos de tareas. <br>**Ver aso** Bot de chat |