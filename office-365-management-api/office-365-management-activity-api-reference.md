---
ms.TocTitle: Office 365 Management Activity API reference
title: Referencia de la API de Actividad de administración de Office 365
description: Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: 76907cf9f22078a232cc20e65ba5fdc12c7f5d7e
ms.sourcegitcommit: 55264094d1ebc2f9968b2d29d5982b1ba4e29118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/04/2019
ms.locfileid: "29735232"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="76458-103">Referencia de la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="76458-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="76458-104">Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76458-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="76458-105">Puede usar acciones y eventos de los registros de auditoría y actividad de Office 365 y Microsoft Azure Active Directory para crear soluciones que proporcionen supervisión, análisis y visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="76458-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="76458-106">Estas soluciones ofrecen a las organizaciones mayor visibilidad de las acciones realizadas en el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="76458-107">Estas acciones y eventos también están disponibles en los informes de actividad de Office 365.</span><span class="sxs-lookup"><span data-stu-id="76458-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="76458-108">Para obtener más información, vea [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](https://support.office.com/es-ES/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="76458-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/es-ES/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="76458-109">La API de Actividad de administración de Office 365 es un servicio web REST que se puede usar para desarrollar soluciones mediante cualquier lenguaje y entorno de hospedaje que admita HTTPS y certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="76458-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="76458-110">La API se basa en Azure AD y el protocolo OAuth2 para la autorización y autenticación.</span><span class="sxs-lookup"><span data-stu-id="76458-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="76458-111">Para acceder a la API desde la aplicación, primero deberá registrarla en Azure AD y configurarla con los permisos apropiados.</span><span class="sxs-lookup"><span data-stu-id="76458-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="76458-112">Esto permitirá que la aplicación solicite los tokens de acceso OAuth2 que necesita para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="76458-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="76458-113">Para obtener más información, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="76458-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="76458-114">Para obtener información sobre el esquema de los datos que devuelve la API de Actividad de administración de Office 365, incluidos los problemas conocidos y los próximos cambios, que podrían afectar a la implementación, vea [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md) (Esquema de la API de Actividad de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="76458-114">For information about the schema of the data that the Office 365 Management Activity API returns, including known issues and upcoming changes, that might affect your implementation, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="76458-115">Trabajar con la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="76458-115">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="76458-116">La API de Actividad de administración de Office 365 agrega acciones y eventos en blobs de contenido específicos del espacio empresarial, que se clasifican según el tipo y el origen del contenido que contienen.</span><span class="sxs-lookup"><span data-stu-id="76458-116">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="76458-117">En la actualidad, se admiten estos tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="76458-117">Currently, these content types are supported:</span></span>

- <span data-ttu-id="76458-118">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="76458-118">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="76458-119">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="76458-119">Audit.Exchange</span></span>
    
- <span data-ttu-id="76458-120">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="76458-120">Audit.SharePoint</span></span>
    
