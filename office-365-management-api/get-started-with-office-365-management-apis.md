---
ms.TocTitle: Get started with Office 365 Management APIs
title: Introducción a las API de administración de Office 365
description: Las API usan Azure AD para proporcionar servicios de autenticación que pueden usarse para conceder derechos a la aplicación con el fin de obtener acceso a esos servicios.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 08f510302c1d19cf3e3e2385f1baab6133153f07
ms.sourcegitcommit: 37737b849f1b2d0484e626002978b1d4ece2c742
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "35936239"
---
# <a name="get-started-with-office-365-management-apis"></a>Introducción a las API de administración de Office 365

Al crear una aplicación que necesita acceso a servicios protegidos, como la API de administración de Office 365, necesita proporcionar un método para que el servicio conozca si la aplicación tiene derechos para obtener acceso a ella. Las API de administración de Office 365 usan Azure AD para proporcionar servicios de autenticación que pueden usarse para conceder derechos a la aplicación con el fin de obtener acceso a esos servicios. 

Hay cuatro pasos principales:

1. **Registrar la aplicación en Azure AD**. Para permitir que una aplicación tenga acceso a las API de administración de Office 365, necesita registrar la aplicación con Azure AD. Esto le permite establecer una identidad para la aplicación y especificar los niveles de permisos necesarios para obtener acceso a las API.
    
2. **Obtener el consentimiento del administrador del espacio empresarial de Office 365**. Un administrador de espacio empresarial de Office 365 tiene que conceder de manera explícita permiso para que la aplicación obtenga acceso a los datos del espacio empresarial mediante las API de administración de Office 365. El proceso de consentimiento es una experiencia basada en explorador para la que el administrador del espacio empresarial tiene que iniciar sesión en la **interfaz de usuario de consentimiento de Azure AD**, revisar los permisos de acceso que solicita la aplicación y, después, conceder o denegar la solicitud. Después de conceder la solicitud, la interfaz de usuario redirige al usuario a la aplicación con un código de autorización en la URL. La aplicación realiza una llamada entre servicios a Azure AD para cambiar este código de autorización por un token de acceso, que contiene información tanto sobre el administrador del espacio empresarial como de la aplicación. Es necesario extraer el id. del espacio empresarial del token de acceso y almacenarlo para su uso futuro.
    
3. **Solicitar tokens de acceso de Azure AD**. Con las credenciales de la aplicación según se configuraron en Azure AD, la aplicación solicita tokens de acceso adicionales para un espacio empresarial con permiso de forma continuada, sin que sean necesarias otras interacciones del administrador del espacio empresarial. Estos tokens de acceso se denominan tokens solo de aplicación porque no incluyen información sobre el administrador del espacio empresarial.
    
4. **Llamar a las API de administración de Office 365**. Los tokens de acceso solo de aplicación se pasan a las API de administración de Office 365 para autenticar y autorizar la aplicación.
    
En el diagrama siguiente, se muestra la secuencia de solicitudes de tokens de acceso y consentimiento.


![Flujo de autorización de introducción a las API de administración](images/authorization-flow.png)

> [!IMPORTANT]
> Para poder acceder a los datos a través de la API de Actividad de administración de Office 365, debe activar el registro de auditoría unificado para su organización de Office 365. Para ello, active el registro de auditoría de Office 365. Para obtener instrucciones, consulte [Activar o desactivar la búsqueda de registros de auditoría de Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off). <br/><br/>No es necesario habilitar un registro de auditoría unificado si solo usa la API de comunicaciones de servicio de Office 365.

## <a name="register-your-application-in-azure-ad"></a>Registrar la aplicación en Azure AD

Las API de administración de Office 365 usan Azure AD para proporcionar autenticación segura a los datos del espacio empresarial de Office 365. Para obtener acceso a las API de administración de Office 365, necesita registrar la aplicación en Azure AD y, como parte de la configuración, especificará los niveles de permisos que necesita la aplicación para obtener acceso a las API.


### <a name="prerequisites"></a>Requisitos previos

