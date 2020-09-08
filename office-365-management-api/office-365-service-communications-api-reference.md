---
ms.TocTitle: Office 365 Service Communications API reference
title: Referencia de API de comunicaciones de servicio de Office 365
description: 'Use esta API para obtener acceso a los datos siguientes: Get Services, Get Current Status, Get Historical Status y Get Messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: a7e99a5920afa03891ac3f48982cdaf40a660e2a
ms.sourcegitcommit: e9de9dea24789e64be9e7161e5e5de9cb4f9797d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2020
ms.locfileid: "47399539"
---
# <a name="office-365-service-communications-api-reference"></a><span data-ttu-id="4065a-103">Referencia de API de comunicaciones de servicio de Office 365</span><span class="sxs-lookup"><span data-stu-id="4065a-103">Office 365 Service Communications API reference</span></span>

<span data-ttu-id="4065a-104">Puede usar la API de comunicaciones de servicio de Office 365 versión 2.0 para obtener acceso a los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4065a-104">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="4065a-105">**Get Services**: obtiene la lista de servicios suscritos.</span><span class="sxs-lookup"><span data-stu-id="4065a-105">**Get Services**: Get the list of subscribed services.</span></span>

- <span data-ttu-id="4065a-106">**Get Current Status**: proporciona una vista en tiempo real de las incidencias de servicio actuales y en curso</span><span class="sxs-lookup"><span data-stu-id="4065a-106">**Get Current Status**: Get a real-time view of current and ongoing service incidents.</span></span>

- <span data-ttu-id="4065a-107">**Get Historical Status**: proporciona una vista histórica de incidencias de servicio.</span><span class="sxs-lookup"><span data-stu-id="4065a-107">**Get Historical Status**: Get a historical view of service incidents.</span></span>

- <span data-ttu-id="4065a-108">**Get Messages**: encuentra comunicaciones de Incidencias y del Centro de mensajes.</span><span class="sxs-lookup"><span data-stu-id="4065a-108">**Get Messages**: Find Incident and Message Center communications.</span></span>

<span data-ttu-id="4065a-109">Actualmente, la API de comunicaciones de servicio de Office 365 contiene datos de los servicios en la nube de Office 365, Yammer, Dynamics CRM y Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="4065a-109">Currently, the Office 365 Service Communications API contains data for Office 365, Yammer, Dynamics CRM and Microsoft Intune cloud services.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="4065a-110">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="4065a-110">The fundamentals</span></span>

