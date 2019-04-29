---
ms.TocTitle: Office 365 Service Communications API reference (preview)
title: Referencia de API de comunicaciones de servicio de Office 365
description: 'Use esta API para obtener acceso a los datos siguientes: Get Services, Get Current Status, Get Historical Status y Get Messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 9b38c4ee73f18bf10c7fa7cbb5b323740dfb5a7e
ms.sourcegitcommit: 336f901a6ed8eb75d99baa4af37d838aeec905c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "33440055"
---
# <a name="office-365-service-communications-api-reference-preview"></a><span data-ttu-id="89a18-103">Referencia de API de comunicaciones de servicio de Office 365</span><span class="sxs-lookup"><span data-stu-id="89a18-103">Office 365 Service Communications API reference (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="89a18-104">En esta documentación, se describen características que están actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="89a18-104">This documentation covers features that are currently in preview.</span></span>

<span data-ttu-id="89a18-105">Puede usar la API de comunicaciones de servicio de Office 365 versión 2.0 para obtener acceso a los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="89a18-105">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="89a18-106">**Get Services**: obtiene la lista de servicios suscritos.</span><span class="sxs-lookup"><span data-stu-id="89a18-106">**Get Services**: Get the list of subscribed services.</span></span>
    
- <span data-ttu-id="89a18-107">**Get Current Status**: obtiene una vista en tiempo real de los eventos de mantenimiento y los incidentes de servicio actuales y continuados</span><span class="sxs-lookup"><span data-stu-id="89a18-107">**Get Current Status**: Get a real-time view of current and ongoing service incidents and maintenance events</span></span>
    
- <span data-ttu-id="89a18-108">**Get Historical Status**: obtiene una vista del historial de estado del servicio, incluidos incidentes de servicio y eventos de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="89a18-108">**Get Historical Status**: Get a historical view of service health, including service incidents and maintenance events.</span></span>
    
- <span data-ttu-id="89a18-109">**Get Messages**: encuentra comunicaciones del Centro de mensajes, de mantenimiento planeado y de incidentes.</span><span class="sxs-lookup"><span data-stu-id="89a18-109">**Get Messages**: Find Incident, Planned Maintenance, and Message Center communications.</span></span>
    
<span data-ttu-id="89a18-110">Actualmente, la API de comunicaciones de servicio de Office 365 contiene datos para estos servicios: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, servicio de identidad, administración de dispositivos móviles, Centro de administración de Partners de Office 365, OneDrive para la Empresa, Parature, OneDrive para la Empresa, Power BI para Office 365, servicio Rights Management, SharePoint Online, Administrador de SHD, Skype Empresarial, Social Engagement y Yammer Enterprise.</span><span class="sxs-lookup"><span data-stu-id="89a18-110">Currently, the Office 365 Service Communications API contains data for the following services: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement, and Yammer Enterprise.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="89a18-111">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="89a18-111">The fundamentals</span></span>

