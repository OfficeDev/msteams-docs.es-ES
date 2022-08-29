---
title: Obtener el id. de reunión y el identificador del organizador para capturar las transcripciones de la reunión
description: Describe el proceso de obtención del id. de reunión y el identificador del organizador para capturar transcripciones de reuniones.
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 316eabb77eb440a171ca6f357e1db8a2f3b18b6b
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2022
ms.locfileid: "67434988"
---
# <a name="obtain-meeting-id-and-organizer-id"></a>Obtener id. de reunión e id. de organizador

La aplicación puede capturar transcripciones de una reunión mediante el identificador de reunión y el identificador de usuario del organizador de la reunión, también conocido como identificador del organizador. Las API de REST de Graph capturan transcripciones basadas en el identificador de reunión y el identificador del organizador que se pasan como parámetros en la API.

> [!NOTE]
> El id. de reunión de las reuniones programadas puede expirar en algunos días si no se usa. Se puede recuperar usando la dirección URL de la reunión para unirse a la reunión. Para más información sobre la escala de tiempo de expiración de reuniones para diferentes tipos de reuniones, vea [Expiración de reunión](/microsoftteams/limits-specifications-teams#meeting-expiration).

Para obtener el id. de reunión y el identificador del organizador para capturar la transcripción, elija una de las dos maneras siguientes:

- [Suscríbase para cambias las notificaciones](#subscribe-to-change-notifications)
- [Usar Bot Framework](#use-bot-framework-to-get-meeting-id-and-organizer-id)

### <a name="subscribe-to-change-notifications"></a>Suscríbase para cambias las notificaciones

Puede suscribir su aplicación para recibir notificaciones de cambios para eventos de reunión programados. Cuando se notifica a la aplicación sobre los eventos de reunión suscritos, puede obtener transcripciones, si está autorizada a través de los permisos de Azure AD necesarios.

La aplicación recibe una notificación sobre el tipo de eventos de reunión para los que está suscrita:

- [Notificación de nivel de usuario](#obtain-meeting-details-using-user-level-notification)
- [Notificación de nivel de inquilino](#obtain-meeting-details-using-tenant-level-notification)

Cuando se notifica a la aplicación de un evento de reunión suscrito, puede recuperar el id. de reunión y el identificador del organizador del mensaje de notificación. En función de los detalles de la reunión obtenidos, la aplicación puede capturar las transcripciones de la reunión una vez finalizada la reunión.

#### <a name="obtain-meeting-details-using-user-level-notification"></a>Obtener detalles de la reunión mediante la notificación de nivel de usuario

Elija suscribir la aplicación a notificaciones de nivel de usuario para obtener transcripciones del evento de reunión de un usuario determinado. Cuando se programa una reunión para ese usuario, se notifica a la aplicación. La aplicación también puede recibir notificaciones de reuniones mediante eventos de calendario.

Para suscribir la aplicación a eventos de calendario, vea [Cambiar las notificaciones de los recursos de Outlook en Microsoft Graph](/graph/outlook-change-notifications-overview).

Use el ejemplo siguiente para suscribirse a notificaciones de nivel de usuario:

```http
    
POST https://graph.microsoft.com/v1.0/subscriptions/
{
    "changeType": "created,updated,deleted",
    "notificationUrl": "https://webhook.azurewebsites.net/api/send/myNotifyClient",
    "resource": "users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events",
    "expirationDateTime": "2022-05-05T14:58:56.7951795+00:00",
    "clientState": "ClientSecret",
    "includeResourceData": false
}
```

Cuando se notifica a la aplicación sobre un evento de reunión suscrito, busca el identificador de evento de calendario en la notificación. Use el identificador de evento para obtener `JoinWebUrl` para recuperar un identificador de chat específico y suscribirse a sus mensajes. Una vez que la aplicación se haya suscrito a los mensajes de chat, siga los pasos indicados para las[ notificaciones de nivel de inquilino](#obtain-meeting-details-using-tenant-level-notification) para obtener el identificador de reunión y el identificador del organizador.

Para obtener el id. de reunión y el identificador del organizador de la notificación de nivel de usuario:

1. **Obtener id. de evento**: la aplicación obtiene la propiedad `eventId` de la carga de notificación.

    <details>
    <summary><b>Ejemplo</b>: carga de notificación</summary>

    ```json
    {
        "subscriptionId": "ef30cdc6-b5ae-4702-b924-f458fd9e5fc3",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "clientState": "ClientSecret",
        "subscriptionExpirationDateTime": "2022-05-05T07:54:53.1886542-07:00",
        "resource": "Users/1273a016-201d-4f95-8083-1b7f99b3edeb/Events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",
        "resourceData": {}
    }
    ```

    En este ejemplo, el `eventID` contenido en `resource` es *AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=*.
    </details>

2. **Obtener la dirección URL de la reunión**: use el identificador de evento para recuperar `joinUrl` que contiene la dirección URL de la reunión.

    Para más información, vea [Obtener evento](/graph/api/event-get).

    Use el ejemplo siguiente para solicitar la dirección URL de la reunión:

    ```http
    GET https://graph.microsoft.com/v1.0/users/1273a016-201d-4f95-8083-1b7f99b3edeb/events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=
    ```

    La carga de respuesta contiene `joinURL`.

    <details>
    <summary><b>Ejemplo</b>: carga de respuesta para obtener la dirección URL de la reunión</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events/$entity",
        "@odata.etag": "W/\"xRVh47aDEU6na1ckNYfMiwABb2Twsg==\"",
        "id": "AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",    
        "start": {
            "dateTime": "2022-05-06T15:00:00.0000000",
            "timeZone": "UTC"
        },
        "end": {
            "dateTime": "2022-05-06T15:30:00.0000000",
            "timeZone": "UTC"
        },
            
        "onlineMeeting": {
            "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjExYzJiMTItZDY1MS00ZGZkLWE5YzQtZTBmNWI1MDg2M2Uw%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%221273a016-201d-4f95-8083-1b7f99b3edeb%22%7d",
            "conferenceId": "438824583",
            "tollNumber": "+1 213-279-1007"
        }    
    }
    ```

    </details>

    La dirección URL de la reunión se encuentra en `joinUrl`.

3. **Obtener id. de conversación de chat**: use la dirección URL de la reunión obtenida en `joinUrl` para obtener el identificador de la conversación de chat. Especifique esta dirección URL de reunión como valor para el parámetro `joinWebUrl` al capturar la reunión relacionada.

    Use el ejemplo siguiente para solicitar el identificador de conversación:

    ``` http
    GET https://graph.microsoft.com/v1.0/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    La carga de respuesta contiene el miembro `threadID` de la propiedad `chatInfo`.
    <br>
    <details>
    <summary><b>Ejemplo</b>: carga de respuesta con id. de conversación</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

    El identificador de chat se encuentra en `threadId`.

4. **Suscribirse a mensajes de chat**: use el identificador de chat para suscribir su aplicación y recibir mensajes de chat para esa reunión en particular. Para más información, vea [Suscribirse a mensajes en un chat](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-in-a-chat).

    Si quiere que la aplicación se suscriba a mensajes con texto específico, consulte [Suscribirse a mensajes de un chat que contengan determinado texto](/graph/teams-changenotifications-chatmessage#example-2-subscribe-to-messages-in-a-chat-that-contain-certain-text).

5. Siga los pasos para las [notificaciones de nivel de inquilino](#obtain-meeting-details-using-tenant-level-notification) para obtener el identificador de reunión y el identificador del organizador.

#### <a name="obtain-meeting-details-using-tenant-level-notification"></a>Obtener detalles de la reunión mediante la notificación de nivel de inquilino

Las notificaciones de nivel de inquilino son útiles si la aplicación está autorizada para acceder a todas las transcripciones de reuniones en el inquilino. Suscriba su aplicación para recibir notificaciones de eventos cuando se inicie la transcripción o finalice la llamada para las reuniones programadas en línea de Teams. Una vez finalizada la reunión, la aplicación puede acceder a la transcripción de la reunión y recuperarla.

Para suscribir la aplicación a notificaciones de nivel de inquilino, consulte [Obtener notificaciones de cambios](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-across-all-chats).

Cuando se notifica a la aplicación sobre eventos de reunión suscritos, busca en las notificaciones la transcripción de los eventos iniciados y finalizados de la reunión. Estos eventos contienen el identificador de chat, que se usa para obtener la entidad de chat y, finalmente, el identificador de reunión y el identificador del organizador.

Para obtener el id. de reunión y el identificador del organizador de la notificación de nivel de inquilino:

1. **Obtener identificador de chat**: la aplicación obtiene la propiedad `chatId` de la notificación para realizar llamadas posteriores. La aplicación puede obtener el identificador de chat de las cargas de:

    - Evento de transcripción iniciada: tipo de evento `callTranscriptEventMessageDetail`

        <details>
        <summary><b>Ejemplo</b>: carga para el evento iniciado de transcripción</summary>

        ```json
        {
        "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787549174')",
        "contentDecryptedBySimulator": {
            "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
            "messageType": "systemEventMessage",
            "createdDateTime": "2022-04-12T18:19:09.174Z",
            "lastModifiedDateTime": "2022-04-12T18:19:09.174Z",
            "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
            "body": {
                "contentType": "html",
                "content": "<systemEventMessage/>"
            },
            "channelIdentity": null,
            "eventDetail": {
                "@odata.type": "#Microsoft.Teams.GraphSvc.callTranscriptEventMessageDetail",
                "callId": "16481de8-3262-419b-abc7-0139e6239515",
                "callTranscriptICalUid": "",
                "meetingOrganizer": {
                    "application": null,
                    "device": null,
                    "user": {
                    "userIdentityType": "aadUser",
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null
                        }
                    }
                }
            },
            "encryptedContent": {}
        }
        ```

        </details>

    - Evento de llamada finalizada: tipo de evento `callEndedEventMessageDetail`

        <details>
        <summary><b>Ejemplo</b>: carga del evento de llamada finalizada</summary>

        ```json
        {
            "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
            "changeType": "created",
            "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
            "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787585457')",
            "resourceData": {},
            "contentDecryptedBySimulator": {
                "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
                "createdDateTime": "2022-04-12T18:19:45.457Z",
                "lastModifiedDateTime": "2022-04-12T18:19:45.457Z",     
                "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
                "eventDetail": {
                    "@odata.type": "#Microsoft.Teams.GraphSvc.callEndedEventMessageDetail",
                    "callId": null,
                    "callDuration": "PT1M44S",
                    "callEventType": "meeting",
                    "callParticipants": [
                    ],
                    "initiator": {
        
                    }
                }
            },
            "encryptedContent": {
                    
            }
        }
        ```

        </details>

2. **Obtener entidad de chat**: la aplicación puede recuperar la entidad de chat mediante el identificador de chat obtenido en el paso 1. Use la entidad de chat para obtener la dirección URL para unirse a la llamada. El miembro `joinWebUrl` de la propiedad `onlineMeetingInfo` contiene esta dirección URL y se usa finalmente para obtener el identificador de reunión. El identificador del organizador también forma parte de la carga de respuesta.

    Para más información sobre la entidad de chat, vea [Obtener chat](/graph/api/chat-get).

    Use el ejemplo siguiente para solicitar una entidad de chat basada en el identificador de chat:

    ``` http
    GET https://graph.microsoft.com/v1.0/chats/19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2
    ```

    La carga de respuesta contiene los siguientes elementos:

    - **Identificador del organizador**: se encuentra en el miembro `id` de la propiedad `organizer` en la carga de respuesta.
    - **Dirección URL de la llamada a la reunión**: esta dirección URL se usa para recuperar el identificador de la reunión y está disponible en la carga de respuesta en uno de los dos escenarios:
        - Si la reunión es una reunión de Teams en línea, el miembro `joinWebUrl` de la propiedad `onlineMeetingInfo` contiene esta dirección URL.
        - Si la reunión no se creó como una reunión en línea desde el cliente de Teams o el cliente de Outlook, contiene el miembro `calendarEventId` en la propiedad `onlineMeetingInfo`. La aplicación puede usar `calendarEventId` para obtener `joinUrl`, que es igual que `joinWebUrl`.

      Para más información acerca de los eventos, vea [Obtener evento](/graph/api/event-get?view=graph-rest-1.0&tabs=http&preserve-view=true).

      Ejemplos de escenarios de carga de respuesta en función del tipo de dirección URL para unirse a la reunión:

        - Reunión de Teams en línea donde `joinWebUrl` está disponible

            <details>
            <summary><b>Ejemplo</b>: carga de respuesta para la reunión en línea</b></summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2",
                "topic": "Test Meet Create Online Meeting",
                "createdDateTime": "2022-04-14T11:30:45.903Z",
                "lastUpdatedDateTime": "2022-04-26T06:27:45.265Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                "calendarEventId": null,
                    "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

        - Reunión programada a través del cliente de Teams o el cliente de Outlook, no marcada como una reunión en línea en la que `calendarEventId` está disponible

            <details>
            <summary><b>Ejemplo</b>: carga de respuesta para la reunión no marcada como en línea</summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm@thread.v2",
                "topic": "Non Online Meeting Teams Client",
                "createdDateTime": "2022-04-26T09:43:23.711Z",
                "lastUpdatedDateTime": "2022-04-26T09:43:46.157Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                    "calendarEventId": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYeAAA=",
                    "joinWebUrl": null,
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

            - Use el ejemplo siguiente para obtener `joinWebUrl` del `calendarEventId`:

              ``` http
                GET https://graph.microsoft.com/beta/users/14b779ae-cb64-47e7-a512-52fd50a4154d/events/AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=
              ```

              En este ejemplo:

                - El identificador del organizador es *14b779ae-cb64-47e7-a512-52fd50a4154d*.

              La carga de respuesta de esta solicitud contiene `joinUrl` en la propiedad `onlineMeeting`.

                > [!NOTE]
                > `joinUrl` es igual que `joinWebUrl`.

              <br>
              <details>
              <summary><b>Ejemplo</b>: carga de respuesta que contiene la dirección URL para unirse a la reunión</summary>

              ```json
              {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/events/$entity",
                "@odata.etag": "W/\"bMMOQZSMbU+4hcmFq11dwAAAkc3Tmw==\"",
                "id": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=",    
                "start": {
                    "dateTime": "2022-04-26T10:30:00.0000000",
                    "timeZone": "UTC"
                },
                "end": {
                    "dateTime": "2022-04-26T11:00:00.0000000",
                    "timeZone": "UTC"
                },    
                "onlineMeeting": {
                    "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d"
                },
                "calendar@odata.associationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')/$ref",
                "calendar@odata.navigationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')"
                }
                ```

              </details>

3. **Obtener id. de reunión**: ahora, la aplicación puede usar `joinWebUrl` para obtener el identificador de reunión.

    Use el ejemplo siguiente para solicitar el identificador de reunión en línea:

    ``` http
    GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    La carga de respuesta contiene el identificador de reunión en el miembro `id` de la propiedad `value`.
    <br>
    <details>
    <summary><b>Ejemplo</b>: carga de respuesta con id. de reunión</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

4. **Capturar transcripción**: el identificador del organizador y el id. de reunión obtenidos en los pasos 2 y 3 permiten a la aplicación capturar las transcripciones de ese evento de reunión en particular.

    Para capturar transcripciones, deberá:

    1. **Recupere el id. de transcripción en función del identificador del organizador y del id. de reunión**:

       Use el ejemplo siguiente para solicitar el identificador de transcripción:

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts
        ```

        En este ejemplo:

        - El id. de reunión se incluye como el valor de `onlineMeetings`: *MSoxNGI3N skypehZS1jYjY0LTQ3ZTctYTUxMi01MmZkNT MeetingNDE1NGQqMCoqMTk6bW VldGluZ19ObVUwTlRreFl6TXRNMlkyTX trackME56UmxMV0ZtTjJZdE5URmlNR001T1dNM 1pqWTJAdGhyZWFkLnYy*.
        - El identificador del organizador es *14b779ae-cb64-47e7-a512-52fd50a4154d*.

        La carga de respuesta contiene el identificador de transcripción para el id. de reunión y el identificador del organizador en el miembro `id` de la propiedad `value`.
        <br>
        <details>
        <summary><b>Ejemplo</b>: carga de respuesta para obtener el identificador de transcripción</summary>

        ```json
        {
            "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts",
            "@odata.count": 1,
            "value": [
                {
                    "id": "MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh",
                    "createdDateTime": "2022-04-14T11:34:39.5662792Z"
                }
            ]
        }
        ```

        En este ejemplo, el identificador de la transcripción es *MSMjMCMjMD Tokens TokensJm TokensgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh*.

        </details>

    1. **Acceda a la transcripción de la reunión y obténgala en función del identificador de transcripción**:

        Use el ejemplo siguiente para solicitar las transcripciones de una reunión específica en el formato `.vtt`:

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts('MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh')/content?$format=text/vtt
        ```

        La carga de respuesta contendrá las transcripciones en formato `.vtt`.

### <a name="use-bot-framework-to-get-meeting-id-and-organizer-id"></a>Usar Bot Framework para obtener el id. de reunión y el identificador del organizador

La aplicación puede usar el Bot Framework para obtener el id. de reunión y el identificador del organizador. El bot puede recibir automáticamente eventos de inicio o finalización de reuniones de todas las reuniones en línea programadas.

Use el ejemplo siguiente para obtener el identificador de reunión y el identificador del organizador mediante una aplicación de bot:

```json
GET /v1/meetings/{meetingId}
```

La carga de respuesta contiene:

- Id. de reunión del miembro `msGraphResourceId` de la propiedad `details`.
- Identificador del organizador en el miembro `id` de la propiedad `organizer`.
<br>
<details>
<summary><b>Ejemplo</b>: carga de respuesta para obtener los detalles de la reunión</b></summary>

```json
{
  details: {
    id: "MCMxOTptZWV0aW5nX05XTTFNVEk1TnpNdE5qZ3pNeTAwWVdRNExUaG1PV1F0WlRnM01UQm1PVGczWW1VekB0aHJlYWQudjIjMA==",
    msGraphResourceId: "MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVldGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM1ltVXpAdGhyZWFkLnYy",
    scheduledStartTime: {
    },
    scheduledEndTime: {
    },
    joinUrl: "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz%40thread.v2/0?context=%7b%22Tid%22%3a%22b3cdf1c8-024a-49e2-a994-f67f830b02f3%22%2c%22Oid%22%3a%226702afb6-109b-4c32-a141-6e65469502b9%22%7d",
    title: "Testing meeting bot 1 - Hun",
    type: "Scheduled",
  },
  conversation: {
    id: "19:meeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz@thread.v2",
    isGroup: true,
    conversationType: "groupChat",
  },
  organizer: {
    id: "29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w",
    tenantId: "b3cdf1c8-024a-49e2-a994-f67f830b02f3",
    aadObjectId: "6702afb6-109b-4c32-a141-6e65469502b9",
  },
}
```

En este ejemplo:

- El identificador de reunión se incluye como el valor de `msGraphResourceId`: *MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVl dGluZ19OV00xTVRJNU56TXROamd6TltMFlAUTOTRMVGht1dRdFpUZzNNVEJtT1RnM 1ltVXpAdGhyZWFkLnYy*.
- El identificador del organizador se incluye como el valor de `id` para `organizer`: *29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w*.

</details>

Una vez que la aplicación obtiene el identificador de reunión y el identificador del organizador, desencadena las API de Graph para capturar el contenido de la transcripción con estos detalles de la reunión.

### <a name="code-samples"></a>Ejemplos de código

Puede probar el siguiente ejemplo de código para una aplicación de bot:

| **Ejemplo de nombre** | **Descripción** | **C#** | **Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
| Transcripción de reuniones | Se trata de una aplicación de ejemplo que muestra cómo obtener la transcripción mediante API de Graph y mostrarla en el módulo de tareas. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/nodejs) |

## <a name="next-step"></a>Paso siguiente

> [!div class="nextstepaction"]
> [API de Graph para capturar transcripciones](/graph/api/resources/calltranscript)
