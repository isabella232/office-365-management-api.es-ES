---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Service Communications API reference
title: Referencia de API de comunicaciones de servicio de Office 365
description: 'Use esta API para obtener acceso a los datos siguientes: Get Services, Get Current Status, Get Historical Status y Get Messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 9845fb5f422160a658b45bd7dd9a5bc6d4635914
ms.sourcegitcommit: ec60dbd5990cfc61b8c000b423e7ade25fa613a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397443"
---
# <a name="office-365-service-communications-api-reference"></a>Referencia de API de comunicaciones de servicio de Office 365

Puede usar la API de comunicaciones de servicio de Office 365 versión 2.0 para obtener acceso a los datos siguientes:

- **Get Services**: obtiene la lista de servicios suscritos.

- **Get Current Status**: proporciona una vista en tiempo real de las incidencias de servicio actuales y en curso

- **Get Historical Status**: proporciona una vista histórica de incidencias de servicio.

- **Get Messages**: encuentra comunicaciones de Incidencias y del Centro de mensajes.

Actualmente, la API de comunicaciones de servicio de Office 365 contiene datos de los servicios en la nube de Office 365, Yammer, Dynamics CRM y Microsoft Intune.

## <a name="the-fundamentals"></a>Conceptos básicos

La URL raíz de la API contiene un identificador de espacio empresarial que establece los ámbitos de las operaciones en un único espacio empresarial:

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

La **API de comunicaciones de servicio de Office 365** es un servicio REST que le permite desarrollar soluciones con cualquier lenguaje web y entorno de hospedaje que admita HTTPS y los certificados X.509. La API usa **Microsoft Azure Active Directory** y el protocolo **OAuth2** para la autenticación y autorización. Para obtener acceso a la API desde la aplicación, primero tendrá que registrarla en Azure AD y configurarla con los permisos en el ámbito adecuado. Esto permitirá a la aplicación solicitar los tokens de acceso de OAuth2 necesarios para llamar a la API. Para obtener más información sobre cómo registrar y configurar una aplicación en Azure AD, vea [Introducción a las API de administración de Office 365](get-started-with-office-365-management-apis.md).

Todas las solicitudes API necesitan el encabezado HTTP de autorización que tiene un token de acceso OAuth2 JWT válido obtenido de Azure AD que contiene la notificación **ServiceHealth.Read**; además, el identificador del espacio empresarial tiene que coincidir con el identificador de espacio empresarial de la URL raíz.

```json
Authorization: Bearer {OAuth2 token}
```

### <a name="request-headers"></a>Encabezados de solicitud

Estos son los encabezados de solicitud compatibles con todas las operaciones de la API de comunicaciones de servicio de Office 365.

|Encabezado|Descripción|
|:-----|:-----|
|**Accept (opcional)**|Las opciones siguientes son representaciones aceptables de la respuesta:<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>[El valor predeterminado si no se especifica el encabezado] **application/json;odata.metadata=none**|
|**Autorización (obligatorio)**|Token de autorización (token de portador de JWT Azure AD) para la solicitud.|

<br/>

### <a name="response-headers"></a>Encabezados de respuesta

Encabezados de respuesta devueltos por todas las operaciones de la API de comunicaciones de servicio de Office 365:

|Encabezado|Descripción|
|:-----|:-----|
|**Content-Length**|Longitud del cuerpo de la respuesta.|
|**Content-Type**|Representación de la respuesta:<br/>**application/json**<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>**application/json;odata.metadata=none**<br/>**odata.streaming=true**|
|**Cache-Control**|Se usa para especificar directivas que tienen que obedecer todos los mecanismos de almacenamiento en caché, así como la cadena de solicitud o respuesta.|
|**Pragma**|Comportamientos específicos de cada implementación.|
|**Expires**|Cuándo tiene que expirar el recurso el cliente.|
|**X-Activity-Id**|Id. de actividad generado por el servidor.|
|**OData-Version**|Versión de OData admitida (4.0).|
|**Date**|Fecha en formato UTC en que se envió la respuesta desde el servidor.|
|**X-Time-Taken**|Tiempo necesario para generar la respuesta (ms).|
|**X-Instance-Name**|Identificador de la instancia de Azure usado para generar la respuesta (con fines de depuración).|
|**Server**|Servidor usado para generar la respuesta (con fines de depuración).|
|**X-ASPNET-Version**|Versión de ASP.NET usada por el servidor que generó la respuesta (con fines de depuración).|
|**X-Powered-By**|Tecnologías usadas en el servidor que generó la respuesta (con fines de depuración).|
|||

<br/>

Estas son las operaciones de la API de comunicaciones de servicio de Office 365.

## <a name="get-services"></a>Get Services

Devuelve la lista de los servicios suscritos.

