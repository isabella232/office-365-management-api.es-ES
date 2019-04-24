---
ms.TocTitle: Get started with Office 365 Management APIs
title: Introducción a las API de administración de Office 365
description: Las API usan Azure AD para proporcionar servicios de autenticación que pueden usarse para conceder derechos a la aplicación con el fin de obtener acceso a esos servicios.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: 09/05/2018
localization_priority: Priority
ms.openlocfilehash: 9732b5a838bdf4c14a6a13af8196704c89dec63d
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "32224074"
---
# <a name="get-started-with-office-365-management-apis"></a><span data-ttu-id="bd686-103">Introducción a las API de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="bd686-103">Get started with Office 365 Management APIs</span></span>

<span data-ttu-id="bd686-104">Al crear una aplicación que necesita acceso a servicios protegidos, como la API de administración de Office 365, necesita proporcionar un método para que el servicio conozca si la aplicación tiene derechos para obtener acceso a ella.</span><span class="sxs-lookup"><span data-stu-id="bd686-104">When you create an application that needs access to secured services like the Office 365 Management APIs, you need to provide a way to let the service know if your application has rights to access it.</span></span> <span data-ttu-id="bd686-105">Las API de administración de Office 365 usan Azure AD para proporcionar servicios de autenticación que pueden usarse para conceder derechos a la aplicación con el fin de obtener acceso a esos servicios.</span><span class="sxs-lookup"><span data-stu-id="bd686-105">The Office 365 Management APIs use Azure AD to provide authentication services that you can use to grant rights for your application to access them.</span></span> 

<span data-ttu-id="bd686-106">Hay cuatro pasos principales:</span><span class="sxs-lookup"><span data-stu-id="bd686-106">There are four key steps:</span></span>

1. <span data-ttu-id="bd686-107">**Registrar la aplicación en Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="bd686-107">**Register your application in Azure AD**.</span></span> <span data-ttu-id="bd686-108">Para permitir que una aplicación tenga acceso a las API de administración de Office 365, necesita registrar la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-108">To allow your application access to the Office 365 Management APIs, you need to register your application in Azure AD.</span></span> <span data-ttu-id="bd686-109">Esto le permite establecer una identidad para la aplicación y especificar los niveles de permisos necesarios para obtener acceso a las API.</span><span class="sxs-lookup"><span data-stu-id="bd686-109">This allows you to establish an identity for your application and specify the permission levels it needs to access the APIs.</span></span>
    
2. <span data-ttu-id="bd686-110">**Obtener el consentimiento del administrador del espacio empresarial de Office 365**.</span><span class="sxs-lookup"><span data-stu-id="bd686-110">**Get Office 365 tenant admin consent**.</span></span> <span data-ttu-id="bd686-111">Un administrador de espacio empresarial de Office 365 tiene que conceder de manera explícita permiso para que la aplicación obtenga acceso a los datos del espacio empresarial mediante las API de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-111">An Office 365 tenant admin must explicitly grant consent to allow your application to access their tenant data by means of the Office 365 Management APIs.</span></span> <span data-ttu-id="bd686-112">El proceso de consentimiento es una experiencia basada en explorador para la que el administrador del espacio empresarial tiene que iniciar sesión en la **interfaz de usuario de consentimiento de Azure AD**, revisar los permisos de acceso que solicita la aplicación y, después, conceder o denegar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="bd686-112">The consent process is a browser-based experience that requires the tenant admin to sign in to the **Azure AD consent UI** and review the access permissions that your application is requesting, and then either grant or deny the request.</span></span> <span data-ttu-id="bd686-113">Después de conceder la solicitud, la interfaz de usuario redirige al usuario a la aplicación con un código de autorización en la URL.</span><span class="sxs-lookup"><span data-stu-id="bd686-113">After consent is granted, the UI redirects the user back to your application with an authorization code in the URL.</span></span> <span data-ttu-id="bd686-114">La aplicación realiza una llamada entre servicios a Azure AD para cambiar este código de autorización por un token de acceso, que contiene información tanto sobre el administrador del espacio empresarial como de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-114">Your application makes a service-to-service call to Azure AD to exchange this authorization code for an access token, which contains information about both the tenant admin and your application.</span></span> <span data-ttu-id="bd686-115">Es necesario extraer el id. del espacio empresarial del token de acceso y almacenarlo para su uso futuro.</span><span class="sxs-lookup"><span data-stu-id="bd686-115">The tenant ID must be extracted from the access token and stored for future use.</span></span>
    
3. <span data-ttu-id="bd686-116">**Solicitar tokens de acceso de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="bd686-116">**Request access tokens from Azure AD**.</span></span> <span data-ttu-id="bd686-117">Con las credenciales de la aplicación según se configuraron en Azure AD, la aplicación solicita tokens de acceso adicionales para un espacio empresarial con permiso de forma continuada, sin que sean necesarias otras interacciones del administrador del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-117">Using your application's credentials as configured in Azure AD, your application requests additional access tokens for a consented tenant on an ongoing basis, without the need for further tenant admin interaction.</span></span> <span data-ttu-id="bd686-118">Estos tokens de acceso se denominan tokens solo de aplicación porque no incluyen información sobre el administrador del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-118">These access tokens are called app-only tokens because they do not include information about the tenant admin.</span></span>
    
4. <span data-ttu-id="bd686-119">**Llamar a las API de administración de Office 365**.</span><span class="sxs-lookup"><span data-stu-id="bd686-119">**Call the Office 365 Management APIs**.</span></span> <span data-ttu-id="bd686-120">Los tokens de acceso solo de aplicación se pasan a las API de administración de Office 365 para autenticar y autorizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-120">The app-only access tokens are passed to the Office 365 Management APIs to authenticate and authorize your application.</span></span>
    
<span data-ttu-id="bd686-121">En el diagrama siguiente, se muestra la secuencia de solicitudes de tokens de acceso y consentimiento.</span><span class="sxs-lookup"><span data-stu-id="bd686-121">The following diagram shows the sequence of consent and access token requests.</span></span>