Para registrar la aplicación en Azure AD, necesita una suscripción a Office 365 y una suscripción a Azure AD asociada a la suscripción de Office 365. Para empezar, puede usar suscripciones de prueba, tanto para Office 365 como para Azure. Para obtener más información, vea [Introducción al programa Office 365 Developer](https://docs.microsoft.com/es-ES/office/developer-program/office-365-developer-program).


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a>Usar el Portal de administración de Azure para registrar una aplicación en Azure AD

Cuando tenga un espacio empresarial de Microsoft con las suscripciones adecuadas, podrá registrar su aplicación en Azure AD.

1. Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com/) con las credenciales del espacio empresarial de Microsoft que tenga la suscripción de Office 365 que quiera usar. También puede obtener acceso al Portal de administración de Azure mediante un vínculo que se muestra en el panel de navegación izquierdo del [Portal de administración de Office](https://portal.office.com/).
    
2. En el panel de navegación izquierdo, seleccione Active Directory (1). Asegúrese de que esté seleccionada la pestaña Directorio (2) y, después, seleccione el nombre del directorio (3).
    
   ![Página de suscripción de Office 365](images/o365-sign-up-page.png)
    
    
3. En la página del directorio, seleccione **Aplicaciones**. En Azure AD, se muestra una lista de las aplicaciones instaladas actualmente en el espacio empresarial.
    
4. Seleccione **Agregar**.
    
   ![Página Administrador de Office 365](images/o365-admin-page.png)
    
    
5. Seleccione **Agregar una aplicación desarrollada por mi organización**.
    
6. Escriba el **NOMBRE** de la aplicación y especifique el **Tipo** como APLICACIÓN WEB O API WEB.
    
7. Escriba las propiedades de la aplicación correspondientes:
    
   - **SIGN-ON URL**. URL donde los usuarios pueden iniciar sesión y usar la aplicación. Puede cambiar este valor más tarde si es necesario.
    
   - **APP ID URI**. URI usado como un identificador lógico único para la aplicación. El URI tiene que estar en un dominio personalizado verificado para que un usuario externo pueda conceder acceso a la aplicación a sus datos en Microsoft Azure AD. Por ejemplo, si el espacio empresarial de Microsoft es **contoso.onmicrosoft.com**, el URI del id. de aplicación podría ser **https://app.contoso.onmicrosoft.com**.
    
8. La aplicación ya está registrada con Azure AD y se le asignó un id. de cliente. Pero hay varios aspectos importantes que aún es necesario configurar en la aplicación.
    

### <a name="configure-your-application-properties-in-azure-ad"></a>Configurar las propiedades de la aplicación en Azure AD

Después de registrar la aplicación, tiene que especificar varias propiedades importantes que determinan cómo funciona la aplicación en Azure AD y la forma en que los administradores de espacios empresariales concederán permiso para que la aplicación obtenga acceso a sus datos mediante las API de administración de Office 365.

Para obtener más información sobre la configuración de aplicaciones de Azure AD en general, vea [Propiedades de objeto de aplicación](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-application-objects).


1. **CLIENT ID**. Azure AD genera automáticamente este valor. La aplicación usará este valor al solicitar el permiso de los administradores de espacios empresariales y al solicitar tokens solo de aplicación desde Azure AD.
    
2. **APPLICATION IS MULTI-TENANT**. Es necesario establecer esta propiedad en **YES** para permitir a los administradores de espacios empresariales conceder permiso a una aplicación para obtener acceso a sus datos mediante las API de administración de Office 365. Si esta propiedad se establece en **NO**, la aplicación solo podrá obtener acceso a los datos de su propio espacio empresarial.
    
3. **REPLY URL**. URL a la que se redirigirá un administrador de espacios empresariales después de conceder el permiso a la aplicación para obtener acceso a sus datos mediante las API de administración de Office 365. Puede configurar varias URL de respuesta si es necesario. Azure establece automáticamente la primera para que coincida con la URL de inicio de sesión que especificó al crear la aplicación, pero puede cambiar este valor si es necesario.
    
Asegúrese de seleccionar **Guardar** después de realizar cambios en estas propiedades.


### <a name="generate-a-new-key-for-your-application"></a>Generar una nueva clave para la aplicación

Las claves, también conocidas como secretos de cliente, se usan al intercambiar un código de autorización por un token de acceso.


1. En el Portal de administración de Azure, seleccione su aplicación y elija **Configurar** en el menú superior. Desplácese hasta **claves**.
    
2. Seleccione la duración de la clave y haga clic en **Guardar**.
    
   ![Página de suscripción de Azure](images/azure-subscription-page.png)
    
    
3. Azure solo mostrará el secreto de aplicación después de guardarlo. Haga clic en el icono del Portapapeles para copiar el secreto de cliente en el Portapapeles.
    
   ![Página de Azure Portal](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > Azure solo muestra el secreto de cliente en el momento en que se genera inicialmente. No se puede volver a esta página y recuperar el secreto de cliente más tarde.

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a>Configurar un certificado X.509 para habilitar las llamadas entre servicios

Una aplicación que se ejecuta en segundo plano, como un demonio servicio, puede usar las credenciales de cliente para solicitar tokens de acceso solo de aplicación sin solicitar de forma repetida el consentimiento del administrador del espacio empresarial después de recibir el consentimiento inicial. 

Para obtener más información, vea [Llamadas entre servicios con credenciales de cliente](https://msdn.microsoft.com/en-us/library/azure/dn645543.aspx).

Necesita configurar un certificado X.509 con la aplicación para usarlo como las credenciales de cliente al solicitar tokens de acceso solo de aplicación desde Azure AD. Este proceso se divide en dos pasos:

- Obtener un certificado X.509. Puede usar un certificado autofirmado o un certificado emitido por una entidad de certificación de confianza pública.
    
- Modificar el manifiesto de la aplicación para incluir la huella digital y la clave pública del certificado.
    
En las instrucciones siguientes, se muestra cómo usar la herramienta _MakeCert_ de Windows SDK o Visual Studio para generar un certificado autofirmado y exportar la clave pública a un archivo con codificación Base 64.


1. En la línea de comandos, ejecute el siguiente comando:
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > Al generar el certificado X.509, asegúrese de que la longitud de la clave sea como mínimo de 2048. Las longitudes de clave más cortas no se aceptan como claves válidas.

2. Abra el complemento MMC de certificados y conéctese a su cuenta de usuario. 
    
3. Busque el nuevo certificado en la carpeta Personal y exporte la clave pública a un archivo con codificación Base 64 (por ejemplo, nombredeempresa.cer). La aplicación usará este certificado para comunicarse con Azure AD, por lo que es importante que se asegure de conservar también el acceso a la clave privada.
    
   > [!NOTE] 
   > Puede usar Windows PowerShell para extraer la huella digital y la clave pública con codificación Base 64. Hay otras plataformas que ofrecen herramientas similares para recuperar propiedades de certificados.

4. Desde el símbolo del sistema de Windows PowerShell, escriba y ejecute los siguientes cmdlets:
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. Guarde los valores de `$base64Thumbprint`, `$base64Value` y `$keyid` para usarlos al actualizar el manifiesto de la aplicación en el siguiente conjunto de pasos.
    
   Con los valores extraídos del certificado y el id. de clave generado, tiene que actualizar el manifiesto de la aplicación en Azure AD.
    
6. En el Portal de administración de Azure, seleccione su aplicación y elija **Configurar** en el menú superior.
    
7. En la barra de comandos, seleccione **Administrar manifiesto** y, después, **Descargar manifiesto**.
    
   ![Visualizar un certificado desde la línea de comandos](images/command-line-certificate-display.png)
    
    
8. Abra el manifiesto descargado para editarlo y reemplace la propiedad vacía KeyCredentials por el siguiente JSON:
    
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
   > La propiedad [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) es una colección que permite cargar varios certificados para escenarios de sustitución o certificados X.509 de eliminación para escenarios de peligro.

9. Guarde los cambios y cargue el archivo de manifiesto de la aplicación actualizado; para ello, haga clic en **Administrar manifiesto** en la barra de comandos, seleccione **Cargar manifiesto**, busque el archivo de manifiesto actualizado y, después, selecciónelo.
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a>Especificar los permisos que necesita la aplicación para obtener acceso a las API de administración de Office 365

Por último, tendrá que especificar exactamente qué permisos necesita su aplicación de las API de administración de Office 365. Para hacerlo, agregue acceso a las API de administración de Office 365 a la aplicación y, después, especifique los permisos necesarios.


1. En el Portal de administración de Azure, seleccione la aplicación y, después, seleccione **Configurar** en el menú superior. Vaya a **Permisos para otras aplicaciones** y seleccione **Agregar aplicación**.
    
   ![Página de Azure AD](images/azure-ad-page.png)
    
    
2. Seleccione las **API de administración de Office 365** (1) para que se muestren en la columna **Seleccionado** (2) y, después, seleccione la marca de verificación en la parte inferior derecha (3) para guardar la selección y volver a la página de configuración principal de la aplicación.
    
   ![Página de aplicaciones de Azure AD](images/azure-ad-apps-page.png)
    
    
3. Las API de administración de Office ahora se muestran en la lista de aplicaciones para las que necesita permisos su aplicación. En **Permisos de aplicación** y **Permisos delegados**, seleccione los permisos que necesita la aplicación. Para obtener más información sobre cada permiso, vea la referencia de API específica.  

   > [!NOTE] 
   > Actualmente, hay cuatro permisos sin usar relacionados con informes de actividades e inteligencia sobre amenazas que se quitarán en el futuro. No seleccione ninguno de estos permisos, ya que no son necesarios.
    
   ![Cuadro de diálogo Agregar una aplicación](images/add-an-application-dialog.png)
    
    
4. Seleccione **Guardar** para guardar la configuración.
    

## <a name="get-office-365-tenant-admin-consent"></a>Obtener el consentimiento del administrador del espacio empresarial de Office 365

Después de configurar la aplicación con los permisos necesarios para usar las API de administración de Office 365, un administrador de espacios empresariales tiene que conceder de manera explícita a las aplicaciones dos permisos para obtener acceso a los datos del espacio empresarial mediante las API. Para conceder el permiso, el administrador del espacio empresarial tiene que iniciar sesión en Azure AD con la URL específica, donde podrá revisar los permisos solicitados de la aplicación. Este paso no es necesario al usar las API para obtener acceso a datos desde su propio espacio empresarial.


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

La URL de redireccionamiento tiene que coincidir o ser una subruta de una de las URL de respuesta configuradas para la aplicación en Azure AD.

Por ejemplo:

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

Para probar la URL de consentimiento, péguela en un explorador e inicie sesión con las credenciales de administrador de Office 365 de un espacio empresarial distinto del espacio empresarial que usó para registrar la aplicación. Verá la solicitud para conceder permisos a la aplicación para usar las API de administración de Office.


![Página agregada de aplicación Azure AD](images/azure-ad-app-added-page.png)

Después de seleccionar **Aceptar**, será redirigido a la página especificada y verá un código en la cadena de consulta. 

Por ejemplo:

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

La aplicación usa este código de autorización para obtener un token de acceso de Azure AD, desde el que se puede extraer el id. de espacio empresarial. Después de extraer y almacenar el id. de espacio empresarial, puede obtener otros tokens de acceso sin que sea necesario que el administrador del espacio empresarial inicie sesión.


## <a name="request-access-tokens-from-azure-ad"></a>Solicitar tokens de acceso de Azure AD

Hay dos métodos para solicitar tokens de acceso desde Azure AD:

- En el [Flujo de concesión de código de autorización](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx), un administrador de espacios empresariales concede el consentimiento explícito, que devuelve un código de autorización a la aplicación. Después, la aplicación intercambia el código de autorización por un token de acceso. Este método es necesario para obtener el consentimiento inicial que necesita la aplicación para obtener acceso a los datos del espacio empresarial mediante la API, y este primer token de acceso es necesario para obtener y almacenar el id. de espacio empresarial.
    
- El [Flujo de concesión de credenciales de cliente](https://msdn.microsoft.com/en-us/library/azure/dn645543.aspx) permite a la aplicación solicitar tokens de acceso posteriores cuando expiren los anteriores, sin que sea necesario que el administrador del espacio empresarial inicie sesión y conceda el permiso de manera explícita. Este método tiene que usarse para las aplicaciones que se ejecutan de forma continua en segundo plano mediante llamadas a la API después de conceder el consentimiento inicial del administrador del espacio empresarial.
    

### <a name="request-an-access-token-using-the-authorization-code"></a>Solicitar un token de acceso mediante el código de autorización

Después de que un administrador de espacio empresarial conceda el permiso, la aplicación recibe un código de autorización como un parámetro de cadena de consulta cuando Azure AD redirige al administrador del espacio empresarial a la URL designada.

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

La aplicación realiza una solicitud HTTP REST POST a Azure AD para cambiar el código de autorización por un token de acceso. Como aún no se conoce el id. del espacio empresarial, la solicitud POST se realizará al punto de conexión “común”, que no tiene insertado el id. de espacio empresarial en la URL:

```http
https://login.windows.net/common/oauth2/token
```

El cuerpo de la llamada POST contiene lo siguiente:

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a>Solicitud de ejemplo

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

En el cuerpo de la respuesta, se incluirán varias propiedades, incluido el token de acceso. 

#### <a name="sample-response"></a>Respuesta de ejemplo

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

El token de acceso devuelto es un token JWT que contiene información sobre el administrador que concedió el permiso y la aplicación que solicita el acceso. En el ejemplo siguiente, se muestra un token sin codificar. La aplicación tiene que extraer el elemento “tid” del id. de espacio empresarial de este token y almacenarlo para que pueda usarse con el fin de solicitar tokens de acceso adicionales cuando expiren, sin la interacción adicional de administrador.

#### <a name="sample-token"></a>Token de ejemplo

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


### <a name="request-an-access-token-by-using-client-credentials"></a>Solicitar un token de acceso mediante las credenciales del cliente

Una vez conocido el id. de espacio empresarial, la aplicación puede realizar llamadas de entre servicios a Azure AD para solicitar tokens de acceso adicionales cuando expiren. Estos tokens solo contienen información sobre la aplicación solicitante, no sobre el administrador que concedió el permiso inicialmente. Para realizar llamadas entre servicios, es necesario que la aplicación use un certificado X.509 para crear la aserción de cliente con el formato de un token de portador JWT con firma SHA256 y con codificación Base 64.

Al desarrollar una aplicación en .NET, puede usar la [Biblioteca de Autenticación de Azure AD (ADAL)](https://docs.microsoft.com/es-ES/azure/active-directory/develop/active-directory-authentication-libraries) para crear aserciones de cliente. Otras plataformas de desarrollo necesitan tener bibliotecas parecidas.

Un token JWT sin codificar está formado por un encabezado y una carga que contiene las propiedades siguientes.

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

#### <a name="sample-jwt-token"></a>Token JWT de ejemplo


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

Después, la aserción de cliente se pasa a Azure AD como parte de la llamada entre servicios para solicitar un token de acceso. Al usar credenciales de cliente para solicitar un token de acceso, use una llamada HTTP POST a un punto de conexión específico de un espacio empresarial, donde se inserta en la URL el id. de espacio empresarial extraído y almacenado anteriormente.


```http
https://login.windows.net/{tenantid}/oauth2/token
```

El cuerpo de la llamada POST contiene lo siguiente:


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a>Solicitud de ejemplo

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

La respuesta será la misma que antes, pero ahora el token no tendrá las mismas propiedades, ya que no contiene las propiedades del administrador que concedió el permiso. 

#### <a name="sample-response"></a>Respuesta de ejemplo

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a>Token de acceso de ejemplo

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


## <a name="build-your-app"></a>Crear una aplicación

Después de registrar la aplicación en Azure AD y configurarla con los permisos necesarios, estará preparado para crear la aplicación. Estos son algunos de los aspectos clave que necesita tener en cuenta al diseñar y crear su aplicación:

- **Experiencia de consentimiento**. Para obtener el consentimiento de los clientes, necesita dirigirlos en un explorador al sitio web de Azure AD con la URL especial descrita anteriormente y, además, necesita disponer de un sitio web al que Azure AD redirija al administrador después de conceder el permiso. El sitio web necesita extraer el código de autorización de la URL y usarlo para solicitar un token de acceso desde el que podrá obtener el id. del espacio empresarial.
    
- **Almacenar el id. de espacio empresarial en el sistema**. Esto es necesario al solicitar tokens de acceso desde Azure AD y al realizar llamadas a las API de administración de Office.
    
- **Administración de tokens de acceso**. Necesitará un componente que solicite y administre tokens de acceso según sea necesario. Si la aplicación realiza llamadas a la API de forma periódica, puede solicitar tokens a petición; o bien, si realiza llamadas a la API de forma continua para recuperar datos, puede solicitar tokens a intervalos regulares (por ejemplo, cada 45 minutos).
    
- **Implemente un agente de escucha de webhook** que necesite la API específica que vaya a usar.
    
- **Almacenamiento y recuperación de datos**. Necesita un componente que recupere datos de cada espacio empresarial, bien mediante la realización de sondeos continuos o en respuesta a notificaciones de webhook, según la API específica que use.
    