<span data-ttu-id="89a18-112">La URL raíz de la API contiene un identificador de espacio empresarial que establece los ámbitos de las operaciones en un único espacio empresarial:</span><span class="sxs-lookup"><span data-stu-id="89a18-112">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="89a18-113">La **API de comunicaciones de servicio de Office 365** es un servicio REST que le permite desarrollar soluciones con cualquier lenguaje web y entorno de hospedaje que admita HTTPS y los certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="89a18-113">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="89a18-114">La API usa **Microsoft Azure Active Directory** y el protocolo **OAuth2** para la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="89a18-114">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="89a18-115">Para obtener acceso a la API desde la aplicación, primero tendrá que registrarla en Azure AD y configurarla con los permisos en el ámbito adecuado.</span><span class="sxs-lookup"><span data-stu-id="89a18-115">To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope.</span></span> <span data-ttu-id="89a18-116">Esto permitirá a la aplicación solicitar los tokens de acceso de OAuth2 necesarios para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="89a18-116">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="89a18-117">Para obtener más información sobre cómo registrar y configurar una aplicación en Azure AD, vea [Introducción a las API de administración de Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="89a18-117">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="89a18-118">Todas las solicitudes API necesitan el encabezado HTTP de autorización que tiene un token de acceso OAuth2 JWT válido obtenido de Azure AD que contiene la notificación **ServiceHealth.Read**; además, el identificador del espacio empresarial tiene que coincidir con el identificador de espacio empresarial de la URL raíz.</span><span class="sxs-lookup"><span data-stu-id="89a18-118">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

<span data-ttu-id="89a18-119">**Encabezados de solicitud**</span><span class="sxs-lookup"><span data-stu-id="89a18-119">**Request headers**</span></span>

<span data-ttu-id="89a18-120">Estos son los encabezados de solicitud compatibles con todas las operaciones de la API de comunicaciones de servicio de Office 365.</span><span class="sxs-lookup"><span data-stu-id="89a18-120">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="89a18-121">Encabezado</span><span class="sxs-lookup"><span data-stu-id="89a18-121">Header</span></span>|<span data-ttu-id="89a18-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-122">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="89a18-123">**Accept (opcional)**</span><span class="sxs-lookup"><span data-stu-id="89a18-123">**Accept (Optional)**</span></span>|<span data-ttu-id="89a18-124">Las opciones siguientes son representaciones aceptables de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="89a18-124">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="89a18-125">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="89a18-125">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="89a18-126">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="89a18-126">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="89a18-127">[El valor predeterminado si no se especifica el encabezado] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="89a18-127">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="89a18-128">**Autorización (obligatorio)**</span><span class="sxs-lookup"><span data-stu-id="89a18-128">**Authorization (Required)**</span></span>|<span data-ttu-id="89a18-129">Token de autorización (token de portador de JWT Azure AD) para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="89a18-129">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|


<br/>

<span data-ttu-id="89a18-130">**Encabezados de respuesta**</span><span class="sxs-lookup"><span data-stu-id="89a18-130">**Response headers**</span></span>

<span data-ttu-id="89a18-131">Encabezados de respuesta devueltos por todas las operaciones de la API de comunicaciones de servicio de Office 365:</span><span class="sxs-lookup"><span data-stu-id="89a18-131">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="89a18-132">Encabezado</span><span class="sxs-lookup"><span data-stu-id="89a18-132">Header</span></span>|<span data-ttu-id="89a18-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-133">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="89a18-134">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="89a18-134">**Content-Length**</span></span>|<span data-ttu-id="89a18-135">Longitud del cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="89a18-135">The length of the response body.</span></span>|
|<span data-ttu-id="89a18-136">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="89a18-136">**Content-Type**</span></span>|<span data-ttu-id="89a18-137">Representación de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="89a18-137">Representation of the response:</span></span><br/><span data-ttu-id="89a18-138">**application/json**</span><span class="sxs-lookup"><span data-stu-id="89a18-138">**application/json**</span></span><br/><span data-ttu-id="89a18-139">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="89a18-139">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="89a18-140">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="89a18-140">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="89a18-141">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="89a18-141">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="89a18-142">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="89a18-142">**odata.streaming=true**</span></span>|
|<span data-ttu-id="89a18-143">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="89a18-143">**Cache-Control**</span></span>|<span data-ttu-id="89a18-144">Se usa para especificar directivas que tienen que obedecer todos los mecanismos de almacenamiento en caché, así como la cadena de solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="89a18-144">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="89a18-145">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="89a18-145">**Pragma**</span></span>|<span data-ttu-id="89a18-146">Comportamientos específicos de cada implementación.</span><span class="sxs-lookup"><span data-stu-id="89a18-146">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="89a18-147">**Expires**</span><span class="sxs-lookup"><span data-stu-id="89a18-147">**Expires**</span></span>|<span data-ttu-id="89a18-148">Cuándo tiene que expirar el recurso el cliente.</span><span class="sxs-lookup"><span data-stu-id="89a18-148">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="89a18-149">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="89a18-149">**X-Activity-Id**</span></span>|<span data-ttu-id="89a18-150">Id. de actividad generado por el servidor.</span><span class="sxs-lookup"><span data-stu-id="89a18-150">The server-generated activity Id.</span></span>|
|<span data-ttu-id="89a18-151">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="89a18-151">**OData-Version**</span></span>|<span data-ttu-id="89a18-152">Versión de OData admitida (4.0).</span><span class="sxs-lookup"><span data-stu-id="89a18-152">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="89a18-153">**Date**</span><span class="sxs-lookup"><span data-stu-id="89a18-153">**Date**</span></span>|<span data-ttu-id="89a18-154">Fecha en formato UTC en que se envió la respuesta desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="89a18-154">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="89a18-155">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="89a18-155">**X-Time-Taken**</span></span>|<span data-ttu-id="89a18-156">Tiempo necesario para generar la respuesta (ms).</span><span class="sxs-lookup"><span data-stu-id="89a18-156">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="89a18-157">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="89a18-157">**X-Instance-Name**</span></span>|<span data-ttu-id="89a18-158">Identificador de la instancia de Azure usado para generar la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="89a18-158">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="89a18-159">**Server**</span><span class="sxs-lookup"><span data-stu-id="89a18-159">**Server**</span></span>|<span data-ttu-id="89a18-160">Servidor usado para generar la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="89a18-160">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="89a18-161">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="89a18-161">**X-ASPNET-Version**</span></span>|<span data-ttu-id="89a18-162">Versión de ASP.NET usada por el servidor que generó la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="89a18-162">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="89a18-163">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="89a18-163">**X-Powered-By**</span></span>|<span data-ttu-id="89a18-164">Tecnologías usadas en el servidor que generó la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="89a18-164">The technologies used in the server that generated the response (for debugging purposes).</span></span>|

<br/>

<span data-ttu-id="89a18-165">Estas son las operaciones de la API de comunicaciones de servicio de Office 365.</span><span class="sxs-lookup"><span data-stu-id="89a18-165">Following are the Office 365 Service Communications API operations.</span></span>


## <a name="get-services"></a><span data-ttu-id="89a18-166">Get Services</span><span class="sxs-lookup"><span data-stu-id="89a18-166">Get Services</span></span>

<span data-ttu-id="89a18-167">Devuelve la lista de los servicios suscritos.</span><span class="sxs-lookup"><span data-stu-id="89a18-167">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="89a18-168">Servicio</span><span class="sxs-lookup"><span data-stu-id="89a18-168">Service</span></span>|<span data-ttu-id="89a18-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-169">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89a18-170">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="89a18-170">**Path**</span></span>| `/Services`||
|<span data-ttu-id="89a18-171">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="89a18-171">**Query-option**</span></span>|<span data-ttu-id="89a18-172">$select</span><span class="sxs-lookup"><span data-stu-id="89a18-172">$select</span></span>|<span data-ttu-id="89a18-173">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="89a18-173">Pick a subset of properties.</span></span>|
|<span data-ttu-id="89a18-174">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89a18-174">**Response**</span></span>|<span data-ttu-id="89a18-175">Lista de entidades de “Service”</span><span class="sxs-lookup"><span data-stu-id="89a18-175">List of "Service" entities</span></span>|<span data-ttu-id="89a18-176">La entidad “Service” contiene “Id” (cadena), “DisplayName” (cadena) y “FeatureNames” (lista de cadenas).</span><span class="sxs-lookup"><span data-stu-id="89a18-176">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="89a18-177">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-177">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

#### <a name="sample-response"></a><span data-ttu-id="89a18-178">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-178">Sample response</span></span>

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


## <a name="get-current-status"></a><span data-ttu-id="89a18-179">Get Current Status</span><span class="sxs-lookup"><span data-stu-id="89a18-179">Get Current Status</span></span>

<span data-ttu-id="89a18-180">Devuelve el estado del servicio durante las 24 horas anteriores.</span><span class="sxs-lookup"><span data-stu-id="89a18-180">Returns the status of the service over the previous 24 hours.</span></span>

||<span data-ttu-id="89a18-181">Servicio</span><span class="sxs-lookup"><span data-stu-id="89a18-181">Service</span></span>|<span data-ttu-id="89a18-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-182">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89a18-183">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="89a18-183">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="89a18-184">**Filtro**</span><span class="sxs-lookup"><span data-stu-id="89a18-184">**Filter**</span></span>|<span data-ttu-id="89a18-185">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="89a18-185">Workload</span></span>|<span data-ttu-id="89a18-186">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-186">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="89a18-187">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="89a18-187">**Query-option**</span></span>|<span data-ttu-id="89a18-188">$select</span><span class="sxs-lookup"><span data-stu-id="89a18-188">$select</span></span>|<span data-ttu-id="89a18-189">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="89a18-189">Pick a subset of properties.</span></span>|
|<span data-ttu-id="89a18-190">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89a18-190">**Response**</span></span>|<span data-ttu-id="89a18-191">Lista de entidades “WorkloadStatus”.</span><span class="sxs-lookup"><span data-stu-id="89a18-191">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="89a18-192">La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).</span><span class="sxs-lookup"><span data-stu-id="89a18-192">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="89a18-193">La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).</span><span class="sxs-lookup"><span data-stu-id="89a18-193">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="89a18-194">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-194">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="89a18-195">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-195">Sample response</span></span>

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


## <a name="get-historical-status"></a><span data-ttu-id="89a18-196">Get Historical Status</span><span class="sxs-lookup"><span data-stu-id="89a18-196">Get Historical Status</span></span>

<span data-ttu-id="89a18-197">Devuelve el historial de estado del servicio, por día, en un intervalo de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="89a18-197">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="89a18-198">Servicio</span><span class="sxs-lookup"><span data-stu-id="89a18-198">Service</span></span>|<span data-ttu-id="89a18-199">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89a18-200">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="89a18-200">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="89a18-201">**Filtros**</span><span class="sxs-lookup"><span data-stu-id="89a18-201">**Filters**</span></span>|<span data-ttu-id="89a18-202">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="89a18-202">Workload</span></span>|<span data-ttu-id="89a18-203">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-203">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="89a18-204">StatusTime</span><span class="sxs-lookup"><span data-stu-id="89a18-204">StatusTime</span></span>|<span data-ttu-id="89a18-205">Permite filtrar por número de días superior a StatusTime (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).</span><span class="sxs-lookup"><span data-stu-id="89a18-205">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="89a18-206">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="89a18-206">**Query-option**</span></span>|<span data-ttu-id="89a18-207">$select</span><span class="sxs-lookup"><span data-stu-id="89a18-207">$select</span></span>|<span data-ttu-id="89a18-208">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="89a18-208">Pick a subset of properties.</span></span>|
|<span data-ttu-id="89a18-209">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89a18-209">**Response**</span></span>|<span data-ttu-id="89a18-210">Lista de entidades “WorkloadStatus”.</span><span class="sxs-lookup"><span data-stu-id="89a18-210">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="89a18-211">La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).</span><span class="sxs-lookup"><span data-stu-id="89a18-211">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="89a18-212">La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).</span><span class="sxs-lookup"><span data-stu-id="89a18-212">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="89a18-213">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-213">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="89a18-214">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-214">Sample response</span></span>

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


## <a name="get-messages"></a><span data-ttu-id="89a18-215">Get Messages</span><span class="sxs-lookup"><span data-stu-id="89a18-215">Get Messages</span></span>

<span data-ttu-id="89a18-216">Devuelve los mensajes sobre el servicio en un intervalo de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="89a18-216">Returns the messages about the service over a certain time range.</span></span> <span data-ttu-id="89a18-217">Use el filtro de tipo para filtrar por mensajes de “incidentes en el servicio”, “mantenimiento planeado” o del “Centro de mensajes”.</span><span class="sxs-lookup"><span data-stu-id="89a18-217">Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="89a18-218">Servicio</span><span class="sxs-lookup"><span data-stu-id="89a18-218">Service</span></span>|<span data-ttu-id="89a18-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="89a18-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89a18-220">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="89a18-220">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="89a18-221">**Filtros**</span><span class="sxs-lookup"><span data-stu-id="89a18-221">**Filters**</span></span>|<span data-ttu-id="89a18-222">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="89a18-222">Workload</span></span>|<span data-ttu-id="89a18-223">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-223">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="89a18-224">StartTime</span><span class="sxs-lookup"><span data-stu-id="89a18-224">StartTime</span></span>|<span data-ttu-id="89a18-225">Permite filtrar por hora de inicio (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).</span><span class="sxs-lookup"><span data-stu-id="89a18-225">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="89a18-226">EndTime</span><span class="sxs-lookup"><span data-stu-id="89a18-226">EndTime</span></span>|<span data-ttu-id="89a18-227">Permite filtrar por hora de finalización (DateTimeOffset, predeterminado: le CurrentTime).</span><span class="sxs-lookup"><span data-stu-id="89a18-227">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="89a18-228">MessageType</span><span class="sxs-lookup"><span data-stu-id="89a18-228">MessageType</span></span>|<span data-ttu-id="89a18-229">Permite filtrar por MessageType (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-229">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="89a18-230">ID</span><span class="sxs-lookup"><span data-stu-id="89a18-230">ID</span></span>|<span data-ttu-id="89a18-231">Permite filtrar por id. (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-231">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="89a18-232">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="89a18-232">**Query-option**</span></span>|<span data-ttu-id="89a18-233">$select</span><span class="sxs-lookup"><span data-stu-id="89a18-233">$select</span></span>|<span data-ttu-id="89a18-234">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="89a18-234">Pick a subset of properties.</span></span>|
||<span data-ttu-id="89a18-235">$top</span><span class="sxs-lookup"><span data-stu-id="89a18-235">$top</span></span>|<span data-ttu-id="89a18-236">Selecciona el mayor número de resultados (predeterminado y máximo $top=100).</span><span class="sxs-lookup"><span data-stu-id="89a18-236">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="89a18-237">$skip</span><span class="sxs-lookup"><span data-stu-id="89a18-237">$skip</span></span>|<span data-ttu-id="89a18-238">Omite el número de resultados (predeterminado: $skip=0).</span><span class="sxs-lookup"><span data-stu-id="89a18-238">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="89a18-239">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="89a18-239">**Response**</span></span>|<span data-ttu-id="89a18-240">Lista de entidades de “Message”.</span><span class="sxs-lookup"><span data-stu-id="89a18-240">List of "Message" entities.</span></span>|<span data-ttu-id="89a18-241">La entidad “Message” contiene “Id” (cadena), “StartTime” (DateTimeOffset), “EndTime” (DateTimeOffset), “Status” (cadena), “Messages” (lista de la entidad “MessageHistory”), “LastUpdatedTime” (DateTimeOffset), “Workload” (cadena), “WorkloadDisplayName” (cadena), “Feature” (cadena), “FeatureDisplayName” (cadena), “MessageType” (enumeración, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="89a18-241">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessageHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="89a18-242">La entidad “MessageHistory” contiene “PublishedTime” (DateTimeOffset), “MessageText” (cadena).</span><span class="sxs-lookup"><span data-stu-id="89a18-242">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="89a18-243">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-243">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="89a18-244">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="89a18-244">Sample response</span></span>

```json
{
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


## <a name="errors"></a><span data-ttu-id="89a18-245">Errores</span><span class="sxs-lookup"><span data-stu-id="89a18-245">Errors</span></span>

<span data-ttu-id="89a18-246">Cuando el servicio encuentre un error, indicará el código de respuesta de error al autor de la llamada mediante la sintaxis estándar de código de error de HTTP.</span><span class="sxs-lookup"><span data-stu-id="89a18-246">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="89a18-247">Según la [especificación de OData versión 4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), se incluye información adicional en el cuerpo de la llamada con errores como un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="89a18-247">As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="89a18-248">Abajo se muestra un ejemplo del cuerpo completo de un error en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="89a18-248">The following is an example of a full JSON error body:</span></span>


```json

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