![Flujo de autorización de introducción a las API de administración](images/authorization-flow.png)


## <a name="register-your-application-in-azure-ad"></a><span data-ttu-id="bd686-123">Registrar la aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd686-123">Register your application in Azure AD</span></span>

<span data-ttu-id="bd686-124">Las API de administración de Office 365 usan Azure AD para proporcionar autenticación segura a los datos del espacio empresarial de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-124">The Office 365 Management APIs use Azure AD to provide secure authentication to Office 365 tenant data.</span></span> <span data-ttu-id="bd686-125">Para obtener acceso a las API de administración de Office 365, necesita registrar la aplicación en Azure AD y, como parte de la configuración, especificará los niveles de permisos que necesita la aplicación para obtener acceso a las API.</span><span class="sxs-lookup"><span data-stu-id="bd686-125">To access the Office 365 Management APIs, you need to register your app in Azure AD, and as part of the configuration, you will specify the permission levels your app needs to access the APIs.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="bd686-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bd686-126">Prerequisites</span></span>

<span data-ttu-id="bd686-127">Para registrar la aplicación en Azure AD, necesita una suscripción a Office 365 y una suscripción a Azure AD asociada a la suscripción de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-127">To register your app in Azure AD, you need a subscription to Office 365 and a subscription to Azure that has been associated with your Office 365 subscription.</span></span> <span data-ttu-id="bd686-128">Para empezar, puede usar suscripciones de prueba, tanto para Office 365 como para Azure.</span><span class="sxs-lookup"><span data-stu-id="bd686-128">You can use trial subscriptions to both Office 365 and Azure to get started.</span></span> <span data-ttu-id="bd686-129">Para obtener más información, vea [Introducción al programa Office 365 Developer](https://docs.microsoft.com/es-ES/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="bd686-129">For more details, see [Welcome to the Office 365 Developer Program](https://docs.microsoft.com/es-ES/office/developer-program/office-365-developer-program).</span></span>


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a><span data-ttu-id="bd686-130">Usar el Portal de administración de Azure para registrar una aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd686-130">Use the Azure Management Portal to register your application in Azure AD</span></span>

<span data-ttu-id="bd686-131">Cuando tenga un espacio empresarial de Microsoft con las suscripciones adecuadas, podrá registrar su aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-131">After you have a Microsoft tenant with the proper subscriptions, you can register your application in Azure AD.</span></span>

