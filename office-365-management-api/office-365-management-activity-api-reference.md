---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management Activity API reference
title: Referencia de la API de Actividad de administración de Office 365
description: Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 94879a2634396868248d3df6a6eb76b9931d9f65
ms.sourcegitcommit: ec60dbd5990cfc61b8c000b423e7ade25fa613a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397429"
---
# <a name="office-365-management-activity-api-reference"></a>Referencia de la API de Actividad de administración de Office 365

Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD. 

Puede usar acciones y eventos de los registros de auditoría y actividad de Office 365 y Microsoft Azure Active Directory para crear soluciones que proporcionen supervisión, análisis y visualización de datos. Estas soluciones ofrecen a las organizaciones mayor visibilidad de las acciones realizadas en el contenido. Estas acciones y eventos también están disponibles en los informes de actividad de Office 365. Para obtener más información, vea [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).

La API de Actividad de administración de Office 365 es un servicio web REST que se puede usar para desarrollar soluciones mediante cualquier lenguaje y entorno de hospedaje que admita HTTPS y certificados X.509. La API se basa en Azure AD y el protocolo OAuth2 para la autorización y autenticación. Para acceder a la API desde la aplicación, primero deberá registrarla en Azure AD y configurarla con los permisos apropiados. Esto permitirá que la aplicación solicite los tokens de acceso OAuth2 que necesita para llamar a la API. Para obtener más información, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).

Para obtener información sobre los datos que devuelve la API de Actividad de administración de Office 365, vea [Esquema de la API de Actividad de administración de Office 365](office-365-management-activity-api-schema.md).

> [!IMPORTANT]
> Para poder acceder a los datos a través de la API de Actividad de administración de Office 365, debe activar el registro de auditoría unificado para su organización de Office 365. Para ello, active el registro de auditoría de Office 365. Para obtener instrucciones, consulte [Activar o desactivar la búsqueda de registros de auditoría de Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).


## <a name="working-with-the-office-365-management-activity-api"></a>Trabajar con la API de Actividad de administración de Office 365

La API de Actividad de administración de Office 365 agrega acciones y eventos en blobs de contenido específicos del espacio empresarial, que se clasifican según el tipo y el origen del contenido que contienen. En la actualidad, se admiten estos tipos de contenido:

- Audit.AzureActiveDirectory
    
- Audit.Exchange
    
- Audit.SharePoint
    
- Audit.General (incluye todas las demás cargas de trabajo que no se incluyen en los tipos de contenido anteriores)

- DLP.All (eventos exclusivos de DLP para todas las cargas de trabajo)
    
Para obtener más información sobre los eventos y las propiedades asociados a estos tipos de contenido, vea [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md) (Esquema de la API de Actividad de administración de Office 365).

Para empezar a recuperar los blobs de contenido para un espacio empresarial, primero se crea una suscripción a los tipos de contenido deseados. Si se van a recuperar blobs de contenido para varios espacios empresariales, cree varias suscripciones a todos los tipos de contenido deseados, una para cada espacio empresarial.

Después de crear una suscripción, puede sondear periódicamente para detectar nuevos blobs de contenido disponibles para descargar, o bien puede registrar un punto de conexión de webhook con la suscripción y se enviarán notificaciones a este punto de conexión cuando haya nuevos blobs de contenido disponibles.


> [!NOTE] 
> Cuando se crea una suscripción, pueden pasar hasta 12 horas hasta que los primeros blobs de contenido estén disponibles para esa suscripción. Para crear los blobs de contenido, se recopilan y agregan acciones y eventos de varios servidores y centros de datos. Como resultado de este proceso distribuido, las acciones y los eventos incluidos en los blobs de contenido no aparecerán necesariamente en el orden en que se producen. Un blob de contenido puede contener acciones y eventos que tuvieron lugar antes de las acciones y los eventos incluidos en un blob de contenido anterior. Estamos trabajando para reducir la latencia entre la aparición de los eventos y las acciones, y su disponibilidad en un blob de contenido, pero no podemos garantizar que aparezcan de forma secuencial.


