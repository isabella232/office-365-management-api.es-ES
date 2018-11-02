---
ms.TocTitle: Office 365 Management APIs overview
title: Información general de las API de administración de Office 365
description: Proporciona una plataforma de extensibilidad única para todas las tareas de administración de los clientes y partners de Office 365, entre las que se incluyen las comunicaciones, la seguridad, el cumplimiento, la generación de informes y la auditoría de servicios.
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
ms.openlocfilehash: b49bbbcaaefa1d33014919eaa5f0da8fd54c0889
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834950"
---
# <a name="office-365-management-apis-overview"></a>Información general de las API de administración de Office 365

Las API de administración de Office 365 proporcionan una plataforma de extensibilidad única para todas las tareas de administración de los clientes y partners de Office 365, entre las que se incluyen las comunicaciones, la seguridad, el cumplimiento, la generación de informes y la auditoría de servicios. Todas las API de administración de Office 365 son coherentes en el diseño y la implementación con el conjunto de aplicaciones actual de las API de REST de Office 365 y usan enfoques estándares comunes del sector, como OAuth v2, OData v4 y JSON. Al igual que las otras API de Office 365, las aplicaciones se registran en Azure Active Directory, lo que brinda a los desarrolladores una forma coherente de autenticar y autorizar sus aplicaciones.

Si tiene preguntas sobre las API de administración de Office 365, publíquelas en [Stack Overflow](http://stackoverflow.com/tags/office365), con la etiqueta [office365].

## <a name="office-365-service-communications-api-preview"></a>API de comunicaciones de servicio de Office 365 (versión preliminar)

La API de comunicaciones de servicio de Office 365 se ha publicado en modo de versión preliminar. Reemplaza la API de comunicaciones de servicio de Office 365 para proporcionar información sobre el estado del servicio a los administradores y a los partners del espacio empresarial. A diferencia de la versión anterior, la nueva API de comunicaciones de servicio ofrece una experiencia de plataforma coherente y las API de REST están creadas de forma acorde, incluido el nombre de la dirección URL, el formato de los datos y la autenticación.

Las características nuevas solo se agregan a la nueva versión de la API, lo que favorece una adopción anticipada por parte de los clientes heredados. Cuando se publicó el anuncio general de la API de comunicaciones de servicio de Office 365, se inició el período de desuso de la versión anterior de la API de comunicaciones de servicio. 

Para ver la referencia de las operaciones, consulte [Referencia de la API de comunicaciones de servicio de Office 365 (versión preliminar)](office-365-service-communications-api-reference.md).


## <a name="office-365-management-activity-api"></a>API de Actividad de administración de Office 365

La API de actividad de administración de Office 365 proporciona información sobre diversas acciones y eventos de usuario, administrador, sistema y directiva de los registros de actividad de Office 365 y Azure Active Directory. Los clientes y los partners pueden usar esta información para crear soluciones de operaciones, seguridad y supervisión de cumplimiento para la empresa o mejorar las existentes. 

Para ver la referencia de las operaciones, consulte [Referencia de la API de Actividad de administración de Office 365](office-365-management-activity-api-reference.md).

## <a name="see-also"></a>Vea también

- [Introducción a las API de administración de Office 365](get-started-with-office-365-management-apis.md)
- [Esquema de la API de Actividad de administración de Office 365](office-365-management-activity-api-schema.md)
- [Solución de problemas de la API de Actividad de administración de Office 365](troubleshooting-the-office-365-management-activity-api.md)
- [API de REST de Office 365](https://docs.microsoft.com/es-ES/previous-versions/office/office-365-api/how-to/platform-development-overview)