<span data-ttu-id="4065a-111">La URL raíz de la API contiene un identificador de espacio empresarial que establece los ámbitos de las operaciones en un único espacio empresarial:</span><span class="sxs-lookup"><span data-stu-id="4065a-111">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="4065a-112">La **API de comunicaciones de servicio de Office 365** es un servicio REST que le permite desarrollar soluciones con cualquier lenguaje web y entorno de hospedaje que admita HTTPS y los certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="4065a-112">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="4065a-113">La API usa **Microsoft Azure Active Directory** y el protocolo **OAuth2** para la autenticación y autorización.</span><span class="sxs-lookup"><span data-stu-id="4065a-113">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="4065a-114">Para obtener acceso a la API desde la aplicación, primero tendrá que registrarla en Azure AD y configurarla con los permisos en el ámbito adecuado.</span><span class="sxs-lookup"><span data-stu-id="4065a-114">To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope.</span></span> <span data-ttu-id="4065a-115">Esto permitirá a la aplicación solicitar los tokens de acceso de OAuth2 necesarios para llamar a la API.</span><span class="sxs-lookup"><span data-stu-id="4065a-115">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="4065a-116">Para obtener más información sobre cómo registrar y configurar una aplicación en Azure AD, vea [Introducción a las API de administración de Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="4065a-116">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="4065a-117">Todas las solicitudes API necesitan el encabezado HTTP de autorización que tiene un token de acceso OAuth2 JWT válido obtenido de Azure AD que contiene la notificación **ServiceHealth.Read**; además, el identificador del espacio empresarial tiene que coincidir con el identificador de espacio empresarial de la URL raíz.</span><span class="sxs-lookup"><span data-stu-id="4065a-117">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

### <a name="request-headers"></a><span data-ttu-id="4065a-118">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="4065a-118">Request headers</span></span>

<span data-ttu-id="4065a-119">Estos son los encabezados de solicitud compatibles con todas las operaciones de la API de comunicaciones de servicio de Office 365.</span><span class="sxs-lookup"><span data-stu-id="4065a-119">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="4065a-120">Encabezado</span><span class="sxs-lookup"><span data-stu-id="4065a-120">Header</span></span>|<span data-ttu-id="4065a-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-121">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="4065a-122">**Accept (opcional)**</span><span class="sxs-lookup"><span data-stu-id="4065a-122">**Accept (Optional)**</span></span>|<span data-ttu-id="4065a-123">Las opciones siguientes son representaciones aceptables de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="4065a-123">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="4065a-124">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="4065a-124">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="4065a-125">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="4065a-125">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="4065a-126">[El valor predeterminado si no se especifica el encabezado] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="4065a-126">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="4065a-127">**Autorización (obligatorio)**</span><span class="sxs-lookup"><span data-stu-id="4065a-127">**Authorization (Required)**</span></span>|<span data-ttu-id="4065a-128">Token de autorización (token de portador de JWT Azure AD) para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="4065a-128">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|

<br/>

### <a name="response-headers"></a><span data-ttu-id="4065a-129">Encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="4065a-129">Response headers</span></span>

<span data-ttu-id="4065a-130">Encabezados de respuesta devueltos por todas las operaciones de la API de comunicaciones de servicio de Office 365:</span><span class="sxs-lookup"><span data-stu-id="4065a-130">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="4065a-131">Encabezado</span><span class="sxs-lookup"><span data-stu-id="4065a-131">Header</span></span>|<span data-ttu-id="4065a-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-132">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="4065a-133">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="4065a-133">**Content-Length**</span></span>|<span data-ttu-id="4065a-134">Longitud del cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="4065a-134">The length of the response body.</span></span>|
|<span data-ttu-id="4065a-135">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="4065a-135">**Content-Type**</span></span>|<span data-ttu-id="4065a-136">Representación de la respuesta:</span><span class="sxs-lookup"><span data-stu-id="4065a-136">Representation of the response:</span></span><br/><span data-ttu-id="4065a-137">**application/json**</span><span class="sxs-lookup"><span data-stu-id="4065a-137">**application/json**</span></span><br/><span data-ttu-id="4065a-138">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="4065a-138">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="4065a-139">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="4065a-139">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="4065a-140">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="4065a-140">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="4065a-141">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="4065a-141">**odata.streaming=true**</span></span>|
|<span data-ttu-id="4065a-142">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="4065a-142">**Cache-Control**</span></span>|<span data-ttu-id="4065a-143">Se usa para especificar directivas que tienen que obedecer todos los mecanismos de almacenamiento en caché, así como la cadena de solicitud o respuesta.</span><span class="sxs-lookup"><span data-stu-id="4065a-143">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="4065a-144">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="4065a-144">**Pragma**</span></span>|<span data-ttu-id="4065a-145">Comportamientos específicos de cada implementación.</span><span class="sxs-lookup"><span data-stu-id="4065a-145">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="4065a-146">**Expires**</span><span class="sxs-lookup"><span data-stu-id="4065a-146">**Expires**</span></span>|<span data-ttu-id="4065a-147">Cuándo tiene que expirar el recurso el cliente.</span><span class="sxs-lookup"><span data-stu-id="4065a-147">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="4065a-148">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="4065a-148">**X-Activity-Id**</span></span>|<span data-ttu-id="4065a-149">Id. de actividad generado por el servidor.</span><span class="sxs-lookup"><span data-stu-id="4065a-149">The server-generated activity Id.</span></span>|
|<span data-ttu-id="4065a-150">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="4065a-150">**OData-Version**</span></span>|<span data-ttu-id="4065a-151">Versión de OData admitida (4.0).</span><span class="sxs-lookup"><span data-stu-id="4065a-151">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="4065a-152">**Date**</span><span class="sxs-lookup"><span data-stu-id="4065a-152">**Date**</span></span>|<span data-ttu-id="4065a-153">Fecha en formato UTC en que se envió la respuesta desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="4065a-153">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="4065a-154">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="4065a-154">**X-Time-Taken**</span></span>|<span data-ttu-id="4065a-155">Tiempo necesario para generar la respuesta (ms).</span><span class="sxs-lookup"><span data-stu-id="4065a-155">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="4065a-156">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="4065a-156">**X-Instance-Name**</span></span>|<span data-ttu-id="4065a-157">Identificador de la instancia de Azure usado para generar la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="4065a-157">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="4065a-158">**Server**</span><span class="sxs-lookup"><span data-stu-id="4065a-158">**Server**</span></span>|<span data-ttu-id="4065a-159">Servidor usado para generar la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="4065a-159">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="4065a-160">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="4065a-160">**X-ASPNET-Version**</span></span>|<span data-ttu-id="4065a-161">Versión de ASP.NET usada por el servidor que generó la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="4065a-161">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="4065a-162">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="4065a-162">**X-Powered-By**</span></span>|<span data-ttu-id="4065a-163">Tecnologías usadas en el servidor que generó la respuesta (con fines de depuración).</span><span class="sxs-lookup"><span data-stu-id="4065a-163">The technologies used in the server that generated the response (for debugging purposes).</span></span>|
|||

<br/>

<span data-ttu-id="4065a-164">Estas son las operaciones de la API de comunicaciones de servicio de Office 365.</span><span class="sxs-lookup"><span data-stu-id="4065a-164">Following are the Office 365 Service Communications API operations.</span></span>

## <a name="get-services"></a><span data-ttu-id="4065a-165">Get Services</span><span class="sxs-lookup"><span data-stu-id="4065a-165">Get Services</span></span>

<span data-ttu-id="4065a-166">Devuelve la lista de los servicios suscritos.</span><span class="sxs-lookup"><span data-stu-id="4065a-166">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="4065a-167">Servicio</span><span class="sxs-lookup"><span data-stu-id="4065a-167">Service</span></span>|<span data-ttu-id="4065a-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-168">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4065a-169">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="4065a-169">**Path**</span></span>| `/Services`||
|<span data-ttu-id="4065a-170">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="4065a-170">**Query-option**</span></span>|<span data-ttu-id="4065a-171">$select</span><span class="sxs-lookup"><span data-stu-id="4065a-171">$select</span></span>|<span data-ttu-id="4065a-172">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="4065a-172">Pick a subset of properties.</span></span>|
|<span data-ttu-id="4065a-173">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="4065a-173">**Response**</span></span>|<span data-ttu-id="4065a-174">Lista de entidades de “Service”</span><span class="sxs-lookup"><span data-stu-id="4065a-174">List of "Service" entities</span></span>|<span data-ttu-id="4065a-175">La entidad “Service” contiene “Id” (cadena), “DisplayName” (cadena) y “FeatureNames” (lista de cadenas).</span><span class="sxs-lookup"><span data-stu-id="4065a-175">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="4065a-176">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-176">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

### <a name="sample-response"></a><span data-ttu-id="4065a-177">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-177">Sample response</span></span>

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

## <a name="get-current-status"></a><span data-ttu-id="4065a-178">Get Current Status</span><span class="sxs-lookup"><span data-stu-id="4065a-178">Get Current Status</span></span>

<span data-ttu-id="4065a-179">Devuelve el estado del servicio de las 24 horas anteriores.</span><span class="sxs-lookup"><span data-stu-id="4065a-179">Returns the status of the service from the previous 24 hours.</span></span>

> [!NOTE] 
> <span data-ttu-id="4065a-180">La respuesta del servicio contendrá el estado y cualquier incidente ocurrido durante las 24 horas anteriores.</span><span class="sxs-lookup"><span data-stu-id="4065a-180">The service response will contain the status and any incidents within the previous 24 hours.</span></span> <span data-ttu-id="4065a-181">El valor de StatusDate o StatusTime devuelto será exactamente de 24 horas antes.</span><span class="sxs-lookup"><span data-stu-id="4065a-181">The StatusDate or StatusTime value returned will be exactly 24 hours in the past.</span></span> <span data-ttu-id="4065a-182">Para obtener la última actualización de un incidente determinado, utilice la función Obtener mensajes y lea el valor LastUpdatedTime del registro de respuesta que coincida con el ID. de la incidencia.</span><span class="sxs-lookup"><span data-stu-id="4065a-182">To get the last update for a particular incident, use the Get Messages functionality and read the LastUpdatedTime value from the response record that matches your incident ID.</span></span> <br/>

<br/>

||<span data-ttu-id="4065a-183">Servicio</span><span class="sxs-lookup"><span data-stu-id="4065a-183">Service</span></span>|<span data-ttu-id="4065a-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-184">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4065a-185">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="4065a-185">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="4065a-186">**Filtro**</span><span class="sxs-lookup"><span data-stu-id="4065a-186">**Filter**</span></span>|<span data-ttu-id="4065a-187">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="4065a-187">Workload</span></span>|<span data-ttu-id="4065a-188">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-188">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="4065a-189">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="4065a-189">**Query-option**</span></span>|<span data-ttu-id="4065a-190">$select</span><span class="sxs-lookup"><span data-stu-id="4065a-190">$select</span></span>|<span data-ttu-id="4065a-191">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="4065a-191">Pick a subset of properties.</span></span>|
|<span data-ttu-id="4065a-192">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="4065a-192">**Response**</span></span>|<span data-ttu-id="4065a-193">Lista de entidades “WorkloadStatus”.</span><span class="sxs-lookup"><span data-stu-id="4065a-193">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="4065a-194">La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).</span><span class="sxs-lookup"><span data-stu-id="4065a-194">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="4065a-195">La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).</span><span class="sxs-lookup"><span data-stu-id="4065a-195">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="4065a-196">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-196">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="4065a-197">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-197">Sample response</span></span>

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

