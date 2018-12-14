---
ms.TocTitle: Office 365 Management Activity API frequently asked questions
title: Preguntas más frecuentes sobre la API de actividad de administración de Office 365
description: Preguntas más frecuentes sobre cómo usar la API de actividad de administración de Office 365
ms.ContentId: ''
ms.topic: reference (API)
ms.date: 09/21/2018
ms.openlocfilehash: 8118f44b04beedf33e98edd5ebc63c85b8c0fbc5
ms.sourcegitcommit: a5a60b603acd9a17d7717420e377d5760e08c7da
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2018
ms.locfileid: "27240627"
---
# <a name="office-365-management-activity-api-frequently-asked-questions"></a>Preguntas más frecuentes sobre la API de actividad de administración de Office 365

#### <a name="what-events-are-audited-for-a-specific-office-365-service"></a>¿Qué eventos se auditan para un servicio de Office 365 específico?

La documentación del esquema de la API de actividad de administración de Office 365 contiene una lista completa de eventos. Para obtener más información, vea [Esquema de la API de actividad de administración de Office 365](office-365-management-activity-api-schema.md).

#### <a name="how-do-i-onboard-to-the-management-activity-api"></a>¿Cómo incorporo la API de actividad de administración?

Para empezar a usar la API de actividad de administración de Office 365, vea [Introducción a las API de administración de Office 365](get-started-with-office-365-management-apis.md).
 
#### <a name="what-is-the-throttling-limit-for-the--management-activity-api"></a>¿Cuál es el límite para la API de actividad de administración?

El límite actual es de 60 000 solicitudes por minuto por id. de editor. 

#### <a name="we-want-to-programmatically-capture-all-events-in-all-workloads-what-is-the-most-reliable-way-to-do-this"></a>Queremos capturar mediante programación todos los eventos de todas las cargas de trabajo. ¿Cuál es la forma más confiable de hacerlo?

Puede hacerlo con las API de actividad de administración de Office 365. Además, le recomendamos que use el **modelo de extracción** debido a los problemas relacionados con el uso de webhooks. Para obtener más información, vea la sección “Uso de webhooks” en [Solución de problemas de la API de actividad de administración de Office 365](troubleshooting-the-office-365-management-activity-api.md#using-webhooks).

#### <a name="is-it-true-that-mailbox-auditing-in-exchange-online-can-only-be-enabled-by-using-powershell"></a>¿Es cierto que la auditoría de buzones en Exchange Online solo puede habilitarse con PowerShell?

Sí. Pero estamos trabajando para habilitar de forma predeterminada la auditoría de buzones para todos los buzones de una organización de Office 365. Para obtener más información, vea “La auditoría de buzones de Exchange se habilitará de forma predeterminada” en el [blog Seguridad, privacidad y cumplimiento de Microsoft](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Exchange-Mailbox-Auditing-will-be-enabled-by-default/ba-p/215171).

#### <a name="are-there-any-differences-in-the-records-that-are-fetched-by-the-management-activity-api-versus-the-records-that-are-returned-by-using-the-audit-log-search-tool-in-the-office-365-security--compliance-center"></a>¿Hay alguna diferencia entre los registros obtenidos por la API de actividad de administración y los registros obtenidos con la herramienta de búsqueda de registros de auditoría del Centro de seguridad y cumplimiento de Office 365?

Los datos obtenidos por ambos métodos son los mismos. No se realiza ningún tipo de filtrado. La única diferencia es que la API obtiene datos de los últimos siete días en cada operación. Al realizar búsquedas en los registros de auditoría desde el Centro de seguridad y cumplimiento (o con el cmdlet correspondiente [Search-UnifiedAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-unifiedauditlog) en Exchange Online), se pueden obtener datos de los últimos 90 días. 
 
#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-event-driven"></a>¿No son más inmediatas las notificaciones de webhook? Después de todo, ¿no están controladas por eventos?

No. Las notificaciones de webhook no están controladas por eventos en el sentido de que el evento desencadena la notificación. Sigue siendo necesario crear el blob de contenido, y la creación del valor de contenido es lo que desencadena la entrega de notificaciones. Recientemente, se produjeron tiempos de espera más largos para las notificaciones al usar un webhook, en comparación con las consultas a la API realizadas directamente con la operación */content*. Por lo tanto, la API de actividad de administración no tiene que considerarse un sistema de alertas de seguridad en tiempo real. Microsoft ofrece otros productos para eso. En relación con la seguridad, las notificaciones de eventos de la API de actividad de administración pueden ser más apropiadas cuando se usan para determinar patrones de uso en períodos prolongados.

#### <a name="when-pulling-the-data-from-the-management-activity-api-there-is-sometimes-a-delay-of-more-than-3-to-5-days-why-is-this"></a>Al obtener los datos de la API de actividad de administración, a veces se produce un retraso de más de 3-5 días. ¿Qué significa esto?

En ocasiones, hay instancias de una interrupción temporal u otros problemas en el servicio de Office 365. En esos casos, se descartan algunos registros de auditoría y el servicio intenta reponerlos. Aunque esto ocurre solo en el 5-10 % de los registros, hay registros que pueden retrasarse en algunas situaciones. Si el retraso es superior a cinco días, vea el panel de estado del servicio en el Centro de administración de Office 365. Si es necesario, también puede abrir una incidencia con el [soporte técnico de Microsoft](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online).

#### <a name="im-encountering-a-throttling-error-in-the-management-activity-api-what-should-i-do"></a>Veo un error de limitación en la API de actividad de administración. ¿Qué tengo que hacer?

Abra una incidencia con el [soporte técnico de Microsoft](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online) y solicite un nuevo límite, e incluya una justificación empresarial para incrementar el límite. Evaluaremos la solicitud y, si es aceptada, incrementaremos el límite.

#### <a name="what-happens-if-i-disable-auditing-for-my-office-365-organization-will-i-still-get-events-via-the-management-activty-api"></a>¿Qué ocurre si deshabilito la auditoría de mi organización de Office 365? ¿Seguiré recibiendo eventos a través de la API de actividad de administración?

No. La auditoría debe estar habilitada para que su organización pueda extraer registros a través de la API de actividad de administración.