> [!NOTE] 
> Los datos confidenciales de DLP solo están disponibles en la API de fuente de actividades para los usuarios a los que se les han concedido permisos "Leer datos confidenciales de DLP". Para obtener más información sobre la prevención de pérdida de datos (DLP), vea [Información general sobre directivas de prevención de pérdida de datos](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).

## <a name="activity-api-operations"></a>Operaciones de la API de Actividad

Todas las operaciones de API están orientadas a un único espacio empresarial y la dirección URL raíz de la API incluye un identificador de espacio empresarial que especifica el contexto del espacio empresarial. El identificador de espacio empresarial es un GUID. Para obtener información sobre cómo conseguir el GUID, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365). 

Como las notificaciones que se envían al webhook incluyen el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales.

La URL del punto de conexión de la API que use está basada en el tipo de plan de suscripción de Microsoft 365 u Office 365 de su organización.

**Plan para empresas**

```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

**Plan de Administración pública GCC**

```http
https://manage-gcc.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

**Plan de Administración pública GCC High**

```http
https://manage.office365.us/api/v1.0/{tenant_id}/activity/feed/{operation}
```

**Plan de Administración pública DoD**

```http
https://manage.protection.apps.mil/api/v1.0/{tenant_id}/activity/feed/{operation}
```

Todas las operaciones de API requieren un encabezado de autorización HTTP con un token de acceso obtenido de Azure AD. El identificador de espacio empresarial en el token de acceso debe coincidir con el de la dirección URL raíz de la API y el token de acceso debe contener la notificación ActivityFeed.Read (que se corresponde con el permiso [Leer datos de actividad de la organización] que ha configurado para la aplicación en Azure AD).

```json
Authorization: Bearer eyJ0e...Qa6wg
```

La API de Actividad admite las operaciones siguientes:

- **Iniciar una suscripción** para empezar a recibir notificaciones y recuperar datos de actividad de un espacio empresarial.
    
- **Detener una suscripción** para dejar de recuperar datos de un espacio empresarial.
    
- **Enumerar las suscripciones actuales**
    
- **Enumerar el contenido disponible** y las direcciones URL de contenido correspondientes.
    
- **Recibir notificaciones** enviadas por un webhook cuando hay contenido nuevo disponible.
    
- **Recuperar contenido** mediante la dirección URL de contenido.
    
- **Enumerar las notificaciones** enviadas por un webhook.

- **Recuperar los nombres descriptivos de recurso** de los objetos de la fuente de datos identificados mediante GUID.
    

## <a name="start-a-subscription"></a>Iniciar una suscripción

Esta operación inicia una suscripción para el tipo de contenido especificado. Si ya existe una suscripción para el tipo de contenido específico, esta operación se usa para:

- Actualizar las propiedades de un webhook activo.
    
- Habilitar un webhook que estaba deshabilitado debido a un exceso de notificaciones con error.
    
- Volver a habilitar un webhook expirado mediante la especificación de una fecha de expiración nula o posterior.
    
- Quitar un webhook.
    