### <a name="status-definitions"></a><span data-ttu-id="4065a-198">Definiciones de estado</span><span class="sxs-lookup"><span data-stu-id="4065a-198">Status definitions</span></span>

<span data-ttu-id="4065a-199">Las definiciones de estado incluyen los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4065a-199">The status definitions include the following values:</span></span>

- <span data-ttu-id="4065a-200">Investigating</span><span class="sxs-lookup"><span data-stu-id="4065a-200">Investigating</span></span>
- <span data-ttu-id="4065a-201">ServiceDegradation</span><span class="sxs-lookup"><span data-stu-id="4065a-201">ServiceDegradation</span></span>
- <span data-ttu-id="4065a-202">ServiceInterruption</span><span class="sxs-lookup"><span data-stu-id="4065a-202">ServiceInterruption</span></span>
- <span data-ttu-id="4065a-203">RestoringService</span><span class="sxs-lookup"><span data-stu-id="4065a-203">RestoringService</span></span>
- <span data-ttu-id="4065a-204">ExtendedRecovery</span><span class="sxs-lookup"><span data-stu-id="4065a-204">ExtendedRecovery</span></span>
- <span data-ttu-id="4065a-205">InvestigationSuspended</span><span class="sxs-lookup"><span data-stu-id="4065a-205">InvestigationSuspended</span></span>
- <span data-ttu-id="4065a-206">ServiceRestored</span><span class="sxs-lookup"><span data-stu-id="4065a-206">ServiceRestored</span></span>
- <span data-ttu-id="4065a-207">FalsePositive</span><span class="sxs-lookup"><span data-stu-id="4065a-207">FalsePositive</span></span>
- <span data-ttu-id="4065a-208">PostIncidentReportPublished</span><span class="sxs-lookup"><span data-stu-id="4065a-208">PostIncidentReportPublished</span></span>
- <span data-ttu-id="4065a-209">ServiceOperational</span><span class="sxs-lookup"><span data-stu-id="4065a-209">ServiceOperational</span></span>

