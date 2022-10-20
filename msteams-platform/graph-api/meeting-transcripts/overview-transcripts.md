---
title: Usar Microsoft Graph para capturar transcripciones de una reunión de Teams
description: Describe el proceso, los escenarios y las API para capturar transcripciones en el escenario posterior a la reunión.
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 48d94bcfb41caf7bff171e4ae25146578c5d5fd8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615306"
---
# <a name="get-meeting-transcripts-using-graph-apis"></a>Obtenga transcripciones de la reunión mediante las API de Graph

Ahora puede configurar la aplicación para capturar transcripciones de las reuniones de Microsoft Teams en el escenario posterior a la reunión. La aplicación puede usar las REST API de Microsoft Graph para acceder y capturar las transcripciones generadas para una reunión de Teams programada de antemano.

Estos son algunos casos de su uso para capturar transcripciones de reuniones mediante Graph API:

| Caso de uso | Cómo ayudan las API de transcripción... |
| --- | --- |
| Necesita obtener transcripciones para capturar conclusiones significativas de varias reuniones en la vertical de Ventas. Requiere tiempo y es ineficaz realizar un seguimiento de todas las reuniones y recuperar las notas de la reunión manualmente. Una vez finalizada la reunión, deberá examinar las conversaciones en todas esas reuniones para obtener información útil. | El uso de las API de Graph en la aplicación para capturar transcripciones de reuniones recupera automáticamente las transcripciones de todas las reuniones pertinentes para su propósito. La aplicación puede recibir notificaciones de reunión y obtener la transcripción cuando se genera una vez finalizada la reunión. A continuación, estos datos se pueden usar para obtener: <br> • Conclusiones agregadas y análisis de inteligencia <br> • Nuevos clientes potenciales y contenidos destacados <br> • Seguimientos y resúmenes de reuniones |
| Como iniciativa de RR. HH., está realizando una sesión de lluvia de ideas para comprender y mejorar la salud y la productividad de los empleados. Tener que tomar continuamente notas para proporcionar un resumen posterior a la reunión puede impedir el flujo de pensamientos, y es posible que no capture todas las sugerencias valiosas. Después de la sesión, necesitará analizar la discusión para recopilar datos y planear mejoras. | El uso de las API de Graph en la aplicación para capturar transcripciones posteriores a la reunión le libera a usted y a los participantes para centrarse por completo en la discusión. El contenido de la transcripción de la reunión está disponible para: <br> • Análisis de compromiso y de opiniones <br> • Enumerar tareas o problemas <br> • Reuniones y notificaciones de seguimiento |

> [!NOTE]
> En el futuro, Microsoft puede solicitarle a usted o a sus clientes que paguen tarifas adicionales en función de la cantidad de datos a los que se acceda a través de la API.

Para capturar la transcripción de una reunión determinada:

- [Configurar los permisos en Azure AD para acceder a la transcripción](#configure-permissions-on-azure-ad-to-access-transcript)
- [Obtener el identificador de reunión y el identificador del organizador](fetch-id.md)
- [Usar las API de Graph para capturar la transcripción](/graph/api/resources/calltranscript)

## <a name="configure-permissions-on-azure-ad-to-access-transcript"></a>Configurar los permisos en Azure AD para acceder a la transcripción

La aplicación debe tener los permisos necesarios para capturar transcripciones. Puede acceder y capturar transcripciones de una reunión de Teams mediante permisos de aplicación para toda la organización o permisos de aplicación de consentimiento específico de recursos (RSC) para una reunión determinada.

### <a name="use-organization-wide-application-permissions"></a>Usar los permisos de la aplicación para toda la organización

Puede configurar la aplicación para acceder a las transcripciones de reuniones en la cuenta empresarial. En este caso, el organizador de la reunión no necesita instalar la aplicación en el chat de reuniones de Teams. Cuando el administrador de inquilinos autoriza los permisos de la aplicación de toda la organización, la aplicación puede leer y acceder a las transcripciones de todas las reuniones de la cuenta empresarial.

Para obtener más información sobre los permisos de la aplicación de toda la organización que se pueden conceder a la aplicación, consulte [Permisos de reunión en línea](/graph/permissions-reference#online-meetings-permissions).

### <a name="use-meeting-specific-rsc-application-permissions"></a>Usar los permisos de aplicación RSC específicos de la reunión

Si quiere que la aplicación capture transcripciones solo de la reunión de Teams donde está instalada, configure el permiso RSC específico de la reunión para la aplicación. Los usuarios autorizados pueden instalar su aplicación en el chat de la reunión. Una vez finalizada la reunión, la aplicación puede realizar la llamada API para obtener la transcripción de esa reunión.

Para obtener más información sobre los permisos de RSC específicos de la reunión que se pueden conceder a la aplicación, consulte [Consentimiento específico de recursos](../rsc/resource-specific-consent.md#resource-specific-permissions-for-a-chat).

Después de configurar los permisos, configure la aplicación para recibir notificaciones de cambio para todos los eventos de reunión pertinentes. Las notificaciones contienen el identificador de reunión y el identificador del organizador que ayudan a acceder al contenido de la transcripción. La aplicación puede capturar la transcripción de una reunión cuando se genera una vez finalizada. El contenido de la transcripción está disponible como `.vtt` o como archivo `.docx`.

Para obtener más información sobre cómo la aplicación puede saber cuándo finalizan las reuniones, consulte [Suscribirse a notificaciones de cambio](fetch-id.md#subscribe-to-change-notifications) y [Usar Bot Framework para obtener el identificador de reunión y el identificador del organizador](fetch-id.md#use-bot-framework-to-get-meeting-id-and-organizer-id).

> [!NOTE]
> El proceso para llamar a Graph API para obtener acceso y recuperar transcripciones sigue siendo el mismo para los permisos de aplicación RSC específicos de la reunión o para los permisos de la aplicación de toda la organización. Actualmente, estas API solo admiten reuniones programadas.

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [Obtener el identificador de reunión y el identificador del organizador](fetch-id.md)

## <a name="see-also"></a>Ver también

- [API avanzadas de reunión](../../apps-in-teams-meetings/meeting-apps-apis.md)