||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/subscriptions/start?contentType={ContentType}`||
|**Parámetros**|contentType|Debe ser un tipo de contenido válido.|
||PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
|**Cuerpo**|webhook|Objeto JSON opcional con tres propiedades:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>address</b>: punto de conexión HTTPS requerido que puede recibir notificaciones.  Se enviará un mensaje de prueba al webhook para validarlo antes de crear la suscripción.</p></li><li><p><b>authId</b>: cadena opcional que se incluirá como el encabezado WebHook-AuthID de las notificaciones que se envían al webhook como medio para identificar y autorizar el origen de la solicitud al webhook.</p></li><li><p><b>expiration</b>: valor de fecha y hora opcional que indica una fecha y hora después de la que no se deben enviar más notificaciones al webhook.</p></li></ul>|
|**Respuesta**|contentType|El tipo de contenido especificado en la llamada.|
||status|El estado de la suscripción. Si una suscripción está deshabilitada, no podrá enumerar o recuperar el contenido.|
||webhook|Las propiedades del webhook especificado en la llamada junto con el estado del webhook. Si el webhook está deshabilitado, no recibirá notificaciones, pero todavía podrá enumerar y recuperar el contenido, siempre que la suscripción esté habilitada.|

#### <a name="sample-request"></a>Solicitud de muestra

```json
POST {root}/subscriptions/start?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Content-Type: application/json; utf-8
Authorization: Bearer eyJ0e...Qa6wg

{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }
}

```


#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
    "contentType": "Audit.SharePoint",
    "status": "enabled",
    "webhook": {
        "status": "enabled",
        "address":  "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": null
    }
}

```


## <a name="webhook-validation"></a>Validación del webhook

Cuando se llama a la operación /start y se especifica un webhook, le enviaremos una notificación de validación a la dirección de webhook especificada para validar que una escucha activa puede aceptar y procesar las notificaciones. Si no recibimos una respuesta HTTP 200 Correcto, no se creará la suscripción. O bien, si se empieza a llamar a /start para agregar un webhook a una suscripción existente y no se recibe una respuesta de HTTP 200 Correcto, el webhook no se agregará y no se cambiará la suscripción.

#### <a name="sample-request"></a>Solicitud de muestra

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a>Respuesta de muestra

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a>Detener una suscripción

Esta operación detiene una suscripción para el tipo de contenido especificado. 

Cuando se detiene una suscripción, ya no recibirá notificaciones y no podrá recuperar el contenido disponible. Si más adelante se reinicia la suscripción, tendrá acceso al contenido nuevo a partir de ese punto. No podrá recuperar el contenido que estaba disponible entre el momento de detener la suscripción y reiniciarla.


||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/subscriptions/stop?contentType={ContentType}`||
|**Parámetros**|contentType|Debe ser un tipo de contenido válido.|
||PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
|**Cuerpo**|(vacío)||
|**Respuesta**|(vacío)|||

#### <a name="sample-request"></a>Solicitud de muestra

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a>Enumerar las suscripciones actuales

Esta operación devuelve una colección de las suscripciones actuales junto con los webhooks asociados.

||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/subscriptions/list`||
|**Parámetros**|PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
|**Cuerpo**|(vacío)||
|**Respuesta**|Matriz JSON|Cada suscripción se representará mediante un objeto JSON con tres propiedades:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>: indica el tipo de contenido.</p></li><li><p><b>status</b>: indica el estado de la suscripción.</p></li><li><p><b>webhook</b>: indica el webhook configurado, junto con el estado (habilitado, deshabilitado, expirado) del webhook.  Si una suscripción no tiene un webhook, la propiedad webhook estará presente pero con un valor NULL.</p></li></ul>|


#### <a name="sample-request"></a>Solicitud de muestra

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType" : "Audit.SharePoint",
        "status": "enabled",
        "webhook": {
            "status": "enabled",
            "address": "https://webhook.myapp.com/o365/",
            "authId": "o365activityapinotification",
            "expiration": null
        }
    },

    ...

    {
        "contentType": "Audit.Exchange",
        "webhook": null
    }
]

