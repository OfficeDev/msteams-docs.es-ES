---
title: Administre sus aplicaciones con el portal para desarrolladores de Microsoft Teams
description: En este módulo, aprenderá a configurar, distribuir y administrar las aplicaciones mediante el Portal para desarrolladores para Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 391d6c671bf7c34a734eed3202df50ebdc4f9eae
ms.sourcegitcommit: e429131d01df7103a467df2c42cdfe41ab822b10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2022
ms.locfileid: "66164244"
---
# <a name="manage-your-teams-apps-using-developer-portal"></a>Administración de las aplicaciones de Teams mediante el Portal para desarrolladores

El <a href="https://dev.teams.microsoft.com" target="_blank">portal para desarrolladores para Teams</a> es la herramienta principal para configurar, distribuir y administrar las aplicaciones de Microsoft Teams. Con el portal para desarrolladores, puede colaborar con compañeros en la aplicación, configurar entornos en tiempo de ejecución y mucho más.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Captura de pantalla que muestra la página principal del portal para desarrolladores para Teams.":::

> [!NOTE]
>
> * Actualmente, el portal para desarrolladores no está disponible para inquilinos de Government Community Cloud (GCC), GCC-High o el Departamento de Defensa (DOD).
> * Sin embargo, puede usar un inquilino normal para compilar una aplicación en el portal para desarrolladores, descargar la aplicación y cargar la aplicación mediante [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) en una nube nacional. Para obtener más información, consulte [Implementaciones nacionales de nube](/graph/deployments).

> [!IMPORTANT]
> Si va a migrar de App Studio al Portal para desarrolladores, en la tabla siguiente se proporciona la información detallada de las características que se admiten en el Portal para desarrolladores:

| Características | App Studio | Portal para desarrolladores |
| --- | --- | --- |
| Análisis de aplicaciones* | ❌ | ✔️ |
| Funcionalidades de la aplicación: bots | ✔️ | ✔️ |
| Funcionalidades de la aplicación: conectores | ✔️ | ✔️ |
| Funcionalidades de la aplicación: extensión de mensajería | ✔️ | ✔️ |
| Funcionalidades de la aplicación: extensión de reunión | ❌ | ✔️ |
| Funcionalidades de la aplicación:Aplicaciones personales | ✔️ | ✔️ |
| Funcionalidades de la aplicación: pestañas | ✔️ | ✔️ |
| Entornos de aplicación | ❌ | ✔️ |
| Idiomas de la aplicación | ✔️ | ✔️ |
| Versión preliminar y descarga del manifiesto de aplicación | ✔️ | ✔️ |
| Planes de aplicación y precios | ❌ | ✔️ |
| Publicación de aplicaciones | ✔️ | ✔️ |
| Permisos de aplicación | ❌ | ✔️ |
| Uso compartido de aplicaciones con co-desarrolladores | ❌ | ✔️ |
| Validación de aplicaciones | ✔️ | ✔️ |
| Creación de una nueva aplicación | ✔️ | ✔️ |
| Impartir un paquete zip | ✔️ | ✔️ |

\**El análisis de aplicaciones estará disponible para disponibilidad general pronto.*

## <a name="register-an-app"></a>Registrar una aplicación

El portal para desarrolladores proporciona un par de maneras de registrar una aplicación Teams:

* Registrar una aplicación nueva.
* Importe un paquete de aplicación existente.

> [!NOTE]
> Si crea una aplicación con el [Kit de herramientas de Microsoft Teams para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), puede administrarla en el portal para desarrolladores.

## <a name="set-up-an-environment"></a>Configurar el entorno de desarrollo

Puede configurar entornos y variables globales para ayudar a realizar la transición de la aplicación del entorno de ejecución local a producción. Las variables globales se usan en todos los entornos.

Para configurar un entorno:

1. En el portal para desarrolladores, seleccione la aplicación en la que está trabajando.
2. Vaya a la página **Entornos** y seleccione **+ Agregar un entorno**.
3. Seleccione **+ Agregar una variable** para crear variables de configuración para el entorno.

Para usar variables:

Use los nombres de variable en lugar de los valores codificados de forma rígida para establecer las configuraciones de la aplicación.

