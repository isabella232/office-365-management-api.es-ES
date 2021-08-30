---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management Activity API schema
title: Esquema de la API de Actividad de administración de Office 365
description: 'El esquema de la API de Actividad de administración de Office 365 se proporciona como un servicio de datos en dos niveles: esquemas comunes y esquemas específicos de productos.'
ms.ContentId: 1c2bf08c-4f3b-26c0-e1b2-90b190f641f5
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: 57c9fb5adcb92d2fd04c6377b7f9a320bbcc8a83
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510163"
---
# <a name="office-365-management-activity-api-schema"></a>Esquema de la API de Actividad de administración de Office 365

El esquema de la API de Actividad de administración de Office 365 se proporciona como un servicio de datos en dos niveles:

- **Esquema común**. La interfaz para acceder a los conceptos básicos de auditoría de Office 365, como Tipo de registro, Hora de creación, Tipo de usuario y Acción, así como para proporcionar dimensiones básicas (como ID de usuario), detalles de ubicación (como la dirección IP del cliente) y servicios específicos. propiedades (como ID de objeto). Establece vistas coherentes y uniformes para que los usuarios extraigan todos los datos de auditoría de Office 365 en varias vistas de nivel superior con los parámetros adecuados, y proporciona un esquema fijo para todos los orígenes de datos, lo que reduce significativamente el costo de aprendizaje. El esquema común tiene origen en los datos del producto que pertenecen a cada equipo de producto, como Exchange, SharePoint, Azure Active Directory, Yammer y OneDrive para la Empresa. Los equipos de productos de Microsoft 365 pueden ampliar el campo de Id. de objeto para agregar propiedades específicas del servicio.

- **Esquema específico de servicio**. Basado en el esquema común para proporcionar un conjunto de atributos específicos del servicio de Microsoft 365; por ejemplo, esquema de SharePoint, esquema de OneDrive para la Empresa y esquema de administración de Exchange.

## <a name="office-365-management-api-schemas"></a>Esquemas de API de administración de Office 365

Este artículo proporciona información sobre el esquema común y para cada esquema específico de producto. En la tabla siguiente, se describen los esquemas disponibles.