1. <span data-ttu-id="bd686-132">Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com/) con las credenciales del espacio empresarial de Microsoft que tenga la suscripción de Office 365 que quiera usar.</span><span class="sxs-lookup"><span data-stu-id="bd686-132">Sign into the [Azure management portal](https://manage.windowsazure.com/), using the credential of your Microsoft tenant that has the subscription to Office 365 you wish to use.</span></span> <span data-ttu-id="bd686-133">También puede obtener acceso al Portal de administración de Azure mediante un vínculo que se muestra en el panel de navegación izquierdo del [Portal de administración de Office](https://portal.office.com/).</span><span class="sxs-lookup"><span data-stu-id="bd686-133">You can also access the Azure Management Portal via a link that appears in the left navigation pane in the [Office admin portal](https://portal.office.com/).</span></span>
    
2. <span data-ttu-id="bd686-134">En el panel de navegación izquierdo, seleccione Active Directory (1).</span><span class="sxs-lookup"><span data-stu-id="bd686-134">In the left navigation panel, choose Active Directory (1).</span></span> <span data-ttu-id="bd686-135">Asegúrese de que esté seleccionada la pestaña Directorio (2) y, después, seleccione el nombre del directorio (3).</span><span class="sxs-lookup"><span data-stu-id="bd686-135">Make sure the Directory tab (2) is selected, and then select the directory name (3).</span></span>
    
   ![Página de suscripción de Office 365](images/o365-sign-up-page.png)
    
    
3. <span data-ttu-id="bd686-137">En la página del directorio, seleccione **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bd686-137">On the directory page, select **Applications**.</span></span> <span data-ttu-id="bd686-138">En Azure AD, se muestra una lista de las aplicaciones instaladas actualmente en el espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-138">Azure AD displays a list of the applications currently installed in your tenancy.</span></span>
    
4. <span data-ttu-id="bd686-139">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bd686-139">Choose **Add**.</span></span>
    
   ![Página Administrador de Office 365](images/o365-admin-page.png)
    
    
5. <span data-ttu-id="bd686-141">Seleccione **Agregar una aplicación desarrollada por mi organización**.</span><span class="sxs-lookup"><span data-stu-id="bd686-141">Select **Add an application my organization is developing**.</span></span>
    
6. <span data-ttu-id="bd686-142">Escriba el **NOMBRE** de la aplicación y especifique el **Tipo** como APLICACIÓN WEB O API WEB.</span><span class="sxs-lookup"><span data-stu-id="bd686-142">Enter the **NAME** of your application and specify the **Type** as WEB APPLICATION AND/OR WEB API.</span></span>
    
7. <span data-ttu-id="bd686-143">Escriba las propiedades de la aplicación correspondientes:</span><span class="sxs-lookup"><span data-stu-id="bd686-143">Enter the appropriate App properties:</span></span>
    
   - <span data-ttu-id="bd686-144">**SIGN-ON URL**.</span><span class="sxs-lookup"><span data-stu-id="bd686-144">**SIGN-ON URL**.</span></span> <span data-ttu-id="bd686-145">URL donde los usuarios pueden iniciar sesión y usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-145">The URL where users can sign in and use your app.</span></span> <span data-ttu-id="bd686-146">Puede cambiar este valor más tarde si es necesario.</span><span class="sxs-lookup"><span data-stu-id="bd686-146">You can change this later as needed.</span></span>
    
   - <span data-ttu-id="bd686-147">**APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="bd686-147">**APP ID URI**.</span></span> <span data-ttu-id="bd686-148">URI usado como un identificador lógico único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-148">The URI used as a unique logical identifier for your app.</span></span> <span data-ttu-id="bd686-149">El URI tiene que estar en un dominio personalizado verificado para que un usuario externo pueda conceder acceso a la aplicación a sus datos en Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-149">The URI must be in a verified custom domain for an external user to grant your app access to their data in Windows Azure AD.</span></span> <span data-ttu-id="bd686-150">Por ejemplo, si el espacio empresarial de Microsoft es **contoso.onmicrosoft.com**, el URI del id. de aplicación podría ser **https://app.contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="bd686-150">For example, if your Microsoft tenant is **contoso.onmicrosoft.com**, the APP ID URI could be **https://app.contoso.onmicrosoft.com**.</span></span>
    
8. <span data-ttu-id="bd686-151">La aplicación ya está registrada con Azure AD y se le asignó un id. de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd686-151">Your app is now registered with Azure AD, and has been assigned a client ID.</span></span> <span data-ttu-id="bd686-152">Pero hay varios aspectos importantes que aún es necesario configurar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-152">However, there are several important aspects of your app left to configure.</span></span>
    

### <a name="configure-your-application-properties-in-azure-ad"></a><span data-ttu-id="bd686-153">Configurar las propiedades de la aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd686-153">Configure your application properties in Azure AD</span></span>

<span data-ttu-id="bd686-154">Después de registrar la aplicación, tiene que especificar varias propiedades importantes que determinan cómo funciona la aplicación en Azure AD y la forma en que los administradores de espacios empresariales concederán permiso para que la aplicación obtenga acceso a sus datos mediante las API de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-154">Now that your application is registered, there are several important properties you must specify that determine how your application functions within Azure AD and how tenant admins will grant consent to allow your application to access their data by using the Office 365 Management APIs.</span></span>

<span data-ttu-id="bd686-155">Para obtener más información sobre la configuración de aplicaciones de Azure AD en general, vea [Propiedades de objeto de aplicación](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="bd686-155">For more information about Azure AD application configuration in general, see [Application Object Properties](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-application-objects).</span></span>


1. <span data-ttu-id="bd686-156">**CLIENT ID**.</span><span class="sxs-lookup"><span data-stu-id="bd686-156">**CLIENT ID**.</span></span> <span data-ttu-id="bd686-157">Azure AD genera automáticamente este valor.</span><span class="sxs-lookup"><span data-stu-id="bd686-157">This value is automatically generated by Azure AD.</span></span> <span data-ttu-id="bd686-158">La aplicación usará este valor al solicitar el permiso de los administradores de espacios empresariales y al solicitar tokens solo de aplicación desde Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-158">Your application will use this value when requesting consent from tenant admins and when requesting app-only tokens from Azure AD.</span></span>
    
2. <span data-ttu-id="bd686-159">**APPLICATION IS MULTI-TENANT**.</span><span class="sxs-lookup"><span data-stu-id="bd686-159">**APPLICATION IS MULTI-TENANT**.</span></span> <span data-ttu-id="bd686-160">Es necesario establecer esta propiedad en **YES** para permitir a los administradores de espacios empresariales conceder permiso a una aplicación para obtener acceso a sus datos mediante las API de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-160">This property must be set to **YES** to allow tenant admins to grant consent to your app to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="bd686-161">Si esta propiedad se establece en **NO**, la aplicación solo podrá obtener acceso a los datos de su propio espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-161">If this property is set to **NO**, your application will only be able to access your own tenant's data.</span></span>
    
3. <span data-ttu-id="bd686-162">**REPLY URL**.</span><span class="sxs-lookup"><span data-stu-id="bd686-162">**REPLY URL**.</span></span> <span data-ttu-id="bd686-163">URL a la que se redirigirá un administrador de espacios empresariales después de conceder el permiso a la aplicación para obtener acceso a sus datos mediante las API de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-163">This is the URL that a tenant admin will be redirected to after granting consent to allow your application to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="bd686-164">Puede configurar varias URL de respuesta si es necesario.</span><span class="sxs-lookup"><span data-stu-id="bd686-164">You can configure multiple reply URLs as needed.</span></span> <span data-ttu-id="bd686-165">Azure establece automáticamente la primera para que coincida con la URL de inicio de sesión que especificó al crear la aplicación, pero puede cambiar este valor si es necesario.</span><span class="sxs-lookup"><span data-stu-id="bd686-165">Azure automatically sets the first one to match the sign-on URL you specified when you created the application, but you can change this value as needed.</span></span>
    
<span data-ttu-id="bd686-166">Asegúrese de seleccionar **Guardar** después de realizar cambios en estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="bd686-166">Be sure to choose **Save** after making any changes to these properties.</span></span>


### <a name="generate-a-new-key-for-your-application"></a><span data-ttu-id="bd686-167">Generar una nueva clave para la aplicación</span><span class="sxs-lookup"><span data-stu-id="bd686-167">Generate a new key for your application</span></span>

<span data-ttu-id="bd686-168">Las claves, también conocidas como secretos de cliente, se usan al intercambiar un código de autorización por un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-168">Keys, also known as client secrets, are used when exchanging an authorization code for an access token.</span></span>


1. <span data-ttu-id="bd686-169">En el Portal de administración de Azure, seleccione su aplicación y elija **Configurar** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="bd686-169">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span> <span data-ttu-id="bd686-170">Desplácese hasta **claves**.</span><span class="sxs-lookup"><span data-stu-id="bd686-170">Scroll down to **keys**.</span></span>
    
2. <span data-ttu-id="bd686-171">Seleccione la duración de la clave y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bd686-171">Select the duration for your key, and choose **Save**.</span></span>
    
   ![Página de suscripción de Azure](images/azure-subscription-page.png)
    
    
3. <span data-ttu-id="bd686-173">Azure solo mostrará el secreto de aplicación después de guardarlo.</span><span class="sxs-lookup"><span data-stu-id="bd686-173">Azure displays the app secret only after saving it.</span></span> <span data-ttu-id="bd686-174">Haga clic en el icono del Portapapeles para copiar el secreto de cliente en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="bd686-174">Select the Clipboard icon to copy the client secret to the Clipboard.</span></span>
    
   ![Página de Azure Portal](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > <span data-ttu-id="bd686-176">Azure solo muestra el secreto de cliente en el momento en que se genera inicialmente.</span><span class="sxs-lookup"><span data-stu-id="bd686-176">Azure only displays the client secret at the time you initially generate it.</span></span> <span data-ttu-id="bd686-177">No se puede volver a esta página y recuperar el secreto de cliente más tarde.</span><span class="sxs-lookup"><span data-stu-id="bd686-177">You cannot navigate back to this page and retrieve the client secret later.</span></span>

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a><span data-ttu-id="bd686-178">Configurar un certificado X.509 para habilitar las llamadas entre servicios</span><span class="sxs-lookup"><span data-stu-id="bd686-178">Configure an X.509 certificate to enable service-to-service calls</span></span>

<span data-ttu-id="bd686-179">Una aplicación que se ejecuta en segundo plano, como un demonio servicio, puede usar las credenciales de cliente para solicitar tokens de acceso solo de aplicación sin solicitar de forma repetida el consentimiento del administrador del espacio empresarial después de recibir el consentimiento inicial.</span><span class="sxs-lookup"><span data-stu-id="bd686-179">An application that is running in the background, such as a daemon or service, can use client credentials to request app-only access tokens without repeatedly requesting consent from the tenant admin after initial consent is granted.</span></span> 

<span data-ttu-id="bd686-180">Para obtener más información, vea [Llamadas entre servicios con credenciales de cliente](https://msdn.microsoft.com/es-ES/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd686-180">For more information, see [Service to Service Calls Using Client Credentials](https://msdn.microsoft.com/es-ES/library/azure/dn645543.aspx).</span></span>

<span data-ttu-id="bd686-181">Necesita configurar un certificado X.509 con la aplicación para usarlo como las credenciales de cliente al solicitar tokens de acceso solo de aplicación desde Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-181">You must configure an X.509 certificate with your application to be used as client credentials when requesting app-only access tokens from Azure AD.</span></span> <span data-ttu-id="bd686-182">Este proceso se divide en dos pasos:</span><span class="sxs-lookup"><span data-stu-id="bd686-182">There are two steps to the process:</span></span>

- <span data-ttu-id="bd686-183">Obtener un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="bd686-183">Obtain an X.509 certificate.</span></span> <span data-ttu-id="bd686-184">Puede usar un certificado autofirmado o un certificado emitido por una entidad de certificación de confianza pública.</span><span class="sxs-lookup"><span data-stu-id="bd686-184">You can use a self-signed certificate or a certificate issued by publicly trusted certificate authority.</span></span>
    
- <span data-ttu-id="bd686-185">Modificar el manifiesto de la aplicación para incluir la huella digital y la clave pública del certificado.</span><span class="sxs-lookup"><span data-stu-id="bd686-185">Modify your application manifest to include the thumbprint and public key of your certificate.</span></span>
    
<span data-ttu-id="bd686-186">En las instrucciones siguientes, se muestra cómo usar la herramienta _MakeCert_ de Windows SDK o Visual Studio para generar un certificado autofirmado y exportar la clave pública a un archivo con codificación Base 64.</span><span class="sxs-lookup"><span data-stu-id="bd686-186">The following instructions show you how to use the Visual Studio or Windows SDK _makecert_ tool to generate a self-signed certificate and export the public key to a base64-encoded file.</span></span>


1. <span data-ttu-id="bd686-187">En la línea de comandos, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bd686-187">From the command line, run the following:</span></span>
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > <span data-ttu-id="bd686-188">Al generar el certificado X.509, asegúrese de que la longitud de la clave sea como mínimo de 2048.</span><span class="sxs-lookup"><span data-stu-id="bd686-188">When you are generating the X.509 certificate, make sure the key length is at least 2048.</span></span> <span data-ttu-id="bd686-189">Las longitudes de clave más cortas no se aceptan como claves válidas.</span><span class="sxs-lookup"><span data-stu-id="bd686-189">Shorter key lengths are not accepted as valid keys.</span></span>

2. <span data-ttu-id="bd686-190">Abra el complemento MMC de certificados y conéctese a su cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="bd686-190">Open the Certificates MMC snap-in and connect to your user account.</span></span> 
    
3. <span data-ttu-id="bd686-191">Busque el nuevo certificado en la carpeta Personal y exporte la clave pública a un archivo con codificación Base 64 (por ejemplo, nombredeempresa.cer).</span><span class="sxs-lookup"><span data-stu-id="bd686-191">Find the new certificate in the Personal folder and export the public key to a base64-encoded file (for example, mycompanyname.cer).</span></span> <span data-ttu-id="bd686-192">La aplicación usará este certificado para comunicarse con Azure AD, por lo que es importante que se asegure de conservar también el acceso a la clave privada.</span><span class="sxs-lookup"><span data-stu-id="bd686-192">Your application will use this certificate to communicate with Azure AD, so make sure you retain access to the private key as well.</span></span>
    
   > [!NOTE] 
   > <span data-ttu-id="bd686-193">Puede usar Windows PowerShell para extraer la huella digital y la clave pública con codificación Base 64.</span><span class="sxs-lookup"><span data-stu-id="bd686-193">You can use Windows PowerShell to extract the thumbprint and base64-encoded public key.</span></span> <span data-ttu-id="bd686-194">Hay otras plataformas que ofrecen herramientas similares para recuperar propiedades de certificados.</span><span class="sxs-lookup"><span data-stu-id="bd686-194">Other platforms provide similar tools to retrieve properties of certificates.</span></span>

4. <span data-ttu-id="bd686-195">Desde el símbolo del sistema de Windows PowerShell, escriba y ejecute los siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="bd686-195">From the Windows PowerShell prompt, type and run the following:</span></span>
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. <span data-ttu-id="bd686-196">Guarde los valores de `$base64Thumbprint`, `$base64Value` y `$keyid` para usarlos al actualizar el manifiesto de la aplicación en el siguiente conjunto de pasos.</span><span class="sxs-lookup"><span data-stu-id="bd686-196">Store the values for `$base64Thumbprint`, `$base64Value`, and `$keyid` to be used when you update your application manifest in the next set of steps.</span></span>
    
   <span data-ttu-id="bd686-197">Con los valores extraídos del certificado y el id. de clave generado, tiene que actualizar el manifiesto de la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-197">Using the values extracted from the certificate and the generated key ID, you must now update your application manifest in Azure AD.</span></span>
    
6. <span data-ttu-id="bd686-198">En el Portal de administración de Azure, seleccione su aplicación y elija **Configurar** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="bd686-198">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span>
    
7. <span data-ttu-id="bd686-199">En la barra de comandos, seleccione **Administrar manifiesto** y, después, **Descargar manifiesto**.</span><span class="sxs-lookup"><span data-stu-id="bd686-199">In the command bar, choose **Manage manifest**, and then choose **Download Manifest**.</span></span>
    
   ![Visualizar un certificado desde la línea de comandos](images/command-line-certificate-display.png)
    
    
8. <span data-ttu-id="bd686-201">Abra el manifiesto descargado para editarlo y reemplace la propiedad vacía KeyCredentials por el siguiente JSON:</span><span class="sxs-lookup"><span data-stu-id="bd686-201">Open the downloaded manifest for editing and replace the empty KeyCredentials property with the following JSON:</span></span>
    
   ```json
      "keyCredentials": [
        {
            "customKeyIdentifier" : "$base64Thumbprint_from_above",
            "keyId": "$keyid_from_above",
            "type": "AsymmetricX509Cert",
            "usage": "Verify",
            "value": "$base64Value_from_above"
        }
    ],
   ```


   > [!NOTE] 
   > <span data-ttu-id="bd686-202">La propiedad [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) es una colección que permite cargar varios certificados para escenarios de sustitución o certificados X.509 de eliminación para escenarios de peligro.</span><span class="sxs-lookup"><span data-stu-id="bd686-202">The [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) property is a collection, making it possible to upload multiple X.509 certificates for rollover scenarios or delete certificates for compromise scenarios.</span></span>

9. <span data-ttu-id="bd686-203">Guarde los cambios y cargue el archivo de manifiesto de la aplicación actualizado; para ello, haga clic en **Administrar manifiesto** en la barra de comandos, seleccione **Cargar manifiesto**, busque el archivo de manifiesto actualizado y, después, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="bd686-203">Save your changes and upload the updated manifest by choosing **Manage manifest** in the command bar, choosing **Upload manifest**, browsing to your updated manifest file, and then selecting it.</span></span>
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a><span data-ttu-id="bd686-204">Especificar los permisos que necesita la aplicación para obtener acceso a las API de administración de Office 365</span><span class="sxs-lookup"><span data-stu-id="bd686-204">Specify the permissions your app requires to access the Office 365 Management APIs</span></span>

<span data-ttu-id="bd686-205">Por último, tendrá que especificar exactamente qué permisos necesita su aplicación de las API de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="bd686-205">Finally, you need to specify exactly what permissions your app requires of the Office 365 Management APIs.</span></span> <span data-ttu-id="bd686-206">Para hacerlo, agregue acceso a las API de administración de Office 365 a la aplicación y, después, especifique los permisos necesarios.</span><span class="sxs-lookup"><span data-stu-id="bd686-206">To do so, you add access to the Office 365 Management APIs to your app, and then you specify the permission(s) you need.</span></span>


1. <span data-ttu-id="bd686-207">En el Portal de administración de Azure, seleccione la aplicación y, después, seleccione **Configurar** en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="bd686-207">In the Azure Management Portal, select your application, and choose **Configure** in the top menu.</span></span> <span data-ttu-id="bd686-208">Vaya a **Permisos para otras aplicaciones** y seleccione **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="bd686-208">Scroll down to **permissions to other applications**, and choose **Add application**.</span></span>
    
   ![Página de Azure AD](images/azure-ad-page.png)
    
    
2. <span data-ttu-id="bd686-210">Seleccione las **API de administración de Office 365** (1) para que se muestren en la columna **Seleccionado** (2) y, después, seleccione la marca de verificación en la parte inferior derecha (3) para guardar la selección y volver a la página de configuración principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-210">Select the **Office 365 Management APIs** (1) so that it appears in the **Selected** column (2), and then select the check mark in the lower right (3) to save your selection and return to the main configuration page for your application.</span></span>
    
   ![Página de aplicaciones de Azure AD](images/azure-ad-apps-page.png)
    
    
3. <span data-ttu-id="bd686-212">Las API de administración de Office ahora se muestran en la lista de aplicaciones para las que necesita permisos su aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-212">The Office Management APIs now appear in the list of applications to which your application requires permissions.</span></span> <span data-ttu-id="bd686-213">En **Permisos de aplicación** y **Permisos delegados**, seleccione los permisos que necesita la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-213">Under both **Application Permissions** and **Delegated Permissions**, select the permissions your application requires.</span></span> <span data-ttu-id="bd686-214">Para obtener más información sobre cada permiso, vea la referencia de API específica.</span><span class="sxs-lookup"><span data-stu-id="bd686-214">Refer to the specific API reference for more details about each permission.</span></span>  

   > [!NOTE] 
   > <span data-ttu-id="bd686-215">Actualmente, hay cuatro permisos sin usar relacionados con informes de actividades e inteligencia sobre amenazas que se quitarán en el futuro.</span><span class="sxs-lookup"><span data-stu-id="bd686-215">There are currently four unused permissions related to activity reports and threat intelligence that will be removed in the future.</span></span> <span data-ttu-id="bd686-216">No seleccione ninguno de estos permisos, ya que no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="bd686-216">Do not select any of these permissions because they are unnecessary.</span></span>
    
   ![Cuadro de diálogo Agregar una aplicación](images/add-an-application-dialog.png)
    
    
4. <span data-ttu-id="bd686-218">Seleccione **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bd686-218">Choose **Save** to save the configuration.</span></span>
    

## <a name="get-office-365-tenant-admin-consent"></a><span data-ttu-id="bd686-219">Obtener el consentimiento del administrador del espacio empresarial de Office 365</span><span class="sxs-lookup"><span data-stu-id="bd686-219">Get Office 365 tenant admin consent</span></span>

<span data-ttu-id="bd686-220">Después de configurar la aplicación con los permisos necesarios para usar las API de administración de Office 365, un administrador de espacios empresariales tiene que conceder de manera explícita a las aplicaciones dos permisos para obtener acceso a los datos del espacio empresarial mediante las API.</span><span class="sxs-lookup"><span data-stu-id="bd686-220">Now that your application is configured with the permissions it needs to use the Office 365 Management APIs, a tenant admin must explicitly grant your application these permissions in order to access their tenant's data by using the APIs.</span></span> <span data-ttu-id="bd686-221">Para conceder el permiso, el administrador del espacio empresarial tiene que iniciar sesión en Azure AD con la URL específica, donde podrá revisar los permisos solicitados de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-221">To grant consent, the tenant admin must sign in to Azure AD by using the following specially constructed URL, where they can review your application's requested permissions.</span></span> <span data-ttu-id="bd686-222">Este paso no es necesario al usar las API para obtener acceso a datos desde su propio espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-222">This step is not required when using the APIs to access data from your own tenant.</span></span>


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

<span data-ttu-id="bd686-223">La URL de redireccionamiento tiene que coincidir o ser una subruta de una de las URL de respuesta configuradas para la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd686-223">The redirect URL must match or be a sub-path under one of the Reply URLs configured for your application in Azure AD.</span></span>

<span data-ttu-id="bd686-224">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd686-224">For example:</span></span>

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

<span data-ttu-id="bd686-225">Para probar la URL de consentimiento, péguela en un explorador e inicie sesión con las credenciales de administrador de Office 365 de un espacio empresarial distinto del espacio empresarial que usó para registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-225">You can test the consent URL by pasting it into a browser and signing in using the credentials of an Office 365 admin for a tenant other than the tenant that you used to register the application.</span></span> <span data-ttu-id="bd686-226">Verá la solicitud para conceder permisos a la aplicación para usar las API de administración de Office.</span><span class="sxs-lookup"><span data-stu-id="bd686-226">You will see the request to grant your application permission to use the Office Management APIs.</span></span>


![Página agregada de aplicación Azure AD](images/azure-ad-app-added-page.png)

<span data-ttu-id="bd686-228">Después de seleccionar **Aceptar**, será redirigido a la página especificada y verá un código en la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="bd686-228">After choosing **Accept**, you are redirected to the specified page, and there will be a code in the query string.</span></span> 

<span data-ttu-id="bd686-229">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd686-229">For example:</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="bd686-230">La aplicación usa este código de autorización para obtener un token de acceso de Azure AD, desde el que se puede extraer el id. de espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-230">Your application uses this authorization code to obtain an access token from Azure AD, from which the tenant ID can be extracted.</span></span> <span data-ttu-id="bd686-231">Después de extraer y almacenar el id. de espacio empresarial, puede obtener otros tokens de acceso sin que sea necesario que el administrador del espacio empresarial inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="bd686-231">After you have extracted and stored the tenant ID, you can obtain subsequent access tokens without requiring the tenant admin to sign in.</span></span>


## <a name="request-access-tokens-from-azure-ad"></a><span data-ttu-id="bd686-232">Solicitar tokens de acceso de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd686-232">Request access tokens from Azure AD</span></span>

<span data-ttu-id="bd686-233">Hay dos métodos para solicitar tokens de acceso desde Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bd686-233">There are two methods for requesting access tokens from Azure AD:</span></span>

- <span data-ttu-id="bd686-234">En el [Flujo de concesión de código de autorización](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx), un administrador de espacios empresariales concede el consentimiento explícito, que devuelve un código de autorización a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-234">The [Authorization Code Grant Flow](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) involves a tenant admin granting explicit consent, which returns an authorization code to your application.</span></span> <span data-ttu-id="bd686-235">Después, la aplicación intercambia el código de autorización por un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-235">Your application then exchanges the authorization code for an access token.</span></span> <span data-ttu-id="bd686-236">Este método es necesario para obtener el consentimiento inicial que necesita la aplicación para obtener acceso a los datos del espacio empresarial mediante la API, y este primer token de acceso es necesario para obtener y almacenar el id. de espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-236">This method is required to obtain the initial consent that your application needs to access the tenant data by using the API, and this first access token is needed in order to obtain and store the tenant ID.</span></span>
    
- <span data-ttu-id="bd686-237">El [Flujo de concesión de credenciales de cliente](https://msdn.microsoft.com/es-ES/library/azure/dn645543.aspx) permite a la aplicación solicitar tokens de acceso posteriores cuando expiren los anteriores, sin que sea necesario que el administrador del espacio empresarial inicie sesión y conceda el permiso de manera explícita.</span><span class="sxs-lookup"><span data-stu-id="bd686-237">The [Client Credentials Grant Flow](https://msdn.microsoft.com/es-ES/library/azure/dn645543.aspx) allows your application to request subsequent access tokens as old ones expire, without requiring the tenant admin to sign in and explicitly grant consent.</span></span> <span data-ttu-id="bd686-238">Este método tiene que usarse para las aplicaciones que se ejecutan de forma continua en segundo plano mediante llamadas a la API después de conceder el consentimiento inicial del administrador del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-238">This method must be used for applications that run continuously in the background calling the APIs once the initial tenant admin consent has been granted.</span></span>
    

### <a name="request-an-access-token-using-the-authorization-code"></a><span data-ttu-id="bd686-239">Solicitar un token de acceso mediante el código de autorización</span><span class="sxs-lookup"><span data-stu-id="bd686-239">Request an access token using the authorization code</span></span>

<span data-ttu-id="bd686-240">Después de que un administrador de espacio empresarial conceda el permiso, la aplicación recibe un código de autorización como un parámetro de cadena de consulta cuando Azure AD redirige al administrador del espacio empresarial a la URL designada.</span><span class="sxs-lookup"><span data-stu-id="bd686-240">After a tenant admin grants consent, your application receives an authorization code as a query string parameter when Azure AD redirects the tenant admin to your designated URL.</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="bd686-241">La aplicación realiza una solicitud HTTP REST POST a Azure AD para cambiar el código de autorización por un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-241">Your application makes an HTTP REST POST to Azure AD to exchange the authorization code for an access token.</span></span> <span data-ttu-id="bd686-242">Como aún no se conoce el id. del espacio empresarial, la solicitud POST se realizará al punto de conexión “común”, que no tiene insertado el id. de espacio empresarial en la URL:</span><span class="sxs-lookup"><span data-stu-id="bd686-242">Because the tenant ID is not yet known, the POST will be to the "common" endpoint, which does not have the tenant ID embedded in the URL:</span></span>

```http
https://login.windows.net/common/oauth2/token
```

<span data-ttu-id="bd686-243">El cuerpo de la llamada POST contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd686-243">The body of the POST contains the following:</span></span>

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a><span data-ttu-id="bd686-244">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-244">Sample request</span></span>

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

<span data-ttu-id="bd686-245">En el cuerpo de la respuesta, se incluirán varias propiedades, incluido el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-245">The body of the response will include several properties, including the access token.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="bd686-246">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-246">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

<span data-ttu-id="bd686-247">El token de acceso devuelto es un token JWT que contiene información sobre el administrador que concedió el permiso y la aplicación que solicita el acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-247">The access token that is returned is a JWT token that includes information about both the admin that granted consent and the application requesting access.</span></span> <span data-ttu-id="bd686-248">En el ejemplo siguiente, se muestra un token sin codificar.</span><span class="sxs-lookup"><span data-stu-id="bd686-248">The following shows an example of an un-encoded token.</span></span> <span data-ttu-id="bd686-249">La aplicación tiene que extraer el elemento “tid” del id. de espacio empresarial de este token y almacenarlo para que pueda usarse con el fin de solicitar tokens de acceso adicionales cuando expiren, sin la interacción adicional de administrador.</span><span class="sxs-lookup"><span data-stu-id="bd686-249">Your application must extract the tenant ID "tid" from this token and store it so that it can be used to request additional access tokens as they expire, without further admin interaction.</span></span>

#### <a name="sample-token"></a><span data-ttu-id="bd686-250">Token de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-250">Sample token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1427246416,
  "nbf": 1427246416,
  "exp": 1427250316,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "amr": [
    "pwd"
  ],
  "oid": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
  "upn": "admin@contoso.onmicrosoft.com",
  "puid": "1003BFFD8EC47CA6",
  "sub": "7XpD5OWAXM1OWmKiVKh1FOkKXV4N3OSRol6mz1pxxhU",
  "given_name": "John",
  "family_name": "Doe",
  "name": "Contoso, Inc.",
  "unique_name": "admin@contoso.onmicrosoft.com",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1",
  "scp": "ActivityFeed.Read ServiceHealth.Read",
  "acr": "1"
}
```


### <a name="request-an-access-token-by-using-client-credentials"></a><span data-ttu-id="bd686-251">Solicitar un token de acceso mediante las credenciales del cliente</span><span class="sxs-lookup"><span data-stu-id="bd686-251">Request an access token by using client credentials</span></span>

<span data-ttu-id="bd686-252">Una vez conocido el id. de espacio empresarial, la aplicación puede realizar llamadas de entre servicios a Azure AD para solicitar tokens de acceso adicionales cuando expiren.</span><span class="sxs-lookup"><span data-stu-id="bd686-252">After the tenant ID is known, your application can make service-to-service calls to Azure AD to request additional access tokens as they expire.</span></span> <span data-ttu-id="bd686-253">Estos tokens solo contienen información sobre la aplicación solicitante, no sobre el administrador que concedió el permiso inicialmente.</span><span class="sxs-lookup"><span data-stu-id="bd686-253">These tokens include information only about the requesting application and not about the admin that originally granted consent.</span></span> <span data-ttu-id="bd686-254">Para realizar llamadas entre servicios, es necesario que la aplicación use un certificado X.509 para crear la aserción de cliente con el formato de un token de portador JWT con firma SHA256 y con codificación Base 64.</span><span class="sxs-lookup"><span data-stu-id="bd686-254">Service-to-service calls require that your application use an X.509 certificate to create client assertion in the form of a base64-encoded, SHA256 signed JWT bearer token.</span></span>

<span data-ttu-id="bd686-255">Al desarrollar una aplicación en .NET, puede usar la [Biblioteca de Autenticación de Azure AD (ADAL)](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-authentication-libraries) para crear aserciones de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd686-255">When you are developing your application in .NET, you can use the [Azure AD Authentication Library (ADAL)](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-authentication-libraries) to create client assertions.</span></span> <span data-ttu-id="bd686-256">Otras plataformas de desarrollo necesitan tener bibliotecas parecidas.</span><span class="sxs-lookup"><span data-stu-id="bd686-256">Other development platforms should have similar libraries.</span></span>

<span data-ttu-id="bd686-257">Un token JWT sin codificar está formado por un encabezado y una carga que contiene las propiedades siguientes.</span><span class="sxs-lookup"><span data-stu-id="bd686-257">An un-encoded JWT token consists of a header and payload that have the following properties.</span></span>

```json
HEADER:

{
  "alg": "RS256",
  "x5t": "{thumbprint of your X.509 certificate used to sign the token",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/{tenantid}/oauth2/token",
  "iss": "{your app client ID}",
  "sub": "{your app client ID}"
  "jti": "{random GUID}",
  "nbf": {epoch time, before which the token is not valid},
  "exp": {epoch time, after which the token is not valid},
}

```

#### <a name="sample-jwt-token"></a><span data-ttu-id="bd686-258">Token JWT de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-258">Sample JWT token</span></span>


```json
HEADER:

{
  "alg": "RS256",
  "x5t": "YyfshJC3rPQ-kpGo5dUaiY5t3iU",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token",
  "iss": "a6099727-6b7b-482c-b509-1df309acc563",
  "sub": "a6099727-6b7b-482c-b509-1df309acc563"
  "jti": "0ce254c4-81b1-4a2e-8436-9a8c3b49dfb9",
  "nbf": 1427248048,
  "exp": 1427248648,
}
```

<span data-ttu-id="bd686-259">Después, la aserción de cliente se pasa a Azure AD como parte de la llamada entre servicios para solicitar un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="bd686-259">The client assertion is then passed to Azure AD as part of a service-to-service call to request an access token.</span></span> <span data-ttu-id="bd686-260">Al usar credenciales de cliente para solicitar un token de acceso, use una llamada HTTP POST a un punto de conexión específico de un espacio empresarial, donde se inserta en la URL el id. de espacio empresarial extraído y almacenado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bd686-260">When using client credentials to request an access token, use an HTTP POST to a tenant-specific endpoint, where the previously extracted and stored tenant ID is embedded in the URL.</span></span>


```http
https://login.windows.net/{tenantid}/oauth2/token
```

<span data-ttu-id="bd686-261">El cuerpo de la llamada POST contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd686-261">The body of the POST contains the following:</span></span>


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a><span data-ttu-id="bd686-262">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-262">Sample request</span></span>

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

<span data-ttu-id="bd686-263">La respuesta será la misma que antes, pero ahora el token no tendrá las mismas propiedades, ya que no contiene las propiedades del administrador que concedió el permiso.</span><span class="sxs-lookup"><span data-stu-id="bd686-263">The response will be the same as before, but the token will not have the same properties, because it does not contain properties of the admin that granted consent.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="bd686-264">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-264">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a><span data-ttu-id="bd686-265">Token de acceso de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bd686-265">Sample access token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1431655194,
  "nbf": 1431655194,
  "exp": 1431659094,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "roles": [
    "ServiceHealth.Read",
    "ActivityFeed.Read"
  ],
  "oid": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "sub": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "idp": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1"
}
```


## <a name="build-your-app"></a><span data-ttu-id="bd686-266">Crear una aplicación</span><span class="sxs-lookup"><span data-stu-id="bd686-266">Build your app</span></span>

<span data-ttu-id="bd686-267">Después de registrar la aplicación en Azure AD y configurarla con los permisos necesarios, estará preparado para crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bd686-267">Now that you have registered your app in Azure AD and configured it with the necessary permissions, you're ready to build your app.</span></span> <span data-ttu-id="bd686-268">Estos son algunos de los aspectos clave que necesita tener en cuenta al diseñar y crear su aplicación:</span><span class="sxs-lookup"><span data-stu-id="bd686-268">The following are some of the key aspects to consider when designing and building your app:</span></span>

- <span data-ttu-id="bd686-269">**Experiencia de consentimiento**.</span><span class="sxs-lookup"><span data-stu-id="bd686-269">**The consent experience**.</span></span> <span data-ttu-id="bd686-270">Para obtener el consentimiento de los clientes, necesita dirigirlos en un explorador al sitio web de Azure AD con la URL especial descrita anteriormente y, además, necesita disponer de un sitio web al que Azure AD redirija al administrador después de conceder el permiso.</span><span class="sxs-lookup"><span data-stu-id="bd686-270">To obtain consent from your customers, you must direct them in a browser to the Azure AD website, using the specially constructed URL described previously, and you must have a website to which Azure AD will redirect the admin once they grant consent.</span></span> <span data-ttu-id="bd686-271">El sitio web necesita extraer el código de autorización de la URL y usarlo para solicitar un token de acceso desde el que podrá obtener el id. del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd686-271">This website must extract the authorization code from the URL and use it to request an access token from which it can obtain the tenant ID.</span></span>
    
- <span data-ttu-id="bd686-272">**Almacenar el id. de espacio empresarial en el sistema**.</span><span class="sxs-lookup"><span data-stu-id="bd686-272">**Store the tenant ID in your system**.</span></span> <span data-ttu-id="bd686-273">Esto es necesario al solicitar tokens de acceso desde Azure AD y al realizar llamadas a las API de administración de Office.</span><span class="sxs-lookup"><span data-stu-id="bd686-273">This will be needed when requesting access tokens from Azure AD and when calling the Office Management APIs.</span></span>
    
- <span data-ttu-id="bd686-274">**Administración de tokens de acceso**.</span><span class="sxs-lookup"><span data-stu-id="bd686-274">**Managing access tokens**.</span></span> <span data-ttu-id="bd686-275">Necesitará un componente que solicite y administre tokens de acceso según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bd686-275">You will need a component that requests and manages access tokens as needed.</span></span> <span data-ttu-id="bd686-276">Si la aplicación realiza llamadas a la API de forma periódica, puede solicitar tokens a petición; o bien, si realiza llamadas a la API de forma continua para recuperar datos, puede solicitar tokens a intervalos regulares (por ejemplo, cada 45 minutos).</span><span class="sxs-lookup"><span data-stu-id="bd686-276">If your app calls the APIs periodically, it can request tokens on demand, or if it calls the APIs continuously to retrieve data, it can request tokens at regular intervals (for example, every 45 minutes).</span></span>
    
- <span data-ttu-id="bd686-277">**Implemente un agente de escucha de webhook** que necesite la API específica que vaya a usar.</span><span class="sxs-lookup"><span data-stu-id="bd686-277">**Implement a webhook listener** as needed by the particular API you are using.</span></span>
    
- <span data-ttu-id="bd686-278">**Almacenamiento y recuperación de datos**.</span><span class="sxs-lookup"><span data-stu-id="bd686-278">**Data retrieval and storage**.</span></span> <span data-ttu-id="bd686-279">Necesita un componente que recupere datos de cada espacio empresarial, bien mediante la realización de sondeos continuos o en respuesta a notificaciones de webhook, según la API específica que use.</span><span class="sxs-lookup"><span data-stu-id="bd686-279">You'll need a component that retrieves data for each tenant, either by using continuous polling or in response to webhook notifications, depending on the particular API you are using.</span></span>
    