1. Escriba `{{` en cualquier campo en el portal para desarrolladores. Aparece una lista desplegable con todas las variables que ha creado para el entorno elegido junto con las variables globales.  
1. Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda de Teams), seleccione el entorno que desea usar. Las configuraciones de la aplicación se actualizan automáticamente en función del entorno.

## <a name="identify-app-owners"></a>Identificación de propietarios de aplicaciones

Cada aplicación incluye una página **Propietarios**, donde puede compartir el registro de la aplicación con compañeros de su organización. El rol **Colaborador** tiene los mismos permisos que el rol **Propietario**, excepto la capacidad de eliminar una aplicación.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configuración de las funcionalidades de la aplicación y otros metadatos importantes

Una aplicación Teams es una aplicación web. Al igual que todas las aplicaciones web, su código fuente se desarrolla normalmente en un IDE o editor de código y se hospeda en algún lugar de la nube (como Azure).

Para instalar y representar la aplicación en Teams, debe incluir un conjunto de configuraciones que Teams reconozca. Esto se ha hecho tradicionalmente creando un manifiesto de aplicación, un archivo JSON que contiene todos los metadatos que Teams necesita para mostrar el contenido de la aplicación. El portal para desarrolladores abstrae este proceso e incluye nuevas características y herramientas que le ayudarán a tener más éxito.

## <a name="test-your-app-directly-in-teams"></a>Pruebe la aplicación directamente en Teams

El portal para desarrolladores proporciona opciones para probar y depurar la aplicación:

* En la página **Información general**, puede ver en una instantánea si las configuraciones de la aplicación se validan en los casos de prueba de Teams tienda.
* El botón **Vista previa en Teams** permite iniciar la aplicación rápidamente en el cliente de Teams para la depuración.

## <a name="distribute-your-app"></a>Distribuir la aplicación

En el portal para desarrolladores, use el botón **Distribuir** para descargar un paquete de aplicación, publicar en su organización o publicar en el almacén de Teams.

Para más información, consulte [Cargar la aplicación en Microsoft Teams](~/concepts/deploy-and-publish/apps-publish-overview.md).

## <a name="analyze-your-apps-usage"></a>Análisis del uso de la aplicación

En el Portal para desarrolladores de Teams, en la página **Información general**, puede ver el número total de usuarios activos de la aplicación.

> [!NOTE]
> Actualmente, el análisis de uso solo está disponible para las nuevas aplicaciones personalizadas publicadas en su organización a través del **Portal para desarrolladores** para Teams (anteriormente App Studio) o importadas en **el Portal para desarrolladores** para Teams después de abril de 2022. El análisis de uso de todas las aplicaciones publicadas en la tienda de Teams está disponible en el **Centro de partners** para obtener más información [Teams informe de uso de aplicaciones](/office/dev/store/teams-apps-usage).

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensual* | Métrica de uso predeterminada. Muestra el recuento de usuarios activos únicos que usaron la aplicación en esa ventana gradual de 30 días en UTC. |
| *A diario* | Muestra el recuento de usuarios activos únicos que usaron la aplicación en un día determinado en UTC. |

El uso de la aplicación para un día determinado se refleja dentro de 24 a 48 horas, y los datos de uso de las nuevas aplicaciones pueden tardar hasta tres o cinco días en reflejarse en los gráficos.

Puede ver el uso de la aplicación y otras conclusiones desde la página **Análisis** . Para acceder a la página:

