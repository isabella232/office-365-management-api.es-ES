---
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Solución de problemas de la API de actividad de administración de Office 365
description: Resumen de las preguntas más frecuentes que recibe el soporte técnico de Microsoft sobre el uso de esta API.
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: f02088f557a10414539952c78542e09b2dc2d90b
ms.sourcegitcommit: 37737b849f1b2d0484e626002978b1d4ece2c742
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "35936232"
---
# <a name="troubleshooting-the-office-365-management-activity-api"></a>Solución de problemas de la API de actividad de administración de Office 365

La API de actividad de administración de Office 365 (también conocida como *API de auditoría unificada*) es solo una parte de las ofertas de seguridad y cumplimiento de Office 365, pero recibe mucha atención porque:

- Permite el acceso mediante programación a varias cargas de trabajo de canalización de auditoría (como SharePoint y Exchange).
- Es la principal interfaz usada por una amplia variedad de productos de proveedores de terceros para agregar e indexar datos de auditoría.

La API de actividad de administración no tiene que confundirse con la API de comunicaciones de servicio de Office 365. La API de actividad de administración se usa para auditar actividades de usuario final en las distintas cargas de trabajo.  La API de comunicaciones de servicio se usa para realizar auditorías de estado y mensajes enviadas por los servicios disponibles en Office 365 (como Dynamics CRM y el servicio de identidad).

A pesar de que tienen relativamente pocas operaciones y una interfaz de REST sencilla, hay una gran confusión en relación con el uso de la API de actividad de administración y los detalles de cómo se recupera exactamente los datos.  Es importante que todos los usuarios que empiecen a usar la API de actividad de administración conozcan que no existe el concepto de consultas por detalles de evento, como la fecha en que se produjo el evento, la colección de sitios que podría haber desencadenado un evento, o bien el tipo de evento.  En su lugar, se crean suscripciones a cargas de trabajo específicas (por ejemplo, SharePoint o Azure AD) y cada suscripción se corresponde con un espacio empresarial.

En este artículo, se proporciona un resumen de las preguntas más frecuentes que recibe el soporte técnico de Microsoft sobre el uso de esta API.  Le mostraremos una selección de scripts de PowerShell sencillos que pueden ayudarle a responder a las preguntas más frecuentes realizadas por los clientes o que pueden permitirle empezar a implementar una solución personalizada al mostrar una demostración de las operaciones principales.  En este artículo, no se explican todas las operaciones, pero encontrará la lista completa en la [Referencia de API de actividad de administración de Office 365](office-365-management-activity-api-reference.md).

## <a name="questions-about-third-party-tools-and-clients"></a>Preguntas sobre clientes y herramientas de terceros

La categoría de preguntas más común para la que ofrecemos soporte técnico actualmente proviene de clientes que usan productos de terceros para descargar y agregar datos de auditoría. Según el producto de terceros usado, los clientes pueden encontrar dificultades con la configuración o experimentar una interrupción o incoherencias en los datos expuestos en estos productos. Es importante conocer que la primera acción que necesitan realizar esos clientes es ponerse en contacto con la organización de soporte técnico de su proveedor. En todas las solicitudes de servicio atendidas por el soporte técnico, los ingenieros solo vieron un único caso en el que la causa se debía a un problema del servicio específico del espacio empresarial.

Pero puede que estos clientes aún tengan algunas preguntas sin respuesta. Es posible que los proveedores insistan en que se trata de un problema del servicio, o bien puede que quiera realizar alguna comprobación inicial antes de ponerse en contacto con su proveedor. 

## <a name="enabling-unified-audit-logging-in-office-365"></a>Habilitar el registro de auditoría unificado en Office 365

Si acaba de configurar una aplicación que está intentando usar la API de Actividad de administración y no funciona, asegúrese de que ha habilitado el registro de auditoría unificado para su organización de Office 365. Para ello, active el registro de auditoría de Office 365. Para obtener instrucciones, consulte [Activar o desactivar la búsqueda de registros de auditoría de Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).