```


## <a name="list-available-content"></a>Enumerar el contenido disponible

Esta operación enumera el contenido disponible actualmente que se puede recuperar para el tipo de contenido especificado. El contenido es una agregación de acciones y eventos recopilados de varios servidores en varios centros de datos. El contenido se mostrará en el orden en que estén disponibles las agregaciones, pero no se garantiza que los eventos y las acciones de las agregaciones sean secuenciales. Se devuelve un error si el estado de la suscripción es deshabilitado.


||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Parámetros**|contentType|Debe ser un tipo de contenido válido.|
||PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
||startTime endTime|Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido. El intervalo de tiempo es inclusivo con respecto a startTime (startTime <= contentCreated) y exclusivo con respecto a endTime (contentCreated < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>AAAA-MM-DD</p></li><li><p>AAAA-MM-DDTHH:MM</p></li><li><p>AAAA-MM-DDTHH:MM:SS</p></li></ul>Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad.  De forma predeterminada, si se omiten startTime y endTime, se devuelve el contenido disponible en las últimas 24 horas.<p>**NOTA**: Aunque se puede especificar un valor de startTime y endTime con más de 24 horas de diferencia, no es recomendable. Además, si obtiene algún resultado en respuesta a una solicitud de más de 24 horas, podrían ser resultados parciales y no deberían tenerse en cuenta. La solicitud se debe emitir con un intervalo de no más de 24 horas entre los valores de startTime y endTime.</p>|
|**Respuesta**|Matriz JSON|El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>: indica el tipo de contenido.</p></li><li><p><b>contentId</b>: una cadena opaca que identifica el contenido de forma única.</p></li><li><p><b>contentUri</b>: la dirección URL que se va a usar al recuperar el contenido.</p></li><li><p><b>contentCreated</b>: la fecha y hora de disponibilidad del contenido.</p></li><li><p><b>contentExpiration</b>: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</p></li></ul>|


#### <a name="sample-request"></a>Solicitud de muestra

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


### <a name="pagination"></a>Paginación

Al enumerar el contenido disponible para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta. Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncarán y se agregará un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados. La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente. Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUri**.


## <a name="receiving-notifications"></a>Recibir notificaciones

Las notificaciones se envían al webhook configurado para una suscripción cuando hay contenido nuevo disponible. Como la notificación incluye el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales para los que tiene suscripciones.

La notificación se realiza como HTTP POST sobre TLS (TLS 1.0 y versiones posteriores) a la dirección del webhook especificado. Si la configuración de webhook incluye un identificador de autenticación, se enviará como un encabezado HTTP: Webhook-AuthID. Cualquier respuesta distinta de HTTP 200 Correcto se considera un error y la notificación se volverá a intentar. También puede configurar el webhook para requerir autenticación basada en certificados de cliente y se autenticará con el certificado manage.office.com.

El cuerpo de la solicitud contendrá una matriz de uno o más objetos JSON que representan los blobs de contenido disponibles. El número de blobs de contenido en cada notificación es limitado para que el tamaño de la notificación sea relativamente pequeño. Como este límite puede cambiar, la implementación debe consultar la longitud de la matriz en lugar de esperar un tamaño fijo. Cada objeto incluirá las mismas propiedades que devuelve la operación /content, junto con el GUID del espacio empresarial al que corresponden los datos y el GUID de la aplicación que creó las suscripciones. Esto permite al webhook establecer el contexto cuando se usa con varios espacios empresariales y aplicaciones.

- **tenantId**: el GUID del espacio empresarial al que pertenece el contenido.
    
- **clientId**: el GUID de la aplicación que creó la suscripción.
    
- **contentType**: indica el tipo de contenido.
    
- **contentId**: una cadena opaca que identifica el contenido de forma única.
    
- **contentUri**: la dirección URL que se va a usar al recuperar el contenido.
    
- **contentCreated**: la fecha y hora de disponibilidad del contenido.
    
- **contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.
    
A continuación se muestra un ejemplo de una notificación.

```json
POST https://webhook.myapp.com/o365/ 
Content-Type: application/json; utf-8
Webhook-AuthID: o365activityapinotification