1. Vaya al **[Portal para desarrolladores para Teams](https://dev.teams.microsoft.com)**.
1. Seleccione **Aplicaciones** en el panel izquierdo.
1. Seleccione la aplicación necesaria en la página **Aplicaciones** .
1. Seleccione **Análisis** en **Información general** o seleccione **Ver detalles** en la tarjeta **Usuarios activos (versión preliminar).**

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.PNG" alt-text="dev-Portal-analytics"lightbox="../../assets/images/tdp/dev-app-portal.PNG":::

A medida que explore métricas individuales en esta página, puede usar el botón **Filtrar** para analizar el uso de la aplicación a partir de las siguientes opciones de filtro:

* Tipo de agregación: este filtro permite agrupar las siguientes métricas por un recuento de usuarios distintos o un recuento de inquilinos o clientes distintos.
* Plataforma
* Sistema operativo
* Área

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.PNG" alt-text="Filter":::

Después de seleccionar los filtros deseados, puede explorar los siguientes widgets individuales:

* [Uso por período de tiempo](#usage-by-time-period)
* [Uso por plataforma y sistema operativo](#usage-by-platform-and-os)
* [Uso por estado de retención](#usage-by-retention-state)
* [Intensidad de uso](#usage-intensity)

### <a name="usage-by-time-period"></a>Uso por período de tiempo

El gráfico **Uso por período de tiempo** muestra el número de usuarios o inquilinos activos que han abierto y usado la aplicación en distintos períodos de tiempo.

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="Period":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| R30 mensual | Cada punto de datos representa un período R30 (30 días graduales) determinado. |
| R28 mensual | Cada punto de datos representa un período R28 (28 días graduales) determinado. |
| R7 semanal| Cada punto de datos representa un período de R7 (7 días consecutivos) determinado. |
| Diario | Cada punto de datos representa un período R1 (1 día gradual) determinado. |

### <a name="usage-by-platform-and-os"></a>Uso por plataforma y sistema operativo

El gráfico **Uso por plataforma y sistema operativo** muestra el uso activo de la aplicación en varios puntos de conexión, como **Windows**, **Mac**, **iOS**, **Android** y **Web**. El mismo usuario o inquilino puede usar una aplicación en varios puntos de conexión. Cada punto de datos representa un período R30 (30 días graduales) determinado.

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="Plataforma":::

### <a name="usage-by-retention-state"></a>Uso por estado de retención

El gráfico **De uso por estado de retención** permite realizar un seguimiento de cuatro métricas de retención o renovación de claves de la aplicación a lo largo del tiempo.

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="Retención":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Nuevos usuarios o inquilinos | Usuarios activos o inquilinos que son nuevos y no han usado la aplicación. |
| Devolver usuarios o inquilinos | Usuarios activos o inquilinos que usaron la aplicación durante un período de tiempo R30 (30 días consecutivos) determinado y el período de tiempo R30 inmediatamente anterior. |
| Usuarios o inquilinos resucitados | Usuarios activos o inquilinos que usaron la aplicación una o varias veces antes, pero no en el período de tiempo R30 inmediatamente anterior. |
| Usuarios o inquilinos vencidos | Usuarios activos o inquilinos que no se vieron durante un período de tiempo R30 determinado, pero que se vieron durante el período de tiempo R30 inmediatamente anterior. |

### <a name="usage-intensity"></a>Intensidad de uso

El gráfico **Intensidad de** uso muestra las métricas clave de intensidad de uso de la aplicación.

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="Intensidad":::

| Métrica | Definición |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Mediana de días usados al mes | Número medio de días en los que se abrió la aplicación en el último período de tiempo R30 (30 días consecutivos). |
| % de uso de más de 5 días | Porcentaje de usuarios activos que han abierto o usado la aplicación más de cinco días en el último período de tiempo de R30. |
| DAU/MAU | La proporción del número medio de usuarios o inquilinos únicos que usaron la aplicación en cada día dividido entre los usuarios activos mensuales para el período de tiempo R30 seleccionado. |

### <a name="app-dashboard"></a>Panel de la aplicación

En la tabla **del panel Mi aplicación** se muestran los datos R30 (30 días graduales) más recientes para cada una de las métricas de las cuatro categorías anteriores y el cambio Mes a mes. Use el selector de tiempo en la parte superior izquierda y seleccione la fecha deseada; puede ver los datos R30 diarios de los últimos 75 días y finales del mes R30 datos durante un máximo de 12 meses.

Puede seleccionar cada uno de estos **nombres de métrica** para ver las tendencias a lo largo del tiempo.

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="aplicación":::

## <a name="use-tools-to-create-app-features"></a>Uso de herramientas para crear características de la aplicación

El portal para desarrolladores también incluye herramientas que le ayudarán a crear algunas características clave de las aplicaciones de Teams. Entre estas herramientas se incluyen las siguientes:

* **Estudio de escenas**: diseñe [escenas personalizadas del modo junto](~/apps-in-teams-meetings/teams-together-mode.md) para reuniones de Teams.
* **Editor de tarjetas adaptables**: cree y obtenga una vista previa de tarjetas adaptables para incluirlas con las aplicaciones.
* **Administración de la plataforma de identidad de Microsoft**: registre las aplicaciones con Azure Active Directory para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.

## <a name="see-also"></a>Vea también

[Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