Si la auditoría unificada no está habilitada, normalmente se producirá un error que contiene la siguiente cadena: `Microsoft.Office.Compliance.Audit.DataServiceException: Tenant <tenantID> does not exist.`

## <a name="connecting-to-the-api"></a>Conectarse a la API

La mayoría de las aplicaciones se conectan a la API con un flujo sencillo de OAuth2 de credenciales de cliente. Por lo tanto, el primer paso es crear una aplicación de Azure AD que tenga los permisos necesarios para obtener acceso a los datos de la API de actividad de administración. La explicación de los pasos para crear un registro de aplicación de Azure AD está fuera del ámbito de este artículo. Para obtener más información, vea [Registrar la aplicación con el espacio empresarial de Azure Active Directory](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-integrating-applications).

### <a name="azure-application-permissions"></a>Permisos de aplicación de Azure

Los tres permisos usados actualmente para la API de actividad de administración de Office 365 son las siguientes:

1. Leer datos de actividad de la organización.
2. Leer información de estado del servicio de la organización.
3. Leer eventos de directiva de prevención de pérdida de datos (DLP), incluida información confidencial detectada. 

> [!NOTE] 
> Necesita habilitar los permisos de aplicación y los permisos delegados como mínimo para los primeros dos conjuntos de permisos anteriores. Leer eventos de directiva DLP solo será necesario si está interesado en las cargas de trabajo de DLP.

### <a name="getting-an-access-token"></a>Obtener un token de acceso