- <span data-ttu-id="76458-121">Audit.General (incluye todas las demás cargas de trabajo que no se incluyen en los tipos de contenido anteriores)</span><span class="sxs-lookup"><span data-stu-id="76458-121">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="76458-122">DLP.All (eventos exclusivos de DLP para todas las cargas de trabajo)</span><span class="sxs-lookup"><span data-stu-id="76458-122">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="76458-123">Para obtener más información sobre los eventos y las propiedades asociados a estos tipos de contenido, vea [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md) (Esquema de la API de Actividad de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="76458-123">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="76458-124">Para empezar a recuperar los blobs de contenido para un espacio empresarial, primero se crea una suscripción a los tipos de contenido deseados.</span><span class="sxs-lookup"><span data-stu-id="76458-124">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="76458-125">Si se van a recuperar blobs de contenido para varios espacios empresariales, cree varias suscripciones a todos los tipos de contenido deseados, una para cada espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="76458-125">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="76458-126">Después de crear una suscripción, puede sondear periódicamente para detectar nuevos blobs de contenido disponibles para descargar, o bien puede registrar un punto de conexión de webhook con la suscripción y se enviarán notificaciones a este punto de conexión cuando haya nuevos blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="76458-126">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="76458-127">Cuando se crea una suscripción, pueden pasar hasta 12 horas hasta que los primeros blobs de contenido estén disponibles para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-127">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="76458-128">Para crear los blobs de contenido, se recopilan y agregan acciones y eventos de varios servidores y centros de datos.</span><span class="sxs-lookup"><span data-stu-id="76458-128">The content blobs are creating by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="76458-129">Como resultado de este proceso distribuido, las acciones y los eventos incluidos en los blobs de contenido no aparecerán necesariamente en el orden en que se producen.</span><span class="sxs-lookup"><span data-stu-id="76458-129">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="76458-130">Un blob de contenido puede contener acciones y eventos que tuvieron lugar antes de las acciones y los eventos incluidos en un blob de contenido anterior.</span><span class="sxs-lookup"><span data-stu-id="76458-130">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="76458-131">Estamos trabajando para reducir la latencia entre la aparición de los eventos y las acciones, y su disponibilidad en un blob de contenido, pero no podemos garantizar que aparezcan de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="76458-131">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we cannot guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="76458-132">Los datos confidenciales de DLP solo están disponibles en la API de fuente de actividades para los usuarios a los que se les han concedido permisos "Leer datos confidenciales de DLP".</span><span class="sxs-lookup"><span data-stu-id="76458-132">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="76458-133">Para obtener más información sobre la prevención de pérdida de datos (DLP), vea [Información general sobre directivas de prevención de pérdida de datos](https://support.office.com/es-ES/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="76458-133">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/es-ES/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="76458-134">Operaciones de la API de Actividad</span><span class="sxs-lookup"><span data-stu-id="76458-134">Activity API operations</span></span>

<span data-ttu-id="76458-135">Todas las operaciones de API están orientadas a un único espacio empresarial y la dirección URL raíz de la API incluye un identificador de espacio empresarial que especifica el contexto del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="76458-135">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="76458-136">El identificador de espacio empresarial es un GUID.</span><span class="sxs-lookup"><span data-stu-id="76458-136">The tenant ID is a GUID.</span></span> <span data-ttu-id="76458-137">Para obtener información sobre cómo conseguir el GUID, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="76458-137">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="76458-138">Como las notificaciones que se envían al webhook incluyen el **identificador de espacio empresarial**, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales.</span><span class="sxs-lookup"><span data-stu-id="76458-138">Because the notifications we send to your webhook include the **tenant ID**, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="76458-139">Todas las operaciones de API requieren un encabezado de autorización HTTP con un token de acceso obtenido de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76458-139">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="76458-140">El identificador de espacio empresarial en el token de acceso debe coincidir con el de la dirección URL raíz de la API y el token de acceso debe contener la notificación ActivityFeed.Read (que se corresponde con el permiso [Leer datos de actividad de la organización] que ha configurado para la aplicación en Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76458-140">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="76458-141">La API de Actividad admite las operaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="76458-141">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="76458-142">**Iniciar una suscripción** para empezar a recibir notificaciones y recuperar datos de actividad de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="76458-142">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="76458-143">**Detener una suscripción** para dejar de recuperar datos de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="76458-143">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="76458-144">**Enumerar las suscripciones actuales**</span><span class="sxs-lookup"><span data-stu-id="76458-144">**List current subscriptions**</span></span>
    
- <span data-ttu-id="76458-145">**Enumerar el contenido disponible** y las direcciones URL de contenido correspondientes.</span><span class="sxs-lookup"><span data-stu-id="76458-145">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="76458-146">**Recibir notificaciones** enviadas por un webhook cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-146">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="76458-147">**Recuperar contenido** mediante la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-147">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="76458-148">**Enumerar las notificaciones** enviadas por un webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-148">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="76458-149">**Recuperar los nombres descriptivos de recurso** de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="76458-149">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="76458-150">Iniciar una suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-150">Start a subscription</span></span>

<span data-ttu-id="76458-151">Esta operación inicia una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-151">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="76458-152">Si ya existe una suscripción para el tipo de contenido específico, esta operación se usa para:</span><span class="sxs-lookup"><span data-stu-id="76458-152">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="76458-153">Actualizar las propiedades de un webhook activo.</span><span class="sxs-lookup"><span data-stu-id="76458-153">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="76458-154">Habilitar un webhook que estaba deshabilitado debido a un exceso de notificaciones con error.</span><span class="sxs-lookup"><span data-stu-id="76458-154">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="76458-155">Volver a habilitar un webhook expirado mediante la especificación de una fecha de expiración nula o posterior.</span><span class="sxs-lookup"><span data-stu-id="76458-155">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="76458-156">Quitar un webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-156">Remove a webhook.</span></span>
    
||<span data-ttu-id="76458-157">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-157">Subscription</span></span>|<span data-ttu-id="76458-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-158">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-159">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-159">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="76458-160">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-160">**Parameters**</span></span>|<span data-ttu-id="76458-161">contentType</span><span class="sxs-lookup"><span data-stu-id="76458-161">contentType</span></span>|<span data-ttu-id="76458-162">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="76458-162">Must be a valid content type.</span></span>|
||<span data-ttu-id="76458-163">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-163">PublisherIdentifier</span></span>|<span data-ttu-id="76458-164">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-164">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-165">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-165">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-166">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-166">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-167">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-167">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-168">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-168">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="76458-169">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="76458-169">**Body**</span></span>|<span data-ttu-id="76458-170">webhook</span><span class="sxs-lookup"><span data-stu-id="76458-170">webhook</span></span>|<span data-ttu-id="76458-171">Objeto JSON opcional con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="76458-171">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-172"><b>address</b>: punto de conexión HTTPS requerido que puede recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="76458-172"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="76458-173">Se enviará un mensaje de prueba al webhook para validarlo antes de crear la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-173">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="76458-174"><b>authId</b>: cadena opcional que se incluirá como el encabezado WebHook-AuthID de las notificaciones que se envían al webhook como medio para identificar y autorizar el origen de la solicitud al webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-174"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="76458-175"><b>expiration</b>: valor de fecha y hora opcional que indica una fecha y hora después de la que no se deben enviar más notificaciones al webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-175"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="76458-176">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-176">**Response**</span></span>|<span data-ttu-id="76458-177">contentType</span><span class="sxs-lookup"><span data-stu-id="76458-177">contentType</span></span>|<span data-ttu-id="76458-178">El tipo de contenido especificado en la llamada.</span><span class="sxs-lookup"><span data-stu-id="76458-178">The content type specified in the call.</span></span>|
||<span data-ttu-id="76458-179">status</span><span class="sxs-lookup"><span data-stu-id="76458-179">status</span></span>|<span data-ttu-id="76458-180">El estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-180">The status of the subscription.</span></span> <span data-ttu-id="76458-181">Si una suscripción está deshabilitada, no podrá enumerar o recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-181">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="76458-182">webhook</span><span class="sxs-lookup"><span data-stu-id="76458-182">webhook</span></span>|<span data-ttu-id="76458-183">Las propiedades del webhook especificado en la llamada junto con el estado del webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-183">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="76458-184">Si el webhook está deshabilitado, no recibirá notificaciones, pero todavía podrá enumerar y recuperar el contenido, siempre que la suscripción esté habilitada.</span><span class="sxs-lookup"><span data-stu-id="76458-184">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="76458-185">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-185">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="76458-186">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-186">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="76458-187">Validación del webhook</span><span class="sxs-lookup"><span data-stu-id="76458-187">Webhook validation</span></span>

<span data-ttu-id="76458-188">Cuando se llama a la operación /start y se especifica un webhook, le enviaremos una notificación de validación a la dirección de webhook especificada para validar que una escucha activa puede aceptar y procesar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="76458-188">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="76458-189">Si no recibimos una respuesta HTTP 200 Correcto, no se creará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-189">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="76458-190">O bien, si se empieza a llamar a /start para agregar un webhook a una suscripción existente y no se recibe una respuesta de HTTP 200 Correcto, el webhook no se agregará y no se cambiará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-190">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="76458-191">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-191">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId) if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="76458-192">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-192">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="76458-193">Detener una suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-193">Stop a subscription</span></span>

<span data-ttu-id="76458-194">Esta operación detiene una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-194">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="76458-195">Cuando se detiene una suscripción, ya no recibirá notificaciones y no podrá recuperar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-195">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="76458-196">Si más adelante se reinicia la suscripción, tendrá acceso al contenido nuevo a partir de ese punto.</span><span class="sxs-lookup"><span data-stu-id="76458-196">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="76458-197">No podrá recuperar el contenido que estaba disponible entre el momento de detener la suscripción y reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="76458-197">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="76458-198">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-198">Subscription</span></span>|<span data-ttu-id="76458-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-200">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-200">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="76458-201">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-201">**Parameters**</span></span>|<span data-ttu-id="76458-202">contentType</span><span class="sxs-lookup"><span data-stu-id="76458-202">contentType</span></span>|<span data-ttu-id="76458-203">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="76458-203">Must be a valid content type.</span></span>|
||<span data-ttu-id="76458-204">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-204">PublisherIdentifier</span></span>|<span data-ttu-id="76458-205">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-205">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-206">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-206">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-207">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-207">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-208">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-208">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-209">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-209">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="76458-210">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="76458-210">**Body**</span></span>|<span data-ttu-id="76458-211">(vacío)</span><span class="sxs-lookup"><span data-stu-id="76458-211">(empty)</span></span>||
|<span data-ttu-id="76458-212">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-212">**Response**</span></span>|<span data-ttu-id="76458-213">(vacío)</span><span class="sxs-lookup"><span data-stu-id="76458-213">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="76458-214">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-214">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="76458-215">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-215">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="76458-216">Enumerar las suscripciones actuales</span><span class="sxs-lookup"><span data-stu-id="76458-216">List current subscriptions</span></span>

<span data-ttu-id="76458-217">Esta operación devuelve una colección de las suscripciones actuales junto con los webhooks asociados.</span><span class="sxs-lookup"><span data-stu-id="76458-217">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="76458-218">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-218">Subscription</span></span>|<span data-ttu-id="76458-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-220">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-220">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="76458-221">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-221">**Parameters**</span></span>|<span data-ttu-id="76458-222">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-222">PublisherIdentifier</span></span>|<span data-ttu-id="76458-223">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-223">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-224">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-224">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-225">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-225">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-226">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-226">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-227">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-227">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="76458-228">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="76458-228">**Body**</span></span>|<span data-ttu-id="76458-229">(vacío)</span><span class="sxs-lookup"><span data-stu-id="76458-229">(empty)</span></span>||
|<span data-ttu-id="76458-230">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-230">**Response**</span></span>|<span data-ttu-id="76458-231">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="76458-231">JSON array</span></span>|<span data-ttu-id="76458-232">Cada suscripción se representará mediante un objeto JSON con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="76458-232">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-233"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-233"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="76458-234"><b>status</b>: indica el estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-234"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="76458-235"><b>webhook</b>: indica el webhook configurado, junto con el estado (habilitado, deshabilitado, expirado) del webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-235"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="76458-236">Si una suscripción no tiene un webhook, la propiedad webhook estará presente pero con un valor NULL.</span><span class="sxs-lookup"><span data-stu-id="76458-236">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="76458-237">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-237">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="76458-238">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-238">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="76458-239">Enumerar el contenido disponible</span><span class="sxs-lookup"><span data-stu-id="76458-239">List available content</span></span>

<span data-ttu-id="76458-240">Esta operación enumera el contenido disponible actualmente que se puede recuperar para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-240">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="76458-241">El contenido es una agregación de acciones y eventos recopilados de varios servidores en varios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="76458-241">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="76458-242">El contenido se mostrará en el orden en que estén disponibles las agregaciones, pero no se garantiza que los eventos y las acciones de las agregaciones sean secuenciales.</span><span class="sxs-lookup"><span data-stu-id="76458-242">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="76458-243">Se devuelve un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="76458-243">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="76458-244">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-244">Subscription</span></span>|<span data-ttu-id="76458-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-245">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-246">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-246">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="76458-247">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-247">**Parameters**</span></span>|<span data-ttu-id="76458-248">contentType</span><span class="sxs-lookup"><span data-stu-id="76458-248">contentType</span></span>|<span data-ttu-id="76458-249">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="76458-249">Must be a valid content type.</span></span>|
||<span data-ttu-id="76458-250">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-250">PublisherIdentifier</span></span>|<span data-ttu-id="76458-251">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-251">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-252">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-252">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-253">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-253">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-254">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-254">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-255">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-255">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="76458-256">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="76458-256">startTime endTime</span></span>|<span data-ttu-id="76458-257">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-257">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="76458-258">El intervalo de tiempo es inclusivo con respecto a startTime (startTime <= contentCreated) y exclusivo con respecto a endTime (contentCreated < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-258">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-259">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="76458-259">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="76458-260">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="76458-260">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="76458-261">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="76458-261">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="76458-262">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="76458-262">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="76458-263">De forma predeterminada, si se omiten startTime y endTime, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="76458-263">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="76458-264">**NOTA**: Aunque se puede especificar un valor de startTime y endTime con más de 24 horas de diferencia, no es recomendable.</span><span class="sxs-lookup"><span data-stu-id="76458-264">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="76458-265">Además, si obtiene algún resultado en respuesta a una solicitud de más de 24 horas, podrían ser resultados parciales y no deberían tenerse en cuenta.</span><span class="sxs-lookup"><span data-stu-id="76458-265">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="76458-266">La solicitud se debe emitir con un intervalo de no más de 24 horas entre los valores de startTime y endTime.</span><span class="sxs-lookup"><span data-stu-id="76458-266">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="76458-267">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-267">**Response**</span></span>|<span data-ttu-id="76458-268">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="76458-268">JSON array</span></span>|<span data-ttu-id="76458-269">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="76458-269">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-270"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-270"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="76458-271"><b>contentId</b>: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="76458-271"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="76458-272"><b>contentUri</b>: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-272"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="76458-273"><b>contentCreated</b>: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-273"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="76458-274"><b>contentExpiration</b>: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="76458-274"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="76458-275">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-275">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="76458-276">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-276">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="76458-277">Paginación</span><span class="sxs-lookup"><span data-stu-id="76458-277">Pagination</span></span>

<span data-ttu-id="76458-278">Al enumerar el contenido disponible para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="76458-278">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="76458-279">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncarán y se agregará un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="76458-279">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="76458-280">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="76458-280">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="76458-281">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="76458-281">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="76458-282">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="76458-282">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="76458-283">Recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="76458-283">Receiving notifications</span></span>

<span data-ttu-id="76458-284">Las notificaciones se envían al webhook configurado para una suscripción cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-284">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="76458-285">Como la notificación incluye el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales para los que tiene suscripciones.</span><span class="sxs-lookup"><span data-stu-id="76458-285">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="76458-286">La notificación se realiza como HTTP POST sobre TLS (TLS 1.0 y versiones posteriores) a la dirección del webhook especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-286">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="76458-287">Si la configuración de webhook incluye un identificador de autenticación, se enviará como un encabezado HTTP: Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="76458-287">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="76458-288">Cualquier respuesta distinta de HTTP 200 Correcto se considera un error y la notificación se volverá a intentar.</span><span class="sxs-lookup"><span data-stu-id="76458-288">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="76458-289">También puede configurar el webhook para requerir autenticación basada en certificados de cliente y se autenticará con el certificado manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="76458-289">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="76458-290">El cuerpo de la solicitud contendrá una matriz de uno o más objetos JSON que representan los blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="76458-290">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="76458-291">El número de blobs de contenido en cada notificación es limitado para que el tamaño de la notificación sea relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="76458-291">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="76458-292">Como este límite puede cambiar, la implementación debe consultar la longitud de la matriz en lugar de esperar un tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="76458-292">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="76458-293">Cada objeto incluirá las mismas propiedades que devuelve la operación /content, junto con el GUID del espacio empresarial al que corresponden los datos y el GUID de la aplicación que creó las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="76458-293">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="76458-294">Esto permite al webhook establecer el contexto cuando se usa con varios espacios empresariales y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="76458-294">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="76458-295">**tenantId**: el GUID del espacio empresarial al que pertenece el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-295">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="76458-296">**clientId**: el GUID de la aplicación que creó la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-296">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="76458-297">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-297">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="76458-298">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="76458-298">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="76458-299">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-299">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="76458-300">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-300">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="76458-301">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="76458-301">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="76458-302">A continuación se muestra un ejemplo de una notificación.</span><span class="sxs-lookup"><span data-stu-id="76458-302">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="76458-303">Error de notificación y reintento</span><span class="sxs-lookup"><span data-stu-id="76458-303">Notification failure and retry</span></span>

<span data-ttu-id="76458-304">El sistema de notificaciones envía las notificaciones cuando hay nuevo contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-304">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="76458-305">Si se producen errores excesivos al enviar las notificaciones, nuestro mecanismo de reintento aumentará de forma exponencial el tiempo entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="76458-305">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="76458-306">Si se siguen produciendo errores, nos reservamos el derecho de deshabilitar el webhook y detener por completo el envío de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="76458-306">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="76458-307">Se puede usar la operación /start para volver a habilitar un webhook deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="76458-307">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="76458-308">Recuperación de contenido</span><span class="sxs-lookup"><span data-stu-id="76458-308">Retrieving content</span></span>

<span data-ttu-id="76458-309">Para recuperar un blob de contenido, realice una solicitud GET en el URI del contenido correspondiente que se incluye en la lista de contenido disponible y en las notificaciones enviadas a un webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-309">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="76458-310">El contenido devuelto será una colección de una más acciones o eventos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="76458-310">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="76458-311">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-311">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="76458-312">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-312">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="76458-313">Enumerar notificaciones</span><span class="sxs-lookup"><span data-stu-id="76458-313">List notifications</span></span>

<span data-ttu-id="76458-314">Esta operación enumera todos los intentos de notificación para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-314">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="76458-315">Si no ha incluido un webhook al iniciar la suscripción para el tipo de contenido, no existirá ninguna notificación para recuperar.</span><span class="sxs-lookup"><span data-stu-id="76458-315">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="76458-316">Como en caso de error se reintentan las notificaciones, esta operación puede devolver varias notificaciones para el mismo contenido, y el orden en el que se envían no coincidirá necesariamente con el orden en que el contenido está disponible (en especial si hay errores y reintentos).</span><span class="sxs-lookup"><span data-stu-id="76458-316">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="76458-317">Puede usar esta operación para ayudar a investigar problemas relacionados con los webhooks y las notificaciones, pero no debería usarla para determinar qué contenido está disponible actualmente para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="76458-317">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="76458-318">En su lugar, use la operación /content.</span><span class="sxs-lookup"><span data-stu-id="76458-318">Use the /content operation instead.</span></span> <span data-ttu-id="76458-319">Se devolverá un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="76458-319">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="76458-320">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-320">Subscription</span></span>|<span data-ttu-id="76458-321">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-321">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-322">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-322">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="76458-323">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-323">**Parameters**</span></span>|<span data-ttu-id="76458-324">contentType</span><span class="sxs-lookup"><span data-stu-id="76458-324">contentType</span></span>|<span data-ttu-id="76458-325">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="76458-325">Must be a valid content type.</span></span>|
||<span data-ttu-id="76458-326">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-326">PublisherIdentifier</span></span>|<span data-ttu-id="76458-327">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-327">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-328">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-328">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-329">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-329">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-330">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-330">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-331">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-331">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="76458-332">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="76458-332">startTime endTime</span></span>|<span data-ttu-id="76458-333">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-333">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="76458-334">El intervalo de tiempo es inclusivo con respecto a _startTime_ ( _startTime_ <= contentCreated) y exclusivo con respecto a _endTime_ (_contentCreated_ < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="76458-334">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-335">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="76458-335">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="76458-336">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="76458-336">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="76458-337">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="76458-337">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="76458-338">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="76458-338">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="76458-339">De forma predeterminada, si se omiten _startTime_ y _endTime_, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="76458-339">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="76458-340">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-340">**Response**</span></span>|<span data-ttu-id="76458-341">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="76458-341">JSON array</span></span>|<span data-ttu-id="76458-342">Las notificaciones disponibles se representarán mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="76458-342">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="76458-343">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-343">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="76458-344">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="76458-344">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="76458-345">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-345">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="76458-346">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="76458-346">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="76458-347">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="76458-347">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="76458-348">**notificationSent**: la fecha y hora de envío de la notificación.</span><span class="sxs-lookup"><span data-stu-id="76458-348">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="76458-349">**notificationStatus**: indica si intento de notificación se ha realizado correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="76458-349">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="76458-350">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-350">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="76458-351">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-351">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="76458-352">Paginación</span><span class="sxs-lookup"><span data-stu-id="76458-352">Pagination</span></span>

<span data-ttu-id="76458-353">Al enumerar el historial de notificaciones para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="76458-353">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="76458-354">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncan y se agrega un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="76458-354">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="76458-355">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="76458-355">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="76458-356">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="76458-356">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="76458-357">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUrl**.</span><span class="sxs-lookup"><span data-stu-id="76458-357">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="76458-358">Recuperar los nombres descriptivos de recurso</span><span class="sxs-lookup"><span data-stu-id="76458-358">Retrieve resource friendly names</span></span>

<span data-ttu-id="76458-359">Esta operación recupera los nombres descriptivos de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="76458-359">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="76458-360">En la actualidad, el único objeto que se admite es "DlpSensitiveType".</span><span class="sxs-lookup"><span data-stu-id="76458-360">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="76458-361">Suscripción</span><span class="sxs-lookup"><span data-stu-id="76458-361">Subscription</span></span>|<span data-ttu-id="76458-362">Descripción</span><span class="sxs-lookup"><span data-stu-id="76458-362">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="76458-363">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="76458-363">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="76458-364">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="76458-364">**Parameters**</span></span>|<span data-ttu-id="76458-365">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-365">PublisherIdentifier</span></span>|<span data-ttu-id="76458-366">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="76458-366">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="76458-367">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="76458-367">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="76458-368">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-368">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="76458-369">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="76458-369">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="76458-370">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-370">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="76458-371">**Encabezados**</span><span class="sxs-lookup"><span data-stu-id="76458-371">**Headers**</span></span>|<span data-ttu-id="76458-372">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="76458-372">Accept-Language</span></span>|<span data-ttu-id="76458-373">Encabezado para especificar el idioma que prefiere para los nombres localizados.</span><span class="sxs-lookup"><span data-stu-id="76458-373">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="76458-374">Por ejemplo, use "en-US" para inglés o "es" para español.</span><span class="sxs-lookup"><span data-stu-id="76458-374">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="76458-375">Si este encabezado no existe, se devolverá el idioma predeterminado (en-US).</span><span class="sxs-lookup"><span data-stu-id="76458-375">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="76458-376">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="76458-376">**Body**</span></span>|<span data-ttu-id="76458-377">(vacío)</span><span class="sxs-lookup"><span data-stu-id="76458-377">(empty)</span></span>||
|<span data-ttu-id="76458-378">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="76458-378">**Response**</span></span>|<span data-ttu-id="76458-379">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="76458-379">JSON array</span></span>|<span data-ttu-id="76458-380">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="76458-380">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-381"><b>id</b>: indica el GUID del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="76458-381"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="76458-382"><b>name</b>: el nombre descriptivo del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="76458-382"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="76458-383">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-383">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="76458-384">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="76458-384">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="76458-385">Limitación de API</span><span class="sxs-lookup"><span data-stu-id="76458-385">API throttling</span></span>

<span data-ttu-id="76458-386">Cada proveedor que codifica la API tiene una cuota dedicada de limitación de solicitudes de 60 000 por minuto.</span><span class="sxs-lookup"><span data-stu-id="76458-386">Each vendor coding against the API has a dedicated quota for request throttling at 60K per minute.</span></span> <span data-ttu-id="76458-387">Para obtener la cuota dedicada, especifique el parámetro PublisherIdentifier en todas las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="76458-387">To get the dedicated quota, specify the parameter PublisherIdentifier in all your requests.</span></span> <span data-ttu-id="76458-388">Las solicitudes que tengan el mismo valor PublisherIdentifier compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="76458-388">Requests with the same PublisherIdentifier will share the same quota.</span></span> <span data-ttu-id="76458-389">Todas las solicitudes sin el valor PublisherIdentifier especificado compartirán la misma cuota como el GUID 00000000-0000-0000-0000-000000000000.</span><span class="sxs-lookup"><span data-stu-id="76458-389">All requests without the PublisherIdentifier specified will share the same quota as GUID 00000000-0000-0000-0000-000000000000.</span></span>

<span data-ttu-id="76458-390">Si Office 365 tiene que recurrir a usted para determinados problemas, asegúrese de que la suscripción para el espacio empresarial cuyo GUID se usa como valor PublisherIdentifier es actual y está actualizado con la información de contacto correcta.</span><span class="sxs-lookup"><span data-stu-id="76458-390">If Office 365 needs to reverse escalate to you in certain issues, make sure the subscription for the tenant whose GUID is used as your PublisherIdentifier is current and updated with the correct contact information.</span></span> <span data-ttu-id="76458-391">No hay requisitos de suscripción para este espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="76458-391">There is no subscription requirement for this tenant.</span></span>

<span data-ttu-id="76458-392">Para los clientes que desarrollan sus propias soluciones con esta API, se recomienda usar el GUID del propio espacio empresarial para evitar la competencia causada por una cuota compartida limitada.</span><span class="sxs-lookup"><span data-stu-id="76458-392">For customers who are developing their own solutions using this API, we recommend using your own tenant GUID to avoid competition caused by a limited shared quota.</span></span>

> [!NOTE] 
> <span data-ttu-id="76458-393">Aunque cada publicador puede enviar hasta 60 000 solicitudes por minuto, Microsoft no garantiza una velocidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="76458-393">Even though each publisher can submit up to 60K requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="76458-394">La velocidad de respuesta depende de varios factores, como el rendimiento del sistema cliente y la capacidad y la velocidad de la red.</span><span class="sxs-lookup"><span data-stu-id="76458-394">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>  <span data-ttu-id="76458-395">Un publicador puede enviar hasta 60 000 solicitudes por minuto, pero no debe esperar recibir respuestas para todas esas solicitudes en ese mismo minuto.</span><span class="sxs-lookup"><span data-stu-id="76458-395">A publisher can submit up to 60K requests per minute, but should not expect to receive responses for all 60K requests within that same minute.</span></span> <span data-ttu-id="76458-396">En cualquier caso, si un publicador quiere realizar pruebas de una aplicación cliente, debe hacerlo en todos los entornos en los que planee ejecutarla, ya que los resultados pueden variar de un entorno a otro.</span><span class="sxs-lookup"><span data-stu-id="76458-396">If anything, should a publisher want to benchmark a client application, they should do so in each different environment that they are planning on running the client application in because results will vary from environment to environment.</span></span>

## <a name="errors"></a><span data-ttu-id="76458-397">Errores</span><span class="sxs-lookup"><span data-stu-id="76458-397">Errors</span></span>

<span data-ttu-id="76458-398">Cuando el servicio encuentra un error, notificará el código de respuesta de error al autor de la llamada, mediante la sintaxis estándar de código de error de HTTP.</span><span class="sxs-lookup"><span data-stu-id="76458-398">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="76458-399">.</span><span class="sxs-lookup"><span data-stu-id="76458-399">.</span></span> <span data-ttu-id="76458-400">En el cuerpo de la llamada con error se incluye información adicional como un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="76458-400">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="76458-401">A continuación se muestra un ejemplo de un cuerpo completo de error JSON:</span><span class="sxs-lookup"><span data-stu-id="76458-401">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="76458-402">Código</span><span class="sxs-lookup"><span data-stu-id="76458-402">Code</span></span>|<span data-ttu-id="76458-403">Mensaje</span><span class="sxs-lookup"><span data-stu-id="76458-403">Message</span></span>|
|<span data-ttu-id="76458-404">AF10001</span><span class="sxs-lookup"><span data-stu-id="76458-404">AF10001</span></span>|<span data-ttu-id="76458-405">El conjunto de permisos ({0}) enviados en la solicitud no incluía el permiso esperado **ActivityFeed.Read**.</span><span class="sxs-lookup"><span data-stu-id="76458-405">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-406">{0} = el conjunto de permisos en el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="76458-406">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="76458-407">AF20001</span><span class="sxs-lookup"><span data-stu-id="76458-407">AF20001</span></span>|<span data-ttu-id="76458-408">Falta el parámetro: {0}.</span><span class="sxs-lookup"><span data-stu-id="76458-408">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-409">{0} = el nombre del parámetro que falta.</span><span class="sxs-lookup"><span data-stu-id="76458-409">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="76458-410">AF20002</span><span class="sxs-lookup"><span data-stu-id="76458-410">AF20002</span></span>|<span data-ttu-id="76458-411">Tipo de parámetro no válido: {0}.</span><span class="sxs-lookup"><span data-stu-id="76458-411">Invalid parameter type: {0}.</span></span> <span data-ttu-id="76458-412">Tipo esperado: {1}</span><span class="sxs-lookup"><span data-stu-id="76458-412">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-413">{0} = el nombre del parámetro no válido.</span><span class="sxs-lookup"><span data-stu-id="76458-413">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="76458-414">{1} = el tipo esperado (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="76458-414">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="76458-415">AF20003</span><span class="sxs-lookup"><span data-stu-id="76458-415">AF20003</span></span>|<span data-ttu-id="76458-416">{0} de expiración proporcionada se establece en una fecha y hora pasadas.</span><span class="sxs-lookup"><span data-stu-id="76458-416">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-417">{0} = la expiración que se pasa en la llamada de API.</span><span class="sxs-lookup"><span data-stu-id="76458-417">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="76458-418">AF20010</span><span class="sxs-lookup"><span data-stu-id="76458-418">AF20010</span></span>|<span data-ttu-id="76458-419">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no coincide con el que se pasa en el token de acceso ({1}).</span><span class="sxs-lookup"><span data-stu-id="76458-419">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-420">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="76458-420">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="76458-421">{1} = el identificador de espacio empresarial que se pasa en el token de acceso</span><span class="sxs-lookup"><span data-stu-id="76458-421">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="76458-422">AF20011</span><span class="sxs-lookup"><span data-stu-id="76458-422">AF20011</span></span>|<span data-ttu-id="76458-423">El identificador de espacio empresarial ({0}) especificado no existe en el sistema o se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="76458-423">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="76458-424">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="76458-424">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-425">AF20012</span><span class="sxs-lookup"><span data-stu-id="76458-425">AF20012</span></span>|<span data-ttu-id="76458-426">El identificador de espacio empresarial ({0}) especificado no está configurado correctamente en el sistema.</span><span class="sxs-lookup"><span data-stu-id="76458-426">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="76458-427">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="76458-427">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-428">AF20013</span><span class="sxs-lookup"><span data-stu-id="76458-428">AF20013</span></span>|<span data-ttu-id="76458-429">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no es un GUID válido.</span><span class="sxs-lookup"><span data-stu-id="76458-429">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="76458-430">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="76458-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-431">AF20020</span><span class="sxs-lookup"><span data-stu-id="76458-431">AF20020</span></span>|<span data-ttu-id="76458-432">El tipo de contenido especificado no es válido.</span><span class="sxs-lookup"><span data-stu-id="76458-432">The specified content type is not valid.</span></span>|
|<span data-ttu-id="76458-433">AF20021</span><span class="sxs-lookup"><span data-stu-id="76458-433">AF20021</span></span>|<span data-ttu-id="76458-434">El punto de conexión de webhook {{0}) no se pudo validar.</span><span class="sxs-lookup"><span data-stu-id="76458-434">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="76458-435">{1}</span><span class="sxs-lookup"><span data-stu-id="76458-435">{1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-436">{0} = dirección del webhook.</span><span class="sxs-lookup"><span data-stu-id="76458-436">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="76458-437">{1} = "El punto de conexión no devolvió HTTP 200".</span><span class="sxs-lookup"><span data-stu-id="76458-437">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="76458-438">o bien, "La dirección debe comenzar con HTTPS".</span><span class="sxs-lookup"><span data-stu-id="76458-438">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="76458-439">AF20022</span><span class="sxs-lookup"><span data-stu-id="76458-439">AF20022</span></span>|<span data-ttu-id="76458-440">No se encontró ninguna suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="76458-440">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="76458-441">AF20023</span><span class="sxs-lookup"><span data-stu-id="76458-441">AF20023</span></span>|<span data-ttu-id="76458-442">{0} ha deshabilitado la suscripción.</span><span class="sxs-lookup"><span data-stu-id="76458-442">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-443">{0} = "un administrador de espacio empresarial" o "un administrador de servicio"</span><span class="sxs-lookup"><span data-stu-id="76458-443">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="76458-444">AF20030</span><span class="sxs-lookup"><span data-stu-id="76458-444">AF20030</span></span>|<span data-ttu-id="76458-445">Se debe especificar la hora de inicio y la hora de finalización (o bien omitirse), con una diferencia menor o igual de 24 horas, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="76458-445">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="76458-446">AF20031</span><span class="sxs-lookup"><span data-stu-id="76458-446">AF20031</span></span>|<span data-ttu-id="76458-447">Entrada nextPage no válida: {0}.</span><span class="sxs-lookup"><span data-stu-id="76458-447">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-448">{0} = el indicador de página siguiente que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="76458-448">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-449">AF20050</span><span class="sxs-lookup"><span data-stu-id="76458-449">AF20050</span></span>|<span data-ttu-id="76458-450">No existe el contenido especificado ({0}).</span><span class="sxs-lookup"><span data-stu-id="76458-450">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-451">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="76458-451">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-452">AF20051</span><span class="sxs-lookup"><span data-stu-id="76458-452">AF20051</span></span>|<span data-ttu-id="76458-453">El contenido solicitado con la clave {0} ya ha expirado.</span><span class="sxs-lookup"><span data-stu-id="76458-453">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="76458-454">El contenido de más de siete días no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="76458-454">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-455">•    {0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="76458-455">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-456">AF20052</span><span class="sxs-lookup"><span data-stu-id="76458-456">AF20052</span></span>|<span data-ttu-id="76458-457">El identificador de contenido {0} en la dirección URL no es válido.</span><span class="sxs-lookup"><span data-stu-id="76458-457">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-458">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="76458-458">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="76458-459">AF20053</span><span class="sxs-lookup"><span data-stu-id="76458-459">AF20053</span></span>|<span data-ttu-id="76458-460">Solo puede haber un idioma en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="76458-460">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="76458-461">AF20054</span><span class="sxs-lookup"><span data-stu-id="76458-461">AF20054</span></span>|<span data-ttu-id="76458-462">Sintaxis incorrecta en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="76458-462">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="76458-463">AF429</span><span class="sxs-lookup"><span data-stu-id="76458-463">AF429</span></span>|<span data-ttu-id="76458-464">Demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="76458-464">Too many requests.</span></span> <span data-ttu-id="76458-465">Método={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="76458-465">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="76458-466">{0} = método HTTP</span><span class="sxs-lookup"><span data-stu-id="76458-466">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="76458-467">{1} = GUID de espacio empresarial usado como PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="76458-467">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="76458-468">AF50000</span><span class="sxs-lookup"><span data-stu-id="76458-468">AF50000</span></span>|<span data-ttu-id="76458-469">Se ha producido un error interno.</span><span class="sxs-lookup"><span data-stu-id="76458-469">An internal error occurred.</span></span> <span data-ttu-id="76458-470">Vuelva a intentar realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="76458-470">Retry the request.</span></span>|