|Información|Servicio|Descripción|
|:-----|:-----|:-----|
|**Ruta**| `/Services`||
|**Opción de consulta**|$select|Selecciona un subconjunto de propiedades.|
|**Respuesta**|Lista de entidades de “Service”|La entidad “Service” contiene “Id” (cadena), “DisplayName” (cadena) y “FeatureNames” (lista de cadenas).|
||||

### <a name="sample-request"></a>Solicitud de muestra

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

### <a name="sample-response"></a>Respuesta de muestra

```json
{
    "value": [
        {
            "Id": "Exchange",
            "DisplayName": "Exchange Online",
            "FeatureNames": [
                "Sign-in",
                "E-Mail and calendar access",
                "E-Mail timely delivery",
                "Management and Provisioning",
                "Voice mail"
            ]
        },
        {
            "Id": "Lync",
            "DisplayName": "Lync Online",
            "FeatureNames": [
                "Audio and Video",
                "Federation",
                "Management and Provisioning",
                "Sign-In",
                "All Features",
                "Dial-In Conferencing",
                "Online Meetings",
                "Instant Messaging",
                "Presence",
                "Mobility"
            ]
        }
    ]
}
```

## <a name="get-current-status"></a>Get Current Status

Devuelve el estado del servicio de las 24 horas anteriores.

> [!NOTE] 
> La respuesta del servicio contendrá el estado y cualquier incidente ocurrido durante las 24 horas anteriores. El valor de StatusDate o StatusTime devuelto será exactamente de 24 horas antes. Para obtener la última actualización de un incidente determinado, utilice la función Obtener mensajes y lea el valor LastUpdatedTime del registro de respuesta que coincida con el ID. de la incidencia. <br/>

<br/>

|Información|Servicio|Descripción|
|:-----|:-----|:-----|
|**Ruta**| `/CurrentStatus`||
|**Filtro**|Carga de trabajo|Filtrar por carga de trabajo (cadena, predeterminado: todo).|
|**Opción de consulta**|$select|Selecciona un subconjunto de propiedades.|
|**Respuesta**|Lista de entidades “WorkloadStatus”.|La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).<br/><br/>La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).|
||||

### <a name="sample-request"></a>Solicitud de muestra

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Respuesta de muestra

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Lync",
            "Workload": "Lync",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Lync Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "AudioVideo",
                    "FeatureGroupDisplayName": "Audio and Video",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Federation",
                    "FeatureGroupDisplayName": "Federation",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "ManagementandProvisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Sign-In",
                    "FeatureGroupDisplayName": "Sign-In",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "All",
                    "FeatureGroupDisplayName": "All Features",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "DialInConferencing",
                    "FeatureGroupDisplayName": "Dial-In Conferencing",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "OnlineMeetings",
                    "FeatureGroupDisplayName": "Online Meetings",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "InstantMessaging",
                    "FeatureGroupDisplayName": "Instant Messaging",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Presence",
                    "FeatureGroupDisplayName": "Presence",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Mobility",
                    "FeatureGroupDisplayName": "Mobility",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        }
    ]
}
```

### <a name="status-definitions"></a>Definiciones de estado

Las definiciones de estado incluyen los siguientes valores:

- Investigating
- ServiceDegradation
- ServiceInterruption
- RestoringService
- ExtendedRecovery
- InvestigationSuspended
- ServiceRestored
- FalsePositive
- PostIncidentReportPublished
- ServiceOperational

Para una descripción de estas definiciones de estado, consulte [Cómo comprobar el estado del servicio de Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/view-service-health#status-definitions).

## <a name="get-historical-status"></a>Get Historical Status

Devuelve el historial de estado del servicio, por día, en un intervalo de tiempo específico.

|Información|Servicio|Descripción|
|:-----|:-----|:-----|
|**Ruta**| `/HistoricalStatus`||
|**Filtros**|Carga de trabajo|Filtrar por carga de trabajo (cadena, predeterminado: todo).|
||StatusTime|Permite filtrar por número de días superior a StatusTime (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).|
|**Opción de consulta**|$select|Selecciona un subconjunto de propiedades.|
|**Respuesta**|Lista de entidades “WorkloadStatus”.|La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).<br/><br/>La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).|
||||

### <a name="sample-request"></a>Solicitud de muestra

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Respuesta de muestra

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-10T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "InformationAvailable",
            "IncidentIds": [
                "EX20870"
            ],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "InformationAvailable"
                }
            ]
        }
    ]
}
```

## <a name="get-messages"></a>Get Messages

Devuelve los mensajes sobre el servicio en un intervalo de tiempo específico. Use el filtro de tipo para filtrar por mensajes de “incidentes en el servicio”, “mantenimiento planeado” o del “Centro de mensajes”.

