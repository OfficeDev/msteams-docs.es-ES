---
title: Administre sus aplicaciones con el portal para desarrolladores de Microsoft Teams
description: En este artículo, aprenderá a configurar, distribuir y administrar las aplicaciones mediante el Portal para desarrolladores para Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 12f1def758e4ef108f9670e0cc696c7ce197e485
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232444"
---
# <a name="manage-your-apps-in-developer-portal"></a>Administración de aplicaciones en el Portal para desarrolladores

Después de crear o cargar la aplicación, puede administrar las aplicaciones en el Portal para desarrolladores con lo siguiente:

* [Información general](#overview)
* [Configurar](#configure)
* [Avanzadas](#advanced)
* [Publicar](#publish)

## <a name="overview"></a>Información general

En la sección **Información general** , puede ver los siguientes componentes para administrar la aplicación:

* Panel

  * En la sección **Panel** de **información general** , puede ver los siguientes componentes para la aplicación:
    * **Validación del almacén de Teams**: la herramienta de validación de aplicaciones comprueba el paquete de la aplicación en los casos de prueba que Microsoft usa al revisar la aplicación.
    * **Anuncio**: Últimas actualizaciones de las aplicaciones en el Portal para desarrolladores para Teams
    * **Usuarios activos (versión preliminar):** muestra el recuento de usuarios activos
    * **Información básica**: muestra el identificador de la aplicación, la versión, la versión del manifiesto, etc.

    :::image type="content" source="../../assets/images/tdp/dashboard-page.png" alt-text="La captura de pantalla es un ejemplo que muestra la página Información general de la aplicación que creó en el Portal para desarrolladores para Teams.":::

* Análisis

    En la página **Análisis** de la sección **Información general** , puede ver el número total de usuarios activos de la aplicación. Para obtener más información, consulta [Analizar el uso de la aplicación](analyze-your-apps-usage-in-developer-portal.md).

## <a name="configure"></a>Configurar

Para instalar y representar la aplicación en Teams, debe incluir un conjunto de configuraciones que Teams reconozca. Para cargar las aplicaciones en Teams, debe tener un manifiesto de aplicación, que contiene todos los detalles de la aplicación para mostrar la aplicación en Teams. Esto se puede lograr con la ayuda de componentes y herramientas que están disponibles en el Portal para desarrolladores.

En la sección **Configurar** , puede ver los siguientes componentes para administrar y acceder a la aplicación:

* **Información básica**: esta sección muestra y permite editar el nombre de la aplicación, el identificador de la aplicación, las descripciones, la versión, la información del desarrollador, las direcciones URL de la aplicación, el identificador de la aplicación (cliente) y el identificador de Microsoft Partner Network.
* **Personalización de marca**: esta página muestra los detalles del icono de la aplicación.
* **Características de** la aplicación: puede agregar las siguientes características a la aplicación:
  * Aplicación personal
  * Bot
  * Connector
  * Escena
  * Aplicación de grupo y canal
  * Extensión de mensajería
  * Extensión de reunión
  * Notificación de fuente de actividad
* **Permisos**: esta sección le permite conceder permisos de dispositivo, permisos de equipo, permisos de chat o reunión y permisos de usuario para la aplicación.
* **Inicio de sesión único**: puede configurar la aplicación para autenticar a los usuarios con el inicio de sesión único (SSO).
* **Idiomas**: puede configurar o cambiar el idioma de la aplicación.
* **Dominio**: puede agregar los dominios para cargar las aplicaciones en el cliente de Teams (por ejemplo: *.example.com).

:::image type="content" source="../../assets/images/tdp/configure.png" alt-text="La captura de pantalla es un ejemplo que muestra cómo configurar características para administrar y acceder a la aplicación en el Portal para desarrolladores.":::

## <a name="advanced"></a>Opciones avanzadas

En la sección **Avanzadas** , puede ver los siguientes componentes para administrar la aplicación en el Portal para desarrolladores:

* **Propietarios**

    Cada aplicación incluye una página **Propietarios** , donde puede compartir el registro de la aplicación con otros usuarios de su organización. Puede agregar el rol **administrador** y **operativo** para administrar quién puede cambiar la configuración de la aplicación. El rol **Operativo** tiene los mismos permisos que el rol **Administrador** , excepto para eliminar una aplicación.

    Para agregar a un propietario:

    1. En la sección **Avanzadas** , seleccione **Propietarios**.
    1. Seleccione **Agregar un propietario**.
    1. Escriba un nombre y seleccione un identificador de usuario en la lista desplegable.
    1. En **Rol**, seleccione **Operador** o **Administrador**.
    1. Seleccione **Agregar**.

* **Contenido de** la aplicación: puede configurar la aplicación con las siguientes características adicionales:
  
  * Indicador de carga: muestra un indicador para que los usuarios sepan que el contenido de la aplicación hospedada (por ejemplo, tabs y módulos de tareas) se está cargando.
  * Modo de pantalla completa: muestra una aplicación personal sin un encabezado de aplicación. Solo se admite para las aplicaciones publicadas en su organización.

* **Entornos**

    Puede configurar entornos y variables globales para ayudar a realizar la transición de la aplicación del entorno de ejecución local a producción. Las variables globales se usan en todos los entornos.

    Para configurar un entorno:

    1. En el Portal para desarrolladores, seleccione las **aplicaciones** que está trabajando.
    1. Vaya a **Entornos** en la sección **Avanzadas** y seleccione **+ Agregar un entorno**.
    1. Seleccione **Agregar**.

  * **Variables globales**

      1. Seleccione **Agregar una variable global** para crear variables de configuración para el entorno.

      Para usar variables globales:

      Use los nombres de variable en lugar de los valores codificados de forma rígida para establecer las configuraciones de la aplicación.

      1. Escriba `{{` en cualquier campo en el portal para desarrolladores. Aparece una lista desplegable con todas las variables que ha creado para el entorno elegido junto con las variables globales.  
      1. Antes de descargar el paquete de la aplicación (por ejemplo, al prepararse para publicar en la tienda de Teams), seleccione el entorno que desea usar. Las configuraciones de la aplicación se actualizan automáticamente en función del entorno.

* **Plan y precios**: puede vincular una oferta de SaaS que ha creado en el Centro de partners de la aplicación.
* **Administración configuración**:
  * Personalización de la aplicación: puede personalizar la aplicación
  * Bloquear aplicación de forma predeterminada: puede bloquear la aplicación de forma predeterminada para los usuarios hasta que un administrador de inquilinos decida habilitarla.

## <a name="publish"></a>Publicar

Puede publicar la aplicación en su organización o en la tienda de Teams.

* **Publique la aplicación en la organización**:

   1. En la página **Información general** de la aplicación, en **Publicar**, seleccione **Publicar en la organización**.
   1. Seleccione **Publicar la aplicación**.

* **Publique la aplicación para almacenarla**:

   1. En la página **Información general** de la aplicación, en **Publicar**, seleccione **Publicar en la Tienda**.
   1. Seleccione **Publicar**.

   > [!NOTE]
   > La herramienta de validación de aplicaciones comprueba el paquete de la aplicación en los casos de prueba que Microsoft usa para revisar la aplicación. Resuelva errores o advertencias y lea la **lista de comprobación de envío** de aplicaciones antes de enviar la aplicación.

   Para descargar el paquete de la aplicación, seleccione el botón **Descargar paquete de la aplicación** en la página Publicar en la tienda.

* **Paquete de** aplicación: el paquete de la aplicación describe cómo se configura la aplicación que incluye características de la aplicación, recursos necesarios y otros atributos importantes en el manifiesto. La pestaña Icono muestra el icono usado para la aplicación.

## <a name="test-your-app-directly-in-teams"></a>Pruebe la aplicación directamente en Teams

El portal para desarrolladores proporciona opciones para probar y depurar la aplicación:

* En la página **Información general** , puede ver una instantánea si la aplicación está configurada y validada en casos de prueba de la tienda Teams.
* El botón **Vista previa en Teams** inicia la aplicación rápidamente en el cliente de Teams para la depuración.

## <a name="use-tools-to-create-app-features"></a>Uso de herramientas para crear características de la aplicación

El Portal para desarrolladores también incluye herramientas que le ayudarán a crear características clave de las aplicaciones de Teams. A continuación se muestran las herramientas:

* **Estudio de escenas**: diseñe [escenas personalizadas del modo junto](~/apps-in-teams-meetings/teams-together-mode.md) para reuniones de Teams.
* **Editor de tarjetas adaptables**: cree y obtenga una vista previa de tarjetas adaptables para incluirlas con las aplicaciones.
* **Administración de la plataforma de identidad de Microsoft**: registre las aplicaciones con Azure Active Directory para ayudar a los usuarios a iniciar sesión y proporcionar acceso a las API.
* **Validación de aplicaciones de la tienda de Teams**: compruebe el paquete de la aplicación en los casos de prueba que Microsoft usa para revisar la aplicación.
* **Administración de bots**: agregue bots conversacionales a la aplicación que se comuniquen con los usuarios, respondan a sus preguntas y les notifiquen proactivamente sobre los cambios y otros eventos.

Para agregar un bot:

1. En el Portal para desarrolladores, seleccione **Herramientas** en el panel izquierdo.
1. Seleccione **Bot management (Administración de bots**).
1. En la página Administración de bots, seleccione **Nuevo bot**.
1. Escriba el nombre y seleccione **Agregar**.

:::image type="content" source="../../assets/images/tdp/tools-in-dev-portal.png" alt-text="La captura de pantalla es un ejemplo que muestra las herramientas del portal para desarrolladores, lo que le ayuda a crear características clave.":::

Desde el portal para desarrolladores, puede ir al portal de Bot Framework y configurar el bot para actualizar el icono y otras propiedades.

## <a name="see-also"></a>Vea también

[Incluir una oferta de SaaS con la aplicación de Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