[
    {
        "tenantId": "{GUID}"
        "clientId": "{GUID}"
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


## <a name="notification-failure-and-retry"></a>Error de notificación y reintento

El sistema de notificaciones envía las notificaciones cuando hay nuevo contenido disponible. Si se producen errores excesivos al enviar las notificaciones, nuestro mecanismo de reintento aumentará de forma exponencial el tiempo entre los reintentos. Si se siguen produciendo errores, nos reservamos el derecho de deshabilitar el webhook y detener por completo el envío de notificaciones. Se puede usar la operación /start para volver a habilitar un webhook deshabilitado.


## <a name="retrieving-content"></a>Recuperación de contenido

Para recuperar un blob de contenido, realice una solicitud GET en el URI del contenido correspondiente que se incluye en la lista de contenido disponible y en las notificaciones enviadas a un webhook. El contenido devuelto será una colección de una más acciones o eventos en formato JSON.

#### <a name="sample-request"></a>Solicitud de muestra

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "CreationTime": "2015-06-29T20:03:19",
        "Id": "80c76bd2-9d81-4c57-a97a-accfc3443dca",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "failed",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "ExtendedProperties": [
            {
                "Name": "LoginError",
                "Value": "-2147217390;PP_E_BAD_PASSWORD;The entered and stored passwords do not match."
            }
        ],
        "Client": "Exchange",
        "LoginStatus": -2147217390,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:03:34",
        "Id": "4e655d3f-35fa-42e0-b050-264b2d255c7a",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "success",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Client": "Exchange",
        "LoginStatus": 0,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:04:55",
        "Id": "b567caf0-088e-4c1c-a4ea-633a1e3d66c8",
        "Operation": "Add User.",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 8,
        "ResultStatus": "success",
        "UserKey": "1003BFFD8EC47CA6@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ObjectId": "user001@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Actor": [
            {
                "ID": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
                "Type": 2
            },
            {
                "ID": "admin@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "1003BFFD8EC47CA6",
                "Type": 3
            }
        ],
        "ActorContextId": "41463f53-8812-40f4-890f-865bf6e35190",
        "InterSystemsId": "c2ced078-ad57-4079-a743-5c37f5284790",
        "IntraSystemId": "d1497f7e-15b4-49aa-83ad-11a17ca4a2f4",
        "Target": [
            {
                "ID": "user001@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "10037FFE91510806",
                "Type": 3
            }
        ],
        "TargetContextId": "41463f53-8812-40f4-890f-865bf6e35190"
    }
]

```


## <a name="list-notifications"></a>Enumerar notificaciones

Esta operación enumera todos los intentos de notificación para el tipo de contenido especificado. Si no ha incluido un webhook al iniciar la suscripción para el tipo de contenido, no existirá ninguna notificación para recuperar. Como en caso de error se reintentan las notificaciones, esta operación puede devolver varias notificaciones para el mismo contenido, y el orden en el que se envían no coincidirá necesariamente con el orden en que el contenido está disponible (en especial si hay errores y reintentos). 

Puede usar esta operación para ayudar a investigar problemas relacionados con los webhooks y las notificaciones, pero no debería usarla para determinar qué contenido está disponible actualmente para la recuperación. En su lugar, use la operación /content. Se devolverá un error si el estado de la suscripción es deshabilitado.


||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Parámetros**|contentType|Debe ser un tipo de contenido válido.|
||PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
||startTime endTime|Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido. El intervalo de tiempo es inclusivo con respecto a _startTime_ ( _startTime_ <= contentCreated) y exclusivo con respecto a _endTime_ (_contentCreated_ < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>AAAA-MM-DD</p></li><li><p>AAAA-MM-DDTHH:MM</p></li><li><p>AAAA-MM-DDTHH:MM:SS</p></li></ul>Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad.  De forma predeterminada, si se omiten _startTime_ y _endTime_, se devuelve el contenido disponible en las últimas 24 horas.|
|**Respuesta**|Matriz JSON|Las notificaciones disponibles se representarán mediante objetos JSON con las propiedades siguientes: <ul><li>**contentType**: indica el tipo de contenido.</li><li>**contentId**: una cadena opaca que identifica el contenido de forma única.</li><li>**contentUri**: la dirección URL que se va a usar al recuperar el contenido. </li><li>**contentCreated**: la fecha y hora de disponibilidad del contenido.</li><li>**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</li><li>**notificationSent**: la fecha y hora de envío de la notificación.</li><li>**notificationStatus**: indica si intento de notificación se ha realizado correctamente o no.</li></ul>|

#### <a name="sample-request"></a>Solicitud de muestra

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z",
        "notificationSent": "2015-05-23T17:36:00.000Z",
        "notificationStatus": "success"

    },
    ...
]

```