|Información|Servicio|Descripción|
|:-----|:-----|:-----|
|**Ruta**| `/Messages`||
|**Filtros**|Carga de trabajo|Filtrar por carga de trabajo (cadena, predeterminado: todo).|
||StartTime|Permite filtrar por hora de inicio (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).|
||EndTime|Permite filtrar por hora de finalización (DateTimeOffset, predeterminado: le CurrentTime).|
||MessageType|Permite filtrar por MessageType (cadena, predeterminado: todo).|
||ID|Permite filtrar por id. (cadena, predeterminado: todo).|
|**Opción de consulta**|$select|Selecciona un subconjunto de propiedades.|
||$top|Selecciona el mayor número de resultados (predeterminado y máximo $top=100).|
||$skip|Omite el número de resultados (predeterminado: $skip=0).|
|**Respuesta**|Lista de entidades de “Message”.|La entidad “Message” contiene “Id” (cadena), “StartTime” (DateTimeOffset), “EndTime” (DateTimeOffset), “Status” (cadena), “Messages” (lista de la entidad “MessageHistory”), “LastUpdatedTime” (DateTimeOffset), “Workload” (cadena), “WorkloadDisplayName” (cadena), “Feature” (cadena), “FeatureDisplayName” (cadena), “MessageType” (enumeración, predeterminado: todo).<br/><br/>La entidad “MessageHistory” contiene “PublishedTime” (DateTimeOffset), “MessageText” (cadena).|
||||

### <a name="sample-request"></a>Solicitud de muestra

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Respuesta de muestra

```json
{
    "value": [
        {
            "Id": "EX20119",
            "Name": "EX20119",
            "Title": null,
            "StartTime": "2015-04-01T22:25:00Z",
            "EndTime": "2015-04-07T21:48:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-01T22:34:28.76Z",
                    "MessageText": "Current Status: Engineers are investigating an issue in which some customers may be experiencing problems accessing or using Exchange Online services or features. This event is actively being investigated. More information will be provided shortly."
                },
                {
                    "PublishedTime": "2015-04-03T18:45:32.56Z",
                    "MessageText": "Current Status: Engineers are implementing a fix within the affected infrastructure to remediate Exchange Online archive access issues. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client.\n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \n\nNext Update by: Monday, April 6, 2015, at 9:00 PM UTC\n"
                },
                {
                    "PublishedTime": "2015-04-06T21:17:34.007Z",
                    "MessageText": "Current Status: Deployment of the fix is almost complete. Engineers are monitoring service health to ensure the issue has been remediated. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client. \n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues. \n\nNext Update by: Tuesday, April 7, 2015, at 10:00 PM UTC "
                },
                {
                    "PublishedTime": "2015-04-08T21:54:49.06Z",
                    "MessageText": "Final Status: Engineers have implemented a fix which remediated end-user impact. \r\n\r\nUser Experience: Affected users were unable to access online archives when using Outlook Web App (OWA).\r\n\r\nCustomer Impact: Customer impact appears to have been limited. This issue only affected hybrid customers.\r\n\r\nIncident Start Time: Monday, March 30, 2015, at 9:28 AM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 8:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the monitoring infrastructure for improvements as this event was reported by customers before an alert prompted a high priority investigation. \r\n\r\nA post-incident report will be available on the Service Health Dashboard within five business days."
                }
            ],
            "LastUpdatedTime": "2015-04-08T21:54:49.55Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        },
        {
            "Id": "EX20789",
            "Name": "EX20789",
            "Title": null,
            "StartTime": "2015-04-06T20:00:00Z",
            "EndTime": "2015-04-07T23:00:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-07T23:26:44.643Z",
                    "MessageText": "Final Status: Engineers have validated that the deployed fix has resolved the issue and that service is restored.\r\n\r\nUser Experience: Affected users were unable to send or receive email while using Exchange Web Services (EWS) on their mobile devices.\r\n\r\nCustomer Impact: Customer impact appeared to be limited during this event. This issue was only affecting customers that use third-party Mobile Device Management software from Good Technology. As a workaround to provide immediate relief from impact, engineers implemented a configuration change for customers who reported this issue to Microsoft Support.\r\n\r\nIncident Start Time: Wednesday, April 1, 2015, at 2:00 PM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 10:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing efforts to improve service resiliency, an update was deployed to the infrastructure that facilitates connections from multiple Exchange Online protocols to mailbox databases. The update, however, contained a code issue that caused connectivity issues in some scenarios. \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the infrastructure update process to prevent reoccurrences of this scenario.\r\n\r\nPlease consider this service notification the final update on the event."
                }
            ],
            "LastUpdatedTime": "2015-04-07T23:26:45.08Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        }
    ]
}
```


## <a name="errors"></a>Errores

Cuando el servicio encuentre un error, indicará el código de respuesta de error al autor de la llamada mediante la sintaxis estándar de código de error de HTTP. Según la [especificación de OData versión 4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), se incluye información adicional en el cuerpo de la llamada con errores como un único objeto JSON. Abajo se muestra un ejemplo del cuerpo completo de un error en formato JSON:


```json
{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}
```
