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
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="15cd5-103">Referencia de la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="15cd5-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="15cd5-104">Use la API de Actividad de administración de Office 365 para recuperar información sobre acciones y eventos de usuario, administrador, sistema y directivas de los registros de actividad de Office 365 y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15cd5-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="15cd5-105">Puede usar acciones y eventos de los registros de auditoría y actividad de Office 365 y Microsoft Azure Active Directory para crear soluciones que proporcionen supervisión, análisis y visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="15cd5-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="15cd5-106">Estas soluciones ofrecen a las organizaciones mayor visibilidad de las acciones realizadas en el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="15cd5-107">Estas acciones y eventos también están disponibles en los informes de actividad de Office 365.</span><span class="sxs-lookup"><span data-stu-id="15cd5-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="15cd5-108">Para obtener más información, vea [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="15cd5-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="15cd5-109">La API de Actividad de administración de Office 365 es un servicio web REST que se puede usar para desarrollar soluciones mediante cualquier lenguaje y entorno de hospedaje que admita HTTPS y certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="15cd5-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="15cd5-110">La API se basa en Azure AD y el protocolo OAuth2 para la autorización y autenticación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="15cd5-111">Para acceder a la API desde la aplicación, primero deberá registrarla en Azure AD y configurarla con los permisos apropiados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="15cd5-112">Esto permitirá que la aplicación solicite los tokens de acceso OAuth2 que necesita para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="15cd5-113">Para obtener más información, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="15cd5-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="15cd5-114">Para obtener información sobre los datos que devuelve la API de Actividad de administración de Office 365, vea [Esquema de la API de Actividad de administración de Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="15cd5-114">For information about the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15cd5-115">Para poder acceder a los datos a través de la API de Actividad de administración de Office 365, debe activar el registro de auditoría unificado para su organización de Office 365.</span><span class="sxs-lookup"><span data-stu-id="15cd5-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="15cd5-116">Para ello, active el registro de auditoría de Office 365.</span><span class="sxs-lookup"><span data-stu-id="15cd5-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="15cd5-117">Para obtener instrucciones, consulte [Activar o desactivar la búsqueda de registros de auditoría de Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span><span class="sxs-lookup"><span data-stu-id="15cd5-117">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="15cd5-118">Trabajar con la API de Actividad de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="15cd5-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="15cd5-119">La API de Actividad de administración de Office 365 agrega acciones y eventos en blobs de contenido específicos del espacio empresarial, que se clasifican según el tipo y el origen del contenido que contienen.</span><span class="sxs-lookup"><span data-stu-id="15cd5-119">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="15cd5-120">En la actualidad, se admiten estos tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="15cd5-120">Currently, these content types are supported:</span></span>

- <span data-ttu-id="15cd5-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="15cd5-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="15cd5-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="15cd5-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="15cd5-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="15cd5-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="15cd5-124">Audit.General (incluye todas las demás cargas de trabajo que no se incluyen en los tipos de contenido anteriores)</span><span class="sxs-lookup"><span data-stu-id="15cd5-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="15cd5-125">DLP.All (eventos exclusivos de DLP para todas las cargas de trabajo)</span><span class="sxs-lookup"><span data-stu-id="15cd5-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="15cd5-126">Para obtener más información sobre los eventos y las propiedades asociados a estos tipos de contenido, vea [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md) (Esquema de la API de Actividad de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="15cd5-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="15cd5-127">Para empezar a recuperar los blobs de contenido para un espacio empresarial, primero se crea una suscripción a los tipos de contenido deseados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-127">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="15cd5-128">Si se van a recuperar blobs de contenido para varios espacios empresariales, cree varias suscripciones a todos los tipos de contenido deseados, una para cada espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-128">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="15cd5-129">Después de crear una suscripción, puede sondear periódicamente para detectar nuevos blobs de contenido disponibles para descargar, o bien puede registrar un punto de conexión de webhook con la suscripción y se enviarán notificaciones a este punto de conexión cuando haya nuevos blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="15cd5-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="15cd5-130">Cuando se crea una suscripción, pueden pasar hasta 12 horas hasta que los primeros blobs de contenido estén disponibles para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="15cd5-131">Para crear los blobs de contenido, se recopilan y agregan acciones y eventos de varios servidores y centros de datos.</span><span class="sxs-lookup"><span data-stu-id="15cd5-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="15cd5-132">Como resultado de este proceso distribuido, las acciones y los eventos incluidos en los blobs de contenido no aparecerán necesariamente en el orden en que se producen.</span><span class="sxs-lookup"><span data-stu-id="15cd5-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="15cd5-133">Un blob de contenido puede contener acciones y eventos que tuvieron lugar antes de las acciones y los eventos incluidos en un blob de contenido anterior.</span><span class="sxs-lookup"><span data-stu-id="15cd5-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="15cd5-134">Estamos trabajando para reducir la latencia entre la aparición de los eventos y las acciones, y su disponibilidad en un blob de contenido, pero no podemos garantizar que aparezcan de forma secuencial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="15cd5-135">Los datos confidenciales de DLP solo están disponibles en la API de fuente de actividades para los usuarios a los que se les han concedido permisos "Leer datos confidenciales de DLP".</span><span class="sxs-lookup"><span data-stu-id="15cd5-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="15cd5-136">Para obtener más información sobre la prevención de pérdida de datos (DLP), vea [Información general sobre directivas de prevención de pérdida de datos](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="15cd5-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="15cd5-137">Operaciones de la API de Actividad</span><span class="sxs-lookup"><span data-stu-id="15cd5-137">Activity API operations</span></span>

<span data-ttu-id="15cd5-138">Todas las operaciones de API están orientadas a un único espacio empresarial y la dirección URL raíz de la API incluye un identificador de espacio empresarial que especifica el contexto del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-138">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="15cd5-139">El identificador de espacio empresarial es un GUID.</span><span class="sxs-lookup"><span data-stu-id="15cd5-139">The tenant ID is a GUID.</span></span> <span data-ttu-id="15cd5-140">Para obtener información sobre cómo conseguir el GUID, vea [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md) (Introducción a las API de administración de Office 365).</span><span class="sxs-lookup"><span data-stu-id="15cd5-140">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span> 

<span data-ttu-id="15cd5-141">Como las notificaciones que se envían al webhook incluyen el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales.</span><span class="sxs-lookup"><span data-stu-id="15cd5-141">Because the notifications we send to your webhook include the tenant ID, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="15cd5-142">La URL del punto de conexión de la API que use está basada en el tipo de plan de suscripción de Microsoft 365 u Office 365 de su organización.</span><span class="sxs-lookup"><span data-stu-id="15cd5-142">The URL for the API endpoint that you use is based on the type of Microsoft 365 or Office 365 subscription plan for your organization.</span></span>

<span data-ttu-id="15cd5-143">**Plan para empresas**</span><span class="sxs-lookup"><span data-stu-id="15cd5-143">**Enterprise plan**</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="15cd5-144">**Plan de Administración pública GCC**</span><span class="sxs-lookup"><span data-stu-id="15cd5-144">**GCC government plan**</span></span>

```http
https://manage-gcc.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="15cd5-145">**Plan de Administración pública GCC High**</span><span class="sxs-lookup"><span data-stu-id="15cd5-145">**GCC High government plan**</span></span>

```http
https://manage.office365.us/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="15cd5-146">**Plan de Administración pública DoD**</span><span class="sxs-lookup"><span data-stu-id="15cd5-146">**DoD government plan**</span></span>

```http
https://manage.protection.apps.mil/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="15cd5-147">Todas las operaciones de API requieren un encabezado de autorización HTTP con un token de acceso obtenido de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15cd5-147">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="15cd5-148">El identificador de espacio empresarial en el token de acceso debe coincidir con el de la dirección URL raíz de la API y el token de acceso debe contener la notificación ActivityFeed.Read (que se corresponde con el permiso [Leer datos de actividad de la organización] que ha configurado para la aplicación en Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15cd5-148">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="15cd5-149">La API de Actividad admite las operaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="15cd5-149">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="15cd5-150">**Iniciar una suscripción** para empezar a recibir notificaciones y recuperar datos de actividad de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-150">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="15cd5-151">**Detener una suscripción** para dejar de recuperar datos de un espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-151">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="15cd5-152">**Enumerar las suscripciones actuales**</span><span class="sxs-lookup"><span data-stu-id="15cd5-152">**List current subscriptions**</span></span>
    
- <span data-ttu-id="15cd5-153">**Enumerar el contenido disponible** y las direcciones URL de contenido correspondientes.</span><span class="sxs-lookup"><span data-stu-id="15cd5-153">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="15cd5-154">**Recibir notificaciones** enviadas por un webhook cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-154">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="15cd5-155">**Recuperar contenido** mediante la dirección URL de contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-155">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="15cd5-156">**Enumerar las notificaciones** enviadas por un webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-156">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="15cd5-157">**Recuperar los nombres descriptivos de recurso** de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="15cd5-157">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="15cd5-158">Iniciar una suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-158">Start a subscription</span></span>

<span data-ttu-id="15cd5-159">Esta operación inicia una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-159">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="15cd5-160">Si ya existe una suscripción para el tipo de contenido específico, esta operación se usa para:</span><span class="sxs-lookup"><span data-stu-id="15cd5-160">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="15cd5-161">Actualizar las propiedades de un webhook activo.</span><span class="sxs-lookup"><span data-stu-id="15cd5-161">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="15cd5-162">Habilitar un webhook que estaba deshabilitado debido a un exceso de notificaciones con error.</span><span class="sxs-lookup"><span data-stu-id="15cd5-162">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="15cd5-163">Volver a habilitar un webhook expirado mediante la especificación de una fecha de expiración nula o posterior.</span><span class="sxs-lookup"><span data-stu-id="15cd5-163">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="15cd5-164">Quitar un webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-164">Remove a webhook.</span></span>
    
||<span data-ttu-id="15cd5-165">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-165">Subscription</span></span>|<span data-ttu-id="15cd5-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-166">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-167">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-167">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="15cd5-168">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-168">**Parameters**</span></span>|<span data-ttu-id="15cd5-169">contentType</span><span class="sxs-lookup"><span data-stu-id="15cd5-169">contentType</span></span>|<span data-ttu-id="15cd5-170">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-170">Must be a valid content type.</span></span>|
||<span data-ttu-id="15cd5-171">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-171">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-172">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-172">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-173">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-173">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-174">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-174">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-175">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-175">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-176">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-176">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="15cd5-177">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="15cd5-177">**Body**</span></span>|<span data-ttu-id="15cd5-178">webhook</span><span class="sxs-lookup"><span data-stu-id="15cd5-178">webhook</span></span>|<span data-ttu-id="15cd5-179">Objeto JSON opcional con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="15cd5-179">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-180"><b>address</b>: punto de conexión HTTPS requerido que puede recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-180"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="15cd5-181">Se enviará un mensaje de prueba al webhook para validarlo antes de crear la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-181">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="15cd5-182"><b>authId</b>: cadena opcional que se incluirá como el encabezado WebHook-AuthID de las notificaciones que se envían al webhook como medio para identificar y autorizar el origen de la solicitud al webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-182"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="15cd5-183"><b>expiration</b>: valor de fecha y hora opcional que indica una fecha y hora después de la que no se deben enviar más notificaciones al webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-183"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-184">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-184">**Response**</span></span>|<span data-ttu-id="15cd5-185">contentType</span><span class="sxs-lookup"><span data-stu-id="15cd5-185">contentType</span></span>|<span data-ttu-id="15cd5-186">El tipo de contenido especificado en la llamada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-186">The content type specified in the call.</span></span>|
||<span data-ttu-id="15cd5-187">status</span><span class="sxs-lookup"><span data-stu-id="15cd5-187">status</span></span>|<span data-ttu-id="15cd5-188">El estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-188">The status of the subscription.</span></span> <span data-ttu-id="15cd5-189">Si una suscripción está deshabilitada, no podrá enumerar o recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-189">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="15cd5-190">webhook</span><span class="sxs-lookup"><span data-stu-id="15cd5-190">webhook</span></span>|<span data-ttu-id="15cd5-191">Las propiedades del webhook especificado en la llamada junto con el estado del webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-191">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="15cd5-192">Si el webhook está deshabilitado, no recibirá notificaciones, pero todavía podrá enumerar y recuperar el contenido, siempre que la suscripción esté habilitada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-192">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="15cd5-193">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-193">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="15cd5-194">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-194">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="15cd5-195">Validación del webhook</span><span class="sxs-lookup"><span data-stu-id="15cd5-195">Webhook validation</span></span>

<span data-ttu-id="15cd5-196">Cuando se llama a la operación /start y se especifica un webhook, le enviaremos una notificación de validación a la dirección de webhook especificada para validar que una escucha activa puede aceptar y procesar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-196">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="15cd5-197">Si no recibimos una respuesta HTTP 200 Correcto, no se creará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-197">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="15cd5-198">O bien, si se empieza a llamar a /start para agregar un webhook a una suscripción existente y no se recibe una respuesta de HTTP 200 Correcto, el webhook no se agregará y no se cambiará la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-198">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="15cd5-199">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-199">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="15cd5-200">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-200">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="15cd5-201">Detener una suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-201">Stop a subscription</span></span>

<span data-ttu-id="15cd5-202">Esta operación detiene una suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-202">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="15cd5-203">Cuando se detiene una suscripción, ya no recibirá notificaciones y no podrá recuperar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-203">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="15cd5-204">Si más adelante se reinicia la suscripción, tendrá acceso al contenido nuevo a partir de ese punto.</span><span class="sxs-lookup"><span data-stu-id="15cd5-204">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="15cd5-205">No podrá recuperar el contenido que estaba disponible entre el momento de detener la suscripción y reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="15cd5-205">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="15cd5-206">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-206">Subscription</span></span>|<span data-ttu-id="15cd5-207">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-207">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-208">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-208">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="15cd5-209">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-209">**Parameters**</span></span>|<span data-ttu-id="15cd5-210">contentType</span><span class="sxs-lookup"><span data-stu-id="15cd5-210">contentType</span></span>|<span data-ttu-id="15cd5-211">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-211">Must be a valid content type.</span></span>|
||<span data-ttu-id="15cd5-212">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-212">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-213">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-213">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-214">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-214">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-215">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-215">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-216">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-216">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-217">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-217">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="15cd5-218">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="15cd5-218">**Body**</span></span>|<span data-ttu-id="15cd5-219">(vacío)</span><span class="sxs-lookup"><span data-stu-id="15cd5-219">(empty)</span></span>||
|<span data-ttu-id="15cd5-220">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-220">**Response**</span></span>|<span data-ttu-id="15cd5-221">(vacío)</span><span class="sxs-lookup"><span data-stu-id="15cd5-221">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="15cd5-222">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-222">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-223">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-223">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="15cd5-224">Enumerar las suscripciones actuales</span><span class="sxs-lookup"><span data-stu-id="15cd5-224">List current subscriptions</span></span>

<span data-ttu-id="15cd5-225">Esta operación devuelve una colección de las suscripciones actuales junto con los webhooks asociados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-225">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="15cd5-226">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-226">Subscription</span></span>|<span data-ttu-id="15cd5-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-227">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-228">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-228">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="15cd5-229">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-229">**Parameters**</span></span>|<span data-ttu-id="15cd5-230">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-230">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-231">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-231">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-232">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-232">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-233">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-233">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-234">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-234">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-235">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-235">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="15cd5-236">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="15cd5-236">**Body**</span></span>|<span data-ttu-id="15cd5-237">(vacío)</span><span class="sxs-lookup"><span data-stu-id="15cd5-237">(empty)</span></span>||
|<span data-ttu-id="15cd5-238">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-238">**Response**</span></span>|<span data-ttu-id="15cd5-239">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="15cd5-239">JSON array</span></span>|<span data-ttu-id="15cd5-240">Cada suscripción se representará mediante un objeto JSON con tres propiedades:</span><span class="sxs-lookup"><span data-stu-id="15cd5-240">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-241"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-241"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="15cd5-242"><b>status</b>: indica el estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-242"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="15cd5-243"><b>webhook</b>: indica el webhook configurado, junto con el estado (habilitado, deshabilitado, expirado) del webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-243"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="15cd5-244">Si una suscripción no tiene un webhook, la propiedad webhook estará presente pero con un valor NULL.</span><span class="sxs-lookup"><span data-stu-id="15cd5-244">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="15cd5-245">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-245">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-246">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-246">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="15cd5-247">Enumerar el contenido disponible</span><span class="sxs-lookup"><span data-stu-id="15cd5-247">List available content</span></span>

<span data-ttu-id="15cd5-248">Esta operación enumera el contenido disponible actualmente que se puede recuperar para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-248">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="15cd5-249">El contenido es una agregación de acciones y eventos recopilados de varios servidores en varios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="15cd5-249">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="15cd5-250">El contenido se mostrará en el orden en que estén disponibles las agregaciones, pero no se garantiza que los eventos y las acciones de las agregaciones sean secuenciales.</span><span class="sxs-lookup"><span data-stu-id="15cd5-250">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="15cd5-251">Se devuelve un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-251">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="15cd5-252">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-252">Subscription</span></span>|<span data-ttu-id="15cd5-253">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-253">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-254">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-254">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="15cd5-255">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-255">**Parameters**</span></span>|<span data-ttu-id="15cd5-256">contentType</span><span class="sxs-lookup"><span data-stu-id="15cd5-256">contentType</span></span>|<span data-ttu-id="15cd5-257">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-257">Must be a valid content type.</span></span>|
||<span data-ttu-id="15cd5-258">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-258">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-259">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-259">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-260">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-260">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-261">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-261">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-262">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-262">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-263">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-263">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="15cd5-264">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="15cd5-264">startTime endTime</span></span>|<span data-ttu-id="15cd5-265">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-265">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="15cd5-266">El intervalo de tiempo es inclusivo con respecto a startTime (startTime <= contentCreated) y exclusivo con respecto a endTime (contentCreated < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-266">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-267">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="15cd5-267">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="15cd5-268">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="15cd5-268">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="15cd5-269">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="15cd5-269">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="15cd5-270">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="15cd5-270">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="15cd5-271">De forma predeterminada, si se omiten startTime y endTime, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="15cd5-271">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="15cd5-272">**NOTA**: Aunque se puede especificar un valor de startTime y endTime con más de 24 horas de diferencia, no es recomendable.</span><span class="sxs-lookup"><span data-stu-id="15cd5-272">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="15cd5-273">Además, si obtiene algún resultado en respuesta a una solicitud de más de 24 horas, podrían ser resultados parciales y no deberían tenerse en cuenta.</span><span class="sxs-lookup"><span data-stu-id="15cd5-273">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="15cd5-274">La solicitud se debe emitir con un intervalo de no más de 24 horas entre los valores de startTime y endTime.</span><span class="sxs-lookup"><span data-stu-id="15cd5-274">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="15cd5-275">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-275">**Response**</span></span>|<span data-ttu-id="15cd5-276">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="15cd5-276">JSON array</span></span>|<span data-ttu-id="15cd5-277">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="15cd5-277">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-278"><b>contentType</b>: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-278"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="15cd5-279"><b>contentId</b>: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="15cd5-279"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="15cd5-280"><b>contentUri</b>: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-280"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="15cd5-281"><b>contentCreated</b>: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-281"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="15cd5-282"><b>contentExpiration</b>: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-282"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="15cd5-283">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-283">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-284">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-284">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="15cd5-285">Paginación</span><span class="sxs-lookup"><span data-stu-id="15cd5-285">Pagination</span></span>

<span data-ttu-id="15cd5-286">Al enumerar el contenido disponible para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="15cd5-286">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="15cd5-287">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncarán y se agregará un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-287">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="15cd5-288">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="15cd5-288">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="15cd5-289">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="15cd5-289">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="15cd5-290">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="15cd5-290">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="15cd5-291">Recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="15cd5-291">Receiving notifications</span></span>

<span data-ttu-id="15cd5-292">Las notificaciones se envían al webhook configurado para una suscripción cuando hay contenido nuevo disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-292">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="15cd5-293">Como la notificación incluye el identificador de espacio empresarial, puede usar el mismo webhook para recibir notificaciones para todos los espacios empresariales para los que tiene suscripciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-293">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="15cd5-294">La notificación se realiza como HTTP POST sobre TLS (TLS 1.0 y versiones posteriores) a la dirección del webhook especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-294">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="15cd5-295">Si la configuración de webhook incluye un identificador de autenticación, se enviará como un encabezado HTTP: Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="15cd5-295">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="15cd5-296">Cualquier respuesta distinta de HTTP 200 Correcto se considera un error y la notificación se volverá a intentar.</span><span class="sxs-lookup"><span data-stu-id="15cd5-296">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="15cd5-297">También puede configurar el webhook para requerir autenticación basada en certificados de cliente y se autenticará con el certificado manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="15cd5-297">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="15cd5-298">El cuerpo de la solicitud contendrá una matriz de uno o más objetos JSON que representan los blobs de contenido disponibles.</span><span class="sxs-lookup"><span data-stu-id="15cd5-298">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="15cd5-299">El número de blobs de contenido en cada notificación es limitado para que el tamaño de la notificación sea relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="15cd5-299">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="15cd5-300">Como este límite puede cambiar, la implementación debe consultar la longitud de la matriz en lugar de esperar un tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="15cd5-300">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="15cd5-301">Cada objeto incluirá las mismas propiedades que devuelve la operación /content, junto con el GUID del espacio empresarial al que corresponden los datos y el GUID de la aplicación que creó las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-301">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="15cd5-302">Esto permite al webhook establecer el contexto cuando se usa con varios espacios empresariales y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-302">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="15cd5-303">**tenantId**: el GUID del espacio empresarial al que pertenece el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-303">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="15cd5-304">**clientId**: el GUID de la aplicación que creó la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-304">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="15cd5-305">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-305">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="15cd5-306">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="15cd5-306">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="15cd5-307">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-307">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="15cd5-308">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-308">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="15cd5-309">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-309">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="15cd5-310">A continuación se muestra un ejemplo de una notificación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-310">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="15cd5-311">Error de notificación y reintento</span><span class="sxs-lookup"><span data-stu-id="15cd5-311">Notification failure and retry</span></span>

<span data-ttu-id="15cd5-312">El sistema de notificaciones envía las notificaciones cuando hay nuevo contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-312">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="15cd5-313">Si se producen errores excesivos al enviar las notificaciones, nuestro mecanismo de reintento aumentará de forma exponencial el tiempo entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="15cd5-313">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="15cd5-314">Si se siguen produciendo errores, nos reservamos el derecho de deshabilitar el webhook y detener por completo el envío de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-314">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="15cd5-315">Se puede usar la operación /start para volver a habilitar un webhook deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-315">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="15cd5-316">Recuperación de contenido</span><span class="sxs-lookup"><span data-stu-id="15cd5-316">Retrieving content</span></span>

<span data-ttu-id="15cd5-317">Para recuperar un blob de contenido, realice una solicitud GET en el URI del contenido correspondiente que se incluye en la lista de contenido disponible y en las notificaciones enviadas a un webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-317">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="15cd5-318">El contenido devuelto será una colección de una más acciones o eventos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="15cd5-318">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="15cd5-319">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-319">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-320">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-320">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="15cd5-321">Enumerar notificaciones</span><span class="sxs-lookup"><span data-stu-id="15cd5-321">List notifications</span></span>

<span data-ttu-id="15cd5-322">Esta operación enumera todos los intentos de notificación para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-322">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="15cd5-323">Si no ha incluido un webhook al iniciar la suscripción para el tipo de contenido, no existirá ninguna notificación para recuperar.</span><span class="sxs-lookup"><span data-stu-id="15cd5-323">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="15cd5-324">Como en caso de error se reintentan las notificaciones, esta operación puede devolver varias notificaciones para el mismo contenido, y el orden en el que se envían no coincidirá necesariamente con el orden en que el contenido está disponible (en especial si hay errores y reintentos).</span><span class="sxs-lookup"><span data-stu-id="15cd5-324">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="15cd5-325">Puede usar esta operación para ayudar a investigar problemas relacionados con los webhooks y las notificaciones, pero no debería usarla para determinar qué contenido está disponible actualmente para la recuperación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-325">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="15cd5-326">En su lugar, use la operación /content.</span><span class="sxs-lookup"><span data-stu-id="15cd5-326">Use the /content operation instead.</span></span> <span data-ttu-id="15cd5-327">Se devolverá un error si el estado de la suscripción es deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-327">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="15cd5-328">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-328">Subscription</span></span>|<span data-ttu-id="15cd5-329">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-329">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-330">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-330">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="15cd5-331">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-331">**Parameters**</span></span>|<span data-ttu-id="15cd5-332">contentType</span><span class="sxs-lookup"><span data-stu-id="15cd5-332">contentType</span></span>|<span data-ttu-id="15cd5-333">Debe ser un tipo de contenido válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-333">Must be a valid content type.</span></span>|
||<span data-ttu-id="15cd5-334">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-334">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-335">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-335">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-336">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-336">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-337">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-337">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-338">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-338">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-339">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-339">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="15cd5-340">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="15cd5-340">startTime endTime</span></span>|<span data-ttu-id="15cd5-341">Fechas y horas (UTC) opcionales que indican el intervalo de tiempo del contenido que se va a devolver, en función de cuándo está disponible ese contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-341">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="15cd5-342">El intervalo de tiempo es inclusivo con respecto a _startTime_ ( _startTime_ <= contentCreated) y exclusivo con respecto a _endTime_ (_contentCreated_ < endTime), de modo que se pueden usar intervalos de tiempo crecientes que no se superpongan para examinar el contenido disponible.</span><span class="sxs-lookup"><span data-stu-id="15cd5-342">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-343">AAAA-MM-DD</span><span class="sxs-lookup"><span data-stu-id="15cd5-343">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="15cd5-344">AAAA-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="15cd5-344">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="15cd5-345">AAAA-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="15cd5-345">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="15cd5-346">Se deben especificar los dos (o bien omitirse) y no debe haber una diferencia de más de 24 horas entre los dos, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="15cd5-346">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="15cd5-347">De forma predeterminada, si se omiten _startTime_ y _endTime_, se devuelve el contenido disponible en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="15cd5-347">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="15cd5-348">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-348">**Response**</span></span>|<span data-ttu-id="15cd5-349">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="15cd5-349">JSON array</span></span>|<span data-ttu-id="15cd5-350">Las notificaciones disponibles se representarán mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="15cd5-350">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="15cd5-351">**contentType**: indica el tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-351">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="15cd5-352">**contentId**: una cadena opaca que identifica el contenido de forma única.</span><span class="sxs-lookup"><span data-stu-id="15cd5-352">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="15cd5-353">**contentUri**: la dirección URL que se va a usar al recuperar el contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-353">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="15cd5-354">**contentCreated**: la fecha y hora de disponibilidad del contenido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-354">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="15cd5-355">**contentExpiration**: la fecha y hora después de la que el contenido ya no estará disponible para su recuperación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-355">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="15cd5-356">**notificationSent**: la fecha y hora de envío de la notificación.</span><span class="sxs-lookup"><span data-stu-id="15cd5-356">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="15cd5-357">**notificationStatus**: indica si intento de notificación se ha realizado correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="15cd5-357">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="15cd5-358">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-358">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-359">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-359">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="15cd5-360">Paginación</span><span class="sxs-lookup"><span data-stu-id="15cd5-360">Pagination</span></span>

<span data-ttu-id="15cd5-361">Al enumerar el historial de notificaciones para un intervalo de tiempo, el número de resultados devueltos está limitado para impedir tiempos de espera de respuesta.</span><span class="sxs-lookup"><span data-stu-id="15cd5-361">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="15cd5-362">Si en el intervalo de tiempo especificado hay más resultados de los que se pueden devolver en una única respuesta, los resultados se truncan y se agrega un encabezado a la respuesta en el que se indica la dirección URL que se va a usar para recuperar la siguiente página de resultados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-362">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="15cd5-363">La dirección URL contendrá los mismos parámetros _startTime_ y _endTime_ que se especificaron en la solicitud original, junto con un parámetro que indica el identificador interno de la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="15cd5-363">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="15cd5-364">Si no se especificaron los parámetros _startTime_ y _endTime_ en la solicitud original, se establecerán para reflejar el intervalo de 24 horas anterior a la solicitud original.</span><span class="sxs-lookup"><span data-stu-id="15cd5-364">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="15cd5-365">Para mostrar todo el contenido disponible para un intervalo de tiempo especificado, es posible que tenga que recuperar varias páginas hasta que reciba una respuesta sin el encabezado **NextPageUrl**.</span><span class="sxs-lookup"><span data-stu-id="15cd5-365">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="15cd5-366">Recuperar los nombres descriptivos de recurso</span><span class="sxs-lookup"><span data-stu-id="15cd5-366">Retrieve resource friendly names</span></span>

<span data-ttu-id="15cd5-367">Esta operación recupera los nombres descriptivos de los objetos de la fuente de datos identificados mediante GUID.</span><span class="sxs-lookup"><span data-stu-id="15cd5-367">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="15cd5-368">En la actualidad, el único objeto que se admite es "DlpSensitiveType".</span><span class="sxs-lookup"><span data-stu-id="15cd5-368">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="15cd5-369">Suscripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-369">Subscription</span></span>|<span data-ttu-id="15cd5-370">Descripción</span><span class="sxs-lookup"><span data-stu-id="15cd5-370">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="15cd5-371">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="15cd5-371">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="15cd5-372">**Parámetros**</span><span class="sxs-lookup"><span data-stu-id="15cd5-372">**Parameters**</span></span>|<span data-ttu-id="15cd5-373">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-373">PublisherIdentifier</span></span>|<span data-ttu-id="15cd5-374">El GUID de espacio empresarial del proveedor que codifica la API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-374">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="15cd5-375">Este **no** es el GUID de aplicación ni el del cliente que usa la aplicación, sino el GUID de la empresa que escribe el código.</span><span class="sxs-lookup"><span data-stu-id="15cd5-375">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="15cd5-376">Este parámetro se usa para limitar la velocidad de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-376">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="15cd5-377">Asegúrese de que este parámetro se especifica en todas las solicitudes emitidas para obtener una cuota dedicada.</span><span class="sxs-lookup"><span data-stu-id="15cd5-377">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="15cd5-378">Todas las solicitudes recibidas sin este parámetro compartirán la misma cuota.</span><span class="sxs-lookup"><span data-stu-id="15cd5-378">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="15cd5-379">**Encabezados**</span><span class="sxs-lookup"><span data-stu-id="15cd5-379">**Headers**</span></span>|<span data-ttu-id="15cd5-380">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="15cd5-380">Accept-Language</span></span>|<span data-ttu-id="15cd5-381">Encabezado para especificar el idioma que prefiere para los nombres localizados.</span><span class="sxs-lookup"><span data-stu-id="15cd5-381">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="15cd5-382">Por ejemplo, use "en-US" para inglés o "es" para español.</span><span class="sxs-lookup"><span data-stu-id="15cd5-382">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="15cd5-383">Si este encabezado no existe, se devolverá el idioma predeterminado (en-US).</span><span class="sxs-lookup"><span data-stu-id="15cd5-383">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="15cd5-384">**Cuerpo**</span><span class="sxs-lookup"><span data-stu-id="15cd5-384">**Body**</span></span>|<span data-ttu-id="15cd5-385">(vacío)</span><span class="sxs-lookup"><span data-stu-id="15cd5-385">(empty)</span></span>||
|<span data-ttu-id="15cd5-386">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="15cd5-386">**Response**</span></span>|<span data-ttu-id="15cd5-387">Matriz JSON</span><span class="sxs-lookup"><span data-stu-id="15cd5-387">JSON array</span></span>|<span data-ttu-id="15cd5-388">El contenido disponible se representará mediante objetos JSON con las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="15cd5-388">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-389"><b>id</b>: indica el GUID del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-389"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="15cd5-390"><b>name</b>: el nombre descriptivo del tipo de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-390"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="15cd5-391">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-391">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="15cd5-392">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="15cd5-392">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="15cd5-393">Limitación de API</span><span class="sxs-lookup"><span data-stu-id="15cd5-393">API throttling</span></span>

<span data-ttu-id="15cd5-394">Las organizaciones que tienen acceso a registros de auditoría a través de la API de Actividad de administración de Office 365 se restringieron con límites en el nivel de editor.</span><span class="sxs-lookup"><span data-stu-id="15cd5-394">Organizations that access auditing logs through the Office 365 Management Activity API were restricted by throttling limits at the publisher level.</span></span> <span data-ttu-id="15cd5-395">Esto significa que, para un editor que extrae datos en nombre de varios clientes, todos los clientes han compartido el límite.</span><span class="sxs-lookup"><span data-stu-id="15cd5-395">This means that for a publisher pulling data on behalf of multiple customers, the limit was shared by all those customers.</span></span>

<span data-ttu-id="15cd5-396">Estamos cambiando de un límite de nivel de editor a un límite de nivel de espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="15cd5-396">We're moving from a publisher-level limit to a tenant-level limit.</span></span> <span data-ttu-id="15cd5-397">El resultado es que cada organización obtendrá su propia cuota de ancho de banda completamente asignada para tener acceso a los datos de auditoría.</span><span class="sxs-lookup"><span data-stu-id="15cd5-397">The result is that each organization will get their own fully allocated bandwidth quota to access their auditing data.</span></span> <span data-ttu-id="15cd5-398">Se asigna inicialmente una línea base de 2 000 solicitudes por minuto a todas las organizaciones.</span><span class="sxs-lookup"><span data-stu-id="15cd5-398">All organizations are initially allocated a baseline of 2,000 requests per minute.</span></span> <span data-ttu-id="15cd5-399">Este no es un límite estático y predefinido, sino que se modela en base a una combinación de factores, incluido el número de puestos en la organización, y que las organizaciones de Office 365 y Microsoft 365 E5 tendrán aproximadamente el doble de ancho de banda que las organizaciones que no son E5.</span><span class="sxs-lookup"><span data-stu-id="15cd5-399">This is not a static, predefined limit but is modeled on a combination of factors including the number of seats in the organization and that Office 365 and Microsoft 365 E5 organizations will get approximately twice as much bandwidth as non-E5 organizations.</span></span> <span data-ttu-id="15cd5-400">También habrá un límite en el ancho de banda máximo para proteger el estado del servicio.</span><span class="sxs-lookup"><span data-stu-id="15cd5-400">There will also be cap on the maximum bandwidth to protect the health of the service.</span></span>

<span data-ttu-id="15cd5-401">Para obtener más información, vea la sección "acceso de banda ancha a la API de Actividad de administración de Office 365" en [Auditoría avanzada en Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span><span class="sxs-lookup"><span data-stu-id="15cd5-401">For more information, see the "High-bandwidth access to the Office 365 Management Activity API" section in [Advanced audit in Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span></span>

> [!NOTE] 
> <span data-ttu-id="15cd5-402">Aunque cada espacio empresarial puede enviar en un principio hasta 2 000 solicitudes por minuto, Microsoft no garantiza una velocidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="15cd5-402">Even though each tenant can initially submit up to 2,000 requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="15cd5-403">La velocidad de respuesta depende de varios factores, como el rendimiento del sistema cliente y la capacidad y la velocidad de la red.</span><span class="sxs-lookup"><span data-stu-id="15cd5-403">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span> 

## <a name="errors"></a><span data-ttu-id="15cd5-404">Errores</span><span class="sxs-lookup"><span data-stu-id="15cd5-404">Errors</span></span>

<span data-ttu-id="15cd5-405">Cuando el servicio encuentra un error, notificará el código de respuesta de error al autor de la llamada, mediante la sintaxis estándar de código de error de HTTP.</span><span class="sxs-lookup"><span data-stu-id="15cd5-405">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="15cd5-406">.</span><span class="sxs-lookup"><span data-stu-id="15cd5-406">.</span></span> <span data-ttu-id="15cd5-407">En el cuerpo de la llamada con error se incluye información adicional como un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="15cd5-407">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="15cd5-408">A continuación se muestra un ejemplo de un cuerpo completo de error JSON:</span><span class="sxs-lookup"><span data-stu-id="15cd5-408">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="15cd5-409">Código</span><span class="sxs-lookup"><span data-stu-id="15cd5-409">Code</span></span>|<span data-ttu-id="15cd5-410">Mensaje</span><span class="sxs-lookup"><span data-stu-id="15cd5-410">Message</span></span>|
|<span data-ttu-id="15cd5-411">AF10001</span><span class="sxs-lookup"><span data-stu-id="15cd5-411">AF10001</span></span>|<span data-ttu-id="15cd5-412">El conjunto de permisos ({0}) enviados en la solicitud no incluía el permiso esperado **ActivityFeed.Read**.</span><span class="sxs-lookup"><span data-stu-id="15cd5-412">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-413">{0} = el conjunto de permisos en el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="15cd5-413">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-414">AF20001</span><span class="sxs-lookup"><span data-stu-id="15cd5-414">AF20001</span></span>|<span data-ttu-id="15cd5-415">Falta el parámetro: {0}.</span><span class="sxs-lookup"><span data-stu-id="15cd5-415">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-416">{0} = el nombre del parámetro que falta.</span><span class="sxs-lookup"><span data-stu-id="15cd5-416">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-417">AF20002</span><span class="sxs-lookup"><span data-stu-id="15cd5-417">AF20002</span></span>|<span data-ttu-id="15cd5-418">Tipo de parámetro no válido: {0}.</span><span class="sxs-lookup"><span data-stu-id="15cd5-418">Invalid parameter type: {0}.</span></span> <span data-ttu-id="15cd5-419">Tipo esperado: {1}</span><span class="sxs-lookup"><span data-stu-id="15cd5-419">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-420">{0} = el nombre del parámetro no válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-420">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="15cd5-421">{1} = el tipo esperado (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="15cd5-421">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-422">AF20003</span><span class="sxs-lookup"><span data-stu-id="15cd5-422">AF20003</span></span>|<span data-ttu-id="15cd5-423">{0} de expiración proporcionada se establece en una fecha y hora pasadas.</span><span class="sxs-lookup"><span data-stu-id="15cd5-423">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-424">{0} = la expiración que se pasa en la llamada de API.</span><span class="sxs-lookup"><span data-stu-id="15cd5-424">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-425">AF20010</span><span class="sxs-lookup"><span data-stu-id="15cd5-425">AF20010</span></span>|<span data-ttu-id="15cd5-426">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no coincide con el que se pasa en el token de acceso ({1}).</span><span class="sxs-lookup"><span data-stu-id="15cd5-426">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-427">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="15cd5-427">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="15cd5-428">{1} = el identificador de espacio empresarial que se pasa en el token de acceso</span><span class="sxs-lookup"><span data-stu-id="15cd5-428">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-429">AF20011</span><span class="sxs-lookup"><span data-stu-id="15cd5-429">AF20011</span></span>|<span data-ttu-id="15cd5-430">El identificador de espacio empresarial ({0}) especificado no existe en el sistema o se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-430">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="15cd5-431">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="15cd5-431">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-432">AF20012</span><span class="sxs-lookup"><span data-stu-id="15cd5-432">AF20012</span></span>|<span data-ttu-id="15cd5-433">El identificador de espacio empresarial ({0}) especificado no está configurado correctamente en el sistema.</span><span class="sxs-lookup"><span data-stu-id="15cd5-433">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="15cd5-434">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="15cd5-434">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-435">AF20013</span><span class="sxs-lookup"><span data-stu-id="15cd5-435">AF20013</span></span>|<span data-ttu-id="15cd5-436">El identificador de espacio empresarial que se pasa en la dirección URL ({0}) no es un GUID válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-436">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="15cd5-437">{0} = el identificador de espacio empresarial que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="15cd5-437">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-438">AF20020</span><span class="sxs-lookup"><span data-stu-id="15cd5-438">AF20020</span></span>|<span data-ttu-id="15cd5-439">El tipo de contenido especificado no es válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-439">The specified content type is not valid.</span></span>|
|<span data-ttu-id="15cd5-440">AF20021</span><span class="sxs-lookup"><span data-stu-id="15cd5-440">AF20021</span></span>|<span data-ttu-id="15cd5-441">El punto de conexión de webhook {{0}) no se pudo validar.</span><span class="sxs-lookup"><span data-stu-id="15cd5-441">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="15cd5-442">{1}</span><span class="sxs-lookup"><span data-stu-id="15cd5-442">{1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-443">{0} = dirección del webhook.</span><span class="sxs-lookup"><span data-stu-id="15cd5-443">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="15cd5-444">{1} = "El punto de conexión no devolvió HTTP 200".</span><span class="sxs-lookup"><span data-stu-id="15cd5-444">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="15cd5-445">o bien, "La dirección debe comenzar con HTTPS".</span><span class="sxs-lookup"><span data-stu-id="15cd5-445">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-446">AF20022</span><span class="sxs-lookup"><span data-stu-id="15cd5-446">AF20022</span></span>|<span data-ttu-id="15cd5-447">No se encontró ninguna suscripción para el tipo de contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-447">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="15cd5-448">AF20023</span><span class="sxs-lookup"><span data-stu-id="15cd5-448">AF20023</span></span>|<span data-ttu-id="15cd5-449">{0} ha deshabilitado la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15cd5-449">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-450">{0} = "un administrador de espacio empresarial" o "un administrador de servicio"</span><span class="sxs-lookup"><span data-stu-id="15cd5-450">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-451">AF20030</span><span class="sxs-lookup"><span data-stu-id="15cd5-451">AF20030</span></span>|<span data-ttu-id="15cd5-452">Se debe especificar la hora de inicio y la hora de finalización (o bien omitirse), con una diferencia menor o igual de 24 horas, y la hora de inicio no debe tener más de siete días de antigüedad. </span><span class="sxs-lookup"><span data-stu-id="15cd5-452">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="15cd5-453">AF20031</span><span class="sxs-lookup"><span data-stu-id="15cd5-453">AF20031</span></span>|<span data-ttu-id="15cd5-454">Entrada nextPage no válida: {0}.</span><span class="sxs-lookup"><span data-stu-id="15cd5-454">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-455">{0} = el indicador de página siguiente que se pasa en la dirección URL</span><span class="sxs-lookup"><span data-stu-id="15cd5-455">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-456">AF20050</span><span class="sxs-lookup"><span data-stu-id="15cd5-456">AF20050</span></span>|<span data-ttu-id="15cd5-457">No existe el contenido especificado ({0}).</span><span class="sxs-lookup"><span data-stu-id="15cd5-457">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-458">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="15cd5-458">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-459">AF20051</span><span class="sxs-lookup"><span data-stu-id="15cd5-459">AF20051</span></span>|<span data-ttu-id="15cd5-460">El contenido solicitado con la clave {0} ya ha expirado.</span><span class="sxs-lookup"><span data-stu-id="15cd5-460">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="15cd5-461">El contenido de más de siete días no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="15cd5-461">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-462">•    {0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="15cd5-462">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-463">AF20052</span><span class="sxs-lookup"><span data-stu-id="15cd5-463">AF20052</span></span>|<span data-ttu-id="15cd5-464">El identificador de contenido {0} en la dirección URL no es válido.</span><span class="sxs-lookup"><span data-stu-id="15cd5-464">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-465">{0} = identificador o dirección URL del recurso</span><span class="sxs-lookup"><span data-stu-id="15cd5-465">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-466">AF20053</span><span class="sxs-lookup"><span data-stu-id="15cd5-466">AF20053</span></span>|<span data-ttu-id="15cd5-467">Solo puede haber un idioma en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="15cd5-467">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="15cd5-468">AF20054</span><span class="sxs-lookup"><span data-stu-id="15cd5-468">AF20054</span></span>|<span data-ttu-id="15cd5-469">Sintaxis incorrecta en el encabezado Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="15cd5-469">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="15cd5-470">AF429</span><span class="sxs-lookup"><span data-stu-id="15cd5-470">AF429</span></span>|<span data-ttu-id="15cd5-471">Demasiadas solicitudes.</span><span class="sxs-lookup"><span data-stu-id="15cd5-471">Too many requests.</span></span> <span data-ttu-id="15cd5-472">Método={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="15cd5-472">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="15cd5-473">{0} = método HTTP</span><span class="sxs-lookup"><span data-stu-id="15cd5-473">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="15cd5-474">{1} = GUID de espacio empresarial usado como PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="15cd5-474">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="15cd5-475">AF50000</span><span class="sxs-lookup"><span data-stu-id="15cd5-475">AF50000</span></span>|<span data-ttu-id="15cd5-476">Se ha producido un error interno.</span><span class="sxs-lookup"><span data-stu-id="15cd5-476">An internal error occurred.</span></span> <span data-ttu-id="15cd5-477">Vuelva a intentar realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15cd5-477">Retry the request.</span></span>|