|Nombre del esquema|Descripción|
|:-----|:-----|
|[Esquema común](#common-schema)|La vista para extraer el tipo de registro, el identificador de usuario, la dirección IP del cliente, el tipo de usuario y la acción con dimensiones principales como propiedades de usuario (como el id. de usuario), las propiedades de ubicación (como la dirección IP del cliente) y las propiedades específicas de productos (como el id. de objeto).|
|[Esquema base de SharePoint](#sharepoint-base-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de SharePoint.|
|[Operaciones de archivos de SharePoint](#sharepoint-file-operations)|Amplía el esquema base de SharePoint con las propiedades específicas de acceso el acceso y la manipulación de archivos en SharePoint.|
|[Esquema de uso compartido de SharePoint](#sharepoint-sharing-schema)|Amplía el esquema base de SharePoint con las propiedades específicas de uso compartido.|
|[Esquema de SharePoint](#sharepoint-schema)|Amplía el esquema base de SharePoint con las propiedades específicas de SharePoint que no están relacionadas con el acceso y la manipulación de archivos.|
|[Esquema de Project](#project-schema)|Amplía el esquema base de SharePoint con las propiedades específicas de Project.|
|[Esquema de administración de Exchange](#exchange-admin-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de administración de Exchange.|
|[Esquema de buzón de Exchange](#exchange-mailbox-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de buzón de Exchange.|
|[Esquema base de Azure Active Directory](#azure-active-directory-base-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de Azure Active Directory.|
|[Esquema de inicio de sesión de Azure Active Directory](#azure-active-directory-account-logon-schema)|Amplía el esquema base de Azure Active Directory con las propiedades específicas para todos los eventos de inicio de sesión de Azure Active Directory.|
|[Esquema de inicio de sesión de STS de Azure Active Directory](#azure-active-directory-secure-token-service-sts-logon-schema)|Amplía el esquema base de Azure Active Directory con las propiedades específicas para todos los eventos de inicio de sesión de servicio de token de seguridad (STS) de Azure Active Directory.|
|[Esquema de Azure Active Directory](#azure-active-directory-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de Azure Active Directory.|
|[Esquema DLP](#dlp-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de prevención de pérdida de datos.|
|[Esquema de Centro de seguridad y cumplimiento](#security-and-compliance-center-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos del Centro de seguridad y cumplimiento.|
|[Esquema de alertas de seguridad y cumplimiento](#security-and-compliance-alerts-schema)|Amplía el esquema común con las propiedades específicas para todos las alertas de seguridad y cumplimiento de Office 365.|
|[Esquema de Yammer](#yammer-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Yammer.|
|[Esquema de base de seguridad del centro de datos](#data-center-security-base-schema)|Amplía el esquema común con las propiedades específicas para todos los datos de auditoría de seguridad del centro de datos.|
|[Esquema de cmdlet de seguridad del centro de datos](#data-center-security-cmdlet-schema)|Amplía el esquema base de seguridad de centro de datos con las propiedades específicas para todos los datos de auditoría cmdlet de seguridad del centro de datos.|
|[Esquema de Microsoft Teams](#microsoft-teams-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Microsoft Teams.|
|[Esquema de respuesta e Investigación de amenazas y Microsoft Defender para Office 365](#microsoft-defender-for-office-365-and-threat-investigation-and-response-schema)|Amplía el esquema común con las propiedades específicas de Defender para Office 365 y la investigación de amenazas y los datos de respuesta.|
|[Esquema de envío](#submission-schema)|Extiende el esquema común con las propiedades específicas para los envíos de usuarios y administradores en Microsoft Defender para Office 365.|
|[Esquema de eventos de investigación y respuesta automatizados](#automated-investigation-and-response-events-in-office-365)|Amplía el esquema común con las propiedades específicas para eventos de investigación y respuesta automatizada de Office 365 (AIR). Para ver un ejemplo, consulte el [Blog de la Comunidad técnica: Mejorar la efectividad de su SOC con Microsoft Defender para Office 365 y la API de administración de O365](https://techcommunity.microsoft.com/t5/microsoft-security-and/improve-the-effectiveness-of-your-soc-with-office-365-atp-and/ba-p/1525185).|
|[Esquema de eventos de higiene](#hygiene-events-schema)|Amplía el esquema común con las propiedades específicas de los eventos en Exchange Online Protection y Microsoft Defender para Office 365.|
|[Esquema de Power BI](#power-bi-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Power BI.|
|[Esquema de Dynamics 365](#dynamics-365-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Dynamics 365.|
|[Esquema de Workplace Analytics](#workplace-analytics-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Microsoft Workplace Analytics.|
|[Esquema de cuarentena](#quarantine-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de cuarentena.|
|[Esquema de Microsoft Forms](#microsoft-forms-schema)|Amplía el esquema común con las propiedades específicas para todos los eventos de Microsoft Forms.|
|[Esquema de etiqueta MIP](#mip-label-schema)|Amplía el esquema común con las propiedades específicas para las etiquetas de confidencialidad que se aplican manual o automáticamente a los mensajes de correo electrónico.|
|[Esquema de Exchange del Cumplimiento de comunicaciones](#communication-compliance-exchange-schema)|Amplía el esquema común con las propiedades específicas para el modelo de lenguaje ofensivo en el Cumplimiento de comunicaciones.|
|||

## <a name="common-schema"></a>Esquema común

**Nombre EntityType**: AuditRecord

|Parámetro|Tipo|¿Es obligatoria?|Descripción|
|:-----|:-----|:-----|:-----|
|Id|Combinación de GUIDEdm.Guid|Sí|Identificador único de un registro de auditoría.|
|RecordType|Self.[AuditLogRecordType](#auditlogrecordtype)|Sí|El tipo de operación indicado por el registro. Vea la tabla [AuditLogRecordType](#auditlogrecordtype) para obtener más información sobre los tipos de registros de auditoría.|
|CreationTime|Edm.Date|Sí|La fecha y hora en formato Hora universal coordinada (UTC) en las que el usuario ha realizado la actividad.|
|Operación|Edm.String|Sí|El nombre de la actividad de usuario o administrador. Para obtener una descripción de las operaciones o actividades más comunes, vea [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](https://go.microsoft.com/fwlink/p/?LinkId=708432). Esta propiedad identifica el nombre del cmdlet ejecutado para la actividad de administración de Exchange. Para eventos DLP, puede ser "DlpRuleMatch", "DlpRuleUndo" o "DlpInfo", que se describen en "Esquema DLP" a continuación.|
|OrganizationId|Edm.Guid|Sí|El GUID del espacio empresarial de Office 365 de su organización. Este valor debe ser siempre el mismo en su organización, independientemente del servicio de Office 365 en el que se produce.|
|UserType|Self.[UserType](#user-type)|Sí|El tipo de usuario que llevó a cabo la operación. Vea la tabla [UserType](#user-type) para obtener más información sobre los tipos de usuarios.|
|UserKey|Edm.String|Sí|Un id. alternativo para el usuario identificado en la propiedad id. de usuario. Por ejemplo, esta propiedad se rellena con el identificador único de passport (PUID) para los eventos efectuados por los usuarios en SharePoint, OneDrive para la Empresa y Exchange. Esta propiedad también puede especificar el mismo valor que la propiedad id. de usuario para los eventos que se producen en otros servicios y eventos efectuados por cuentas del sistema.|
|Carga de trabajo|Edm.String|No|El servicio de Office 365 en el que se produjo la actividad. 
|ResultStatus|Edm.String|No|Indica si la acción (especificada en la propiedad Operation) se completó correctamente o no. Los valores posibles son **Succeeded**, **PartiallySucceeded** o **Failed**. Para la actividad de administración de Exchange, el valor es **True** o **False**.<br/><br/>**Importante**: las distintas cargas de trabajo pueden sobrescribir el valor de la propiedad ResultStatus. Por ejemplo, para eventos de inicio de sesión STS de Azure Active Directory, un valor de **Succeeded** para ResultStatus solo indica que la operación HTTP se ha realizado correctamente. No significa que el inicio de sesión se ha realizado correctamente. Para determinar si el inicio de sesión real se ha realizado correctamente o no, vea la propiedad LogonError en el [esquema de inicio de sesión de STS de Azure Active Directory](#azure-active-directory-secure-token-service-sts-logon-schema). Si se produce un error al iniciar sesión, el valor de esta propiedad contendrá el motivo del intento de inicio de sesión incorrecto. |
|ObjectId|Edm.string|No|Para la actividad de SharePoint y OneDrive para la Empresa, el nombre de la ruta de acceso completo del archivo o carpeta al que obtuvo acceso el usuario. Para el registro de auditoría de Exchange, el nombre del objeto modificado por el cmdlet.|
|UserId|Edm.string|Sí|El UPN (nombre principal de usuario) del usuario que llevó a cabo la acción (especificado en la propiedad Operation) que ha provocado el registro; por ejemplo, `my_name@my_domain_name`. Tenga en cuenta que también se incluyen los registros de las actividades efectuadas por las cuentas del sistema (como SHAREPOINT\system o NT AUTHORITY\SYSTEM). En SharePoint, otro valor que se muestra en la propiedad UserId es app@sharepoint. Esto indica que el "usuario" que llevó a cabo esta actividad era una aplicación que tiene los permisos necesarios en SharePoint para realizar acciones en toda la organización (como buscar en un sitio de SharePoint o en una cuenta de OneDrive) en nombre de un usuario, un administrador o un servicio. Para obtener más información, lea [El usuario app@sharepoint en los registros de auditoría.](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#the-appsharepoint-user-in-audit-records) |
|ClientIP|Edm.String|Sí|La dirección IP del dispositivo que se ha usado cuando la actividad se ha registrado. La dirección IP se muestra en el formato de dirección IPv4 o IPv6.<br/><br/>Para ciertos servicios, el valor que se visualiza en esta propiedad puede ser la dirección IP de una aplicación de confianza (por ejemplo, Office en las aplicaciones web) que llama al servicio en nombre de un usuario y no la dirección IP del dispositivo utilizado por la persona que realizó la actividad. <br/><br/>También, para eventos relacionados con Azure Active Directory, la dirección IP no se registra y el valor de la propiedad ClientIP está `null`.|
|Ámbito|Self.[AuditLogScope](#auditlogscope)|No|¿Este evento fue creado por un servicio hospedado de Office 365 o por un servidor local? Los valores posibles son **online** y **onprem**. Observe que SharePoint es la única carga de trabajo que actualmente envía eventos locales a Office 365.|
|||||

### <a name="enum-auditlogrecordtype---type-edmint32"></a>Enum: AuditLogRecordType - Tipo: Edm.Int32

#### <a name="auditlogrecordtype"></a>AuditLogRecordType

|Valor|Nombre del miembro|Descripción|
|:-----|:-----|:-----|
|1|ExchangeAdmin|Eventos del registro de auditoría de administración de Exchange.|
|2|ExchangeItem|Eventos de un registro de auditoría de buzón de Exchange para las acciones que se realizan en un solo elemento, como la creación o recepción de un mensaje de correo electrónico.|
|3|ExchangeItemGroup|Eventos de un registro de auditoría de buzón de Exchange para las acciones que se pueden realizar varios elementos, como mover o eliminar uno o varios mensajes de correo electrónico.|
|4|SharePoint|Eventos de SharePoint.|
|6|SharePointFileOperation|Eventos de operación de archivo de SharePoint.|
|7|OneDrive|Eventos de OneDrive para la Empresa.|
|8|AzureActiveDirectory|Eventos de Azure Active Directory.|
|9|AzureActiveDirectoryAccountLogon|Eventos de inicio de sesión OrgId de Azure Active Directory (obsoleto).|
|10|DataCenterSecurityCmdlet|Eventos de cmdlet de seguridad del centro de datos.|
|11|ComplianceDLPSharePoint|Eventos de Protección de pérdida de datos (DLP) en SharePoint y OneDrive para la Empresa.|
|13|ComplianceDLPExchange|Eventos de Protección de pérdida de datos (DLP) en SharePoint Exchange, cuando se configura mediante la directiva DLP unificada. Los eventos DLP basados en las reglas de transporte de Exchange no son compatibles.|
|14|SharePointSharingOperation|Eventos de uso compartido de SharePoint.|
|15|AzureActiveDirectoryStsLogon|Eventos de inicio de sesión de servicio de token de seguridad (STS) en Azure Active Directory.|
|16|SkypeForBusinessPSTNUsage|Eventos de la red telefónica conmutada (RTC) de Skype Empresarial.|
|17|SkypeForBusinessUsersBlocked|Eventos del usuario bloqueado de Skype Empresarial.|
|18|SecurityComplianceCenterEOPCmdlet|Acciones de administración del Centro de seguridad y cumplimiento.|
|19|ExchangeAggregatedOperation|Eventos de auditoría del buzón de Exchange agregado.|
|20|PowerBIAudit|Eventos de Power BI.|
|21|CRM|Eventos de Dynamics 365.|
|22|Yammer|Eventos de Yammer.|
|23|SkypeForBusinessCmdlets|Eventos de Skype Empresarial.|
|24|Descubrimiento|Eventos de actividades de eDiscovery realizadas ejecutando búsquedas de contenido y administrando casos de eDiscovery en el Centro de seguridad y cumplimiento.|
|25|MicrosoftTeams|Eventos de Microsoft Teams.|
|28|ThreatIntelligence|Eventos de suplantación de identidad y malware de Exchange Online Protection y Microsoft Defender para Office 365.|
|29|MailSubmission|Eventos de envío desde Exchange Online Protection y Microsoft Defender para Office 365.|
|30|MicrosoftFlow|Eventos de Microsoft Power Automate (conocido anteriormente como Microsoft Flow).|
|31|AeD|Eventos de eDiscovery avanzado.|
|32|MicrosoftStream|Eventos de Microsoft Stream.|
|33|ComplianceDLPSharePointClassification|Eventos relacionados con la clasificación DLP en SharePoint.|
|34|ThreatFinder|Eventos relacionados con la campaña de Microsoft Defender para Office 365.|
|35|Project|Eventos de Microsoft Project.|
|36|SharePointListOperation|Eventos en la Lista de SharePoint.|
|37|SharePointCommentOperation|Eventos de comentario de SharePoint.|
|38|DataGovernance|Eventos relacionados con las directivas y etiquetas de retención en el Centro de seguridad y cumplimiento|
|39|Kaizala|Eventos de Kaizala.|
|40|SecurityComplianceAlerts|Señales de alertas de seguridad y cumplimiento.|
|41|ThreatIntelligenceUrl|Tiempo de bloqueo de Vínculos seguros y eventos de invalidación de bloqueo de Microsoft Defender para Office 365.|
|42|SecurityComplianceInsights|Eventos relacionados con las perspectivas e informes en el centro de seguridad y cumplimiento de Office 365.|
|43|MIPLabel|Eventos relacionados con la detección en la canalización de Transporte de mensajes de correo electrónico que se han etiquetado (manual o automáticamente) con etiquetas de confidencialidad. |
|44|WorkplaceAnalytics|Eventos de Workplace Analytics.|
|45|PowerAppsApp|Eventos de Power Apps.|
|46|PowerAppsPlan|Eventos de los planes de suscripción a Power Apps. |
|47|ThreatIntelligenceAtpContent|Eventos de suplantación de identidad y malware para archivos en SharePoint, OneDrive para la Empresa y Microsoft Teams de Microsoft Defender para Office 365.|
|48|LabelContentExplorer|Eventos relacionados con el [explorador de contenido de clasificación de datos](/microsoft-365/compliance/data-classification-content-explorer).|
|49|TeamsHealthcare|Eventos relacionados con la [aplicación Pacientes](/MicrosoftTeams/expand-teams-across-your-org/healthcare/patients-audit) en Microsoft Teams para asistencia sanitaria.|
|50|ExchangeItemAggregated|Eventos relacionados con [la acción MailItemsAccessed de auditoría de buzón](/microsoft-365/compliance/mailitemsaccessed-forensics-investigations)|
|51|HygieneEvent|Eventos relacionados con la protección de correo no deseado saliente. |
|52|DataInsightsRestApiAudit|Perspectiva sobre los datos de los eventos API de REST.|
|53|InformationBarrierPolicyApplication|Eventos relacionados con la aplicación de directivas de barrera de información.|
|54|SharePointListItemOperation|Eventos en la lista de SharePoint.|
|55|SharePointContentTypeOperation|Eventos de tipo de contenido de lista de SharePoint.|
|56|SharePointFieldOperation|Eventos en el campo de lista de SharePoint.|
|57|MicrosoftTeamsAdmin|Eventos de administrador de Teams.|
|58|HRSignal|Eventos relacionados con las señales de datos de RRHH que son compatibles con la solución de Administración de riesgos internos.|
|59|MicrosoftTeamsDevice|Eventos del dispositivo de Teams.|
|60|MicrosoftTeamsAnalytics|Eventos de análisis de Teams.|
|61|InformationWorkerProtection|Eventos relacionados con las alertas de usuario en peligro.|
|62|Campaña|Eventos de campaña por correo electrónico de Microsoft Defender para Office 365.|
|63|DLPEndpoint|Eventos de DLP del punto de conexión.|
|64|AirInvestigation|Eventos de respuesta ante incidentes automatizada (AIR)|
|65|Cuarentena|Eventos de cuarentena.|
|66|MicrosoftForms|Eventos de Microsoft Forms.|
|67|ApplicationAudit|Eventos de auditoría de la aplicación.|
|68|ComplianceSupervisionExchange|Eventos que son controlados por el modelo de lenguaje vulgar del Cumplimiento de comunicaciones.|
|69|CustomerKeyServiceEncryption|Eventos relacionados con el servicio de cifrado de la clave del cliente.|
|70|OfficeNative|Eventos relacionados con las etiquetas de confidencialidad aplicadas a los documentos de Office.|
|71|MipAutoLabelSharePointItem|Eventos de etiquetado automático en SharePoint.|
|72|MipAutoLabelSharePointPolicyLocation|Eventos de la directiva de etiquetado automático en SharePoint.|
|73|MicrosoftTeamsShifts|Eventos de Turnos de Teams.|
|75|MipAutoLabelExchangeItem|Eventos de etiquetado automático en Exchange.|
|76|CortanaBriefing|Eventos del Informe de tareas pendientes del correo electrónico.|
|77|Búsqueda|Eventos relacionados con la realización de consultas de búsqueda en SharePoint y Exchange.|
|78|WDATPAlerts|Eventos relacionados con las alertas generadas por Windows Defender para el punto de conexión.|
|81|MDATPAudit|Eventos de Microsoft Defender para punto de conexión.|
|82|SensitivityLabelPolicyMatch|Eventos que se generan cuando se abre o se le cambia el nombre a un archivo etiquetado con una etiqueta de confidencialidad.|
|83|SensitivityLabelAction|Evento generado cuando se aplican, actualizan o quitan las etiquetas de confidencialidad de un archivo.|
|84|SensitivityLabeledFileAction|Eventos que se generan cuando se abre o se le cambia el nombre a un archivo etiquetado con una etiqueta de confidencialidad.|
|85|AttackSim|Eventos del Simulador de ataques.|
|86|AirManualInvestigation|Eventos relacionados con las investigaciones manuales de Investigación y respuesta automatizadas (AIR). |
|87|SecurityComplianceRBAC|Eventos RBAC de seguridad y cumplimiento.|
|88|UserTraining|Eventos de formación del Simulador de ataques en Microsoft Defender para Office 365.|
|89|AirAdminActionInvestigation|Eventos relacionados con las acciones del administrador en Investigación y respuesta automatizadas (AIR).|
|90|MSTIC|Eventos de inteligencia contra amenazas de Microsoft Defender para Office 365.|
|91|PhysicalBadgingSignal|Eventos relacionados con las señales de las insignias físicas que son compatibles con la solución de la Administración de riesgos internos.|
|93|AipDiscover|Eventos del escáner de Azure Information Protection (AIP).|
|94|AipSensitivityLabelAction|Eventos de etiqueta de confidencialidad de AIP. |
|95|AipProtectionAction|Eventos de protección de AIP.|
|96|AipFileDeleted|Eventos de eliminación de archivos de AIP.|
|97|AipHeartBeat|Eventos de latidos del corazón de AIP.|
|98|MCASAlerts|Eventos correspondientes a las alertas activadas por Microsoft Cloud App Security.|
|99|OnPremisesFileShareScannerDlp|Eventos relacionados con la detección de datos confidenciales en los recursos compartidos de los archivos.|
|100|OnPremisesSharePointScannerDlp|Eventos relacionados con la detección de datos confidenciales en SharePoint.|
|101|ExchangeSearch|Eventos relacionados con el uso de Outlook en la Web (OWA) para buscar elementos del buzón.|
|102|SharePointSearch|Eventos relacionados con la búsqueda del sitio principal de SharePoint de una organización.|
|103|PrivacyInsights|Eventos de información de privacidad.|
|105|MyAnalyticsSettings|Eventos de MyAnalytics.|
|106|SecurityComplianceUserChange|Eventos relacionados con la modificación o eliminación de un usuario.|
|107|ComplianceDLPExchangeClassification|Eventos de clasificación de Exchange DLP.|
|109|MipExactDataMatch|Eventos de clasificación de Correspondencia exacta de datos (EDM).|
||||

### <a name="enum-user-type---type-edmint32"></a>Enum: Tipo de usuario - Tipo: Edm.Int32

#### <a name="user-type"></a>Tipo de usuario

|Valor|Nombre del miembro|Descripción|
|:-----|:-----|:-----|
|0|Regular|Un usuario normal.|
|1|Reserved|Un usuario reservado.|
|2|Admin|Un administrador.|
|3|DcAdmin|Un operador de centros de datos de Microsoft.|
|4|Sistema|Una cuenta del sistema.|
|5|Application|Una aplicación.|
|6|ServicePrincipal|Un servicio principal.|
|7|CustomPolicy|Una directiva personalizada.|
|8|SystemPolicy|Una directiva del sistema|
||||

### <a name="enum-auditlogscope---type-edmint32"></a>Enum: AuditLogScope - Tipo: Edm.Int32

#### <a name="auditlogscope"></a>AuditLogScope

|Valor|Nombre del miembro|Descripción|
|:-----|:-----|:-----|
|0|Online|Este evento fue creado por un servicio hospedado de O365.|
|1|Onprem|Este evento fue creado por un servidor local.|
||||

## <a name="sharepoint-base-schema"></a>Esquema base de SharePoint

|**Parámetro**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Site|Edm.Guid|No|El GUID del sitio donde se encuentra el archivo o la carpeta a la que obtuvo acceso el usuario.|
|ItemType|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[ItemType](#itemtype)"|No|El tipo de objeto al que se obtuvo acceso o que se modificó. Vea la tabla [ItemType](#itemtype) para obtener más información sobre los tipos de objetos.|
|EventSource|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[EventSource](#eventsource)"|No|Identifica que un evento se produjo en SharePoint. Los valores posibles son **SharePoint** u **ObjectModel**.|
|SourceName|Edm.String|No|La entidad que ha activado la operación auditada. Los valores posibles son SharePoint u **ObjectModel**.|
|UserAgent|Edm.String|No|Información sobre el cliente o el explorador del usuario. Esta información la proporciona el cliente o el explorador.|
|MachineDomainInfo|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|No|Información sobre las operaciones de sincronización de dispositivos. Esta información se registra solo si está presente en la solicitud.|
|MachineId|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|No|Información sobre las operaciones de sincronización de dispositivos. Esta información se registra solo si está presente en la solicitud.|
|||||

### <a name="enum-itemtype---type-edmint32"></a>Enum: ItemType - Tipo: Edm.Int32

#### <a name="itemtype"></a>ItemType

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Invalid|El elemento no es ninguno de los tipos de elementos que se muestran en esta tabla.|
|1|File|Y el elemento es un archivo.|
|5|Folder|Y el elemento es una carpeta.|
|6|Web|Y el elemento es una web.|
|7|Site|El elemento es un sitio.|
|8|Tenant|El elemento es un inquilino.|
|9|DocumentLibrary|El elemento es una biblioteca de documentos.|
|11|Page|El elemento es una página.|
||||

### <a name="enum-eventsource---type-edmint32"></a>Enum: EventSource - Tipo: Edm.Int32

#### <a name="eventsource"></a>EventSource

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|SharePoint|El origen del evento es SharePoint.|
|1|ObjectModel|El origen del evento es ObjectModel.|
||||

### <a name="enum-sharepointauditoperation---type-edmint32"></a>Enum: SharePointAuditOperation - Tipo: Edm.Int32

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|AccessInvitationAccepted|El destinatario de una invitación para ver o editar un archivo compartido (o carpeta) que ha obtenido acceso al archivo compartido haciendo clic en el vínculo de la invitación.|
|AccessInvitationCreated|El usuario envía una invitación a otra persona (dentro o fuera de su organización) para ver o editar una carpeta o un archivo compartido en un sitio de SharePoint o de OneDrive para la Empresa. Los detalles de la entrada de evento identifican el nombre del archivo que se ha compartido, el usuario al que se envió la invitación y el tipo de los permisos de uso compartido seleccionados por la persona que envió la invitación.|
|AccessInvitationExpired|Una invitación enviada a un usuario externo caduca. De forma predeterminada, una invitación enviada a un usuario fuera de su organización expira después de 7 días si no se acepta la invitación.|
|AccessInvitationRevoked|El administrador del sitio o el propietario de un sitio o un documento en SharePoint o en OneDrive para la Empresa retira una invitación enviada a un usuario fuera de su organización. Una invitación solo se puede retirar antes de ser aceptada.|
|AccessInvitationUpdated|El usuario que creó y envió una invitación a otra persona para ver o editar una carpeta o un archivo compartido en un sitio de SharePoint o de OneDrive para la Empresa vuelve a enviar la invitación.|
|AccessRequestApproved|El administrador del sitio o el propietario de un sitio o un documento en SharePoint o en OneDrive para la Empresa aprueba una solicitud de usuario para acceder al sitio o documento.|
|AccessRequestCreated|El usuario solicita acceso a un sitio o un documento en SharePoint o en OneDrive para la empresa para el que no tienen permiso de acceso. |
|AccessRequestRejected|El administrador del sitio o el propietario de un sitio o un documento en SharePoint rechaza una solicitud de usuario para acceder al sitio o documento.|
|ActivationEnabled|Los usuarios pueden habilitar para el explorador plantillas de formulario que no contienen código de formulario, requieren plena confianza, habilitan representación en un dispositivo móvil o usan conexión de datos administrada por un administrador del servidor.|
|AdministratorAddedToTermStore|Administrador de almacén de términos agregado.|
|AdministratorDeletedFromTermStore|Administrador de almacén de términos eliminado.|
|AllowGroupCreationSet|El administrador del sitio o el propietario agrega un nivel de permisos al sitio de SharePoint o de OneDrive para la Empresa que permite que un usuario al que se ha asignado ese permiso cree un grupo para ese sitio.|
|AppCatalogCreated|El catálogo de aplicaciones se creó para que las aplicaciones empresariales personalizadas estén disponibles en su entorno de SharePoint.|
|AuditPolicyRemoved|La directiva del ciclo de vida del documento se ha quitado de una colección de sitios.|
|AuditPolicyUpdate|La directiva del ciclo de vida del documento se ha actualizado para una colección de sitios.|
|AzureStreamingEnabledSet|El propietario de un portal de vídeo permitió el streaming de vídeo desde Azure.|
|CollaborationTypeModified|Se ha modificado el tipo de colaboración permitido en sitios (por ejemplo, intranet, extranet o público).|
|ConnectedSiteSettingModified|El usuario ha creado, modificado o eliminado el vínculo entre un proyecto y un sitio de proyecto o el usuario ha modificado la configuración de sincronización en el vínculo en Project Web App.|
|CreateSSOApplication|La aplicación de destino que se creó en el servicio de almacenamiento seguro.|
|CustomFieldOrLookupTableCreated|El usuario ha creado un campo personalizado o un elemento o tabla de búsqueda en Project Web App.|
|CustomFieldOrLookupTableDeleted|El usuario ha eliminado un campo personalizado o un elemento o tabla de búsqueda en Project Web App.|
|CustomFieldOrLookupTableModified|El usuario ha modificado un campo personalizado o un elemento o tabla de búsqueda en Project Web App.|
|CustomizeExemptUsers|El administrador global ha personalizado la lista de agentes de usuario exentos en el centro de administración de SharePoint. Puede especificar qué agentes de usuario están exentos de recibir una página web completa para indexarla. Esto significa que cuando un agente de usuario que ha especificado como exento encuentra un formulario de InfoPath, el formulario se devolverá como un archivo XML en lugar de como una página web completa. Esto acelera la indexación de formularios de InfoPath.|
|DefaultLanguageChangedInTermStore*|Se ha cambiado la configuración de idioma en el almacén de terminología.|
|DelegateModified|El usuario ha creado o modificado un delegado de seguridad en Project Web App.|
|DelegateRemoved|El usuario ha eliminado un delegado de seguridad en Project Web App.|
|DeleteSSOApplication|Se ha eliminado una aplicación SSO.|
|eDiscoveryHoldApplied|Se ha colocado una conservación local en un origen de contenido. Una colección de sitios de eDiscovery administra las retenciones locales (por ejemplo, el Centro de eDiscovery) en SharePoint.|
|eDiscoveryHoldRemoved|Se ha eliminado una conservación local de un origen de contenido. Una colección de sitios de eDiscovery administra las retenciones locales (por ejemplo, el Centro de eDiscovery) en SharePoint.|
|eDiscoverySearchPerformed|Se ha realizado una búsqueda de eDiscovery con una colección de sitios de eDiscovery en SharePoint.|
|EngagementAccepted|El usuario acepta una interacción de recursos en Project Web App.|
|EngagementModified|El usuario modifica una interacción de recursos en Project Web App.|
|EngagementRejected|El usuario rechaza una interacción de recursos en Project Web App.|
|EnterpriseCalendarModified|El usuario copia, modifica o eliminar un calendario de empresa en Project Web App.|
|EntityDeleted|El usuario elimina a planilla de horas trabajadas en Project Web App.|
|EntityForceCheckedIn|El usuario fuerza una protección en un calendario, un campo personalizado o una tabla de búsqueda en Project Web App.|
|ExemptUserAgentSet|El administrador global agrega un agente de usuario a la lista de agentes de usuario exentos en el centro de administración de SharePoint.|
|FileAccessed|La cuenta del sistema o el usuario accede a un archivo en un sitio de SharePoint o de OneDrive para la Empresa. Las cuentas del sistema también pueden generar eventos FileAccessed.|
|FileCheckOutDiscarded|El usuario descarta (o deshace) la extracción del repositorio de un archivo. Eso significa que cualquier cambio que haya realizado en el archivo cuando estaba extraído del repositorio se descarta y no se guarda en la versión del documento de la biblioteca de documentos.|
|FileCheckedIn|El usuario inserta en el repositorio un documento que se extrajo de una biblioteca de documentos de SharePoint o de OneDrive para la Empresa.|
|FileCheckedOut|El usuario extrae un documento ubicado en una biblioteca de documentos de SharePoint o de OneDrive para la Empresa. Los usuarios pueden extraer del repositorio y modificar documentos que se han compartido con ellos.|
|FileCopied|El usuario copia un documento de un sitio de SharePoint o de OneDrive para la Empresa. El archivo copiado puede guardarse en otra carpeta del sitio.|
|FileDeleted|El usuario elimina un documento de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileDeletedFirstStageRecycleBin|El usuario elimina un archivo de la papelera de reciclaje de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileDeletedSecondStageRecycleBin|El usuario elimina un archivo de la papelera de reciclaje de segundo nivel de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileDownloaded|El usuario descarga un documento de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileFetched|Este evento se ha sustituido por el evento FileAccessed y está en desuso.|
|FileModified|La cuenta de sistema o el usuario modifica el contenido o las propiedades de un documento ubicado en un sitio de SharePoint o de OneDrive para la Empresa.|
|FileMoved|El usuario mueve un documento desde su ubicación actual en un sitio de SharePoint o de OneDrive para la Empresa a una nueva ubicación.|
|FilePreviewed|El usuario obtiene la vista previa de un documento de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileRenamed|El usuario cambia el nombre de un documento de un sitio de SharePoint o de OneDrive para la Empresa.|
|FileRestored|El usuario restaura un documento de una papelera de reciclaje de un sitio de SharePoint o de OneDrive para la Empresa. |
|FileSyncDownloadedFull|El usuario establece una relación de sincronización y descarga archivos correctamente por primera vez en su equipo desde una biblioteca de documentos de SharePoint o de OneDrive para la Empresa.|
|FileSyncDownloadedPartial|El usuario descarga correctamente cualquier cambio en los archivos de una biblioteca de documentos de SharePoint o de OneDrive para la Empresa. Este evento indica que los cambios realizados en los archivos de la biblioteca de documentos se descargaron en el equipo del usuario. Solo se descargaron los cambios porque el usuario había descargado previamente la biblioteca de documentos (como se indica en el evento FileSyncDownloadedFull).|
|FileSyncUploadedFull|El usuario establece una relación de sincronización y carga archivos correctamente por primera vez desde su equipo a una biblioteca de documentos de SharePoint o de OneDrive para la Empresa.|
|FileSyncUploadedPartial|El usuario carga correctamente los cambios en los archivos en una biblioteca de documentos de SharePoint o de OneDrive para la Empresa. Este evento indica que cualquier cambio realizado en la versión local de un archivo de una biblioteca de documentos se carga correctamente en dicha biblioteca. Solo se descargan los cambios porque el usuario había cargado anteriormente esos archivos (como se indica en el evento FileSyncUploadedFull).|
|FileUploaded|El usuario carga un documento en una carpeta en un sitio de SharePoint o de OneDrive para la Empresa. |
|FileViewed|Este evento se ha sustituido por el evento FileAccessed y está en desuso.|
|FolderCopied|El usuario copia una carpeta de un sitio de SharePoint o de OneDrive para la Empresa en otra ubicación de SharePoint o de OneDrive para la Empresa.|
|FolderCreated|El usuario crea una carpeta en un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderDeleted|El usuario elimina una carpeta de un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderDeletedFirstStageRecycleBin|El usuario elimina una carpeta de la papelera de reciclaje de un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderDeletedSecondStageRecycleBin|El usuario elimina una carpeta de la papelera de reciclaje de segundo nivel de un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderModified|El usuario modifica una carpeta en un sitio de SharePoint o de OneDrive para la Empresa. Este evento incluye cambios de metadatos de carpeta, como etiquetas y propiedades.|
|FolderMoved|El usuario mueve una carpeta desde un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderRenamed|El usuario cambia el nombre de una carpeta en un sitio de SharePoint o de OneDrive para la Empresa.|
|FolderRestored|El usuario restaura una carpeta de la papelera de reciclaje de un sitio de SharePoint o de OneDrive para la Empresa.|
|GroupAdded|El propietario o administrador del sitio crea un grupo para un sitio de SharePoint o de OneDrive para la Empresa, o realiza una tarea que tiene como resultado la creación de un grupo. Por ejemplo, la primera vez que un usuario crea un vínculo para compartir un archivo, se agrega un grupo del sistema al sitio de OneDrive para la Empresa del usuario. Este evento también puede ser un resultado de que un usuario crease un vínculo con permisos de edición para un archivo compartido.|
|GroupRemoved|El usuario elimina un grupo de un sitio de SharePoint o de OneDrive para la Empresa. |
|GroupUpdated|El propietario o el administrador del sitio cambia la configuración de un grupo para un sitio de SharePoint o de OneDrive para la Empresa. Esto puede incluir cambiar el nombre del grupo, quién puede ver o editar la pertenencia al grupo y cómo se controlan las solicitudes de pertenencia.|
|LanguageAddedToTermStore|Se agregó un idioma al almacén de términos.|
|LanguageRemovedFromTermStore|Se quitó un idioma del almacén de términos.|
|LegacyWorkflowEnabledSet|El propietario o administrador del sitio agrega el tipo de contenido de tarea de flujo de trabajo de SharePoint al sitio. Los administradores globales también pueden habilitar los flujos de trabajo para toda la organización en el Centro de administración de SharePoint.|
|LookAndFeelModified|El usuario modifica un inicio rápido, los formatos de gráfico de Gantt o los formatos de grupo.  O bien, el usuario crea, modifica o elimina una vista en Project Web App.|
|ManagedSyncClientAllowed|El usuario establece correctamente una relación de sincronización con un sitio de SharePoint o de OneDrive para la Empresa. La relación de sincronización es correcta porque el equipo del usuario es un miembro de un dominio que se ha agregado a la lista de dominios (denominada lista de destinatarios seguros) que puede obtener acceso a las bibliotecas de documentos de su organización. Para obtener más información sobre esta característica, vea [Usar SharePoint Online PowerShell](https://go.microsoft.com/fwlink/p/?LinkID=534609) para habilitar la sincronización de OneDrive para los dominios que están en la lista de destinatarios seguros.|
|MaxQuotaModified|Se ha modificado la cuota máxima de un sitio.|
|MaxResourceUsageModified|Se ha modificado el uso máximo permitido de recursos para un sitio.|
|MySitePublicEnabledSet|El administrador del servicio SharePoint ha configurado la marca que habilita a los usuarios para tener Mis sitios en modo público.|
|NewsFeedEnabledSet|El propietario o el administrador activa la fuente RSS para un sitio de SharePoint o de OneDrive para la Empresa. Los administradores globales pueden habilitar las fuentes RSS para toda la organización en el Centro de administración de SharePoint.|
|ODBNextUXSettings|Se ha habilitado la nueva interfaz de usuario de OneDrive para la Empresa.|
|OfficeOnDemandSet|El administrador del sitio habilita Office a petición, lo que permite a los usuarios obtener acceso a la última versión de las aplicaciones de escritorio de Office. Office a petición se habilita en el Centro de administración de SharePoint y requiere una suscripción a Office 365 que incluye aplicaciones de Office completas e instaladas.|
|PageViewed|El usuario mira una página de un documento de un sitio de SharePoint o de OneDrive para la Empresa. Esto no incluye la visualización de archivos de la biblioteca de documentos de un sitio de SharePoint o de OneDrive para la Empresa en un explorador.|
|PeopleResultsScopeSet|El administrador del sitio crea o cambia el origen de resultados para las búsquedas de personas para un sitio de SharePoint.|
|PermissionSyncSettingModified|El usuario modifica la configuración de sincronización de permisos de proyecto en Project Web App.|
|PermissionTemplateModified|El usuario crea, modifica o elimina una plantilla de permisos en Project Web App.|
|PortfolioDataAccessed|El usuario accede al contenido de cartera (biblioteca de controlador, priorización de controlador, análisis de cartera) en Project Web App.|
|PortfolioDataModified|El usuario crea, modifica o elimina datos de cartera (biblioteca de controlador, priorización de controlador, análisis de cartera) en Project Web App.|
|PreviewModeEnabledSet|El administrador del sitio habilita la vista previa de documentos de un sitio de SharePoint.|
|ProjectAccessed|El usuario obtiene acceso al contenido del proyecto en Project Web App.|
|ProjectCheckedIn|El usuario inserta un proyecto que extrajo de Project Web App.|
|ProjectCheckedOut|El usuario extrae un proyecto que se encuentra en Project Web App. Los usuarios pueden desproteger y realizar cambios en los proyectos para los que tienen permiso de apertura.|
|ProjectCreated|El usuario crea un proyecto en Project Web App.|
|ProjectDeleted|El usuario elimina un proyecto en Project Web App.|
|ProjectForceCheckedIn|El usuario fuerza una inserción en un proyecto en Project Web App.|
|ProjectModified|El usuario modifica un proyecto en Project Web App.|
|ProjectPublished|El usuario publica un proyecto en Project Web App.|
|ProjectWorkflowRestarted|El usuario reinicia un flujo de trabajo en Project Web App.|
|PWASettingsAccessed|El usuario obtiene acceso a la configuración de Project Web App a través de CSOM.|
|PWASettingsModified|El usuario modifica la configuración de Project Web App.|
|QueueJobStateModified|El usuario cancela o reinicia un trabajo de cola en Project Web App.|
|QuotaWarningEnabledModified|Advertencia de modificación de la cuota de almacenamiento.|
|RenderingEnabled|Las plantillas de formulario habilitadas para el explorador se representarán mediante InfoPath Forms Services.|
|ReportingAccessed|El usuario obtuvo acceso al punto de conexión de informes en Project Web App.|
|ReportingSettingModified|El usuario modifica la configuración de informes en Project Web App.|
|ResourceAccessed|El usuario obtiene acceso a un contenido de recursos de empresa en Project Web App.|
|ResourceCheckedIn|El usuario inserta un recurso de empresa que extrajo de Project Web App.|
|ResourceCheckedOut|El usuario extrae un recurso de empresa ubicado en Project Web App.|
|ResourceCreated|El usuario crea un recurso de empresa en Project Web App.|
|ResourceDeleted|El usuario elimina un recurso de empresa en Project Web App.|
|ResourceForceCheckedIn|El usuario fuerza una inserción de un recurso de empresa en Project Web App.|
|ResourceModified|El usuario modifica un recurso de empresa en Project Web App.|
|ResourcePlanCheckedInOrOut|El usuario inserta o extrae un plan de recursos en Project Web App.|
|ResourcePlanModified|El usuario modifica un plan de recursos en Project Web App.|
|ResourcePlanPublished|El usuario publica un plan de recursos en Project Web App.|
|ResourceRedacted|El usuario redacta un recurso de empresa quitando toda la información personal en Project Web App.|
|ResourceWarningEnabledModified|Advertencia de modificación de la cuota de recursos.|
|SSOGroupCredentialsSet|Las credenciales de grupo configuradas en el Servicio de almacenamiento seguro.|
|SSOUserCredentialsSet|Las credenciales de usuario configuradas en el Servicio de almacenamiento seguro.|
|SearchCenterUrlSet|La dirección URL del centro de búsqueda configurada.|
|SecondaryMySiteOwnerSet|Un usuario ha agregado un propietario secundario para su sitio.|
|SecurityCategoryModified|El usuario crea, modifica o elimina una categoría de seguridad en Project Web App.|
|SecurityGroupModified|El usuario crea, modifica o elimina un grupo de seguridad en Project Web App.|
|SendToConnectionAdded|El administrador global crea una nueva conexión Enviar a en la página Administración de registros en el Centro de administración de SharePoint. Una conexión Enviar a especifica la configuración de un repositorio de documentos o un centro de registros. Cuando crea una conexión Enviar a, un Organizador de contenido puede enviar documentos a la ubicación especificada.|
|SendToConnectionRemoved|El administrador global elimina una conexión Enviar a en la página Administración de registros en el Centro de administración de SharePoint.|
|SharedLinkCreated|El usuario crea un vínculo a un archivo compartido en SharePoint o en OneDrive para la Empresa. Este vínculo puede enviarse a otras personas para proporcionarles acceso al archivo. Un usuario puede crear dos tipos de vínculos: un vínculo que permite al usuario ver y editar el archivo compartido o un vínculo que solo permite al usuario ver el archivo.|
|SharedLinkDisabled|El usuario deshabilita (permanentemente) un vínculo para compartir un archivo creado.|
|SharingInvitationAccepted *|El usuario acepta una invitación para compartir un archivo o carpeta. Este evento se registra cuando un usuario comparte un archivo con otros usuarios.|
|SharingRevoked|El usuario deja de compartir un archivo o carpeta que se había compartido con otros usuarios. Este evento se registra cuando un usuario deja de compartir un archivo con otros usuarios.|
|SharingSet|El usuario comparte un archivo o carpeta que se encuentra en SharePoint o en OneDrive para la Empresa con otro usuario de su organización.|
|SiteAdminChangeRequest|Solicitudes de usuario para que se les agregue como administrador de colección de sitios para una colección de sitios de SharePoint. Los administradores de colección de sitios tienen permisos de control total para la colección de sitios y todos los subsitios.|
|SiteCollectionAdminAdded*|El administrador de colección de sitios o el propietario agrega a una persona como un administrador de colección de sitios de un sitio de SharePoint o de OneDrive para la Empresa. Los administradores de colección de sitios tienen permisos de control total para la colección de sitios y todos los sub sitios.|
|SiteCollectionCreated| El administrador global crea una nueva colección de sitios de su organización de SharePoint.|
|SiteRenamed|El propietario o el administrador cambia el nombre de un sitio de SharePoint o de OneDrive para la Empresa.|
|StatusReportModified|El usuario crea, modifica o elimina un informe de estado en Project Web App.|
|SyncGetChanges|El usuario hace clic en **Sincronización** en la Bandeja de acción en SharePoint o OneDrive para la Empresa para sincronizar los cambios en un archivo en una biblioteca de documentos en su equipo.|
|TaskStatusAccessed|El usuario obtiene el estado de una o varias tareas en Project Web App.|
|TaskStatusApproved|El usuario aprueba una actualización de estado de una o varias tareas en Project Web App.|
|TaskStatusRejected|El usuario rechaza una actualización de estado de una o varias tareas en Project Web App.|
|TaskStatusSaved|El usuario guarda una actualización de estado de una o varias tareas en Project Web App.|
|TaskStatusSubmitted|El usuario envía una actualización de estado de una o varias tareas en Project Web App.|
|TimesheetAccessed|El usuario obtiene acceso a una planilla de horas trabajadas en Project Web App.|
|TimesheetApproved|El usuario aprueba una planilla de horas trabajadas en Project Web App.|
|TimesheetRejected|El usuario rechaza una planilla de horas trabajadas en Project Web App.|
|TimesheetSaved|El usuario guarda una planilla de horas trabajadas en Project Web App.|
|TimesheetSubmitted|El usuario envía una planilla de horas trabajadas de estado en Project Web App.|
|UnmanagedSyncClientBlocked|El usuario intenta establecer una relación de sincronización con un sitio de SharePoint o de OneDrive para la Empresa desde un equipo que no es miembro del dominio de su organización o es un miembro de un dominio que no se ha agregado a la lista de dominios (denominada la lista de destinatarios seguros) que puede obtener acceso a las bibliotecas de documentos de su organización. La relación de sincronización no se permite y el equipo del usuario queda bloqueado para sincronizar, descargar o cargar archivos en una biblioteca de documentos. Para obtener más información sobre esta característica, vea [Usar cmdlets de Windows PowerShell para habilitar la sincronización de OneDrive para los dominios que están en la lista de destinatarios seguros](/powershell/module/sharepoint-online/index).|
|UpdateSSOApplication|La aplicación de destino se actualizó en el Servicio de almacenamiento seguro.|
|UserAddedToGroup|El propietario o el administrador agrega a un usuario a un grupo en un sitio de SharePoint o de OneDrive para la Empresa. Agregar a un usuario a un grupo concede al usuario los permisos asignados al grupo. |
|UserRemovedFromGroup|El propietario o el administrador quita a un usuario de un grupo en un sitio de SharePoint o de OneDrive para la Empresa. Después de quitar la persona, no se le concede los permisos asignados al grupo. |
|WorkflowModified|El usuario crea, modifica o elimina un tipo de proyecto empresarial o fases de flujo de trabajo o fases de Project Web App.|
|||||

## <a name="sharepoint-file-operations"></a>Operaciones de archivos de SharePoint

Los eventos de SharePoint relacionados con archivos que aparecen en la sección "Actividades de archivos y carpetas" en [ Buscar el registro de auditoría en el Centro de protección y seguridad ](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance) utilizan este esquema.

|**Parámetro**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|SiteUrl|Edm.String|Sí|La dirección URL del sitio donde se encuentra el archivo o la carpeta a la que obtuvo acceso el usuario.|
|SourceRelativeUrl|Edm.String|No|La dirección URL de la carpeta que contiene el archivo al que obtuvo acceso el usuario. La combinación de los valores de los parámetros _SiteURL_, _SourceRelativeURL_ y _SourceFileName_ es lo mismo que el valor de la propiedad **ObjectID**, que es el nombre de la ruta de acceso completa del archivo al que obtuvo acceso el usuario.|
|SourceFileName|Edm.String|Sí|El nombre del archivo o carpeta al que obtuvo acceso el usuario.|
|SourceFileExtension|Edm.String|No|La extensión del archivo al que obtuvo acceso el usuario. Esta propiedad está en blanco si el objeto al que se obtuvo acceso es una carpeta.|
|DestinationRelativeUrl|Edm.String|No|La dirección URL de la carpeta de destino donde se copia o se mueve un archivo. La combinación de los valores de los parámetros _SiteURL_, _DestinationRelativeURL_ y _DestinationFileName_ es lo mismo que el valor de la propiedad **ObjectID**, que es el nombre de la ruta de acceso completa del archivo que se copió. Esta propiedad se muestra únicamente para los eventos FileCopied y FileMoved.|
|DestinationFileName|Edm.String|No|El nombre del archivo que se copia o mueve. Esta propiedad se muestra únicamente para los eventos FileCopied y FileMoved.|
|DestinationFileExtension|Edm.String|No|La extensión del archivo que se copia o mueve. Esta propiedad se muestra únicamente para los eventos FileCopied y FileMoved.|
|UserSharedWith|Edm.String|No|El usuario con el que se compartió un recurso.|
|SharingType|Edm.String|No|El tipo de permisos de uso compartido que se asignan al usuario con el que se compartió el recurso. Este usuario se identifica mediante el parámetro _UserSharedWith_.|
|||||

## <a name="sharepoint-sharing-schema"></a>Esquema de uso compartido de SharePoint

 Los eventos de SharePoint relacionados con el uso compartido de archivos. Se diferencian de los eventos relacionados con archivos y carpetas en que un usuario realiza una acción que tiene algún efecto en otro usuario. Para obtener información sobre el esquema de uso compartido de SharePoint, vea [Uso compartido de auditoría en el registro de auditoría de Office 365](/microsoft-365/compliance/use-sharing-auditing
).

|**Parámetro**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|TargetUserOrGroupName |Edm.String|No|Almacena el UPN o el nombre del grupo o usuario de destino con el que se compartió un recurso.|
|TargetUserOrGroupType|Edm.String|No|Identifica si el usuario o grupo de destino es un miembro, invitado, grupo o partner. |
|EventData|Código XML|No|Transmite información de seguimiento sobre la acción de uso compartido que se ha producido, como agregar un usuario a un grupo o conceder permisos de edición.|
|||||

## <a name="sharepoint-schema"></a>Esquema de SharePoint

Los eventos de SharePoint que aparecen en [ Buscar el registro de auditoría en el Centro de protección y seguridad ](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance) (excluyendo los eventos de archivos y de carpetas) utilizan este esquema.

|**Parámetro**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|CustomEvent|Edm.String|No|Cadena opcional para los eventos personalizados.|
|EventData|Edm.String|No|Carga opcional para los eventos personalizados.|
|ModifiedProperties|Collection(ModifiedProperty)|No|La propiedad se incluye para los eventos de administración, como agregar un usuario como miembro de un sitio o un grupo de administradores de colección de sitios. La propiedad incluye el nombre de la propiedad modificada (por ejemplo, el grupo de administradores del sitio), el nuevo valor de la propiedad modificada (como el usuario agregado como administrador de sitio) y el valor anterior del objeto modificado.|
|||||

## <a name="project-schema"></a>Esquema de Project

|**Parámetro**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Entidad|Edm.String|Sí| [ProjectEntity](#project-entity) para la que fue la auditoría.|
|Acción|Edm.String|Sí|[ProjectAction](#project-action) que se realizó.|
|OnBehalfOfResId|Edm.Guid|No|El id. de recurso en nombre del cual se realizó la acción.|
|||||

### <a name="enum-project-action---type-edmint32"></a>Enum: Project acción - Tipo: Edm.Int32

#### <a name="project-action"></a>Acción de proyecto

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|Aceptadas|El usuario aceptó un evento o un flujo de trabajo.|
|Accessed|El usuario obtuvo acceso a una entidad.|
|Activated|El usuario activó una entidad, un evento o un flujo de trabajo.|
|Cancelled|El usuario canceló un evento o un flujo de trabajo.|
|CheckedIn|El usuario insertó una entidad.|
|CheckedOut|El usuario extrajo una entidad.|
|Copied|El usuario copió una entidad.|
|Created|El usuario creó una entidad.|
|Deactivated|El usuario desactivó una entidad.|
|Deleted|El usuario eliminó una entidad.|
|Exported|El usuario exportó una entidad.|
|ForceCheckedIn|El usuario causó que se forzase la inserción de una entidad.|
|Modified|El usuario modificó una entidad.|
|Published|El usuario publicó una entidad.|
|Redacted|El usuario redactó una entidad.|
|Rejected|El usuario rechazó una entidad.|
|Restarted|El usuario reinició un evento o un flujo de trabajo.|
|Saved|El usuario guardó una entidad.|
|Sent|El usuario envió una entidad.|
|Submitted|El usuario envió un flujo de trabajo o una entidad para su revisión.|
|||||

### <a name="enum-project-entity---type-edmint32"></a>Enum: Project Entity - Tipo: Edm.Int32

#### <a name="project-entity"></a>Entidad del proyecto

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|CustomField|Representa de un campo personalizado de empresa.|
|Driver|Representa un controlador de cartera.|
|DriverPrioritization|Representa una priorización de la cartera.|
|Engagement|Representa una interacción de recurso.|
|EnterpriseCalendar|Representa un calendario de recursos de empresa.|
|EnterpriseProjectType|Representa un tipo de proyecto empresarial.|
|FiscalPeriod|Representa un período fiscal.|
|GanttChartFormat|Representa un formato de gráfico de Gantt.|
|GroupingFormat|Representa un formato de agrupación de vista.|
|LineClassification|Representa una clasificación de línea de parte de horas.|
|LookupTable|Representa una tabla de búsqueda empresarial.|
|PermissionTemplate|Representa una plantilla de permisos de seguridad.|
|PortfolioAnalysis|Representa un análisis de cartera.|
|Project|Representa un proyecto.|
|QueueJob|Representa un trabajo de cola.|
|QuickLaunch|Representa un elemento de inicio rápido.|
|Reporting|Representa el punto de conexión de creación de informes.|
|Resource|Representa de un recurso de empresa.|
|ResourcePlan|Representa un plan de recursos asociado a un proyecto.|
|SecurityCategory|Representa una categoría de seguridad.|
|SecurityGroup|Representa un grupo de seguridad.|
|Setting|Representa una configuración de Project Web App|
|Statusing|Representa una actualización de estado de tarea.|
|StatusReport|Representa un informe de estado.|
|TimeReportingPeriod|Representa un período de tiempo de un parte de horas|
|Timesheet|Representa una entidad de parte de horas.|
|TimesheetAuditLog|Representa un registro de auditoría de parte de horas.|
|TimesheetManager|Representa el administrador de un parte de horas.|
|UserDelegate|Representa una delegación de usuario para otro usuario.|
|View|Representa una definición de vista.|
|WorkflowPhase|Representa una fase de un flujo de trabajo.|
|WorkflowStage|Representa una fase de un flujo de trabajo.|
|||||

## <a name="exchange-admin-schema"></a>Esquema de administración de Exchange

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|ModifiedObjectResolvedName|Edm.String|No|Este es el nombre descriptivo del objeto modificado por el cmdlet. Esto solo se registra si el cmdlet modifica el objeto.|
|Parámetros|Collection(Common.NameValuePair)|No|El nombre y valor de todos los parámetros usados con el cmdlet que se identifica en la propiedad Operations.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|No|La propiedad está incluida para eventos de administración. La propiedad incluye el nombre de la propiedad modificada, el nuevo valor de la propiedad modificada y el valor anterior del objeto modificado.|
|ExternalAccess|Edm.Boolean|Sí|Especifica si el cmdlet lo ejecutó un usuario de la organización, el personal del centro de datos de Microsoft o una cuenta de servicio del centro de datos, o un administrador delegado. El valor **False** indica que el cmdlet lo ejecutó algún usuario de su organización. El valor **True** indica que el cmdlet lo ejecutó el personal del centros de datos, una cuenta de servicio del centro de datos o un administrador delegado.|
|OriginatingServer|Edm.String|No|El nombre del servidor desde el que se ejecutó el cmdlet.|
|OrganizationName|Edm.String|No|El nombre del inquilino.|
|||||

## <a name="exchange-mailbox-schema"></a>Esquema de buzón de Exchange

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|LogonType|Self.[LogonType](#logontype)|No| Indica el tipo de usuario que obtuvo acceso al buzón y llevó a cabo la operación que se ha registrado.|
|InternalLogonType|Self.[LogonType](#logontype)|No|Reservado para uso interno.|
|MailboxGuid|Edm.String|No|El GUID de Exchange del buzón al que se obtuvo acceso.|
|MailboxOwnerUPN|Edm.String|No|La dirección de correo electrónico del propietario del buzón al que se obtuvo acceso.|
|MailboxOwnerSid|Edm.String|No|El SID del propietario del buzón.|
|MailboxOwnerMasterAccountSid|Edm.String|No|SID de la cuenta principal de la cuenta del propietario del buzón.|
|LogonUserSid|Edm.String|No|El SID del usuario que realizó la operación.|
|LogonUserDisplayName|Edm.String|No|El nombre descriptivo del usuario que realizó la operación.|
|ExternalAccess|Edm.Boolean|Sí|Esto tiene el valor true si el dominio del usuario que inició sesión es diferente del dominio del propietario del buzón.|
|OriginatingServer |Edm.String|No|Representa dónde se originó la operación.|
|OrganizationName|Edm.String|No|El nombre del inquilino.|
|ClientInfoString|Edm.String|No|Información sobre el cliente de correo electrónico que se usó para realizar la operación, como la versión de explorador, la versión de Outlook o información del dispositivo móvil.|
|ClientIPAddress|Edm.String|No|La dirección IP del dispositivo que se ha usado cuando la operación se ha registrado. La dirección IP se muestra en el formato de dirección IPv4 o IPv6.|
|ClientMachineName|Edm.String|No|El nombre del equipo que hospeda al cliente de Outlook.|
|ClientProcessName|Edm.String|No|El cliente de correo electrónico que se usó para acceder al buzón. |
|ClientVersion|Edm.String|No|La versión del cliente de correo electrónico.|
|||||

### <a name="enum-logontype---type-edmint32"></a>Enum: LogonType - Tipo: Edm.Int32

#### <a name="logontype"></a>LogonType

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Owner|El propietario del buzón|
|1|Admin|Un usuario con privilegios de administrador para el buzón de un usuario.|
|2|Delegated|Un usuario con privilegios de delegado para el buzón de un usuario.|
|3|Transport|Un servicio de transporte en el centro de datos de Microsoft.|
|4|SystemService|Una cuenta de servicio del centro de datos de Microsoft|
|5|BestAccess|Reservado para uso interno.|
|6|DelegatedAdmin|Un administrador delegado.|
|||||

### <a name="exchangemailboxauditgrouprecord-schema"></a>Esquema ExchangeMailboxAuditGroupRecord

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Folder|Self.[ExchangeFolder](#exchangefolder-complex-type)|No|La carpeta donde se encuentra un grupo de elementos.|
|CrossMailboxOperations|Edm.Boolean|No|Indica si la operación implicó más de un buzón.|
|DestMailboxId|Edm.Guid|No|Establece si el valor del parámetro CrossMailboxOperations es **True**. Especifica el GUID del buzón de correo de destino.|
|DestMailboxOwnerUPN|Edm.String|No|Establece si el valor del parámetro CrossMailboxOperations es **True**. Especifica el UPN del propietario del buzón de correo de destino.|
|DestMailboxOwnerSid|Edm.String|No|Establece si el valor del parámetro CrossMailboxOperations es **True**. Especifica el SID del buzón de correo de destino.|
|DestMailboxOwnerMasterAccountSid|Edm.String|No|Establece si el valor del parámetro CrossMailboxOperations es **True**. Especifica el SID de la cuenta principal y el SID del propietario del buzón de destino.|
|DestFolder|Self.[ExchangeFolder](#exchangefolder-complex-type)|No|La carpeta de destino, para operaciones como Mover.|
|Folders|Collection(Self.[ExchangeFolder](#exchangefolder-complex-type))|No|Información sobre las carpetas de origen implicadas en una operación; por ejemplo, si las carpetas están seleccionadas y después se eliminan.|
|AffectedItems|Collection(Self.[ExchangeItem](#exchangeitem-complex-type))|No|Información sobre cada elemento del grupo.|
|||||

### <a name="exchangemailboxauditrecord-schema"></a>Esquema ExchangeMailboxAuditRecord

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Item|Self.[ExchangeItem](#exchangeitem-complex-type)|No|Representa el elemento para el que se ha realizado la operación|
|ModifiedProperties|Collection(Edm.String)|No|Por determinar|
|SendAsUserSmtp|Edm.String|No|Dirección SMTP del usuario que se está suplantando.|
|SendAsUserMailboxGuid|Edm.Guid|No|El GUID de Exchange del buzón al que se obtuvo acceso para enviar un correo electrónico.|
|SendOnBehalfOfUserSmtp|Edm.String|No|Dirección SMTP del usuario en cuyo nombre se envía el correo electrónico.|
|SendOnBehalfOfUserMailboxGuid|Edm.Guid|No|El GUID de Exchange del buzón al que se obtuvo acceso para enviar correo en su nombre.|
|||||

### <a name="exchangeitem-complex-type"></a>Tipo complejo ExchangeItem

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Sí|Id. de la tienda.|
|Subject|Edm.String|No|La línea de asunto del mensaje al que se obtuvo acceso.|
|ParentFolder|Edm.ExchangeFolder|No|El nombre de la carpeta donde se encuentra el elemento omitido.|
|Attachments|Edm.String|No|Una lista de los nombres y el tamaño de archivo de todos los elementos que se adjuntan al mensaje.|
|||||

### <a name="exchangefolder-complex-type"></a>Tipo complejo ExchangeFolder

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Sí|El id. del objeto de carpeta.|
|Path|Edm.String|No|El nombre de la carpeta del buzón donde se encuentra el mensaje al que se obtuvo acceso.|
|||||

## <a name="azure-active-directory-base-schema"></a>Esquema base de Azure Active Directory

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AzureActiveDirectoryEventType|Self.[AzureActiveDirectoryEventType](#azureactivedirectoryeventtype)|Sí|El tipo de evento de Azure AD. |
|ExtendedProperties|Collection(Common.NameValuePair)|No|Las propiedades extendidas del evento de Azure AD.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|No|Esta propiedad está incluida para eventos de administración. La propiedad incluye el nombre de la propiedad modificada, el nuevo valor de la propiedad modificada y el valor anterior de la propiedad modificada.|
|||||

### <a name="enum-azureactivedirectoryeventtype---type--edmint32"></a>Enum: AzureActiveDirectoryEventType - Tipo: Edm.Int32

#### <a name="azureactivedirectoryeventtype"></a>AzureActiveDirectoryEventType

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|AccountLogon|El evento de inicio de sesión de la cuenta.|
|AzureApplicationAuditEvent|El evento de seguridad de la aplicación de Azure.|
|||||

## <a name="azure-active-directory-account-logon-schema"></a>Esquema de inicio de sesión de Azure Active Directory

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Application|Edm.String|No|La aplicación que desencadena el evento de inicio de sesión de la cuenta, como Office 15.|
|Client|Edm.String|No|Información sobre el dispositivo del cliente, el sistema operativo del dispositivo y explorador del dispositivo que se usó para del evento de inicio de sesión de cuenta.|
|LoginStatus|Edm.Int32|Sí|Esta propiedad procede directamente de OrgIdLogon.LoginStatus. Puede realizarse la asignación de varios errores de inicio de sesión interesantes mediante algoritmos de alerta.|
|UserDomain|Edm.String|Sí|La información de identidad del inquilino (TII).|
|||||

### <a name="enum-credentialtype---type-edmint32"></a>Enum: CredentialType - Tipo: Edm.Int32

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|-1|Other|Otra autenticación.|
|0|Password|La credencial de usuario es el nombre de usuario y la contraseña.|
|1|MobilePhone|La credencial de usuario es el teléfono móvil.|
|2|SecretQuestion|La credencial de usuario es la pregunta secreta.|
|3|SecurePin|La credencial de usuario es el PIN seguro.|
|4|SecurePinReset|La credencial de usuario es el restablecimiento del PIN seguro.|
|11|EasyID|La credencial de usuario es el EasyID.|
|14|PasswordIndexCredentialType|La credencial de usuario es PasswordIndexCredentialType.|
|16|Device|La credencial de usuario es un dispositivo.|
|17|ForeignRealmIndex|La credencial de usuario es ForeignRealmIndex.|
|||||

### <a name="enum-logintype---type-edmint32"></a>Enum: LoginType - Tipo: Edm.Int32

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|-1|Other|Otro tipo i.|
|1|InitialAuth|Inicie sesión con la autenticación inicial|
|2|CookieCopy|Inicie sesión con la cookie.|
|3|SilentReAuth|Inicie sesión con la reautenticación silenciosa.|
|||||

### <a name="enum-authenticationmethod---type-edmint32"></a>Enum: AuthenticationMethod - Tipo: Edm.Int32

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Min|El método de autenticación es un método mín|
|1|Password|El método de autenticación es una contraseña.|
|2|Digest|El método de autenticación es un resumen.|
|3|ProxyAuth|El método de autenticación es un ProxyAuth.|
|4|InfoCard|El método de autenticación es un InfoCard.|
|5|DAToken|El método de autenticación es un DAToken.|
|6|Sha1RememberMyPassword|El método de autenticación es una Sha1RememberMyPassword.|
|7|LMPasswordHash|El método de autenticación es un LMPasswordHash.|
|8|ADFSFederatedToken|El método de autenticación es un ADFSFederatedToken.|
|9|EID|El método de autenticación es un EID.|
|10|DeviceID|El método de autenticación es un DeviceID. |
|11|MD5|El método de autenticación es un MD5.|
|12|EncProxyPasswordHash|El método de autenticación es un EncProxyPasswordHash.|
|13|LWAFederation|El método de autenticación es un LWAFederation.|
|14|Sha1HashedPassword|El método de autenticación es un Sha1HashedPassword.|
|15|SecurePin|El método de autenticación es un PIN seguro.|
|16|SecurePinReset|El método de autenticación es un restablecimiento de PIN seguro.|
|17|SAML20PostSimpleSign|El método de autenticación es un SAML20PostSimpleSign.|
|18|SAML20Post|El método de autenticación es un SAML20Post.|
|19|OneTimeCode|El método de autenticación es un código de un solo uso.|
|||||

## <a name="azure-active-directory-schema"></a>Esquema de Azure Active Directory

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Actor|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|No|El usuario o una entidad de servicio que efectuó la acción.|
|ActorContextId|Edm.String|No|El GUID de la organización a la que pertenece el agente.|
|ActorIpAddress|Edm.String|No|La dirección IP del actor en formato de dirección IPV4 o IPV6.|
|InterSystemsId|Edm.String|No|El GUID que realiza un seguimiento de las acciones de componentes en el servicio de Office 365.|
|IntraSystemsId|Edm.String|No|El GUID que genera Azure Active Directory para realizar un seguimiento de la acción.|
|SupportTicketId|Edm.String|No|El id. del vale de soporte de cliente para la acción en situaciones de "actuar en nombre de".|
|Target|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|No|El usuario para el que se realizó la acción (identificada por la propiedad Operation).|
|TargetContextId|Edm.String|No|El GUID de la organización a la que pertenece el usuario de destino.|
|||||

### <a name="complex-type-identitytypevaluepair"></a>Tipo complejo IdentityTypeValuePair

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Id.|Edm.String|Sí|El valor de la identidad dada el tipo.|
|Type|Self.IdentityType|Sí|El tipo de la identidad.|
|||||

### <a name="enum-identitytype---type-edmint32"></a>Enum: IdentityType - Tipo: Edm.Int32

#### <a name="identitytype"></a>IdentityType

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|Claim|La identidad es una notificación para el propósito de autorización.|
|Name|El actor de la acción de auditoría o el nombre para mostrar de la identidad de destino.|
|Other|La identidad del actor es otro tipo, como ObjectId en GUID generado por el servicio de Office 365.|
|PUID|El agente de acción de auditoría o el identificador único de Microsoft .NET Passport (PUID) de destino.|
|SPN|La identidad de una entidad de servicio si la acción la ejecuta el servicio de Office 365.|
|UPN|El nombre principal del usuario.|
|||||

## <a name="azure-active-directory-secure-token-service-sts-logon-schema"></a>Esquema de inicio de sesión de servicio de token de seguridad (STS) de Azure Active Directory

|**Parameters**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|ApplicationId|Edm.String|No|El GUID que representa la aplicación que solicita el inicio de sesión. Se puede buscar el nombre para mostrar a través de la API de Graph de Azure Active Directory.|
|Client|Edm.String|No|Información de dispositivo cliente, proporcionada por el explorador que realiza el inicio de sesión.|
|DeviceProperties|Collection(Common.NameValuePair)|No|Esta propiedad incluye varios detalles de dispositivos, como Id., nombre para mostrar, SO, navegador, IsCompliant, IsCompliantAndManaged, SessionId, y DeviceTrustType. La propiedad DeviceTrustType puede tener los siguientes valores:<br/><br/>**0**: Registro de Azure AD<br/> **1**: Unirse a Azure AD<br/> **2**: Unido a Azure AD híbrido|
|ErrorCode|Edm.String|No|Para inicios de sesión con errores (donde el valor de la propiedad Operation es UserLoginFailed), esta propiedad contiene el código de error STS (AADSTS) de Azure Active Directory. Para ver descripciones de estos códigos de error, consulte [Códigos de error de autenticación y autorización](/azure/active-directory/develop/reference-aadsts-error-codes#aadsts-error-codes). Un valor de `0` indica que el inicio de sesión se ha realizado correctamente.|
|LogonError|Edm.String|No|En el caso de los inicios de sesión con errores, esta propiedad contiene una descripción legible del motivo del error en el inicio de sesión.|
|||||

## <a name="dlp-schema"></a>Esquema DLP

Los eventos DLP están disponibles para Exchange Online, SharePoint Online y OneDrive para la Empresa. Tenga en cuenta que los eventos DLP en Exchange solo están disponibles para los eventos basados en directiva DLP unificada (por ejemplo, configurados mediante el Centro de seguridad y cumplimiento). Los eventos DLP basados en las reglas de transporte de Exchange no son compatibles.

Los eventos DLP (prevención de pérdida de datos) siempre tendrán UserKey="DlpAgent" en el esquema común. Hay tres tipos de DlpEvents que se almacenan como el valor de la propiedad Operation del esquema común:

- DlpRuleMatch: indica que se encontró una coincidencia con una regla. Estos eventos se encuentran en Exchange, SharePoint Online y en OneDrive para la Empresa. Para Exchange incluye los falsos positivos y reemplazar información. En SharePoint Online y en OneDrive para la Empresa, los falsos positivos y los reemplazos generan eventos independientes.

- DlpRuleUndo: solo existen en SharePoint Online y en OneDrive para la Empresa e indican que una acción de la directiva aplicada anteriormente se ha "deshecho", debido a la designación de falso positivo o reemplazo por el usuario, o porque el documento ya no está sujeto a directiva (ya sea debido a cambio de directiva o a cambios al contenido del documento).

- DlpInfo: solo se encuentran en SharePoint Online y en OneDrive para la Empresa e indican una designación de falso positivo, pero no se ha "deshecho" ninguna acción.

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|SharePointMetaData|Self.[SharePointMetadata](#sharepointmetadata-complex-type)|No|Describe los metadatos sobre el documento en SharePoint o en OneDrive para la Empresa, que contiene la información confidencial.|
|ExchangeMetaData|Self.[ExchangeMetadata](#exchangemetadata-complex-type)|No|Describe los metadatos sobre el mensaje de correo electrónico que contiene la información confidencial.|
|ExceptionInfo|Edm.String|No|Identifica los motivos por los que ya no se aplica una directiva o cualquier información sobre falsos positivos o invalidación indicada por el usuario final.|
|PolicyDetails|Collection(Self.[PolicyDetails](#policydetails-complex-type))|Sí|Información sobre 1 o más directivas que ha desencadenado el evento DLP.|
|SensitiveInfoDetectionIsIncluded|Boolean|Sí|Indica si el evento contiene el valor del tipo de datos confidenciales y el contexto del contenido de origen. Obtener acceso a los datos confidenciales requiere el permiso "Leer eventos de directiva DLP como información confidencial" en Azure Active Directory.|
|||||

### <a name="sharepointmetadata-complex-type"></a>Tipo complejo SharePointMetadata

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|From|Edm.String|Sí|El usuario ha desencadenado el evento. Se trata de FileOwner, LastModifier o LastSharer.|
|itemCreationTime|Edm.Date|Sí|Datetimestamp en UTC de cuando se registró el evento.|
|SiteCollectionGuid|Edm.Guid|Sí|El GUID de la colección de sitios.|
|SiteCollectionUrl|Edm.String|Sí|El nombre del sitio de SharePoint.|
|FileName|Edm.String|Sí|El nombre de la ruta de acceso.|
|FileOwner|Edm.String|Sí|El propietario del documento.|
|FilePathUrl|Edm.String|Sí|La dirección URL del documento|
|DocumentLastModifier|Edm.String|Sí|El usuario que ha modificado por última vez el documento.|
|DocumentSharer|Edm.String|Sí|El usuario que ha modificado por última vez el uso compartido del documento.|
|UniqueId|Edm.String|Sí|Un GUID que identifica el archivo.|
|LastModifiedTime|Edm.DateTime|Sí|Marca de tiempo en UTC que indica la última vez que se modificó el documento.|
|IsViewableByExternalUsers|Edm.Boolean|Sí|Determina si el archivo es accesible para cualquier usuario externo.|
|||||

### <a name="exchangemetadata-complex-type"></a>Tipo complejo ExchangeMetadata

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|MessageID|Edm.String|Sí|El identificador de mensaje de correo electrónico que ha desencadenado el evento.|
|From|Edm.String|Sí|El usuario que envió el correo electrónico.|
|To|Collection(Edm.String)|No|Un conjunto de direcciones de correo electrónico que estaban en la línea Para del mensaje.|
|CC|Collection(Edm.String)|No|Un conjunto de direcciones de correo electrónico que estaban en la línea CC del mensaje.|
|BCC|Collection(Edm.String)|No|Un conjunto de direcciones de correo electrónico que estaban en la línea CCO del mensaje.|
|Subject|Edm.String|Sí|El asunto del mensaje de correo electrónico.|
|Sent|Edm.DateTime|Sí|La hora en UTC a la que se envió el correo electrónico.|
|RecipientCount|Edm.Int32|Sí|El número total de todos los destinatarios en las líneas Para, CC y CCO del mensaje.|
|||||

### <a name="policydetails-complex-type"></a>Tipo complejo PolicyDetails

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|PolicyId|Edm.Guid|Sí|El GUID de la directiva DLP para el evento.|
|PolicyName|Edm.String|Sí|El nombre descriptivo de la directiva DLP para el evento.|
|Rules|Collection(Self.[Rules](#rules-complex-type))|Sí|Información sobre las reglas de la directiva coincidentes para el evento.|
|||||

### <a name="rules-complex-type"></a>Tipos complejo reglas

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|RuleId|Edm.Guid|Sí|El GUID de la regla DLP para el evento.|
|RuleName|Edm.String|Sí|El nombre descriptivo de la regla DLP para el evento.|
|Acciones|Collection(Edm.String)|No|Una lista de acciones como resultado de un evento RuleMatch DLP.|
|OverriddenActions|Collection(Edm.String)|No|Una lista de acciones realizadas anteriormente que ahora se han deshecho como resultado de un evento DLPRuleUndo. |
|Severity|Edm.String|No|La gravedad (baja, media y alta) de la coincidencia de regla.|
|RuleMode|Edm.String|Sí|Indica si la regla DLP solo se ha configurado para Aplicar, Auditar con notificación o Solo auditar.|
|ConditionsMatched|Self.[ConditionsMatched](#conditionsmatched-complex-type)|No|Información sobre las condiciones de la regla para las que se han encontrado coincidencias para el evento.|
|||||

### <a name="conditionsmatched-complex-type"></a>Tipo complejo ConditionsMatched

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|SensitiveInformation|Collection(Self.[SensitiveInformation](#sensitiveinformation-complex-type))|No|Información sobre el tipo de información confidencial que se detectó.|
|DocumentProperties|Collection(NameValuePair)|No|Información sobre las propiedades del documento que activaron una coincidencia de regla.|
|OtherConditions|Collection(NameValuePair)|No|Una lista de los pares de valores clave que describe cualquier otra condición para la que se encontrón coincidencias.|
|||||

### <a name="sensitiveinformation-complex-type"></a>Tipo complejo SensitiveInformation

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.Int|Sí|La confianza agregada de todas las coincidencias de patrón para el tipo de información confidencial.|
|Count|Edm.Int|Sí|El número total de instancias confidenciales detectadas.|
|Ubicación|Edm.String|No||
|SensitiveType|Edm.Guid|Sí|Un GUID que identifica el tipo de información confidencial detectado.|
|SensitiveInformationDetections|Self.SensitiveInformationDetections|No|La matriz de objetos que contienen datos de información confidencial con los siguientes detalles: valor coincidente y contexto de valor coincidente.|
|SensitiveInformationDetailedClassificationAttributes|Collection(SensitiveInformationDetailedConfidenceLevelResult)|Sí|Información sobre el recuento del tipo de información confidencial detectado para cada uno de los tres niveles de confianza (alto, medio y bajo) y si coincide o no con la regla DLP.|
|SensitiveInformationTypeName|Edm.String|No|El nombre del tipo de información confidencial.|
|UniqueCount|Edm.Int32|Sí|El recuento único de instancias confidenciales detectadas.|
|||||

### <a name="sensitiveinformationdetailedclassificationattributes-complex-type"></a>Tipo complejo SensitiveInformationDetailedClassificationAttributes

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.int32|Sí|El nivel de confianza del patrón que se detectó.|
|Count|Edm.Int32|Sí|El número de instancias confidenciales detectadas para un nivel de confianza particular.|
|IsMatch|Edm.Boolean|Sí|Indica si el recuento dado y el nivel de confianza del tipo confidencial detectado dan como resultado una coincidencia de la regla DLP.|
|||||

### <a name="sensitiveinformationdetections-complex-type"></a>Tipo complejo SensitiveInformationDetections

Los datos confidenciales de DLP solo están disponibles en la API de fuente de actividades para los usuarios a los que se les han concedido permisos "Leer datos confidenciales de DLP".

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|DetectedValues|Collection(Common.NameValuePair)|Sí|Una matriz de información confidencial que se detectó. La información contiene pares de valor con Value = valor coincidente (p. ej. Valor de tarjeta de crédito) y Context = un fragmento de contenido de origen que contiene el valor coincidente. |
|ResultsTruncated|Edm.Boolean|Sí|Indica si los registros se truncan debido al gran número de resultados. |
|||||

### <a name="exceptioninfo-complex-type"></a>Tipo complejo ExceptionInfo

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Reason|Edm.String|No|Para un evento DLPRuleUndo, indica por qué ya no se aplica la regla, lo que puede deberse a uno de los estos tres motivos: Invalidación, Cambio del documento o Cambio de directiva|
|FalsePositive|Edm.Boolean|No|Indica si el usuario designó este evento como un falso positivo.|
|Justificación|Edm.String|No|Si el usuario decidió invalidar la directiva, cualquier justificación especificada por el usuario se captura aquí.|
|Rules|Collection(Edm.Guid)|No|Una colección de GUID para las reglas que se designó como un falso positivo o invalidación o por la que se deshizo una acción.|
|||||

## <a name="security-and-compliance-center-schema"></a>Esquema de Centro de seguridad y cumplimiento

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|No|La fecha y hora en que se ejecutó el cmdlet.|
|ClientRequestId|Edm.String|No|Un GUID que puede usarse para correlacionar este cmdlet con las operaciones de UX del Centro de seguridad y cumplimiento. Esta información solo la utiliza el soporte de Microsoft.|
|CmdletVersion|Edm.String|No|La versión de compilación del cmdlet cuando se ejecutó.|
|EffectiveOrganization|Edm.String|No|El GUID de la organización que se han visto afectada por el cmdlet. (En desuso: este parámetro dejará de aparecer en el futuro.)|
|UserServicePlan|Edm.String|No|El plan de servicio de Exchange Online Protection asignado al usuario que ejecutó el cmdlet.|
|ClientApplication|Edm.String|No|Si una aplicación ejecutó el cmdlet, en lugar de un PowerShell remoto, este campo contiene el nombre de la aplicación.|
|Parámetros|Edm.String|No|El nombre y valor de los parámetros usados con el cmdlet que no incluyen información de identificación personal.|
|NonPiiParameters|Edm.String|No|El nombre y valor de los parámetros usados con el cmdlet que incluyen información de identificación personal. (En desuso: este campo dejará de aparecer en el futuro y su contenido se combinará con el campo Parameters.)|
|||||

## <a name="security-and-compliance-alerts-schema"></a>Esquema de alertas de seguridad y cumplimiento

Las señales de alerta son:

- Todas las alertas basadas en [directivas de alerta en el centro de seguridad y cumplimiento](/office365/securitycompliance/alert-policies#default-alert-policies).
- Alertas relacionadas con Office 365 generadas en [Office 365 Cloud App Security](/office365/securitycompliance/office-365-cas-overview) y [Microsoft Cloud App Security](/cloud-app-security/what-is-cloud-app-security).

Los UserId y UserKey de estos eventos son siempre SecurityComplianceAlerts. Hay tres tipos de alerta que se almacenan como el valor de la propiedad Operation del esquema común:

- AlertTriggered: una nueva alerta se genera debido a una coincidencia de directiva.

- AlertEntityGenerated: una nueva entidad se agrega a una alerta. Este evento solo es aplicables a las alertas generadas según directivas de Alerta en el Centro de seguridad y cumplimiento. Cada alerta generada puede estar asociada con uno o varios de estos eventos. Por ejemplo, una directiva de alerta está definida para desencadenar una alerta si un usuario elimina más de 100 archivos en 5 minutos. Si dos usuarios superan el umbral aproximadamente al mismo tiempo, habrá dos eventos AlertEntityGenerated, pero solo un evento AlertTriggered.

- AlertUpdated: se realizó una actualización de los metadatos de una alerta. Este evento se registra cuando el estado de una alerta se cambia (por ejemplo, de "Activo" a "Resuelto") y cuando alguien agrega un comentario a la alerta.

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AlertId|Edm.Guid|Sí|El GUID de la alerta.|
|AlertType|Self.String|Sí|Tipo de la alerta. Los tipos de alertas son: <ul><li>Sistema</li><li>Personalizado|
|Nombre|Edm.String|Sí|Nombre de la alerta.|
|PolicyId|Edm.Guid|No|El GUID de la directiva que activó la alerta.|
|Estado|Edm.String|No|Estado de la alerta. Los estados son: <ul><li><p>Activo</li><li>Investigando</li><li>Resuelto</li><li>Descartada|
|Severity|Edm.String|No|Gravedad de la alerta. Los niveles de gravedad son: <ul><li>Bajo</li><li>Mediano</li><li>Alto</li></ul>|
|Categoría|Edm.String|No|Categoría de la alerta. Las categorías son: <ul><li>AccessGovernance</li><li>DataGovernance</li><li>DataLossPrevention</li><li>InsiderRiskManagement</li><li>MailFlow</li><li>ThreatManagement</li><li>Otros|
|Origen|Edm.String|No|Origen de la alerta. Los orígenes son: <ul><li>Centro de seguridad y cumplimiento de Office 365</li><li>Cloud App Security|
|Comentarios|Edm.String|No|Comentarios de los usuarios que han visto la alerta. De forma predeterminada, es "Nueva alerta".|
|Datos|Edm.String|No|El blob de datos detallados de la alerta o la entidad de la alerta.|
|AlertEntityId|Edm.String|No|El identificador de la entidad alerta. Este parámetro solo es válido para los eventos AlertEntityGenerated.|
|EntityType|Edm.String|No|Tipo de la alerta o entidad de la alerta. Los tipos de entidad incluyen: <ul><li>Usuario</li><li>Destinatarios</li><li>Remitente</li><li>MalwareFamily</li></ul>Este parámetro solo es válido para los eventos AlertEntityGenerated.|
|||||

## <a name="yammer-schema"></a>Esquema de Yammer

Los eventos Yammer listados en [Buscar el registro de auditoría en el](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#yammer-activities)Centro de Seguridad y Cumplimiento utilizarán este esquema.

|**Parámetros**|**Tipo**|**Obligatorio**|**Descripción**|
|:-----|:-----|:-----|:-----|
|ActorUserId|Edm.String|No|El correo electrónico del usuario que llevó a cabo la operación.|
|ActorYammerUserId|Edm.Int64|No|El id. del usuario que llevó a cabo la operación.|
|DataExportType|Edm.String|No|Devuelve "data" si la exportación de datos incluye mensajes, notas, archivos, temas, usuarios y grupos; devuelve "user" si la exportación de datos incluye únicamente a los usuarios.|
|FileId|Edm.Int64|No|Id. del archivo en la operación. |
|FileName|Edm.String|No|Nombre del archivo en la operación. Se mostrará en blanco si no es relevante para la operación.|
|GroupName|Edm.String|No|Nombre del grupo en la operación. Se mostrará en blanco si no es relevante para la operación.|
|IsSoftDelete|Edm.Boolean|No|Devuelve "true" si se establece la directiva de retención de datos de la red en Eliminación temporal; devuelve "false" si se establece la directiva de retención de datos de la red en Eliminación.|
|MessageId|Edm.Int64|No|Id. del mensaje en la operación.|
|YammerNetworkId|Edm.Int64|No|El id. de la red del usuario que llevó a cabo la operación.|
|TargetUserId|Edm.String|No|El correo electrónico del usuario de destino en la operación. Se mostrará en blanco si no es relevante para la operación.|
|TargetYammerUserId|Edm.Int64|No|El id. del usuario de destino en la operación.|
|VersionId|Edm.Int64|No|El id. de versión del archivo en la operación.|
|||||

## <a name="data-center-security-base-schema"></a>Esquema de base de seguridad del centro de datos

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|DataCenterSecurityEventType|Self.[DataCenterSecurityEventType](#datacentersecurityeventtype)|Sí|El tipo de evento cmdlet en el cuadro de bloqueo.|
|||||

### <a name="enum-datacentersecurityeventtype---type-edmint32"></a>Enum: DataCenterSecurityEventType - Tipo: Edm.Int32

#### <a name="datacentersecurityeventtype"></a>DataCenterSecurityEventType

|**Nombre del miembro**|**Descripción**|
|:-----|:-----|
|DataCenterSecurityCmdletAuditEvent|Este es el valor de enumeración para el tipo de evento de auditoría de cmdlet.|
|||

## <a name="data-center-security-cmdlet-schema"></a>Esquema de cmdlet de seguridad del centro de datos

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Sí|La hora de inicio de la ejecución del cmdlet.|
|EffectiveOrganization|Edm.String|Sí|El nombre del inquilino al que iba dirigido el cmdlet o la elevación.|
|ElevationTime|Edm.Date|Sí|La hora de inicio de la elevación.|
|ElevationApprover|Edm.String|Sí|El nombre de un administrador de Microsoft.|
|ElevationApprovedTime|Edm.Date|No|La marca de tiempo para cuando se apruebe la elevación.|
|ElevationRequestId|Edm.Guid|Sí|Identificador exclusivo para la solicitud de elevación.|
|ElevationRole|Edm.String|No|El rol para la que se solicitó la elevación.|
|ElevationDuration|Edm.Int32|Sí|La duración en la que la elevación estuvo activa.|
|GenericInfo|Edm.String|No|Usado para comentarios y otra información genérica.|
|||||

## <a name="microsoft-teams-schema"></a>Esquema de Microsoft Teams

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AddOnGuid|Edm.Guid|No|Un identificador único del complemento que generó el evento.|
|AddOnName|Edm.String|No|El nombre del complemento que generó el evento.|
|AddOnType|Self.[AddOnType](#addontype)|No|El tipo de complemento que generó el evento.|
|ChannelGuid|Edm.Guid|No|Un identificador único para el canal que se audita.|
|ChannelName|Edm.String|No|El nombre del canal que se audita.|
|ChannelType|Edm.String|No|El tipo de canal que se está auditando (estándar o privado).|
|ExtraProperties|Collection(Self.[KeyValuePair](#keyvaluepair-complex-type))|No|Una lista de propiedades adicionales.|
|HostedContents|Colección(Auto.[HostedContent](#hostedcontent-complex-type))|No|Una colección de contenidos alojados en el chat o en el canal.|
|Members|Collection(Self.[MicrosoftTeamsMember](#microsoftteamsmember-complex-type))|No|Una lista de usuarios en un equipo.|
|MessageId|Edm.String|No|Un identificador de mensaje de un canal o chat.|
|MessageURLs|Edm.String|No|Disponible para cualquier URL enviada en los mensajes de Teams.|
|Mensajes|Colección(Auto.[Mensaje](#message-complex-type))|No|Una colección de mensajes del chat o del canal.|
|MessageSizeInBytes|Edm.Int64|No|El tamaño de un mensaje de chat o canal en bytes con codificación UTF-16.|
|Nombre|Edm.String|No|Solo está disponible para eventos de configuración. Nombre de la configuración que ha cambiado.|
|NewValue|Edm.String|No|Solo está disponible para eventos de configuración. Valor nuevo de la configuración.|
|OldValue|Edm.String|No|Solo está disponible para eventos de configuración. Valor antiguo de la configuración.|
|SubscriptionId|Edm.String|No|Un identificador único de una suscripción de notificación de cambios de Microsoft Graph.|
|TabType|Edm.String|No|Solo está disponible para los eventos de pestaña. El tipo de pestaña que generó el evento.|
|TeamGuid|Edm.Guid|No|Un identificador único del equipo que se audita.|
|TeamName|Edm.String|No|El nombre del equipo que se audita.|
||||

### <a name="microsoftteamsmember-complex-type"></a>Tipo complejo MicrosoftTeamsMember

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|UPN|Edm.String|No|El nombre principal del usuario.|
|Role|Self.[MemberRoleType](#memberroletype)|No|El rol de usuario en el equipo.|
|DisplayName|Edm.String|No|El nombre para mostrar del usuario.|
|||||

### <a name="enum-memberroletype---type-edmint32"></a>Enum: MemberRoleType - Tipo: Edm.Int32

#### <a name="memberroletype"></a>MemberRoleType

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Member|Un usuario que es un miembro del equipo.|
|1|Owner|Un usuario que es el propietario del equipo.|
|2|Guest|Un usuario que no es un miembro del equipo.|
||||

### <a name="keyvaluepair-complex-type"></a>Tipo complejo KeyValuePair

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Key |Edm.String|No|La clave del par clave-valor.|
|Valor|Edm.String|No|El valor del par clave-valor.|
|||||

### <a name="enum-addontype---type-edmint32"></a>Enum: AddOnType - Tipo: Edm.Int32

#### <a name="addontype"></a>AddOnType

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|1|Bot|Un bot de Microsoft Teams.|
|2|Connector|Un conector de Microsoft Teams.|
|3|Tab|Una pestaña de Microsoft Teams.|
||||

### <a name="hostedcontent-complex-type"></a>Tipo complejo HostedContent

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Id|Edm.String|Sí|Un identificador único del contenido del mensaje alojado.|
|SizeInBytes|Edm.Int64|No|El tamaño del contenido del mensaje alojado en bytes.|
|||||

### <a name="message-complex-type"></a>Tipo complejo Mensaje

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AADGroupId|Edm.String|No|Un identificador único del grupo en Azure Active Directory al que pertenece el mensaje.|
|Id|Edm.String|Sí|Un identificador único del mensaje del chat o del canal.|
|ChannelGuid|Edm.String|No|Un identificador único del canal al que pertenece el mensaje.|
|ChannelName|Edm.String|No|El nombre del canal al que pertenece el mensaje.|
|ChannelType|Edm.String|No|El tipo de canal al que pertenece el mensaje.|
|ChatName|Edm.String|No|El nombre del chat al que pertenece el mensaje.|
|ChatThreadId|Edm.String|No|Un identificador único del chat al que pertenece el mensaje.|
|ParentMessageId|Edm.String|No|Un identificador único del mensaje de chat o canal principal.|
|SizeInBytes|Edm.Int64|No|El tamaño del mensaje en bytes con codificación UTF-16.|
|TeamGuid|Edm.String|No|Un identificador único del equipo al que pertenece el mensaje.|
|TeamName|Edm.String|No|El nombre del equipo al que pertenece el mensaje.|
|Versión|Edm.String|No|La versión del mensaje del chat o del canal.|
|||||
 
## <a name="microsoft-defender-for-office-365-and-threat-investigation-and-response-schema"></a>Esquema de Investigación y respuesta de amenazas y Microsoft Defender para Office 365

[Microsoft Defender para Office 365](/office365/securitycompliance/office-365-atp) y los eventos de Investigación y respuesta de amenazas están disponibles para los clientes de Office 365 que tienen una suscripción de Defender para Office 365 Plan 1, Defender para Office 365 Plan 2 o E5. Cada evento en la fuente de Defender para Office 365 corresponde a los siguientes eventos que se determinó que contenían una amenaza:

- Un mensaje de correo electrónico enviado o recibido por un usuario de la organización para el que se realizan detecciones en los mensajes en el momento de entrega y de [Purga automáticamente](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15). 

- Direcciones URL en las que ha hecho clic un usuario de la organización que se han detectado como malintencionadas en el momento del clic según la protección de [Vínculos seguros en Defender para Office 365](/office365/securitycompliance/atp-safe-links).  

- Un archivo en SharePoint Online, OneDrive para la Empresa o Microsoft Teams que la protección de [Microsoft Defender para Office 365](/office365/securitycompliance/atp-for-spo-odb-and-teams) ha detectado como malintencionado.

- Una alerta que se desencadena y que inició una [investigación automatizada](/office365/securitycompliance/automated-investigation-response-office).

> [!NOTE]
> Las funciones de Microsoft Defender para Office 365 y de Investigación y respuesta de amenazas de Office 365 (anteriormente conocida como Inteligencia sobre amenazas de Office 365) ahora forman parte de Microsoft Defender para Office 365 Plan 2, con funciones de protección contra amenazas adicionales. Para más información, consulte [Planes y precios de Microsoft Defender para Office 365](https://products.office.com/exchange/advance-threat-protection) y la [Descripción del servicio de Defender para Office 365](/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).

### <a name="email-message-events"></a>Eventos de mensaje de correo electrónico

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AttachmentData|Collection(Self.[AttachmentData](#attachmentdata))|No|Datos sobre los datos adjuntos en el mensaje de correo electrónico que ha desencadenado el evento.|
|DetectionType|Edm.String|Sí|El tipo de detección (por ejemplo, **Inline** : detectado durante la entrega; **Delayed**: detectado después de la entrega; **ZAP**: mensajes eliminados por la [purga automática](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15)). Los eventos con el tipo de detección ZAP normalmente irán precedidos de un mensaje con el tipo de detección **Delayed**.|
|DetectionMethod|Edm.String|Sí|El método o la tecnología usada por Defender para Office 365 para la detección.|
|InternetMessageId|Edm.String|Sí|El Id. del mensaje de Internet.|
|NetworkMessageId|Edm.String|Sí|El id. de mensaje de red en línea de Exchange.|
|P1Sender|Edm.String|Sí|La ruta de devolución del remitente del mensaje de correo electrónico.|
|P2Sender|Edm.String|Sí|El remitente del mensaje de correo electrónico.|
|Policy|Self.[Policy](#policy-type-and-action-type)|Sí|El tipo de directiva de filtrado (por ejemplo, **Filtro de correo no deseado** o **Antiphishing**) y el tipo de acción relacionada (como el **correo no deseado de alta confianza**, **correo no deseado** o **suplantación de identidad**) relevantes para el mensaje de correo electrónico.|
|Policy|Self.[PolicyAction](#policy-action)|Sí|La acción configurada en la directiva de filtrado (por ejemplo, **Mover a la carpeta de correo no deseado** o **Cuarentena**) relevante para el mensaje de correo electrónico.|
|P2Sender|Edm.String|Sí|El **De:** el remitente del mensaje de correo electrónico.|
|Recipients|Collection(Edm.String)|Sí|Una matriz de los destinatarios del mensaje de correo electrónico.|
|SenderIp|Edm.String|Sí|La dirección IP que envió el correo electrónico de Office 365. La dirección IP se muestra en el formato de dirección IPv4 o IPv6.|
|Subject|Edm.String|Sí|La línea de asunto del mensaje.|
|Verdict|Edm.String|Sí|El veredicto del mensaje.|
|MessageTime|Edm.Date|Sí|Fecha y hora en formato de hora universal coordinada (UTC) en la que el mensaje se ha recibido o enviado.|
|EventDeepLink|Edm.String|Sí|Vínculo profundo para el evento de correo electrónico en los informes en tiempo real o el explorador en el Centro de seguridad y cumplimiento de Office 365.|
|Acción de transferencia |Edm.String|Sí|La acción de entrega original en el mensaje de correo electrónico.|
|Ubicación de entrega original |Edm.String|Sí|La ubicación de entrega original del mensaje de correo electrónico.|
|Última ubicación de entrega |Edm.String|Sí|La última ubicación de entrega del mensaje de correo electrónico en el momento del evento.|
|Directionality |Edm.String|Sí|Identifica si un mensaje de correo electrónico era entrante, saliente o un mensaje dentro de la organización.|
|ThreatsAndDetectionTech |Edm.String|Sí|Las amenazas y las tecnologías de detección correspondientes. Este campo expone todas las amenazas en un mensaje de correo electrónico, incluida la última adición en el veredicto de correo no deseado.  Por ejemplo, ["Phish: [Spoof DMARC]","Spam: [reputación malintencionada de URL]"]. A continuación se describen las diferentes tecnologías de detección y amenazas de detección.|
|AdditionalActionsAndResults |Collection(Edm.String)|No|Las acciones adicionales que se tomaron sobre el correo electrónico, como ZAP o Remediación Manual. También incluye los resultados correspondientes.|
|Conectores |Edm.String|No|Nombres y GUID de los conectores asociados al correo electrónico.|
|AuthDetails |Collection(Self.[AuthDetails](#authdetails))|No|Las comprobaciones de autenticación que se realizan para el correo electrónico. También incluye los valores de SPF, DKIM, DMARC y CompAuth.|
|SystemOverrides |Collection(Self.[SystemOverrides](#systemoverrides))|No|Invalidaciones aplicables al correo electrónico. Pueden ser invalidaciones del sistema o del usuario.|
|Nivel de confianza de cebo |Edm.String|No|Indica el nivel de confianza asociado al veredicto de cebo. Puede ser normal o alto.|  
|||||

> [!NOTE]
> Le recomendamos que use el nuevo campo ThreatsAnd DetectionionTech porque muestra varios veredictos y las tecnologías de detección actualizadas. Esto también se alinea con los valores que vería en otras experiencias como el Explorador de amenazas y La búsqueda avanzada de amenazas. 

### <a name="detection-technologies"></a>Tecnologías de detección

|**Nombre**|**Descripción**|
|:-----|:-----|
|Filtro general |Señales de suplantación de identidad (phishing) basadas en reglas.|
|Suplantación de marca | El tipo de archivo de los datos adjuntos.|
|Suplantación de seguridad de dominio externo |El remitente está intentando suplantación de identidad de algún otro dominio.|
|Suplantación electrónica DMARC |Error de autenticación DMARC para los mensajes.|
|Dominio de suplantación | Suplantación de dominios que el cliente es propietario o define.|
|Detonación de archivos |Los datos adjuntos de archivos no son seguros durante el análisis detonado.|
|Reputación de los archivos |Datos adjuntos de archivos marcados como malo debido a una mala reputación.|
|Reputación de detonación de archivos |Datos adjuntos de archivo marcados como malo debido a la reputación de detonación anterior.|
|Coincidencia de huella digital |El mensaje se marcó como malo debido a mensajes anteriores.|
|Suplantación de inteligencia de buzón |Suplantación basada en la inteligencia de buzón.|
|Reputación de dominio |Análisis en función de la reputación del dominio.|
|Suplantación de seguridad para la organización |  El remitente está intentando suplantar electrónicamente el dominio del destinatario. |
|Filtro avanzado |  Señales de suplantación de identidad (phishing) basadas en el aprendizaje automático.|
|Motor antimalware    | Detección de los motores antimalware. |
|Detección de análisis mixto   | Varios filtros han contribuido al veredicto de este mensaje. |
|Reputación malintencionada de URL   | El mensaje se considera malo debido a una URL malintencionada. |
|Detonación de URL | El mensaje se considera malo debido a una detonación anterior de URL malintencionada. |
|Reputación de detonación de URL| El mensaje se considera malo debido a una detonación de URL malintencionada. |
|Suplantación de usuarios|    Suplantación de usuarios definidos por el administrador o aprendidos con la inteligencia de buzones.|
|Campaña   |Mensajes identificados como parte de una campaña.|

### <a name="attachmentdata-complex-type"></a>Tipo complejo AttachmentData

#### <a name="attachmentdata"></a>AttachmentData

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|FileName|Edm.String|Sí|El nombre de archivo de los datos adjuntos.|
|FileType|Edm.String|Sí|El tipo de archivo de los datos adjuntos.|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Sí|El veredicto de malware del archivo.|
|MalwareFamily|Edm.String|No|La familia de malware del archivo.|
|SHA256|Edm.String|Sí|El hash SHA256 del archivo.|
|||||

> [!NOTE]
> Dentro de la familia de malware, podrá ver el nombre exacto de MalwareFamiily (por ejemplo, HTML/Phish.VS! MSR) o carga malintencionada como una cadena estática. Una carga malintencionada debe tratarse como correo electrónico malintencionado cuando no se identifica un nombre específico.

### <a name="systemoverrides-complex-type"></a>Tipo complejo de SystemOverrides
 
#### <a name="systemoverrides"></a>SystemOverrides

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Detalles|Edm.String|No|Detalles sobre la invalidación específica (como ETR o remitente seguro) que se aplicó.|
|FinalOverride|Edm.String|No|Indica la invalidación que ha afectado a la entrega en el caso de que haya varias.|
|Resultado|Edm.String|No|Indica si el correo electrónico se estableció como permitido o bloqueado en función de la invalidación.|
|Origen|Edm.String|No|Indica si la invalidación la configuró el usuario o el espacio empresarial.|
|||||

### <a name="authdetails-complex-type"></a>Tipo complejo AuthDetails
 
#### <a name="authdetails"></a>AuthDetails
 
|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Nombre|Edm.String|No|Nombre de la comprobación de autenticación específica, como DKIM o DMARC.|
|Valor|Edm.String|No|Valor asociado a la comprobación de autenticación específica, como True o False.|
|||||
 
### <a name="enum-fileverdict---type-edmint32"></a>Enum: FileVerdict - Tipo: Edm.Int32

#### <a name="fileverdict"></a>FileVerdict

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Good|No hay amenazas detectadas.|
|1|Bad|Malware detectado en el archivo adjunto.|
|-1|Error|Error de análisis o examen.|
|-2|Timeout|Se agotó el tiempo de espera del análisis o el examen.|
|-3|Pending|El análisis o el examen no se completó.|
|||||

### <a name="enum-policy---type-edmint32"></a>Enum: Policy - Type: Edm.Int32

#### <a name="policy-type-and-action-type"></a>Tipo de directiva y tipo de acción

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|1|Anti-spam, HSPM|Acción de correo no deseado de alta confianza (HSPM) en la Directiva contra correo no deseado.|
|2|Anti-spam, SPM|Acción de correo no deseado (SPM) en la Directiva contra correo no deseado.|
|3|Anti-spam, Bulk|Acción masiva en la Directiva contra correo no deseado.|
|4|Anti-spam, PHSH|Acción de suplantación de identidad (PHSH) en la Directiva contra correo no deseado.|
|5|Anti-phish, DIMP|Acción de suplantación de dominios (DIMP) en la Directiva antiphishing.|
|6|Anti-phish, UIMP|Acción de suplantación de usuarios (UIMP) en la Directiva antiphishing.|
|7|Anti-phish, SPOOF|Acción de suplantación en la Directiva antiphishing.|
|8|Anti-phish, GIMP|La acción de inteligencia de buzón en la directiva ANTIPHISH.|
|9|Programas anti-malware, AMP| La acción de la directiva contra malware en la directiva antimalware.|
|10|Datos adjuntos seguros, SAP| La acción de directiva en la directiva Datos adjuntos seguros en Defender para Office 365.|
|11|Regla de transporte de Exchange, ETR| La acción de directiva en la regla de transporte de Exchange.|
|12|Antimalware, ZAPM| La acción de directiva de malware en la Directiva antimalware que se aplica a la purga automática de cero horas (ZAP).|
|13|Anti-phish, ZAPP| La acción política en la política antiphish aplicada a ZAP.|
|14|Anti-phish, ZAPS| La acción de la directiva de correo no deseado en la directiva contra correo no deseado aplicada a ZAP.|
|15|Filtro de correo no deseado, correo electrónico de suplantación de identidad de alta confianza (HPHISH)|Acción de correo electrónico de suplantación de identidad de alta confianza en la Directiva contra correo no deseado.|
|17|Filtro de correo no deseado, Directiva de correo no deseado saliente (OSPM)|Acción de directiva en la directiva de filtro de correo no deseado saliente en filtro de correo electrónico no deseado.|
||||

### <a name="enum-policyaction---type-edmint32"></a>Enum: PolicyAction - Type: Edm.Int32

#### <a name="policy-action"></a>Acción de directiva

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|MoveToJMF|La acción de directiva es moverse a la carpeta correo no deseado.|
|1|AddXHeader|La acción de directiva es agregar el encabezado X al mensaje de correo electrónico.|
|2|ModifySubject|La acción de directiva es modificar el asunto del mensaje de correo electrónico con la información especificada por la directiva de filtrado.|
|3|Redirect|La acción de directiva es redirigir el mensaje de correo electrónico a la dirección de correo electrónico especificada por la directiva de filtrado.|
|4|Delete|La acción de directiva es eliminar (quitar) el mensaje de correo electrónico.|
|5|Quarantine|La acción de directiva es poner en cuarentena el mensaje de correo electrónico.|
|6|NoAction| La directiva está configurada para no realizar ninguna acción en el mensaje de correo electrónico.|
|7|BccMessage|La acción de directiva consiste en enviar en CCO el mensaje de correo electrónico a la dirección de correo electrónico especificada por la directiva de filtrado.|
|8|ReplaceAttachment|La acción de directiva es reemplazar los datos adjuntos del mensaje de correo electrónico tal como especifica la directiva de filtrado.|
||||

### <a name="url-time-of-click-events"></a>Eventos de tiempo de clic de URL

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|UserId|Edm.String|Sí|El identificador (por ejemplo, la dirección de correo electrónico) para el usuario que hizo clic en la dirección URL.|
|AppName|Edm.String|Sí|El servicio de Office 365 desde el que se hizo clic en la dirección URL (por ejemplo, Correo).|
|URLClickAction|Self.[URLClickAction](#urlclickaction)|Sí|Acción de clic para la dirección URL según las directivas de la organización para [Vínculos seguros en Defender para Office 365](/office365/securitycompliance/atp-safe-links).|
|SourceId|Edm.String|Sí|El identificador para el servicio de Office 365 desde el que se hizo clic en la dirección URL (por ejemplo, para el correo es el id. de mensaje de red de Exchange Online).|
|TimeOfClick|Edm.Date|Sí|La fecha y hora en formato Hora universal coordinada (UTC) cuando el usuario hizo clic en la dirección URL.|
|URL|Edm.String|Sí|Dirección URL en la que el usuario hizo clic.|
|UserIp|Edm.String|Sí|La dirección IP para el usuario que hizo clic en la dirección URL. La dirección IP se muestra en el formato de dirección IPv4 o IPv6.|
|||||

### <a name="enum-urlclickaction---type-edmint32"></a>Enum: URLClickAction - Tipo: Edm.Int32

#### <a name="urlclickaction"></a>URLClickAction

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|2|Blockpage|Usuario bloqueado para navegar a la dirección URL por [Vínculos seguros en Defender para Office 365](/office365/securitycompliance/atp-safe-links).|
|3|PendingDetonationPage|Usuario presentado con la página de detonación pendiente por [Vínculos seguros en Defender para Office 365](/office365/securitycompliance/atp-safe-links).|
|4|BlockPageOverride|Usuario bloqueado para navegar a la dirección URL por [Vínculos seguros de Office 365 ATP](/office365/securitycompliance/atp-safe-links); sin embargo, el usuario ha omitido el bloqueo para navegar a la URL.|
|5|PendingDetonationPageOverride|Usuario presentado con la página de detonación pendiente por [Vínculos seguros en Defender para Office 365](/office365/securitycompliance/atp-safe-links); sin embargo, el usuario ha omitido el bloqueo para navegar a la URL.|
|||||

### <a name="file-events"></a>Eventos de archivo

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|FileData|Self.[FileData](#filedata)|Sí|Datos sobre el archivo que ha desencadenado el evento.|
|SourceWorkload|Self.[SourceWorkload](#sourceworkload)|Sí|Carga de trabajo o servicio en el que se encontró el archivo (por ejemplo, SharePoint Online, OneDrive para la Empresa o Microsoft Teams)
|DetectionMethod|Edm.String|Sí|El método o la tecnología usada por Microsoft Defender para Office 365 para la detección.|
|LastModifiedDate|Edm.Date|Sí|Fecha y hora en formato de hora universal coordinada (UTC) en la que el archivo fue creado o modificado por última vez.|
|LastModifiedBy|Edm.String|Sí|El identificador (por ejemplo, la dirección de correo electrónico) para el usuario que creó o modificó por última vez el archivo.|
|EventDeepLink|Edm.String|Sí|Vínculo profundo para el evento de archivo en los informes en tiempo real o el explorador en el Centro de seguridad y cumplimiento.|
|||||

### <a name="filedata-complex-type"></a>Tipos complejo FileData

#### <a name="filedata"></a>FileData

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|DocumentId|Edm.String|Sí|Identificador único para el archivo en Microsoft Teams, OneDrive o SharePoint.|
|FileName|Edm.String|Sí|Nombre del archivo que ha desencadenado el evento.|
|FilePath|Edm.String|Sí|Ruta de acceso (ubicación) para el archivo en Microsoft Teams, OneDrive o SharePoint.|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Sí|El veredicto de malware del archivo.|
|MalwareFamily|Edm.String|No|La familia de malware del archivo.|
|SHA256|Edm.String|Sí|El hash SHA256 del archivo.|
|FileSize|Edm.String|Sí|Tamaño del archivo en bytes.|
|||||

### <a name="enum-sourceworkload---type-edmint32"></a>Enum: SourceWorkload - Tipo: Edm.Int32

#### <a name="sourceworkload"></a>SourceWorkload

|**Valor**|**Nombre del miembro**|
|:-----|:-----|
|0|SharePoint Online|
|1|OneDrive para la Empresa|
|2|Microsoft Teams|
|||||

## <a name="submission-schema"></a>Esquema de envío

Los eventos de [envío](/microsoft-365/security/office-365-security/report-junk-email-messages-to-microsoft) están disponibles para cada [cliente de Office 365, ya que incluye la seguridad](/microsoft-365/security/office-365-security/overview). Esto incluye las organizaciones que usan Exchange Online Protection y Microsoft Defender para Office 365. Cada evento de la fuente de envío corresponde a falsos positivos o falsos negativos que se enviaron como:

- **Envío de administrador**. Mensajes, archivos o direcciones URL enviados a Microsoft para su análisis.
- **Elemento notificado por el usuario**. Mensajes notificados por los usuarios finales al administrador o a Microsoft para su revisión.

### <a name="submission-events"></a>Eventos de envío

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|AdminSubmissionRegistered|Edm.String|No|El envío del administrador está registrado y pendiente de procesamiento.|
|AdminSubmissionDeliveryCheck|Edm.String|No|El sistema de envío de administrador comprobó la directiva del correo electrónico.|
|AdminSubmissionSubmitting|Edm.String|No|El sistema de envío de administrador está enviando el correo electrónico.|
|AdminSubmissionSubmitted|Edm.String|No|El sistema de envío de administrador ha enviado el correo electrónico.|
|AdminSubmissionTriage|Edm.String|No|El envío del administrador se evalúa por un calificador.|
|AdminSubmissionTimeout|Edm.String|No|El envío del administrador ha agotado el tiempo de espera sin ningún resultado.|
|UserSubmission|Edm.String|No|Un usuario final notificó primero el envío.|
|UserSubmissionTriage|Edm.String|No|El evaluador evalúa el envío del usuario.|
|CustomSubmission|Edm.String|No|Un mensaje notificado por un usuario se envió al buzón personalizado de la organización, tal como se establece en la configuración de mensajes notificados por el usuario.|
|AttackSimUserSubmission|Edm.String|No|El mensaje notificado por el usuario era en realidad un mensaje de entrenamiento de simulación de cebo.|
|AdminSubmissionTablAllow|Edm.String|No|Se creó un permiso en el momento del envío para tomar medidas inmediatamente en mensajes similares mientras se vuelve a examinar.|
|SubmissionNotification|Edm.String|No|Los comentarios del administrador se envían al usuario final.|
|||||

## <a name="automated-investigation-and-response-events-in-office-365"></a>Eventos de investigación y respuesta automatizada en Office 365

Los eventos de [Investigación y respuesta automatizada (AIR) de Office 365](/office365/securitycompliance/automated-investigation-response-office) están disponibles para los clientes de Office 365 que tienen una suscripción que incluye Microsoft Defender para Office 365 Plan 2 u Office 365 E5. Los eventos de investigación se registran en función de un cambio en el estado de investigación. Por ejemplo, cuando un administrador realiza una acción que cambia el estado de una investigación de Acciones pendientes a Completada, se registra un evento.

Actualmente, solo se registran las investigaciones automatizadas. (Próximamente estarán disponibles eventos para las investigaciones generadas manualmente). Se registran los siguientes valores de estado:

- Investigación iniciada
- No se encontraron amenazas
- Finalizado por el sistema
- Acción pendiente
- Amenazas encontradas
- Corregido
- Error
- Finalizado por limitación
- Finalizado por el usuario
- En funcionamiento

### <a name="main-investigation-schema"></a>Esquema de investigación principal

|Nombre    |Tipo    |Descripción  |
|----|----|----|
|InvestigationId    |Edm.String    |Identificador de la investigación/GUID |
|InvestigationName    |Edm.String    |Nombre de la investigación |
|InvestigationType    |Edm.String    |Tipo de investigación Puede tomar uno de los siguientes valores:<br/>- Mensajes notificados por el usuario<br/>- Malware purgado automáticamente<br/>- Suplantación de identidad purgada automáticamente<br/>- Cambio de veredicto de dirección URL<p>(Las investigaciones manuales no están disponibles actualmente, pero lo estarán próximamente). |
|LastUpdateTimeUtc    |Edm.Date    |Hora UTC de la última actualización para una investigación |
|StartTimeUtc    |Edm.Date    |Hora de inicio de una investigación |
|Estado     |Edm.String     |Estado de investigación, En ejecución, Acciones pendientes, etc. |
|DeeplinkURL    |Edm.String    |Dirección URL de vínculo profundo de una investigación en el Centro de seguridad y cumplimiento de Office 365 |
|Acciones |Colección (Edm.String)    |Colección de acciones recomendada por una investigación |
|Datos    |Edm.String    |Cadena de datos que contiene más información sobre las entidades de investigación e información sobre las alertas relacionadas con la investigación. Las entidades están disponibles en un nodo independiente dentro del blob de datos. |
||||

### <a name="actions"></a>Acciones

|Field    |Tipo    |Descripción |
|----|----|----|
|Id.     |Edm.String    |Id. de la acción|
|ActionType    |Edm.String    |El tipo de la acción, como la corrección de un correo electrónico |
|ActionStatus    |Edm.String    |Los valores son: <br/>- Pendiente<br/>- En ejecución<br/>- Esperando al recurso<br/>- Completada<br/>- Error |
|ApprovedBy    |Edm.String    |Es NULL si se aprueba automáticamente; en caso contrario, el nombre de usuario o el identificador (estará disponible próximamente) |
|TimestampUtc    |Edm.DateTime    |La marca de tiempo del cambio de estado de la acción |
|ActionId    |Edm.String    |Identificador único de la acción |
|InvestigationId    |Edm.String    |Identificador único de la investigación |
|RelatedAlertIds    |Collection(Edm.String)    |Alertas relacionadas con una investigación |
|StartTimeUtc    |Edm.DateTime    |Marca de tiempo de creación de la acción |
|EndTimeUtc    |Edm.DateTime    |Marca de tiempo de la actualización del estado final de la acción |
|Identificadores de recursos     |Edm.String     |Constituido por el Identificador del inquilino de Azure Active Directory|
|Entidades    |Collection(Edm.String)    |Lista de una o más entidades afectadas por acción |
|Identificadores de alertas relacionadas    |Edm.String    |Alerta relacionada con una investigación |
||||

### <a name="entities"></a>Entidades

#### <a name="mailmessage-email"></a>MailMessage (correo electrónico)

|Field    |Tipo    |Descripción  |
|----|----|----|
|Tipo    |Edm.String    |"mensaje de correo"  |
|Archivos    |Colección (Self.File) |Más información sobre los archivos de los datos adjuntos de este mensaje |
|Destinatario    |Edm.String    |El destinatario de este mensaje de correo |
|Direcciones URL    |Collection (self.URL) |Las direcciones URL que contiene este mensaje de correo  |
|Remitente    |Edm.String    |La dirección de correo electrónico del remitente  |
|SenderIP    |Edm.String    |La dirección IP del remitente  |
|ReceivedDate    |Edm.DateTime    |La fecha de recepción de este mensaje  |
|NetworkMessageId    |Edm.Guid     |El identificador del mensaje de red de este mensaje de correo  |
|InternetMessageId    |Edm.String  |El identificador de internet de este mensaje de correo |
|Subject    |Edm.String    |El asunto de este mensaje de correo  |
||||

#### <a name="ip"></a>IP

|Field    |Tipo    |Descripción  |
|----|----|----|
|Tipo    |Edm.String    |"ip" |
|Address    |Edm.String    |La dirección IP como cadena, tal como `127.0.0.1`
||||

#### <a name="url"></a>URL

|Field    |Tipo    |Descripción  |
|----|----|----|
|Tipo    |Edm.String    |"url" |
|Url    |Edm.String    |La dirección URL completa a la que señala una entidad  |
||||

#### <a name="mailbox-also-equivalent-to-the-user"></a>Buzón de correo (también equivalente al usuario) 

|Field    |Tipo    |Descripción |
|----|----|----|
|Tipo    |Edm.String    |"mailbox"  |
|MailboxPrimaryAddress    |Edm.String    |La dirección principal del buzón de correo  |
|DisplayName    |Edm.String    |El nombre para mostrar del buzón de correo |
|Upn    |Edm.String    |El UPN del buzón de correo  |
||||

#### <a name="file"></a>Archivo

|Field    |Tipo    |Descripción  |
|----|----|----|
|Tipo    |Edm.String    |"file" |
|Nombre    |Edm.String    |El nombre de archivo sin la ruta de acceso |
FileHashes |Colección (Edm.String)    |Los hash de archivo asociados al archivo |
||||

#### <a name="filehash"></a>FileHash

|Field    |Tipo    |Descripción |
|----|----|----|
|Tipo    |Edm.String    |"filehash" |
|Algoritmo    |Edm.String    |El tipo de algoritmo de hash, que puede ser uno de estos valores:<br/>- Desconocido<br/>- MD5<br/>- SHA1<br/>- SHA256<br/>- SHA256AC
|Valor    |Edm.String    |El valor del hash  |
||||

#### <a name="mailcluster"></a>MailCluster

|Field    |Tipo    |Descripción   |
|----|----|----|
|Tipo    |Edm.String    |"MailCluster" <br/>Determina el tipo de entidad que se tratará |
|NetworkMessageIds    |Colección (Edm.String)    |Lista de los identificadores de mensajes de correo que forman parte del clúster de correo |
|CountByDeliveryStatus    |Colecciones (Edm.String)    |Recuento de mensajes de correo por representación de cadena DeliveryStatus  |
|CountByThreatType    |Colecciones (Edm.String) |Recuento de mensajes de correo por representación de cadena ThreatType |
|Amenazas    |Colecciones (Edm.String)    |Las amenazas de los mensajes de correo que forman parte del clúster de correo. Entre las amenazas se incluyen valores como Phish y Malware. |
|Consulta    |Edm.String    |La consulta que se usó para identificar los mensajes del clúster de correo electrónico  |
|QueryTime    |Edm.DateTime    |La hora de la consulta  |
|MailCount    |Edm.Int    |El número de mensaje de correo que forman parte del clúster de correo.  |
|Origen    |String    |El origen del clúster de correo; el valor del origen del clúster. |
||||

## <a name="hygiene-events-schema"></a>Esquema de eventos de higiene

Los eventos de higiene se relacionan con la protección de correo no deseado saliente. Estos eventos se relacionan con los usuarios a los que no se les permite enviar correo electrónico. Para más información, vea:

- [Protección contra correo no deseado saliente](/microsoft-365/security/office-365-security/outbound-spam-controls)

- [Quitar usuarios bloqueados del portal de usuarios restringidos en Office 365](/microsoft-365/security/office-365-security/removing-user-from-restricted-users-portal-after-spam)

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Description**|
|:-----|:-----|:-----|:-----|
|Auditoría|Edm.String|No|Información del sistema relacionada con el evento de higiene.|
|Evento|Edm.String|No|El tipo de evento de higiene. Los valores para este parámetro son **Listado** o **Suprimido**.|
|EventId|Edm.Int64|No|El ID. del tipo de evento de higiene.|
|EventValue|Edm.String|No|El usuario que se vio impactado.|
|Reason|Edm.String|No|Detalles sobre el evento de higiene.|
|||||

## <a name="power-bi-schema"></a>Esquema de Power BI

Los eventos de Power BI que aparecen en [Buscar el registro de auditoría en el Centro de protección de Office 365](/power-bi/service-admin-auditing#activities-audited-by-power-bi) utilizarán este esquema.

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
| AppName               | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | El nombre de la aplicación donde se ha producido el evento. |
| DashboardName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | El nombre del panel donde se ha producido el evento. |
| DataClassification    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | La [clasificación de los datos](/power-bi/service-data-classification), en caso de haberla, para el panel donde se ha producido el evento. |
| DatasetName           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | El nombre del conjunto de datos donde se ha producido el evento. |
| MembershipInformation | Collection([MembershipInformationType](#membershipinformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | Información de pertenencia del grupo. |
| OrgAppPermission      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | Lista de permisos para una aplicación de organización (toda la organización, determinados usuarios o grupos específicos). |
| ReportName            | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | El nombre del informe donde se ha producido el evento. |
| SharingInformation    | Collection([SharingInformationType](#sharinginformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"    |  No  | Información acerca de la persona a la que se envía una invitación para uso compartido. |
| SwitchState           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | Información sobre el estado de los diversos modificadores de nivel de inquilino. |
| WorkSpaceName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  No  | El nombre del área de trabajo donde se ha producido el evento. |
|||||

### <a name="membershipinformationtype-complex-type"></a>Tipo complejo MembershipInformationType

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
| MemberEmail | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | La dirección de correo electrónico del grupo. |
| Estado      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | Actualmente no se rellena. |
|||||

### <a name="sharinginformationtype-complex-type"></a>Tipo complejo SharingInformationType

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
| RecipientEmail    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | La dirección de correo electrónico del destinatario de una invitación para uso compartido. |
| RecipientName    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | El nombre del destinatario de una invitación para uso compartido. |
| ResharePermission | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  No  | Los permisos que se conceden al destinatario. |
|||||

## <a name="dynamics-365-schema"></a>Esquema de Dynamics 365

Los registros de auditoría para eventos relacionados con las aplicaciones controladas por modelos en eventos de Dynamics 365 usan un esquema de operación de base y de entidad. Para más información, consulte [Habilitar y usar el Registro de actividad](/power-platform/admin/enable-use-comprehensive-auditing#model-driven-apps-in-dynamics-365-schema).

### <a name="dynamics-365-base-schema"></a>Esquema base de Dynamics 365

| **Parámetros**     | **Tipo**            | **¿Es obligatoria?** | **Descripción**|
|:------------------ | :------------------ | :--------------|:--------------|
|CrmOrganizationUniqueName|Edm.String|Sí|Nombre único de la organización.|
|InstanceUrl|Edm.String|Sí|Dirección URL de la instancia.|
|ItemUrl|Edm.String|No|La dirección URL al registro.|
|ItemType|Edm.String|No|El nombre de la entidad.|
|UserAgent|Edm.String|No|Identificador de GUID de usuario único en la organización.|
|Fields|Collection(Common.NameValuePair)|No|Un objeto JSON que contiene las parejas de clave y valor de propiedad que se crearon o actualizaron.|
|||||

### <a name="dynamics-365-entity-operation-schema"></a>Esquema de operaciones de entidad de Dynamics 365

Los eventos de entidad de aplicaciones controladas por modelos en Dynamics 365 usan este esquema para desarrollar a partir del esquema base de Dynamics 365. Este esquema incluye información sobre la operación de la entidad que desencadenó el evento auditado.

| **Parámetros**     | **Tipo**            | **¿Es obligatoria?** | **Descripción**|
|:------------------ | :------------------ | :--------------|:--------------|
|EntityId|Edm.Guid|No|El identificador único de la entidad.|
|EntityName|Edm.String|Sí|El nombre único de la entidad en la organización. Un ejemplo de una entidad es `contact` o `authentication`.|
|Message|Edm.String|Sí|Este parámetro contiene la operación que se realizó relacionada con la entidad. Por ejemplo, si se creó un nuevo contacto, el valor de la propiedad Message es `Create` y el valor correspondiente de la propiedad EntityName es `contact`.|
|Consulta|Edm.String|No|Los parámetros de la consulta de filtro que se usaron al ejecutar la operación FetchXML.|
|PrimaryFieldValue|Edm.String|No|Indica el valor del atributo que es el campo principal de la entidad.|
|||||

## <a name="workplace-analytics-schema"></a>Esquema de Workplace Analytics

Los eventos de Workplace Analytics que aparecen en [Buscar el registro de auditoría en el Centro de seguridad y cumplimiento de Office 365](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-workplace-analytics-activities) utilizarán este esquema.

| **Parámetros**     | **Tipo**            | **¿Es obligatoria?** | **Descripción**|
|:------------------ | :------------------ | :--------------|:--------------|
| WpaUserRole        | Edm.String | No     | El rol de Workplace Analytics del usuario que realizó la operación.|
| ModifiedProperties | Colección (Common.ModifiedProperty) | No | Esta propiedad incluye el nombre de la propiedad modificada, el nuevo valor de la propiedad modificada y el valor anterior de la propiedad modificada.|
| OperationDetails   | Colección (Common.NameValuePair)    | No | Una lista de propiedades extendidas de la configuración que se ha cambiado. Cada propiedad tendrá un **Name** y un **Value**.|
||||

## <a name="quarantine-schema"></a>Esquema de cuarentena

Los eventos de cuarentena que aparecen en [Buscar el registro de auditoría en el Centro de seguridad y cumplimiento de Office 365](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#quarantine-activities) usarán este esquema. Para obtener más información sobre la cuarentena, vea [Mensajes de correo electrónico en cuarentena en Office 365](/microsoft-365/security/office-365-security/quarantine-email-messages).

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|RequestType|Self.[RequestType](#enum-requesttype---type-edmint32)|No|El tipo de solicitud de cuarentena que realizó un usuario.|
|RequestSource|Self.[RequestSource](#enum-requestsource---type-edmint32)|No|El origen de la solicitud de cuarentena puede ser el Centro de seguridad y cumplimento (SCC), un cmdlet o un URLlink.|
|NetworkMessageId|Edm.String|No|El id. de mensaje de red del mensaje de correo electrónico en cuarentena.|
|ReleaseTo|Edm.String|No|El destinatario del mensaje de correo electrónico.|
|||||

### <a name="enum-requesttype---type-edmint32"></a>Enum: RequestType - Tipo: Edm.Int32

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|Preview|Solicitud de un usuario para obtener una vista previa de un mensaje de correo electrónico que se considera peligroso.|
|1|Delete|Solicitud de un usuario para eliminar un mensaje de correo electrónico que se considera peligroso.|
|2|Release|Solicitud de un usuario para liberar un mensaje de correo electrónico que se considera peligroso.|
|3|Export|Solicitud de un usuario para exportar un mensaje de correo electrónico que se considera peligroso.|
|4|ViewHeader|Solicitud de un usuario para ver el encabezado un mensaje de correo electrónico que se considera peligroso.|
||||

### <a name="enum-requestsource---type-edmint32"></a>Enum: RequestSource - Tipo: Edm.Int32

|**Valor**|**Nombre del miembro**|**Descripción**|
|:-----|:-----|:-----|
|0|SCC|El centro de seguridad y cumplimento (SCC) es el origen desde el que se puede crear la solicitud de un usuario para obtener una vista previa del encabezado de un mensaje de correo electrónico potencialmente peligroso, eliminarlo, liberarlo, exportarlo o verlo. |
|1|Cmdlet|Un cmdlet es el origen desde el que se puede crear la solicitud de un usuario para obtener una vista previa del encabezado de un mensaje de correo electrónico potencialmente peligroso, eliminarlo, liberarlo, exportarlo o verlo.|
|2|URLlink|Este es un origen desde el que se puede crear la solicitud de un usuario para obtener una vista previa del encabezado de un mensaje de correo electrónico potencialmente peligroso, eliminarlo, liberarlo, exportarlo o verlo.|
||||

## <a name="microsoft-forms-schema"></a>Esquema de Microsoft Forms

Los eventos de Microsoft Forms que aparecen en [Buscar el registro de auditoría en el Centro de seguridad y cumplimiento de Office 365](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities) utilizarán este esquema.

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|FormsUserTypes|Collection(Self.[FormsUserTypes](#formsusertypes))|Sí|El rol del usuario que realizó la acción.  Los valores de este parámetro son Admin (Administrador), Owner (Propietario), Responder (Respondedor) o Coauthor (Coautor).|
|SourceApp|Edm.String|Sí|Indica si la acción proviene del sitio web de Forms o de otra aplicación.|
|FormName|Edm.String|No|El nombre del formulario actual.|
|FormId |Edm.String|No|El ID del formulario de destino.|
|FormTypes|Collection(Self.[FormTypes](#formtypes))|No|Indica si se trata de un Formulario, un Cuestionario o una Encuesta.|
|ActivityParameters|Edm.String|No|Cadena JSON que contiene parámetros de actividad. Para más información, consulte [Buscar en el registro de auditoría del Centro de seguridad y cumplimiento de Office 365](/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities).|
||||

### <a name="enum-formsusertypes---type-edmint32"></a>Enum: FormsUserTypes - Type: Edm.Int32

#### <a name="formsusertypes"></a>FormsUserTypes

|**Valor**|**Tipo de formulario de usuario**|**Descripción**|
|:-----|:-----|:-----|
|0|Admin|Un administrador que tenga acceso al formulario.|
|1|Owner|El usuario propietario del equipo.|
|2|Responder|Un usuario que ha enviado una respuesta a un formulario.|
|3|Coauthor|Un usuario que ha usado un vínculo de colaboración proporcionado por el propietario del formulario para iniciar sesión y editar un formulario.|
||||

### <a name="enum-formtypes---type-edmint32"></a>Enum: FormTypes - Type: Edm.Int32

#### <a name="formtypes"></a>FormTypes

|**Valor**|**Tipos de formulario**|**Descripción**|
|:-----|:-----|:-----|
|0|Formulario|Formularios creados con la opción Nuevo formulario.|
|1|Cuestionario|Cuestionarios creados con la opción Nuevo cuestionario.  Un cuestionario es un tipo especial de formulario que incluye características adicionales, como valores de puntuación, calificación automática y manual, y comentarios.|
|2|Encuesta|Encuestas creadas con la opción Nueva encuesta. Una encuesta es un tipo especial de formulario que incluye características adicionales, como la integración con CMS y la compatibilidad con Reglas de flujo.|
||||

## <a name="mip-label-schema"></a>Esquema de etiqueta MIP

Los eventos del esquema de etiquetas de Microsoft Information Protection (MIP) se activan cuando Microsoft 365 detecta un mensaje de correo procesado por agentes en la canalización de transporte a la que se ha aplicado una etiqueta de confidencialidad. Es posible que la etiqueta de confidencialidad se haya aplicado manual o automáticamente, y puede que se haya aplicado dentro o fuera de la canalización de transporte. Las etiquetas de confidencialidad se pueden aplicar automáticamente a los mensajes de correo electrónico mediante directivas de etiqueta de aplicación automática.

El propósito de este esquema de auditoría es representar la suma de todas las actividades de correo electrónico que impliquen etiquetas de confidencialidad. Es decir, debe haber una actividad de auditoría registrada para cada mensaje de correo electrónico que se envía a o desde los usuarios de la organización que tienen una etiqueta de confidencialidad aplicada, independientemente de cuándo o cómo se aplicó la etiqueta de confidencialidad. Para más información sobre las etiquetas de confidencialidad, vea:

- [Información sobre las etiquetas de confidencialidad](/microsoft-365/compliance/sensitivity-labels)

- [Aplicar una etiqueta de confidencialidad automáticamente al contenido](/microsoft-365/compliance/apply-sensitivity-label-automatically)

|**Parámetros**|**Tipo**|**¿Es obligatoria?**|**Descripción**|
|:-----|:-----|:-----|:-----|
|Remitente|Edm.String|No|La dirección de correo electrónico en el campo De del mensaje de correo electrónico.|
|Receptores|Collection(Edm.String)|No|Todas las direcciones de correo electrónico en los campos Para, CC y CCO del mensaje de correo electrónico.|
|NombreElemento|Edm.String|No|La cadena en el campo Asunto del mensaje de correo electrónico.|
|LabelId|Edm.Guid|No|El GUID de la etiqueta de confidencialidad aplicada al mensaje de correo electrónico.|
|LabelName|Edm.String|No|El nombre de la etiqueta de confidencialidad aplicada al mensaje de correo electrónico.|
|LabelAction|Edm.String|No|Las acciones especificadas por la etiqueta de confidencialidad que se aplicaron al mensaje de correo electrónico antes de que el mensaje entrara a la canalización de transporte de correo.|
|LabelAppliedDateTime|Edm.Date|No|La fecha en la que se aplicó la etiqueta de confidencialidad al mensaje de correo electrónico.|
|ApplicationMode|Edm.String|No|Especifica cómo se aplicó la etiqueta de confidencialidad al mensaje de correo electrónico. El valor **Privileged** indica que un usuario ha aplicado manualmente la etiqueta. El valor **Standard** indica que la etiqueta se aplicó automáticamente por un proceso de etiquetado del lado del cliente o del servicio.|
|||||

## <a name="communication-compliance-exchange-schema"></a>Esquema de Exchange del Cumplimiento de comunicaciones

Los eventos del Cumplimiento de comunicaciones que aparecen en el registro de auditoría de Office 365 usan este esquema. Esto incluye los registros de auditoría de la operación **SupervisoryReviewOLAudit**, que se generan cuando el contenido del mensaje de correo contiene lenguaje vulgar que ha sido identificado por los modelos de correo no deseado con una precisión \>= 99,5 %.

|**Parámetros**  |**Tipo**|**¿Es obligatoria?** |**Descripción**|
|:---------------|:-------|:--------------|:--------------|
| ExchangeDetails |[ExchangeDetails](#exchangedetails)|No|Propiedades del mensaje de correo electrónico que activó el evento SupervisoryReviewOLAudit.|
|||||

### <a name="enum-exchangedetails---type-exchangedetails"></a>Enum: ExchangeDetails - Tipo: ExchangeDetails

#### <a name="exchangedetails"></a>ExchangeDetails

| **Nombre del miembro**   | **Tipo**| **Descripción**|
|:----------------- | :-------|:---------------|
| NetworkMessageId  |Edm.Guid|El identificador del mensaje de red de este mensaje de correo|
| InternetMessageId |Edm.String|El identificador de internet de este mensaje de correo|
| AttachmentData|Collection ([AttachmentDetails](#attachmentdetails))|Información sobre los archivos adjuntos de los mensaje de correo electrónico.|
| Recipientes|Collection(Edm.String)|Todas las direcciones de correo electrónico en los campos Para, CC y CCO del mensaje de correo electrónico. |
| Subject|Edm.String|El texto en el campo Asunto del mensaje de correo electrónico.|
| MessageTime|Edm.Date|La fecha y la hora de envío del mensaje de correo.|
| From| Edm.String|La dirección de correo electrónico en el campo De del mensaje de correo electrónico.|
| Directionality|Edm.String|El estado de origen del mensaje de correo electrónico.|
||||

### <a name="enum-attachmentdetails---type-edmint32"></a>Enum: AttachmentDetails - Tipo: Edm.Int32

#### <a name="attachmentdetails"></a>AttachmentDetails

| **Nombre del miembro** | **Tipo**   | **Descripción**|
|:--------------- |:---------- | :--------------|
| FileName        | Edm.String | El nombre del archivo adjunto al mensaje de correo electrónico.|
| FileType        | Edm.String | La extensión del archivo adjunto al mensaje de correo electrónico.|
| SHA256          | Edm.String | El hash SHA-256 del archivo adjunto al mensaje de correo electrónico.|
||||