### <a name="pagination"></a>Paginación

Al enumerar el historial de notificaciones para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta. Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncan y se agrega un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados. La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente. Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUrl**.

## <a name="retrieve-resource-friendly-names"></a>Recuperar los nombres descriptivos de recurso

Esta operación recupera los nombres descriptivos de los objetos de la fuente de datos identificados mediante GUID. En la actualidad, el único objeto que se admite es "DlpSensitiveType". 


||Suscripción|Descripción|
|:-----|:-----|:-----|
|**Ruta de acceso**| `/resources/dlpSensitiveTypes`||
|**Parámetros**|PublisherIdentifier|El GUID de espacio empresarial del proveedor que codifica la API. Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código. Este parámetro se usa para limitar la velocidad de la solicitud. Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada. Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.|
|**Encabezados**|Accept-Language|Encabezado para especificar el idioma que prefiere para los nombres localizados. Por ejemplo, use "en-US" para inglés o "es" para español. Si este encabezado no existe, se devolverá el idioma predeterminado (en-US).|
|**Cuerpo**|(vacío)||
|**Respuesta**|Matriz JSON|El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>id</b>: indica el GUID del tipo de información confidencial.</p></li><li><p><b>name</b>: el nombre descriptivo del tipo de información confidencial.</p></li></ul>|

#### <a name="sample-request"></a>Solicitud de muestra

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a>Respuesta de muestra

```json
HTTP/1.1 200 OK

[
    {
        "id": "50842eb7-edc8-4019-85dd-5a5c1f2bb085",
        "name": "CreditCardNumber"
    }, 
    {
        "id": "0e9b3178-9678-47dd-a509-37222ca96b42",
        "name": "EUDebitCardNumber"
    }, 
    ...
    {
    }
]

```

## <a name="api-throttling"></a>Limitación de API

Las organizaciones que tienen acceso a registros de auditoría a través de la API de Actividad de administración de Office 365 se restringieron con límites en el nivel de editor. Esto significa que, para un editor que extrae datos en nombre de varios clientes, todos los clientes han compartido el límite.

Estamos cambiando de un límite de nivel de editor a un límite de nivel de espacio empresarial. El resultado es que cada organización obtendrá su propia cuota de ancho de banda completamente asignada para tener acceso a los datos de auditoría. Se asigna inicialmente una línea base de 2 000 solicitudes por minuto a todas las organizaciones. Este no es un límite estático y predefinido, sino que se modela en base a una combinación de factores, incluido el número de puestos en la organización, y que las organizaciones de Office 365 y Microsoft 365 E5 tendrán aproximadamente el doble de ancho de banda que las organizaciones que no son E5. También habrá un límite en el ancho de banda máximo para proteger el estado del servicio.

Para obtener más información, vea la sección "acceso de banda ancha a la API de Actividad de administración de Office 365" en [Auditoría avanzada en Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).

> [!NOTE] 
> Aunque cada espacio empresarial puede enviar en un principio hasta 2 000 solicitudes por minuto, Microsoft no garantiza una velocidad de respuesta. La velocidad de respuesta depende de varios factores, como el rendimiento del sistema cliente y la capacidad y la velocidad de la red. 

