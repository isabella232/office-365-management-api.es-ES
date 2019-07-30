---
ms.TocTitle: Office 365 Management Activity API reference
title: Referencia de la API de Actividad de administración de Office 365
description: Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: d6cdef5f0445ef0fa551be3080d4ce28595a1e9f
ms.sourcegitcommit: 784b581a699c6d0ab7939ea621d5ecbea71925ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2019
ms.locfileid: "35924829"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="545f9-103">Referencia de la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="545f9-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="545f9-104">Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="545f9-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="545f9-105">Puede usar acciones y eventos de los registros de auditoría y actividad de Office 365 y Microsoft Azure Active Directory para crear soluciones que proporcionen supervisión, análisis y visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="545f9-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="545f9-106">Estas soluciones ofrecen a las organizaciones mayor visibilidad de las acciones realizadas en el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="545f9-107">Estas acciones y eventos también están disponibles en los informes de actividad de Office 365.</span><span class="sxs-lookup"><span data-stu-id="545f9-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="545f9-108">Para obtener más información, vea [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](https://support.office.com/es-ES/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="545f9-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="545f9-109">La API de Actividad de administración de Office 365 es un servicio web REST que se puede usar para desarrollar soluciones mediante cualquier lenguaje y entorno de hospedaje que admita HTTPS y certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="545f9-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="545f9-110">La API se basa en Azure AD y el protocolo OAuth2 para la autorización y autenticación.</span><span class="sxs-lookup"><span data-stu-id="545f9-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="545f9-111">Para acceder a la API desde la aplicación, primero deberá registrarla en Azure AD y configurarla con los permisos apropiados.</span><span class="sxs-lookup"><span data-stu-id="545f9-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="545f9-112">Esto permitirá que la aplicación solicite los tokens de acceso OAuth2 que necesita para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="545f9-113">Para obtener más información, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="545f9-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="545f9-114">Para obtener información sobre los datos que devuelve la API de Actividad de administración de Office 365, vea [Esquema de la API de Actividad de administración de Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="545f9-114">For information about the schema of the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="545f9-115">Para poder acceder a los datos a través de la API de Actividad de administración de Office 365, debe activar el registro de auditoría unificado para su organización de Office 365.</span><span class="sxs-lookup"><span data-stu-id="545f9-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="545f9-116">Para ello, active el registro de auditoría de Office 365.</span><span class="sxs-lookup"><span data-stu-id="545f9-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="545f9-117">Para obtener instrucciones, consulte [Activar o desactivar la búsqueda de registros de auditoría de Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span><span class="sxs-lookup"><span data-stu-id="545f9-117">[Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="545f9-118">Trabajar con la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="545f9-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="545f9-119">La API de Actividad de administración de Office 365 agrega acciones y eventos en blobs de contenido específicos del espacio empresarial, que se clasifican según el tipo y el origen del contenido que contienen.</span><span class="sxs-lookup"><span data-stu-id="545f9-119">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="545f9-120">En la actualidad, se admiten estos tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="545f9-120">Currently, these content types are supported:</span></span>

- <span data-ttu-id="545f9-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="545f9-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="545f9-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="545f9-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="545f9-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="545f9-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="545f9-124">Audit.General (incluye todas las demás cargas de trabajo que no se incluyen en los tipos de contenido anteriores)</span><span class="sxs-lookup"><span data-stu-id="545f9-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="545f9-125">DLP.All (eventos exclusivos de DLP para todas las cargas de trabajo)</span><span class="sxs-lookup"><span data-stu-id="545f9-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="545f9-126">Para obtener más información sobre los eventos y las propiedades asociados a estos tipos de contenido, vea [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md) (Esquema de la API de Actividad de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="545f9-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="545f9-127">Para empezar a recuperar los blobs de contenido para un espacio empresarial, primero se crea una suscripción a los tipos de contenido deseados.</span><span class="sxs-lookup"><span data-stu-id="545f9-127">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="545f9-128">Si se van a recuperar blobs de contenido para varios espacios empresariales, cree varias suscripciones a todos los tipos de contenido deseados, una para cada espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="545f9-128">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="545f9-129">Después de crear una suscripción, puede sondear periódicamente para detectar nuevos blobs de contenido disponibles para descargar, o bien puede registrar un punto de conexión de webhook con la suscripción y se enviarán notificaciones a este punto de conexión cuando haya nuevos blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="545f9-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="545f9-130">Cuando se crea una suscripción, pueden pasar hasta 12 horas hasta que los primeros blobs de contenido estén disponibles para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="545f9-131">Para crear los blobs de contenido, se recopilan y agregan acciones y eventos de varios servidores y centros de datos.</span><span class="sxs-lookup"><span data-stu-id="545f9-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="545f9-132">Como resultado de este proceso distribuido, las acciones y los eventos incluidos en los blobs de contenido no aparecerán necesariamente en el orden en que se producen.</span><span class="sxs-lookup"><span data-stu-id="545f9-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="545f9-133">Un blob de contenido puede contener acciones y eventos que tuvieron lugar antes de las acciones y los eventos incluidos en un blob de contenido anterior.</span><span class="sxs-lookup"><span data-stu-id="545f9-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="545f9-134">Estamos trabajando para reducir la latencia entre la aparición de los eventos y las acciones, y su disponibilidad en un blob de contenido, pero no podemos garantizar que aparezcan de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="545f9-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="545f9-135">Los datos confidenciales de DLP solo están disponibles en la API de fuente de actividades para los usuarios a los que se les han concedido permisos "Leer datos confidenciales de DLP".</span><span class="sxs-lookup"><span data-stu-id="545f9-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="545f9-136">Para obtener más información sobre la prevención de pérdida de datos (DLP), vea [Información general sobre directivas de prevención de pérdida de datos](https://support.office.com/es-ES/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="545f9-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/en-us/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="545f9-137">Operaciones de la API de Actividad</span><span class="sxs-lookup"><span data-stu-id="545f9-137">Activity API operations</span></span>

<span data-ttu-id="545f9-138">Todas las operaciones de API están orientadas a un único espacio empresarial y la dirección URL raíz de la API incluye un identificador de espacio empresarial que especifica el contexto del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="545f9-138">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="545f9-139">El identificador de espacio empresarial es un GUID.</span><span class="sxs-lookup"><span data-stu-id="545f9-139">The tenant ID is a GUID.</span></span> <span data-ttu-id="545f9-140">Para obtener información sobre cómo conseguir el GUID, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="545f9-140">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="545f9-141">Como las notificaciones que se envían al webhook incluyen el **identificador de espacio empresarial**, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales.</span><span class="sxs-lookup"><span data-stu-id="545f9-141">Because the notifications we send to your webhook include the **tenant ID**, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="545f9-142">Todas las operaciones de API requieren un encabezado de autorización HTTP con un token de acceso obtenido de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="545f9-142">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="545f9-143">El identificador de espacio empresarial en el token de acceso debe coincidir con el de la dirección URL raíz de la API y el token de acceso debe contener la notificación ActivityFeed.Read (que se corresponde con el permiso [Leer datos de actividad de la organización] que ha configurado para la aplicación en Azure AD).</span><span class="sxs-lookup"><span data-stu-id="545f9-143">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="545f9-144">La API de Actividad admite las operaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="545f9-144">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="545f9-145">**Iniciar una suscripción** para empezar a recibir notificaciones y recuperar datos de actividad de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="545f9-145">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="545f9-146">**Detener una suscripción** para dejar de recuperar datos de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="545f9-146">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="545f9-147">**Enumerar las suscripciones actuales**</span><span class="sxs-lookup"><span data-stu-id="545f9-147">**List current subscriptions**</span></span>
    
- <span data-ttu-id="545f9-148">**Enumerar el contenido disponible** y las direcciones URL de contenido correspondientes.</span><span class="sxs-lookup"><span data-stu-id="545f9-148">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="545f9-149">**Recibir notificaciones** enviadas por un webhook cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-149">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="545f9-150">**Recuperar contenido** mediante la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-150">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="545f9-151">**Enumerar las notificaciones** enviadas por un webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-151">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="545f9-152">**Recuperar los nombres descriptivos de recurso** de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="545f9-152">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="545f9-153">Iniciar una suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-153">Start a subscription</span></span>

<span data-ttu-id="545f9-154">Esta operación inicia una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-154">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="545f9-155">Si ya existe una suscripción para el tipo de contenido específico, esta operación se usa para:</span><span class="sxs-lookup"><span data-stu-id="545f9-155">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="545f9-156">Actualizar las propiedades de un webhook activo.</span><span class="sxs-lookup"><span data-stu-id="545f9-156">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="545f9-157">Habilitar un webhook que estaba deshabilitado debido a un exceso de notificaciones con error.</span><span class="sxs-lookup"><span data-stu-id="545f9-157">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="545f9-158">Volver a habilitar un webhook expirado mediante la especificación de una fecha de expiración nula o posterior.</span><span class="sxs-lookup"><span data-stu-id="545f9-158">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="545f9-159">Quitar un webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-159">Remove a webhook.</span></span>
    
||<span data-ttu-id="545f9-160">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-160">Subscription</span></span>|<span data-ttu-id="545f9-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-161">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-162">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-162">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="545f9-163">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-163">**Parameters**</span></span>|<span data-ttu-id="545f9-164">contentType</span><span class="sxs-lookup"><span data-stu-id="545f9-164">contentType</span></span>|<span data-ttu-id="545f9-165">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-165">Must be a valid content type.</span></span>|
||<span data-ttu-id="545f9-166">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-166">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-167">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-167">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-168">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-168">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-169">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-169">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-170">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-170">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-171">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-171">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="545f9-172">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="545f9-172">**Body**</span></span>|<span data-ttu-id="545f9-173">webhook</span><span class="sxs-lookup"><span data-stu-id="545f9-173">webhook</span></span>|<span data-ttu-id="545f9-174">Objeto JSON opcional con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="545f9-174">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-175"><b>address</b>: punto de conexión HTTPS requerido que puede recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-175"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="545f9-176">Se enviará un mensaje de prueba al webhook para validarlo antes de crear la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-176">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="545f9-177"><b>authId</b>: cadena opcional que se incluirá como el encabezado WebHook-AuthID de las notificaciones que se envían al webhook como medio para identificar y autorizar el origen de la solicitud al webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-177"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="545f9-178"><b>expiration</b>: valor de fecha y hora opcional que indica una fecha y hora después de la que no se deben enviar más notificaciones al webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-178"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="545f9-179">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-179">**Response**</span></span>|<span data-ttu-id="545f9-180">contentType</span><span class="sxs-lookup"><span data-stu-id="545f9-180">contentType</span></span>|<span data-ttu-id="545f9-181">El tipo de contenido especificado en la llamada.</span><span class="sxs-lookup"><span data-stu-id="545f9-181">The content type specified in the call.</span></span>|
||<span data-ttu-id="545f9-182">status</span><span class="sxs-lookup"><span data-stu-id="545f9-182">status</span></span>|<span data-ttu-id="545f9-183">El estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-183">The status of the subscription.</span></span> <span data-ttu-id="545f9-184">Si una suscripción está deshabilitada, no podrá enumerar o recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-184">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="545f9-185">webhook</span><span class="sxs-lookup"><span data-stu-id="545f9-185">webhook</span></span>|<span data-ttu-id="545f9-186">Las propiedades del webhook especificado en la llamada junto con el estado del webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-186">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="545f9-187">Si el webhook está deshabilitado, no recibirá notificaciones, pero todavía podrá enumerar y recuperar el contenido, siempre que la suscripción esté habilitada.</span><span class="sxs-lookup"><span data-stu-id="545f9-187">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="545f9-188">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-188">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="545f9-189">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-189">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="545f9-190">Validación del webhook</span><span class="sxs-lookup"><span data-stu-id="545f9-190">Webhook validation</span></span>

<span data-ttu-id="545f9-191">Cuando se llama a la operación /start y se especifica un webhook, le enviaremos una notificación de validación a la dirección de webhook especificada para validar que una escucha activa puede aceptar y procesar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-191">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="545f9-192">Si no recibimos una respuesta HTTP 200 Correcto, no se creará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-192">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="545f9-193">O bien, si se empieza a llamar a /start para agregar un webhook a una suscripción existente y no se recibe una respuesta de HTTP 200 Correcto, el webhook no se agregará y no se cambiará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-193">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="545f9-194">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-194">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="545f9-195">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-195">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="545f9-196">Detener una suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-196">Stop a subscription</span></span>

<span data-ttu-id="545f9-197">Esta operación detiene una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-197">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="545f9-198">Cuando se detiene una suscripción, ya no recibirá notificaciones y no podrá recuperar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-198">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="545f9-199">Si más adelante se reinicia la suscripción, tendrá acceso al contenido nuevo a partir de ese punto.</span><span class="sxs-lookup"><span data-stu-id="545f9-199">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="545f9-200">No podrá recuperar el contenido que estaba disponible entre el momento de detener la suscripción y reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="545f9-200">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="545f9-201">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-201">Subscription</span></span>|<span data-ttu-id="545f9-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-202">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-203">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-203">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="545f9-204">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-204">**Parameters**</span></span>|<span data-ttu-id="545f9-205">contentType</span><span class="sxs-lookup"><span data-stu-id="545f9-205">contentType</span></span>|<span data-ttu-id="545f9-206">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-206">Must be a valid content type.</span></span>|
||<span data-ttu-id="545f9-207">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-207">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-208">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-208">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-209">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-209">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-210">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-210">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-211">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-211">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-212">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-212">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="545f9-213">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="545f9-213">**Body**</span></span>|<span data-ttu-id="545f9-214">(vacío)</span><span class="sxs-lookup"><span data-stu-id="545f9-214">(empty)</span></span>||
|<span data-ttu-id="545f9-215">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-215">**Response**</span></span>|<span data-ttu-id="545f9-216">(vacío)</span><span class="sxs-lookup"><span data-stu-id="545f9-216">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="545f9-217">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-217">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="545f9-218">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-218">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="545f9-219">Enumerar las suscripciones actuales</span><span class="sxs-lookup"><span data-stu-id="545f9-219">List current subscriptions</span></span>

<span data-ttu-id="545f9-220">Esta operación devuelve una colección de las suscripciones actuales junto con los webhooks asociados.</span><span class="sxs-lookup"><span data-stu-id="545f9-220">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="545f9-221">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-221">Subscription</span></span>|<span data-ttu-id="545f9-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-222">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-223">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-223">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="545f9-224">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-224">**Parameters**</span></span>|<span data-ttu-id="545f9-225">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-225">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-226">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-226">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-227">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-227">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-228">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-228">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-229">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-229">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-230">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-230">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="545f9-231">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="545f9-231">**Body**</span></span>|<span data-ttu-id="545f9-232">(vacío)</span><span class="sxs-lookup"><span data-stu-id="545f9-232">(empty)</span></span>||
|<span data-ttu-id="545f9-233">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-233">**Response**</span></span>|<span data-ttu-id="545f9-234">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="545f9-234">JSON array</span></span>|<span data-ttu-id="545f9-235">Cada suscripción se representará mediante un objeto JSON con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="545f9-235">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-236"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-236"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="545f9-237"><b>status</b>: indica el estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-237"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="545f9-238"><b>webhook</b>: indica el webhook configurado, junto con el estado (habilitado, deshabilitado, expirado) del webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-238"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="545f9-239">Si una suscripción no tiene un webhook, la propiedad webhook estará presente pero con un valor NULL.</span><span class="sxs-lookup"><span data-stu-id="545f9-239">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="545f9-240">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-240">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="545f9-241">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-241">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="545f9-242">Enumerar el contenido disponible</span><span class="sxs-lookup"><span data-stu-id="545f9-242">List available content</span></span>

<span data-ttu-id="545f9-243">Esta operación enumera el contenido disponible actualmente que se puede recuperar para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-243">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="545f9-244">El contenido es una agregación de acciones y eventos recopilados de varios servidores en varios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="545f9-244">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="545f9-245">El contenido se mostrará en el orden en que estén disponibles las agregaciones, pero no se garantiza que los eventos y las acciones de las agregaciones sean secuenciales.</span><span class="sxs-lookup"><span data-stu-id="545f9-245">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="545f9-246">Se devuelve un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="545f9-246">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="545f9-247">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-247">Subscription</span></span>|<span data-ttu-id="545f9-248">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-248">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-249">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-249">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="545f9-250">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-250">**Parameters**</span></span>|<span data-ttu-id="545f9-251">contentType</span><span class="sxs-lookup"><span data-stu-id="545f9-251">contentType</span></span>|<span data-ttu-id="545f9-252">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-252">Must be a valid content type.</span></span>|
||<span data-ttu-id="545f9-253">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-253">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-254">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-254">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-255">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-255">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-256">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-256">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-257">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-257">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-258">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-258">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="545f9-259">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="545f9-259">startTime endTime</span></span>|<span data-ttu-id="545f9-260">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-260">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="545f9-261">El intervalo de tiempo es inclusivo con respecto a startTime (startTime <= contentCreated) y exclusivo con respecto a endTime (contentCreated < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-261">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-262">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="545f9-262">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="545f9-263">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="545f9-263">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="545f9-264">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="545f9-264">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="545f9-265">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="545f9-265">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="545f9-266">De forma predeterminada, si se omiten startTime y endTime, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="545f9-266">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="545f9-267">**NOTA**: Aunque se puede especificar un valor de startTime y endTime con más de 24 horas de diferencia, no es recomendable.</span><span class="sxs-lookup"><span data-stu-id="545f9-267">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="545f9-268">Además, si obtiene algún resultado en respuesta a una solicitud de más de 24 horas, podrían ser resultados parciales y no deberían tenerse en cuenta.</span><span class="sxs-lookup"><span data-stu-id="545f9-268">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="545f9-269">La solicitud se debe emitir con un intervalo de no más de 24 horas entre los valores de startTime y endTime.</span><span class="sxs-lookup"><span data-stu-id="545f9-269">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="545f9-270">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-270">**Response**</span></span>|<span data-ttu-id="545f9-271">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="545f9-271">JSON array</span></span>|<span data-ttu-id="545f9-272">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="545f9-272">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-273"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-273"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="545f9-274"><b>contentId</b>: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="545f9-274"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="545f9-275"><b>contentUri</b>: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-275"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="545f9-276"><b>contentCreated</b>: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-276"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="545f9-277"><b>contentExpiration</b>: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="545f9-277"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="545f9-278">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-278">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="545f9-279">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-279">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="545f9-280">Paginación</span><span class="sxs-lookup"><span data-stu-id="545f9-280">Pagination</span></span>

<span data-ttu-id="545f9-281">Al enumerar el contenido disponible para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="545f9-281">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="545f9-282">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncarán y se agregará un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="545f9-282">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="545f9-283">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="545f9-283">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="545f9-284">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="545f9-284">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="545f9-285">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="545f9-285">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="545f9-286">Recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="545f9-286">Receiving notifications</span></span>

<span data-ttu-id="545f9-287">Las notificaciones se envían al webhook configurado para una suscripción cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-287">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="545f9-288">Como la notificación incluye el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales para los que tiene suscripciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-288">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="545f9-289">La notificación se realiza como HTTP POST sobre TLS (TLS 1.0 y versiones posteriores) a la dirección del webhook especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-289">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="545f9-290">Si la configuración de webhook incluye un identificador de autenticación, se enviará como un encabezado HTTP: Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="545f9-290">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="545f9-291">Cualquier respuesta distinta de HTTP 200 Correcto se considera un error y la notificación se volverá a intentar.</span><span class="sxs-lookup"><span data-stu-id="545f9-291">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="545f9-292">También puede configurar el webhook para requerir autenticación basada en certificados de cliente y se autenticará con el certificado manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="545f9-292">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="545f9-293">El cuerpo de la solicitud contendrá una matriz de uno o más objetos JSON que representan los blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="545f9-293">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="545f9-294">El número de blobs de contenido en cada notificación es limitado para que el tamaño de la notificación sea relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="545f9-294">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="545f9-295">Como este límite puede cambiar, la implementación debe consultar la longitud de la matriz en lugar de esperar un tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="545f9-295">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="545f9-296">Cada objeto incluirá las mismas propiedades que devuelve la operación /content, junto con el GUID del espacio empresarial al que corresponden los datos y el GUID de la aplicación que creó las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-296">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="545f9-297">Esto permite al webhook establecer el contexto cuando se usa con varios espacios empresariales y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-297">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="545f9-298">**tenantId**: el GUID del espacio empresarial al que pertenece el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-298">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="545f9-299">**clientId**: el GUID de la aplicación que creó la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-299">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="545f9-300">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-300">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="545f9-301">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="545f9-301">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="545f9-302">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-302">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="545f9-303">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-303">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="545f9-304">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="545f9-304">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="545f9-305">A continuación se muestra un ejemplo de una notificación.</span><span class="sxs-lookup"><span data-stu-id="545f9-305">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="545f9-306">Error de notificación y reintento</span><span class="sxs-lookup"><span data-stu-id="545f9-306">Notification failure and retry</span></span>

<span data-ttu-id="545f9-307">El sistema de notificaciones envía las notificaciones cuando hay nuevo contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-307">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="545f9-308">Si se producen errores excesivos al enviar las notificaciones, nuestro mecanismo de reintento aumentará de forma exponencial el tiempo entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="545f9-308">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="545f9-309">Si se siguen produciendo errores, nos reservamos el derecho de deshabilitar el webhook y detener por completo el envío de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="545f9-309">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="545f9-310">Se puede usar la operación /start para volver a habilitar un webhook deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="545f9-310">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="545f9-311">Recuperación de contenido</span><span class="sxs-lookup"><span data-stu-id="545f9-311">Retrieving content</span></span>

<span data-ttu-id="545f9-312">Para recuperar un blob de contenido, realice una solicitud GET en el URI del contenido correspondiente que se incluye en la lista de contenido disponible y en las notificaciones enviadas a un webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-312">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="545f9-313">El contenido devuelto será una colección de una más acciones o eventos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="545f9-313">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="545f9-314">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-314">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="545f9-315">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-315">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="545f9-316">Enumerar notificaciones</span><span class="sxs-lookup"><span data-stu-id="545f9-316">List notifications</span></span>

<span data-ttu-id="545f9-317">Esta operación enumera todos los intentos de notificación para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-317">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="545f9-318">Si no ha incluido un webhook al iniciar la suscripción para el tipo de contenido, no existirá ninguna notificación para recuperar.</span><span class="sxs-lookup"><span data-stu-id="545f9-318">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="545f9-319">Como en caso de error se reintentan las notificaciones, esta operación puede devolver varias notificaciones para el mismo contenido, y el orden en el que se envían no coincidirá necesariamente con el orden en que el contenido está disponible (en especial si hay errores y reintentos).</span><span class="sxs-lookup"><span data-stu-id="545f9-319">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="545f9-320">Puede usar esta operación para ayudar a investigar problemas relacionados con los webhooks y las notificaciones, pero no debería usarla para determinar qué contenido está disponible actualmente para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="545f9-320">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="545f9-321">En su lugar, use la operación /content.</span><span class="sxs-lookup"><span data-stu-id="545f9-321">Use the /content operation instead.</span></span> <span data-ttu-id="545f9-322">Se devolverá un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="545f9-322">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="545f9-323">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-323">Subscription</span></span>|<span data-ttu-id="545f9-324">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-324">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-325">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-325">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="545f9-326">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-326">**Parameters**</span></span>|<span data-ttu-id="545f9-327">contentType</span><span class="sxs-lookup"><span data-stu-id="545f9-327">contentType</span></span>|<span data-ttu-id="545f9-328">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-328">Must be a valid content type.</span></span>|
||<span data-ttu-id="545f9-329">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-329">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-330">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-330">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-331">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-331">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-332">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-332">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-333">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-333">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-334">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-334">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="545f9-335">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="545f9-335">startTime endTime</span></span>|<span data-ttu-id="545f9-336">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-336">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="545f9-337">El intervalo de tiempo es inclusivo con respecto a _startTime_ ( _startTime_ <= contentCreated) y exclusivo con respecto a _endTime_ (_contentCreated_ < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="545f9-337">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-338">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="545f9-338">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="545f9-339">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="545f9-339">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="545f9-340">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="545f9-340">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="545f9-341">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="545f9-341">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="545f9-342">De forma predeterminada, si se omiten _startTime_ y _endTime_, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="545f9-342">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="545f9-343">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-343">**Response**</span></span>|<span data-ttu-id="545f9-344">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="545f9-344">JSON array</span></span>|<span data-ttu-id="545f9-345">Las notificaciones disponibles se representarán mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="545f9-345">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="545f9-346">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-346">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="545f9-347">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="545f9-347">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="545f9-348">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-348">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="545f9-349">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="545f9-349">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="545f9-350">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="545f9-350">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="545f9-351">**notificationSent**: la fecha y hora de envío de la notificación.</span><span class="sxs-lookup"><span data-stu-id="545f9-351">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="545f9-352">**notificationStatus**: indica si intento de notificación se ha realizado correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="545f9-352">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="545f9-353">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-353">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="545f9-354">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-354">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="545f9-355">Paginación</span><span class="sxs-lookup"><span data-stu-id="545f9-355">Pagination</span></span>

<span data-ttu-id="545f9-356">Al enumerar el historial de notificaciones para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="545f9-356">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="545f9-357">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncan y se agrega un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="545f9-357">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="545f9-358">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="545f9-358">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="545f9-359">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="545f9-359">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="545f9-360">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUrl**.</span><span class="sxs-lookup"><span data-stu-id="545f9-360">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="545f9-361">Recuperar los nombres descriptivos de recurso</span><span class="sxs-lookup"><span data-stu-id="545f9-361">Retrieve resource friendly names</span></span>

<span data-ttu-id="545f9-362">Esta operación recupera los nombres descriptivos de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="545f9-362">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="545f9-363">En la actualidad, el único objeto que se admite es "DlpSensitiveType".</span><span class="sxs-lookup"><span data-stu-id="545f9-363">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="545f9-364">Suscripción</span><span class="sxs-lookup"><span data-stu-id="545f9-364">Subscription</span></span>|<span data-ttu-id="545f9-365">Descripción</span><span class="sxs-lookup"><span data-stu-id="545f9-365">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="545f9-366">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="545f9-366">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="545f9-367">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="545f9-367">**Parameters**</span></span>|<span data-ttu-id="545f9-368">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-368">PublisherIdentifier</span></span>|<span data-ttu-id="545f9-369">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="545f9-369">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="545f9-370">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="545f9-370">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="545f9-371">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-371">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="545f9-372">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="545f9-372">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="545f9-373">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-373">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="545f9-374">**Encabezados**</span><span class="sxs-lookup"><span data-stu-id="545f9-374">**Headers**</span></span>|<span data-ttu-id="545f9-375">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="545f9-375">Accept-Language</span></span>|<span data-ttu-id="545f9-376">Encabezado para especificar el idioma que prefiere para los nombres localizados.</span><span class="sxs-lookup"><span data-stu-id="545f9-376">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="545f9-377">Por ejemplo, use "en-US" para inglés o "es" para español.</span><span class="sxs-lookup"><span data-stu-id="545f9-377">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="545f9-378">Si este encabezado no existe, se devolverá el idioma predeterminado (en-US).</span><span class="sxs-lookup"><span data-stu-id="545f9-378">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="545f9-379">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="545f9-379">**Body**</span></span>|<span data-ttu-id="545f9-380">(vacío)</span><span class="sxs-lookup"><span data-stu-id="545f9-380">(empty)</span></span>||
|<span data-ttu-id="545f9-381">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="545f9-381">**Response**</span></span>|<span data-ttu-id="545f9-382">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="545f9-382">JSON array</span></span>|<span data-ttu-id="545f9-383">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="545f9-383">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-384"><b>id</b>: indica el GUID del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="545f9-384"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="545f9-385"><b>name</b>: el nombre descriptivo del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="545f9-385"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="545f9-386">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-386">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="545f9-387">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="545f9-387">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="545f9-388">Limitación de API</span><span class="sxs-lookup"><span data-stu-id="545f9-388">API throttling</span></span>

<span data-ttu-id="545f9-389">Cada proveedor que codifica la API tiene una cuota dedicada de limitación de solicitudes de 60 000 por minuto.</span><span class="sxs-lookup"><span data-stu-id="545f9-389">Each vendor coding against the API has a dedicated quota for request throttling at 60K per minute.</span></span> <span data-ttu-id="545f9-390">Para obtener la cuota dedicada, especifique el parámetro PublisherIdentifier en todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="545f9-390">To get the dedicated quota, specify the parameter PublisherIdentifier in all your requests.</span></span> <span data-ttu-id="545f9-391">Las solicitudes que tengan el mismo valor PublisherIdentifier compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="545f9-391">Requests with the same PublisherIdentifier will share the same quota.</span></span> <span data-ttu-id="545f9-392">Todas las solicitudes sin el valor PublisherIdentifier especificado compartirán la misma cuota como el GUID 00000000-0000-0000-0000-000000000000.</span><span class="sxs-lookup"><span data-stu-id="545f9-392">All requests without the PublisherIdentifier specified will share the same quota as GUID 00000000-0000-0000-0000-000000000000.</span></span>

<span data-ttu-id="545f9-393">Si Office 365 tiene que recurrir a usted para determinados problemas, asegúrese de que la suscripción para el espacio empresarial cuyo GUID se usa como valor PublisherIdentifier es actual y está actualizado con la información de contacto correcta.</span><span class="sxs-lookup"><span data-stu-id="545f9-393">If Office 365 needs to reverse escalate to you in certain issues, make sure the subscription for the tenant whose GUID is used as your PublisherIdentifier is current and updated with the correct contact information.</span></span> <span data-ttu-id="545f9-394">No hay requisitos de suscripción para este espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="545f9-394">There is no subscription requirement for this tenant.</span></span>

<span data-ttu-id="545f9-395">Para los clientes que desarrollan sus propias soluciones con esta API, se recomienda usar el GUID del propio espacio empresarial para evitar la competencia causada por una cuota compartida limitada.</span><span class="sxs-lookup"><span data-stu-id="545f9-395">For customers who are developing their own solutions using this API, we recommend using your own tenant GUID to avoid competition caused by a limited shared quota.</span></span>

> [!NOTE] 
> <span data-ttu-id="545f9-396">Aunque cada publicador puede enviar hasta 60 000 solicitudes por minuto, Microsoft no garantiza una velocidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="545f9-396">Even though each publisher can submit up to 60K requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="545f9-397">La velocidad de respuesta depende de varios factores, como el rendimiento del sistema cliente y la capacidad y la velocidad de la red.</span><span class="sxs-lookup"><span data-stu-id="545f9-397">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>  <span data-ttu-id="545f9-398">Un publicador puede enviar hasta 60 000 solicitudes por minuto, pero no debe esperar recibir respuestas para todas esas solicitudes en ese mismo minuto.</span><span class="sxs-lookup"><span data-stu-id="545f9-398">A publisher can submit up to 60K requests per minute, but should not expect to receive responses for all 60K requests within that same minute.</span></span> <span data-ttu-id="545f9-399">En cualquier caso, si un publicador quiere realizar pruebas de una aplicación cliente, debe hacerlo en todos los entornos en los que planee ejecutarla, ya que los resultados pueden variar de un entorno a otro.</span><span class="sxs-lookup"><span data-stu-id="545f9-399">If anything, should a publisher want to benchmark a client application, they should do so in each different environment that they are planning on running the client application in because results will vary from environment to environment.</span></span>

## <a name="errors"></a><span data-ttu-id="545f9-400">Errores</span><span class="sxs-lookup"><span data-stu-id="545f9-400">Errors</span></span>

<span data-ttu-id="545f9-401">Cuando el servicio encuentra un error, notificará el código de respuesta de error al autor de la llamada, mediante la sintaxis estándar de código de error de HTTP.</span><span class="sxs-lookup"><span data-stu-id="545f9-401">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="545f9-402">.</span><span class="sxs-lookup"><span data-stu-id="545f9-402"></span></span> <span data-ttu-id="545f9-403">En el cuerpo de la llamada con error se incluye información adicional como un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="545f9-403">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="545f9-404">A continuación se muestra un ejemplo de un cuerpo completo de error JSON:</span><span class="sxs-lookup"><span data-stu-id="545f9-404">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="545f9-405">Código</span><span class="sxs-lookup"><span data-stu-id="545f9-405">Code</span></span>|<span data-ttu-id="545f9-406">Mensaje</span><span class="sxs-lookup"><span data-stu-id="545f9-406">Message</span></span>|
|<span data-ttu-id="545f9-407">AF10001</span><span class="sxs-lookup"><span data-stu-id="545f9-407">AF10001</span></span>|<span data-ttu-id="545f9-408">El conjunto de permisos ({0}) enviados en la solicitud no incluía el permiso esperado **ActivityFeed.Read**.</span><span class="sxs-lookup"><span data-stu-id="545f9-408">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-409">{0} = el conjunto de permisos en el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="545f9-409">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="545f9-410">AF20001</span><span class="sxs-lookup"><span data-stu-id="545f9-410">AF20001</span></span>|<span data-ttu-id="545f9-411">Falta el parámetro: {0}.</span><span class="sxs-lookup"><span data-stu-id="545f9-411">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-412">{0} = el nombre del parámetro que falta.</span><span class="sxs-lookup"><span data-stu-id="545f9-412">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="545f9-413">AF20002</span><span class="sxs-lookup"><span data-stu-id="545f9-413">AF20002</span></span>|<span data-ttu-id="545f9-414">Tipo de parámetro no válido: {0}.</span><span class="sxs-lookup"><span data-stu-id="545f9-414">Invalid parameter type: {0}.</span></span> <span data-ttu-id="545f9-415">Tipo esperado: {1}</span><span class="sxs-lookup"><span data-stu-id="545f9-415">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-416">{0} = el nombre del parámetro no válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-416">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="545f9-417">{1} = el tipo esperado (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="545f9-417">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="545f9-418">AF20003</span><span class="sxs-lookup"><span data-stu-id="545f9-418">AF20003</span></span>|<span data-ttu-id="545f9-419">{0} de expiración proporcionada se establece en una fecha y hora pasadas.</span><span class="sxs-lookup"><span data-stu-id="545f9-419">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-420">{0} = la expiración que se pasa en la llamada de API.</span><span class="sxs-lookup"><span data-stu-id="545f9-420">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="545f9-421">AF20010</span><span class="sxs-lookup"><span data-stu-id="545f9-421">AF20010</span></span>|<span data-ttu-id="545f9-422">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no coincide con el que se pasa en el token de acceso ({1}).</span><span class="sxs-lookup"><span data-stu-id="545f9-422">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-423">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="545f9-423">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="545f9-424">{1} = el identificador de espacio empresarial que se pasa en el token de acceso</span><span class="sxs-lookup"><span data-stu-id="545f9-424">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="545f9-425">AF20011</span><span class="sxs-lookup"><span data-stu-id="545f9-425">AF20011</span></span>|<span data-ttu-id="545f9-426">El identificador de espacio empresarial ({0}) especificado no existe en el sistema o se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="545f9-426">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="545f9-427">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="545f9-427">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-428">AF20012</span><span class="sxs-lookup"><span data-stu-id="545f9-428">AF20012</span></span>|<span data-ttu-id="545f9-429">El identificador de espacio empresarial ({0}) especificado no está configurado correctamente en el sistema.</span><span class="sxs-lookup"><span data-stu-id="545f9-429">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="545f9-430">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="545f9-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-431">AF20013</span><span class="sxs-lookup"><span data-stu-id="545f9-431">AF20013</span></span>|<span data-ttu-id="545f9-432">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no es un GUID válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-432">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="545f9-433">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="545f9-433">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-434">AF20020</span><span class="sxs-lookup"><span data-stu-id="545f9-434">AF20020</span></span>|<span data-ttu-id="545f9-435">El tipo de contenido especificado no es válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-435">The specified content type is not valid.</span></span>|
|<span data-ttu-id="545f9-436">AF20021</span><span class="sxs-lookup"><span data-stu-id="545f9-436">AF20021</span></span>|<span data-ttu-id="545f9-437">El punto de conexión de webhook {{0}) no se pudo validar.</span><span class="sxs-lookup"><span data-stu-id="545f9-437">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="545f9-438">{1}</span><span class="sxs-lookup"><span data-stu-id="545f9-438"></span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-439">{0} = dirección del webhook.</span><span class="sxs-lookup"><span data-stu-id="545f9-439">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="545f9-440">{1} = "El punto de conexión no devolvió HTTP 200".</span><span class="sxs-lookup"><span data-stu-id="545f9-440">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="545f9-441">o bien, "La dirección debe comenzar con HTTPS".</span><span class="sxs-lookup"><span data-stu-id="545f9-441">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="545f9-442">AF20022</span><span class="sxs-lookup"><span data-stu-id="545f9-442">AF20022</span></span>|<span data-ttu-id="545f9-443">No se encontró ninguna suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="545f9-443">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="545f9-444">AF20023</span><span class="sxs-lookup"><span data-stu-id="545f9-444">AF20023</span></span>|<span data-ttu-id="545f9-445">{0} ha deshabilitado la suscripción.</span><span class="sxs-lookup"><span data-stu-id="545f9-445">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-446">{0} = "un administrador de espacio empresarial" o "un administrador de servicio"</span><span class="sxs-lookup"><span data-stu-id="545f9-446">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="545f9-447">AF20030</span><span class="sxs-lookup"><span data-stu-id="545f9-447">AF20030</span></span>|<span data-ttu-id="545f9-448">Se debe especificar la hora de inicio y la hora de finalización (o bien omitirse), con una diferencia menor o igual de 24 horas, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="545f9-448">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="545f9-449">AF20031</span><span class="sxs-lookup"><span data-stu-id="545f9-449">AF20031</span></span>|<span data-ttu-id="545f9-450">Entrada nextPage no válida: {0}.</span><span class="sxs-lookup"><span data-stu-id="545f9-450">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-451">{0} = el indicador de página siguiente que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="545f9-451">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-452">AF20050</span><span class="sxs-lookup"><span data-stu-id="545f9-452">AF20050</span></span>|<span data-ttu-id="545f9-453">No existe el contenido especificado ({0}).</span><span class="sxs-lookup"><span data-stu-id="545f9-453">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-454">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="545f9-454">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-455">AF20051</span><span class="sxs-lookup"><span data-stu-id="545f9-455">AF20051</span></span>|<span data-ttu-id="545f9-456">El contenido solicitado con la clave {0} ya ha expirado.</span><span class="sxs-lookup"><span data-stu-id="545f9-456">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="545f9-457">El contenido de más de siete días no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="545f9-457">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-458">•    {0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="545f9-458">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-459">AF20052</span><span class="sxs-lookup"><span data-stu-id="545f9-459">AF20052</span></span>|<span data-ttu-id="545f9-460">El identificador de contenido {0} en la dirección URL no es válido.</span><span class="sxs-lookup"><span data-stu-id="545f9-460">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-461">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="545f9-461">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="545f9-462">AF20053</span><span class="sxs-lookup"><span data-stu-id="545f9-462">AF20053</span></span>|<span data-ttu-id="545f9-463">Solo puede haber un idioma en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="545f9-463">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="545f9-464">AF20054</span><span class="sxs-lookup"><span data-stu-id="545f9-464">AF20054</span></span>|<span data-ttu-id="545f9-465">Sintaxis incorrecta en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="545f9-465">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="545f9-466">AF429</span><span class="sxs-lookup"><span data-stu-id="545f9-466">AF429</span></span>|<span data-ttu-id="545f9-467">Demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="545f9-467">Too many requests.</span></span> <span data-ttu-id="545f9-468">Método={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="545f9-468">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="545f9-469">{0} = método HTTP</span><span class="sxs-lookup"><span data-stu-id="545f9-469">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="545f9-470">{1} = GUID de espacio empresarial usado como PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="545f9-470">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="545f9-471">AF50000</span><span class="sxs-lookup"><span data-stu-id="545f9-471">AF50000</span></span>|<span data-ttu-id="545f9-472">Se ha producido un error interno.</span><span class="sxs-lookup"><span data-stu-id="545f9-472">An internal error occurred.</span></span> <span data-ttu-id="545f9-473">Vuelva a intentar realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="545f9-473">Retry the request.</span></span>|