<span data-ttu-id="4065a-210">Para una descripción de estas definiciones de estado, consulte [Cómo comprobar el estado del servicio de Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/view-service-health#status-definitions).</span><span class="sxs-lookup"><span data-stu-id="4065a-210">For a description of these status definitions, see [How to check Microsoft 365 service health](https://docs.microsoft.com/microsoft-365/enterprise/view-service-health#status-definitions).</span></span>

## <a name="get-historical-status"></a><span data-ttu-id="4065a-211">Get Historical Status</span><span class="sxs-lookup"><span data-stu-id="4065a-211">Get Historical Status</span></span>

<span data-ttu-id="4065a-212">Devuelve el historial de estado del servicio, por día, en un intervalo de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="4065a-212">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="4065a-213">Servicio</span><span class="sxs-lookup"><span data-stu-id="4065a-213">Service</span></span>|<span data-ttu-id="4065a-214">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-214">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4065a-215">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="4065a-215">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="4065a-216">**Filtros**</span><span class="sxs-lookup"><span data-stu-id="4065a-216">**Filters**</span></span>|<span data-ttu-id="4065a-217">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="4065a-217">Workload</span></span>|<span data-ttu-id="4065a-218">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-218">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="4065a-219">StatusTime</span><span class="sxs-lookup"><span data-stu-id="4065a-219">StatusTime</span></span>|<span data-ttu-id="4065a-220">Permite filtrar por número de días superior a StatusTime (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).</span><span class="sxs-lookup"><span data-stu-id="4065a-220">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="4065a-221">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="4065a-221">**Query-option**</span></span>|<span data-ttu-id="4065a-222">$select</span><span class="sxs-lookup"><span data-stu-id="4065a-222">$select</span></span>|<span data-ttu-id="4065a-223">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="4065a-223">Pick a subset of properties.</span></span>|
|<span data-ttu-id="4065a-224">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="4065a-224">**Response**</span></span>|<span data-ttu-id="4065a-225">Lista de entidades “WorkloadStatus”.</span><span class="sxs-lookup"><span data-stu-id="4065a-225">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="4065a-226">La entidad “WorkloadStatus” contiene “Id” (cadena), “Workload” (carga de trabajo), “StatusTime” (DateTimeOffset), “WorkloadDisplayName” (cadena), “Status” (cadena), “IncidentIds” (lista de cadenas) y FeatureGroupStatusCollection (lista de elementos “FeatureStatus”).</span><span class="sxs-lookup"><span data-stu-id="4065a-226">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="4065a-227">La entidad “FeatureStatus” contiene “Feature” (cadena), “FeatureGroupDisplayName” (cadena) y “FeatureStatus” (cadena).</span><span class="sxs-lookup"><span data-stu-id="4065a-227">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="4065a-228">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-228">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="4065a-229">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-229">Sample response</span></span>

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

## <a name="get-messages"></a><span data-ttu-id="4065a-230">Get Messages</span><span class="sxs-lookup"><span data-stu-id="4065a-230">Get Messages</span></span>

<span data-ttu-id="4065a-231">Devuelve los mensajes sobre el servicio en un intervalo de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="4065a-231">Returns the messages about the service over a certain time range.</span></span> <span data-ttu-id="4065a-232">Use el filtro de tipo para filtrar por mensajes de “incidentes en el servicio”, “mantenimiento planeado” o del “Centro de mensajes”.</span><span class="sxs-lookup"><span data-stu-id="4065a-232">Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="4065a-233">Servicio</span><span class="sxs-lookup"><span data-stu-id="4065a-233">Service</span></span>|<span data-ttu-id="4065a-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="4065a-234">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4065a-235">**Ruta**</span><span class="sxs-lookup"><span data-stu-id="4065a-235">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="4065a-236">**Filtros**</span><span class="sxs-lookup"><span data-stu-id="4065a-236">**Filters**</span></span>|<span data-ttu-id="4065a-237">Carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="4065a-237">Workload</span></span>|<span data-ttu-id="4065a-238">Filtrar por carga de trabajo (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-238">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="4065a-239">StartTime</span><span class="sxs-lookup"><span data-stu-id="4065a-239">StartTime</span></span>|<span data-ttu-id="4065a-240">Permite filtrar por hora de inicio (DateTimeOffset, predeterminado: ge CurrentTime - 7 días).</span><span class="sxs-lookup"><span data-stu-id="4065a-240">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="4065a-241">EndTime</span><span class="sxs-lookup"><span data-stu-id="4065a-241">EndTime</span></span>|<span data-ttu-id="4065a-242">Permite filtrar por hora de finalización (DateTimeOffset, predeterminado: le CurrentTime).</span><span class="sxs-lookup"><span data-stu-id="4065a-242">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="4065a-243">MessageType</span><span class="sxs-lookup"><span data-stu-id="4065a-243">MessageType</span></span>|<span data-ttu-id="4065a-244">Permite filtrar por MessageType (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-244">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="4065a-245">ID</span><span class="sxs-lookup"><span data-stu-id="4065a-245">ID</span></span>|<span data-ttu-id="4065a-246">Permite filtrar por id. (cadena, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-246">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="4065a-247">**Opción de consulta**</span><span class="sxs-lookup"><span data-stu-id="4065a-247">**Query-option**</span></span>|<span data-ttu-id="4065a-248">$select</span><span class="sxs-lookup"><span data-stu-id="4065a-248">$select</span></span>|<span data-ttu-id="4065a-249">Selecciona un subconjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="4065a-249">Pick a subset of properties.</span></span>|
||<span data-ttu-id="4065a-250">$top</span><span class="sxs-lookup"><span data-stu-id="4065a-250">$top</span></span>|<span data-ttu-id="4065a-251">Selecciona el mayor número de resultados (predeterminado y máximo $top=100).</span><span class="sxs-lookup"><span data-stu-id="4065a-251">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="4065a-252">$skip</span><span class="sxs-lookup"><span data-stu-id="4065a-252">$skip</span></span>|<span data-ttu-id="4065a-253">Omite el número de resultados (predeterminado: $skip=0).</span><span class="sxs-lookup"><span data-stu-id="4065a-253">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="4065a-254">**Respuesta**</span><span class="sxs-lookup"><span data-stu-id="4065a-254">**Response**</span></span>|<span data-ttu-id="4065a-255">Lista de entidades de “Message”.</span><span class="sxs-lookup"><span data-stu-id="4065a-255">List of "Message" entities.</span></span>|<span data-ttu-id="4065a-256">La entidad “Message” contiene “Id” (cadena), “StartTime” (DateTimeOffset), “EndTime” (DateTimeOffset), “Status” (cadena), “Messages” (lista de la entidad “MessageHistory”), “LastUpdatedTime” (DateTimeOffset), “Workload” (cadena), “WorkloadDisplayName” (cadena), “Feature” (cadena), “FeatureDisplayName” (cadena), “MessageType” (enumeración, predeterminado: todo).</span><span class="sxs-lookup"><span data-stu-id="4065a-256">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessageHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="4065a-257">La entidad “MessageHistory” contiene “PublishedTime” (DateTimeOffset), “MessageText” (cadena).</span><span class="sxs-lookup"><span data-stu-id="4065a-257">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="4065a-258">Solicitud de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-258">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="4065a-259">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="4065a-259">Sample response</span></span>

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


## <a name="errors"></a><span data-ttu-id="4065a-260">Errores</span><span class="sxs-lookup"><span data-stu-id="4065a-260">Errors</span></span>

<span data-ttu-id="4065a-261">Cuando el servicio encuentre un error, indicará el código de respuesta de error al autor de la llamada mediante la sintaxis estándar de código de error de HTTP.</span><span class="sxs-lookup"><span data-stu-id="4065a-261">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="4065a-262">Según la [especificación de OData versión 4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), se incluye información adicional en el cuerpo de la llamada con errores como un único objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="4065a-262">As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="4065a-263">Abajo se muestra un ejemplo del cuerpo completo de un error en formato JSON:</span><span class="sxs-lookup"><span data-stu-id="4065a-263">The following is an example of a full JSON error body:</span></span>


```json
{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}
```