## <a name="errors"></a>Errores

Cuando el servicio encuentra un error, notificará el código de respuesta de error al autor de la llamada, mediante la sintaxis estándar de código de error de HTTP. . En el cuerpo de la llamada con error se incluye información adicional como un único objeto JSON. A continuación se muestra un ejemplo de un cuerpo completo de error JSON: 

```json

{ 
    "error":{ 
        "code":"AF50000",
        "message": "An internal server error occurred. Retry the request."
    } 
}

```


|||
|:-----|:-----|
|Código|Mensaje|
|AF10001|El conjunto de permisos ({0}) enviados en la solicitud no incluía el permiso esperado **ActivityFeed.Read**.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = el conjunto de permisos en el token de acceso.</p></li></ul>|
|AF20001|Falta el parámetro: {0}. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = el nombre del parámetro que falta.</p></li></ul>|
|AF20002|Tipo de parámetro no válido: {0}. Tipo esperado: {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = el nombre del parámetro no válido.</p></li><li><p>{1} = el tipo esperado (int, datetime, guid).</p></li></ul>|
|AF20003|{0} de expiración proporcionada se establece en una fecha y hora pasadas.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = la expiración que se pasa en la llamada de API.</p></li></ul>|
|AF20010|El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no coincide con el que se pasa en el token de acceso ({1}).<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = el identificador de espacio empresarial que se pasa en la dirección URL</p></li><li><p>{1} = el identificador de espacio empresarial que se pasa en el token de acceso</p></li></ul>|
|AF20011|El identificador de espacio empresarial ({0}) especificado no existe en el sistema o se ha eliminado. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   {0} = el identificador de espacio empresarial que se pasa en la dirección URL</p></li></ul>|
|AF20012|El identificador de espacio empresarial ({0}) especificado no está configurado correctamente en el sistema. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    {0} = el identificador de espacio empresarial que se pasa en la dirección URL</p></li></ul>|
|AF20013|El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no es un GUID válido.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> {0} = el identificador de espacio empresarial que se pasa en la dirección URL</p></li></ul>|
|AF20020|El tipo de contenido especificado no es válido.|
|AF20021|El punto de conexión de webhook {{0}) no se pudo validar. {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = dirección del webhook.</p></li><li><p>{1} = "El punto de conexión no devolvió HTTP 200". o bien, "La dirección debe comenzar con HTTPS".</p></li></ul>|
|AF20022|No se encontró ninguna suscripción para el tipo de contenido especificado.|
|AF20023|{0} ha deshabilitado la suscripción.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = "un administrador de espacio empresarial" o "un administrador de servicio"</p></li></ul>|
|AF20030|Se debe especificar la hora de inicio y la hora de finalización (o bien omitirse), con una diferencia menor o igual de 24 horas, y la hora de inicio no debe tener más de siete días de antigüedad. |
|AF20031|Entrada nextPage no válida: {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = el indicador de página siguiente que se pasa en la dirección URL</p></li></ul>|
|AF20050|No existe el contenido especificado ({0}).<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = identificador o dirección URL del recurso</p></li></ul>|
|AF20051|El contenido solicitado con la clave {0} ya ha expirado. El contenido de más de siete días no se puede recuperar.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>•    {0} = identificador o dirección URL del recurso</p></li></ul>|
|AF20052|El identificador de contenido {0} en la dirección URL no es válido.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = identificador o dirección URL del recurso</p></li></ul>|
|AF20053|Solo puede haber un idioma en el encabezado Accept-Language.|
|AF20054|Sintaxis incorrecta en el encabezado Accept-Language.|
|AF429|Demasiadas solicitudes. Método={0}, PublisherId={1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = método HTTP</p></li><li><p>{1} = GUID de espacio empresarial usado como PublisherIdentifier</p></li></ul>|
|AF50000|Se ha producido un error interno. Vuelva a intentar realizar la solicitud.|