El siguiente script de PowerShell usa el id. de aplicación y el secreto de cliente para obtener el token de OAuth2 desde el punto de conexión de autenticación de la API de actividad de administración. Después, coloca el token de acceso en la variable de matriz `$headerParams`, que se adjuntará a la solicitud HTTP: 

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://manage.office.com"
# auth
$body = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
$headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"} 
```

La variable `$oauth` contendrá el objeto response, que tiene varias propiedades, incluido el token de acceso. Un ejemplo de respuesta es:

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

## <a name="checking-your-subscriptions"></a>Comprobar las suscripciones

Si ha experimentado una interrupción del flujo de datos a un cliente o una solución de la API de actividad de administración existente, puede que se pregunte si hubo algún problema con la suscripción. Para comprobar las suscripciones activas, agregue lo siguiente al script anterior:

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a>Respuesta de ejemplo 

```json
StatusCode        : 200
Status Description : OK
Content           : [{"contentType":"Audit.Exchange","status":"enabled","webhook":null},{"contentType":"Audit.SharePoint","status":"enabled","webhook":{"authId":"","address":"https://mvcwebapiwebhookreceiver.azurewebsite...
RawContent        : HTTP/1.1 200 OK
                    Pragma: no-cache
                    Content-Length: 266
                    Cache-Control: no-cache
                    Content-Type: application/json; charset=utf-8
                    Expires: -1
                    Server: Microsoft-IIS/8.5,Microsoft-IIS/8.5
                    X-AspNet-Versi...
Forms             : {}
Headers           : {[Pragma, no-cache], [Content-Length, 266], [Cache-Control, no-cache], [Content-Type, application/json; charset=utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 266
```

Esto indica que el espacio empresarial tiene habilitadas las suscripciones Audit.Exchange y Audit.SharePoint. La suscripción de Exchange no tiene habilitado ningún webhook (nulo) y la suscripción de SharePoint tiene habilitado un webhook, donde se muestra la dirección del punto de conexión registrado.

## <a name="creating-a-new-subscription"></a>Crear una suscripción

Para crear una suscripción, use la operación /start:

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"
```

> [!NOTE] 
> Recuerde que se rellenó `$headerParams` en la primera parte del script de la sección [Conectarse a la API](#connecting-to-the-api) de este artículo.

El código anterior creará una suscripción al tipo de contenido Audit.AzureActiveDirectory, con un webhook nulo. Después, puede comprobar la suscripciones con el código que se incluye en la sección [Comprobar la suscripciones de este artículo](#checking-your-subscriptions).

## <a name="checking-content-availability"></a>Comprobar la disponibilidad del contenido

Para comprobar los blobs de contenido que se crearon durante un período específico, puede agregar la línea siguiente al script en la sección “Conectarse al API”:

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

En el ejemplo anterior, se obtienen todas las notificaciones de contenido disponibles el día actual (es decir, desde las 00:00 UTC hasta la hora actual). Para especificar otro período de tiempo (teniendo en cuenta que el período de tiempo máximo para el que pueden realizarse consultas es de 24 horas), agregue los parámetros *starttime* y *endtime* al URI; por ejemplo:

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE] 
> Necesita usar ambos parámetros (*starttime* y *endtime*) o ninguno.

La solicitud anterior devolverá un objeto JSON con una colección de notificaciones que estuvieron disponibles durante el período de tiempo especificado. La respuesta será similar a esta:

```json
[{      "contentUri" : "https://manage.office.com/api/v1.0/<<your_tenant_guid>>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT] 
> - La propiedad *contentUri* es el URI desde el que se puede recuperar el blob de contenido. El blob en sí es lo que contiene los detalles del evento; contendrá detalles sobre 1-N eventos. Aunque puede haber 30 objetos JSON en la colección, es posible que haya muchos más eventos detallados en esos 30 URI de contenido.
> - La propiedad *contentCreated* no es la fecha en que se creó el evento de la notificación. Se trata de la fecha en que se creó la notificación. Los eventos indicados en el blob puede que se crearan antes que el blob de contenido. Por lo tanto, no se pueden realizar consultas a la API directamente para eventos que se produjeron en un período específico.

### <a name="paging-contents-for-busy-tenants"></a>Paginación de contenidos para espacios empresariales con carga elevada

Un gran número de espacios empresariales de Office 365 tienen miles de eventos que se generan cada hora. Si es el caso de su organización e intenta ejecutar una consulta en un período de 24 horas, como en el ejemplo anterior, puede que necesite recuperar más notificaciones de las que se devuelven en una respuesta. En ese caso, tendrá que implementar un bucle lógico de algún tipo que compruebe los encabezados de respuesta cada vez para el valor del encabezado **NextPageUrl:**. Para obtener más información, vea la sección [Paginación](office-365-management-activity-api-reference.md#pagination) en la referencia de API de actividad de administración de Office 365. 

La lógica para este bucle será parecida a lo siguiente:

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

Puede que resulte difícil probar este código en bucle, a no ser que tenga un espacio empresarial muy activo. En nuestras pruebas, intentamos ejecutar varios miles de operaciones de actualización en un script y no pudimos generar un número de notificaciones lo suficientemente grande para poder enviar el encabezado **NextPageUrl**.

## <a name="using-webhooks"></a>Uso de webhooks

Hay dos formas de obtener una notificación que indique que se crearon blobs de contenido. El método de *inserción* se implementa con un punto de conexión de webhook, que es una aplicación web creada y hospedada por su cuenta o en una plataforma en la nube. El webhook se registra en el momento de crear una suscripción a un tipo de contenido auditado. También puede agregar un registro de webhook a una suscripción existente con el método siguiente. Para usar el método de *inserción*, es necesario realizar una consulta en un intervalo de tiempo específico (no superior a 24 horas) con la [operación /content](office-365-management-activity-api-reference.md#list-available-content). La respuesta indicará los blobs de contenido que se crearon durante el período especificado.

Antes de agregar un webhook, tenga en cuenta los siguientes dos problemas:

1. Microsoft desaconseja el uso de webhooks debido a la dificultad de realizar operaciones de depuración y solución de problemas. Normalmente, hospedaría un punto de conexión de WebApi que responda a solicitudes entrantes. Muchos clientes usan entornos de hospedaje (sobre el que no tienen control total) o entornos locales (que tienen dificultades para permitir las solicitudes HTTP entrantes). El soporte técnico ha identificado muchos problemas en los que las solicitudes entrantes desde la canalización de auditoría de Office 365 se bloquearon por un firewall o enrutador. En este caso, la API implementará un algoritmo de retroceso, que puede resultar confuso y podría deshabilitar el webhook en la suscripción.

2. El webhook necesita estar preparado para responder de inmediato a una solicitud de validación después de ejecutar la operación de inicio. Si hay un error de código en la aplicación del webhook, la validación producirá errores y no se habilitará el webhook. Para obtener información sobre el esquema de solicitud de validación, vea la sección [Validación de webhook](office-365-management-activity-api-reference.md#webhook-validation) en la referencia de API de actividad de administración de Office 365. Es muy recomendable que tenga en cuenta las dificultades de producir un webhook preparado para entornos de producción con el fin de responder a notificaciones de la API de actividad de administración.

Si decide implementar un webhook, es necesario probarlo para verificar que el punto de conexión esté preparado para proporcionar una respuesta HTTP 200 (tanto para la solicitud de validación como para las solicitudes de notificación normales) antes de llamar por primera vez a cualquier operación /start que especifique un punto de conexión de webhook. Normalmente, usaría una solicitud ficticia desde la API para probar esta disponibilidad. Vea detenidamente las secciones [Validación de webhook](office-365-management-activity-api-reference.md#webhook-validation) y [Recuperación de contenido](office-365-management-activity-api-reference.md#retrieving-content) en la referencia de API de actividad de administración de Office 365 para comprender el esquema de estos dos tipos de solicitudes.

Para agregar una suscripción con un punto de conexión de webhook, agregue un parámetro de cuerpo en la solicitud POST al punto de conexión /start; por ejemplo:

```json
$body = '{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }}'
$uri = "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed//subscriptions/start?contentType=Audit.SharePoint"
Invoke-RestMethod -Method Post -uri $uri -Headers $headerParams -Body $body
```

Inmediatamente después de esta llamada, se enviará una solicitud de validación a `https://webhook.myapp.com/o365/ …` y es necesario que haya un agente de escucha preparado para responder, según la descripción de la sección [Validación de webhook](office-365-management-activity-api-reference.md#webhook-validation) que encontrará en la referencia de API de actividad de administración de Office 365. El agente de escucha tiene que responder con HTTP 200. Si ejecuta inmediatamente la operación /list en este momento, no verá el webhook con valores distintos de nulo hasta que la validación devuelva un resultado correcto.

### <a name="checking-notifications-to-webhooks"></a>Comprobar notificaciones a webhooks

Es importante distinguir entre la operación /notifications y la operación /content. Comprobar las notificaciones solo es relevante si se suscribió a un punto de conexión de webhook. Esta operación le permitirá conocer si los intentos de envío de notificaciones al webhook se completaron correctamente o no. Esta operación no tiene que usarse para mostrar una lista del contenido disponible. Para realizar una comprobación cruzada de la disponibilidad del contenido en comparación con lo que recibió en el webhook, use la operación /content. Asegúrese de comprobar antes las notificaciones con errores mediante la [operación /notifications](office-365-management-activity-api-reference.md#list-notifications).

## <a name="requesting-content-blobs-and-throttling"></a>Solicitar blobs de contenido y limitación

Después de obtener una lista de URI de contenido, necesita solicitar los blobs especificados por los URI. Este es un ejemplo de cómo solicitar un blob de contenido con PowerShell. En este ejemplo, se da por hecho que ya usó un ejemplo anterior en la sección [Obtener un token de acceso](#getting-an-access-token) de este artículo para obtener un token de acceso y que lo rellenó con la variable `$headerParams` correspondiente.

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

Tenga en cuenta los siguientes aspectos sobre la variable *$uri* del ejemplo anterior:

- Usamos comillas simples para que los símbolos *$* no se interpreten como variables en PowerShell.
- Todo el URI se devolverá en la propiedad *contentUri* de la respuesta a la llamada anterior al punto de conexión /content. Los tokens de marcador de posición solo se muestran con fines ilustrativos.

Al intentar recuperar los blobs de contenido disponibles, un gran número de clientes (en su mayoría, con espacios empresariales con una gran cantidad de contenido) experimentaron errores similares a estos:

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

Es probable que esto se deba a la limitación. Tenga en cuenta que es probable que el valor del parámetro PublisherId indique que el cliente no especificó el valor *PublisherIdentifier* en la solicitud. Además, tenga en cuenta que el nombre de parámetro correcto es *PublisherIdentifier*, incluso aunque vea *PublisherId* en las respuestas de error 403.

> [!NOTE] 
> En la referencia de API, el parámetro *PublisherIdentifier* se muestra en todas las operaciones de la API, pero también tiene que incluirse en la solicitud GET a la URL de contentUri al recuperar el blob de contenido.

Si realiza llamadas API sencillas para la solución de problemas (por ejemplo, para comprobar si una suscripción específica está activa), puede omitir de forma segura el parámetro *PublisherIdentifier*, pero todo el código para entornos de producción tiene que contener el parámetro *PublisherIdentifier* en todas las llamadas.

Si implementa un cliente para el espacio empresarial de la empresa, *PublisherIdentifier* es el GUID de espacio empresarial. Si crea un complemento o aplicación de ISV para varios clientes, el elemento *PublisherIdentifier* tiene que ser el GUID del espacio empresarial del ISV, y no el GUID del espacio empresarial de la compañía del usuario final.

Si incluye el elemento *PublisherIdentifier* válido, estará en un grupo que tiene permiso para realizar 60 000 solicitudes por minuto por espacio empresarial. Este es un número de solicitudes excepcionalmente elevado. Pero, si no incluye el parámetro *PublisherIdentifier*, estará en el grupo general con permiso para realizar 60 000 solicitudes por minuto para todos los espacios empresariales. En este caso, es más que probable que se produzcan limitaciones en las llamadas. Para evitar esto, siga este procedimiento para solicitar un blob de contenido con el elemento *PublisherIdentifier*:

```powershell
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

En el ejemplo anterior, se da por hecho que la variable *$response* se rellenó con la respuesta a una solicitud al punto de conexión /content y que en la variable *$headerParams* se incluye un token de acceso válido. El script obtiene el primer elemento de la matriz de los URI de contenido de la respuesta y, después, invoca una llamada GET para descargar ese blob y colocarlo en la variable *$contents*. Es probable que el código recorra en bucle la colección contentUri y que emita la llamada GET por cada elemento *contentUri*.

## <a name="frequently-asked-questions-about-the-office-365-management-api"></a>Preguntas más frecuentes sobre la API de administración de Office 365

#### <a name="what-is-the-maximum-time-i-will-have-to-wait-before-a-notification-is-sent-about-a-given-office-365-event"></a>¿Cuál es el máximo de tiempo que tendré que esperar antes de que se envíe una notificación sobre un evento específico de Office 365?

No hay ninguna latencia máxima garantizada para la entrega de notificaciones (es decir, no existe un contrato de nivel de servicio). Según la experiencia del soporte técnico de Microsoft, la mayoría de las notificaciones se enviaron en un plazo de una hora del evento. Con frecuencia, la latencia es mucho más breve, pero también puede ser más larga. Esto varía según la carga de trabajo; pero, como norma general, la mayoría de las notificaciones se entregarán en un plazo de 24 horas desde que se produjo el evento original.

#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-are-event-driven"></a>¿No son más inmediatas las notificaciones de webhook? Después de todo, ¿no están controladas por eventos?

No. Las notificaciones de webhook no están controladas por eventos en el sentido de que el evento desencadena la notificación. Sigue siendo necesario crear el blob de contenido, y la creación del valor de contenido es lo que desencadena la entrega de notificaciones. Recientemente, se produjeron tiempos de espera más largos para las notificaciones al usar un webhook, en comparación con las consultas a la API realizadas directamente con la operación /content. Por lo tanto, la API de actividad de administración no tiene que considerarse un sistema de alertas de seguridad en tiempo real. Microsoft ofrece otros productos para eso. En relación con la seguridad, las notificaciones de eventos de la API de actividad de administración pueden ser más apropiadas cuando se usan para determinar patrones de uso en períodos prolongados. 

#### <a name="can-i-query-the-management-activity-api-for-a-particular-event-id-or-recordtype-or-other-properties-in-the-content-blob"></a>¿Puedo realizar consultas a la API de actividad de administración para un id. de evento o elemento RecordType específicos, o bien otras propiedades del blob de contenido?

No. No piense que los datos disponibles mediante la API de actividad de administración se “registran” en el sentido tradicional. En su lugar, piense en esto como un volcado de los detalles del evento. Tiene que decidir si quiere recopilar todos los detalles de los eventos, almacenarlos e indexarlos localmente y, después, implementar su propia lógica de consulta con una aplicación personalizada o una herramienta de terceros.

#### <a name="how-do-i-know-the-data-coming-from-my-existing-auditing-solution-which-collects-data-from-the-management-activity-api-is-accurate-and-complete"></a>¿Cómo sé que los datos que provienen de mi solución de auditoría existente, que recopila datos de la API de actividad de administración, son precisos y completos?

La respuesta breve es que Microsoft no ofrece ningún tipo de registro que le permita realizar una comprobación cruzada de una aplicación específica o una aplicación de terceros (ISV). Hay otros productos de seguridad de Microsoft que obtienen sus datos de la misma canalización, pero esos productos se encuentran fuera del ámbito de esta explicación y no pueden usarse para realizar una comprobación cruzada directamente de la API de actividad de administración. Si quiere conocer las posibles discrepancias entre los datos que proporciona su solución existente y los datos esperados, le recomendamos que implemente las operaciones indicadas anteriormente. Pero esto puede resultar difícil, según la forma en que la herramienta o solución existente muestre una lista de los datos y los indexe. Si la solución existente solo presenta datos ordenados por la hora de creación del evento en sí, no existe ninguna forma de consultar la API mediante la hora de creación del evento para que pueda comparar los conjuntos de resultados. En este escenario, tendrá que recopilar los blobs de contenido notificados durante varios días, indexarlos u ordenarlos de forma manual y, después, realizar una comparación aproximada.

#### <a name="how-long-will-the-content-blobs-remain-available"></a>¿Durante cuánto tiempo estarán disponibles los blobs de contenido?

Los blobs de contenido están disponibles durante siete días después de la disponibilidad de la notificación del bloque de contenido. Esto quiere decir que, si se produce un retraso significativo en la creación del blob de contenido, dispondrá de más tiempo (el retraso más siete días) después de la fecha de creación del evento real antes de que el valor de contenido deje de estar disponible.

#### <a name="if-there-is-a-24-hour-delay-in-getting-a-notification-doesnt-that-mean-i-will-have-only-6-days-to-retrieve-the-content-blob"></a>Si se produce un retraso de 24 horas al obtener una notificación, ¿no quiere decir que solo dispondré de seis días para recuperar el blob de contenido?

No. Incluso si la notificación se retrasa durante un período inusualmente largo (por ejemplo, en el caso de una interrupción del servicio), seguiría disponiendo de siete días después de la primera disponibilidad de la notificación para descargar el blob de contenido relacionado con el evento original.












