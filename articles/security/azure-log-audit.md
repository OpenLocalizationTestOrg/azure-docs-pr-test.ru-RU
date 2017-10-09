---
title: "aaaAzure ведение журнала и аудит | Документы Microsoft"
description: "Дополнительные сведения об использовании ведения журнала данных toogain полное представление о своем приложении."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Ведение журналов и аудит Azure
## <a name="introduction"></a>Введение
### <a name="overview"></a>Обзор
tooassist текущим и потенциальным клиентам Azure в понимании и использовании hello различных безопасности возможности, доступные в и вокруг hello платформы Azure, корпорация Майкрософт разработала ряд технические документы, обзоры безопасности, советы и рекомендации и контрольные списки. разделы Hello диапазоне с точки зрения полноте и разнообразии и периодически обновляются. Этот документ является частью этого ряда, показанных в следующем разделе абстрактный hello.
### <a name="azure-platform"></a>Платформа Azure
Azure представляет собой платформу открытая и гибкая облачная служба, которая поддерживает hello широкий выбор операционных систем, языкам программирования, платформ, средства, баз данных и устройств.

Вот что вы можете, к примеру, делать:
-   запускать контейнеры Linux с интеграцией Docker;

-   создавать приложения с помощью JavaScript, Python, .NET, PHP, Java и Node.js;

-   создавать серверные части для устройств iOS, Android и Windows.

Общедоступное облако Azure службы поддерживают hello уже зависит от одной технологии миллионам разработчиков и ИТ-специалистов и доверия.

Когда сборки или перенести ИТ-ресурсов для поставщика облачных служб, зависит от возможности tooprotect этой организации приложений и данных с помощью hello элементы управления службами и hello они обеспечивают безопасность hello toomanage облачных ресурсов.

Из tooapplications территории hello для размещения миллионы клиентов одновременно предназначен инфраструктуры Azure и предоставляет trustworthy основу, на которой предприятия требованиям их безопасности. Кроме того, Azure предоставляет широкий набор toocontrol возможности безопасности можно настроить параметры и hello их, чтобы вы могли изменять toomeet hello уникальные требования к безопасности для развертываний. Данный документ поможет вам выполнить эти требования.

### <a name="abstract"></a>Аннотация
Аудит и ведение журнала событий безопасности и связанные с ними оповещения являются важной составляющей стратегии защиты данных. Журналы безопасности и отчеты предоставляют Электронная запись о подозрительных действий, а также обнаруживать закономерности, которые могут указывать успешной или неуспешной попытки проникновения внешней сети hello, а также внутренние атаки справки. Можно использовать аудит активности пользователей toomonitor, документ соответствие нормативным требованиям, выполнения анализа и многое другое. Оповещения немедленно уведомляют о возникающих событиях безопасности.

Службы Microsoft Azure и продукты позволяют аудита безопасности можно настроить и ведение журнала toohelp параметры определять пропуски в политиках безопасности и механизмов и устраните эти toohelp пропуски предотвращения нарушений. Майкрософт предлагают некоторые (и в некоторых случаях всех) из следующих вариантов hello: централизованный контроль ведения журнала и анализ систем tooprovide непрерывного видимость; своевременные оповещения; и toohelp отчеты, управлять hello большой объем информации, создаваемой устройств и служб.

Интегрируется со сторонними программными решениями аудита данных журналов Microsoft Azure может быть экспортированного tooSecurity систем инцидента и событий систем SIEM для анализа

В данном документе представлена вводная информация о создании, сборе и анализе журналов безопасности из служб, размещенных в Azure, которая поможет вам получить подробные сведения о безопасности в развернутых службах Azure. область в этом техническом документе Hello является ограниченной tooapplications и служб встроенного и развернутого в Azure.

> [!Note]
> Выполнение некоторых рекомендаций из этого документа может привести к более интенсивному использованию ресурсов хранилища, сетевых или вычислительных ресурсов, а следовательно, к дополнительным затратам на лицензии или подписки.

## <a name="types-of-logs-in-azure"></a>Типы журналов в Azure
Облачные приложения являются сложными и содержат множество подвижных частей. Журналы обеспечивают tooensure данных, приложение остается копии и запуска в рабочем состоянии. Он также помогает вам toostave выключено потенциальных проблем или устранить за те. Кроме того можно использовать ведение журнала данных toogain полное представление о своем приложении. Эти знания можно помочь tooimprove производительность приложения и удобства поддержки или автоматизации действий, которые в противном случае требуют вмешательства.

Azure создает подробные журналы для каждой службы Azure. Эти журналы подразделяются на следующие основные категории:
-   **Управление/журналы** предоставить видимость hello операций СОЗДАНИЯ диспетчера ресурсов Azure, UPDATE и DELETE. К этому типу относятся, например, [журналы действий Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).

-   **Журналы плоскости данных** предоставить видимость hello событий, возникающих в рамках использования hello ресурс Azure. Примером такого журнала: hello Windows события системы безопасности, и журналы приложений на виртуальной машине и hello [журналы диагностики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) настроить с помощью монитора Azure


-   Журналы **обработанных событий** предоставляют сведения о проанализированных событиях и оповещениях, которые были обработаны от вашего имени. К примерам таких событий относятся [оповещения центра безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Обработав и проанализировав вашу подписку, [центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) предоставляет лаконичные оповещения безопасности.

Hello следующей таблице список самых важных типов журналов, доступных в Azure.

| Категория журнала | Тип журнала | Применение | Интеграция |
| ------------ | -------- | ------ | ----------- |
|[Журналы действий](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|События уровня управления с ресурсами Azure Resource Manager.| Глубже понять hello операций, которые были выполнены на ресурсы в вашей подписке.|   REST API и [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).|
|[Журналы диагностики Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|часто данные об операции hello ресурсы диспетчера ресурсов Azure в подписке| Дают представление об операциях, выполняемых самим ресурсом.| Azure Monitor, [Stream](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).|
|[Служба отчетов AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Журналы и отчеты|Сведения о действиях входа пользователей и системных действиях управления пользователями и группами.|[Graph API](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Виртуальные машины и облачные службы](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Журнал событий Windows и системный журнал Linux|  Записывает системные данные и данные ведения журнала на виртуальных машинах hello и передает эти данные в учетной записи хранения по своему усмотрению.| Использование Windows [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (хранилище системы диагностики Microsoft Azure) и Linux в Azure Monitor.|
|[Аналитика службы хранилища](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Обеспечивает ведение журнала хранилища и предоставляет данные метрик для учетной записи хранения.|Предоставляет сведения, которые можно применять для трассировки запросов, анализа тенденций использования и диагностики проблем учетной записи хранения.|  API-Интерфейс REST или hello [клиентской библиотеки](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Журналы потоков для группы безопасности сети (NSG)](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|Используют формат JSON и показывает входящие и исходящие потоки на основе правил.|Позволяют просмотреть сведения о входящем и исходящем IP-трафике в группе безопасности сети.|[Наблюдатель за сетями](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application insight](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Журналы, исключения и пользовательские системы диагностики.|  Служба управления производительностью приложений (APM) для веб-разработчиков на нескольких платформах.| REST API, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/).|
|Обработка данных и оповещения системы безопасности| Оповещения центра безопасности Azure и оповещения OMS.| Сведения о безопасности и оповещения.|   Интерфейсы REST API, JSON.|

### <a name="activity-log"></a>Журнал действий
Hello [журнал действий Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), позволяет контролировать hello операций, которые были выполнены на ресурсы в вашей подписке. Hello журнал действий ранее была известна как «Журналы аудита» или «Операционные журналы», так как он выводит [события плоскости управления](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) для ваших подписок. С помощью hello журнал действий, можно определить hello», кто и когда» для любой записи операции (PUT, POST, удаление), затраченное на hello ресурсам в подписке. Вы также можете понимать hello состояние операции hello и другие соответствующие свойства. Hello журнал действий не выполняет операций чтения (GET).

Здесь PUT, POST, DELETE ссылается операций записи hello tooall журнал действий содержит hello ресурсов. Например, можно использовать toofind журналы действий hello ошибку при устранении неполадок или toomonitor показано, как пользователь в вашей организации изменить ресурс.

![Журнал действий](./media/azure-log-audit/azure-log-audit-fig1.png)


Может получать события из журналов действий с помощью портала Azure hello [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), командлеты PowerShell и [API REST Azure монитор](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Данные в журналах действий хранятся в течении 19 дней.

Сценарии интеграции
-   [Создание оповещений электронной почты или веб-перехватчика, активируемых событием журнала действий.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Потоковую передачу tooan концентратора событий](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) продукты для использования службой сторонних или пользовательских analytics решение, например PowerBI.

-   Анализировать их в PowerBI, с помощью hello [пакет содержимого для PowerBI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Сохраните tooa учетной записи хранилища для архивации или ручной проверки.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Можно указать срок хранения по hello (в днях) с помощью профилей журнала.

-   Запрос и просмотреть его в hello портал Azure.

-   Обращение к журналу с помощью командлетов PowerShell, интерфейса командной строки или REST API.

-   Экспорт hello журнал действий с помощью профилей журнала слишком[аналитика журналов](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Можно использовать учетную запись хранения или [пространство имен концентратора событий](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) не находится в hello той же подписке, как hello отправке журналов. Hello пользователь, настраивающий приветствия должен иметь соответствующие hello [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooboth подписки
### <a name="azure-diagnostic-logs"></a>Журналы диагностики Azure
Ресурс, который предоставляет широкие возможности, часто данные об операции hello этого ресурса, создаваемых Azure журналы диагностики. Hello содержимое этих журналов зависит от типа ресурса (например, [системные журналы событий Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)являются одной категории журнала диагностики для виртуальных машин и [больших двоичных объектов, таблиц и журналы очереди](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) делятся на категории журналов диагностики для хранения учетных записей) и отличаться от hello журнал действий, который позволяет контролировать hello операций, которые были выполнены на ресурсы в вашей подписке.

![Журналы диагностики Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

Журналы диагностики Azure можно настроить несколькими способами, в том числе с помощью портала Azure, PowerShell, интерфейса командной строки и REST API.

**Сценарии интеграции**
-   Сохранить их tooa [учетной записи хранилища](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) проверка аудита или вручную. Можно указать срок хранения по hello (в днях) с помощью параметров диагностики hello.

-   [Поток их концентраторов tooEvent](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) продукты для использования службой сторонних разработчиков или решения пользовательских анализа, таких как [PowerBI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Анализ журналов с помощью [OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

**Поддерживаемые службы, схема для журналов диагностики и поддерживаемого категории журналов для каждого типа ресурса**


| служба | Схемы и документы | Тип ресурса | Категория |
| ------- | ------------- | ------------- | -------- |
|Подсистема балансировки нагрузки| [Служба анализа журналов для балансировщика нагрузки Azure (предварительная версия)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|группы сетевой безопасности;|[Аналитика журналов для групп безопасности сети](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Шлюзы приложений|[Ведение журнала диагностики для шлюза приложений](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|хранилище ключей;|[Ведение журнала хранилища ключей Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|поиск Azure;|[Включение и использование аналитики поискового трафика](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Хранилище озера данных|[Доступ к журналам диагностики Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Аудит|
|Аналитика озера данных|[Доступ к журналам диагностики для Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Аудит|
|||Microsoft.DataLakeAnalytics/accounts|Requests (Запросы)|
|||Microsoft.DataLakeStore/accounts|Requests (Запросы)|
|Приложения логики|[Настраиваемая схема отслеживания сообщений B2B для приложений логики](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Пакетная служба Azure|[Ведение журналов диагностики пакетной службы Azure](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Служба автоматизации Azure|[Log Analytics для службы автоматизации Azure](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Концентраторы событий|[Журналы диагностики концентраторов событий Azure](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Анализ потока|[Журналы диагностики задания](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Выполнение|
|||Microsoft.StreamAnalytics/streamingjobs|Разработка|
|Служебная шина|[Журналы диагностики служебной шины Azure](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Отчеты Azure Active Directory
Azure Active Directory (Azure AD) формирует отчеты о безопасности, активности и аудите каталога. Hello [отчет об аудите Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) помогает клиентам tooidentify привилегированные действия, которые возникли в своем Azure Active Directory. Привилегированные действия включают повышение изменения (например, Создание роли или сброс пароля), изменение конфигурации политики (например, политики паролей) или toodirectory изменений конфигурации (например, изменения toodomain параметры федерации).

Hello отчеты предоставляют запись аудита hello hello событий имени субъекта hello, выполнившего действие hello, hello целевой ресурс влияет изменение hello и hello даты и времени (UTC). Клиенты, могут tooretrieve hello список событий аудита для их Azure Active Directory через hello [портал Azure](https://portal.azure.com/), как описано в [просмотреть журналы аудита](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Ниже приведен список включенных отчетов hello:

| Отчеты о безопасности | Отчеты об активности | Отчеты об аудите |
| :--------------- | :--------------- | :------------ |
|Попытки входа из неизвестных источников| Использование приложения: сводка| Отчет об аудите каталога|
|"Операции входа после нескольких неудачных попыток";|  Использование приложения: подробности||
|"Операции входа из нескольких географических регионов".|    Панель мониторинга приложений||
|Попытки входа с IP-адресов с подозрительными действиями|   Ошибки подготовки учетной записи||
|Нестандартные действия при входе|    Устройства отдельного пользователя||
|Попытки входа с возможно инфицированных устройств|   Активность отдельного пользователя||
|Пользователи с аномальными событиями при входе| Отчет о действиях групп||
||Отчет о событиях регистрации для сброса пароля||
||Действие сброса пароля|||

Hello данные этих отчетов могут быть полезны tooyour приложений, таких как систем SIEM, аудита и средства бизнес-аналитики. Hello Azure AD сообщивший об API обеспечивают программный доступ к данным toohello через набор API на основе REST. Эти [интерфейсы API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) можно вызвать, используя различные языки программирования и инструменты.

События в hello отчета об аудите AD Azure хранятся в течение 180 дней.

> [!Note]
> Дополнительные сведения о хранении отчетов см. в статье [Политики хранения отчетов Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Для клиентов, заинтересованных в хранения их события аудита в течение более длительного хранения, hello Reporting API можно использовать запросу tooregularly [события аудита](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) в отдельное хранилище данных.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Журналы виртуальных машин, полученные с помощью системы диагностики Azure
[Диагностика Azure](https://docs.microsoft.com/azure/azure-diagnostics) — возможность hello в Azure, которая включает hello сбор диагностических данных с развернутым приложением. Можно использовать расширения диагностики hello из нескольких разных источников. В настоящее время поддерживаются [веб-роли и рабочие роли в облачной службе Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me),

![Журналы виртуальных машин, полученные с помощью системы диагностики Azure](./media/azure-log-audit/azure-log-audit-fig3.png)

[виртуальные машины Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) под управлением Microsoft Windows и [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Включить систему диагностики Azure на виртуальной машине можно следующим образом.

-   С помощью Visual Studio, в разделе [tootrace используйте Visual Studio виртуальных машинах Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Включение диагностики на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics).

-   [Используйте PowerShell tooset диагностики на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Создание виртуальной машины Windows с мониторингом и диагностикой с использованием шаблона Azure Resource Manager](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>аналитики хранилища
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) ведет журнал и предоставляет данные метрик для учетной записи хранения. Можно использовать этот tootrace запросы данных, анализа тенденций использования и диагностики проблем с вашей учетной записи хранилища. Ведение журналов аналитики хранилища для hello [службам больших двоичных объектов, очередей и таблиц.](https://docs.microsoft.com/azure/storage/storage-introduction) Аналитика хранилища заносит в журнал подробные сведения о службе хранилища tooa успешных и неудачных запросах.

Эти сведения можно использовать toomonitor отдельных запросов и toodiagnose проблем со службой хранилища. Запросы вносятся в журнал наилучшим возможным образом. Записи журнала создаются только в том случае, если имеются запросы, адресованные hello конечной точки службы. Например если учетной записи хранения имеет действие в конечной точки большого двоичного объекта, но не в ее конечных точек таблиц или очередей, только записывает относится создается toohello службы BLOB-объектов.

toouse аналитики хранилища ее необходимо включить отдельно для каждой службы требуется toomonitor. Его можно включить в hello [портал Azure](https://portal.azure.com/); Дополнительные сведения см. в разделе [отслеживание учетной записи хранилища в hello портал Azure.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Можно также включить аналитики хранилища программно через hello API-интерфейса REST или клиентской библиотеки hello. Используйте tooenable операции Set Service Properties hello аналитики хранилища по отдельности для каждой службы.

Hello статистические данные хранятся в известном большом двоичном объекте (для ведения журнала) и в известных таблицах (для метрик), к которым можно получить с помощью службы BLOB-объектов hello и API службы таблиц.

Аналитике хранилища установлено ограничение в 20 ТБ для hello объема хранимых данных, которая независима от hello общее ограничение для вашей учетной записи хранилища. Все журналы хранятся в [блочных BLOB-объектах](https://docs.microsoft.com/azure/storage/storage-analytics) в контейнере $logs, который автоматически создается при включении Storage Analytics для учетной записи хранения.

> [!Note]
> Дополнительную информацию о выставлении счетов и политиках хранения данных см. в разделе [Storage Analytics and Billing](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing) (Storage Analytics и выставление счетов).
>
> [!Note]
> Дополнительные сведения об ограничениях учетных записей хранения см. в разделе [Целевые показатели масштабируемости и производительности службы хранилища Azure](https://docs.microsoft.com/azure/storage/storage-scalability-targets).

регистрируются следующие типы запросов на проверку подлинности и анонимный Hello.



| Аутентифицированные  | Анонимные|
| :------------- | :-------------|
| Успешные запросы. | Успешные запросы. |
|Неудачные запросы, в том числе из-за ошибок, связанных с временем ожидания, регулированием, сетью, авторизацией и др. | Запросы, в которых используется подписанный URL-адрес (SAS), в том числе неудачные и успешные запросы. |
| Запросы, в которых используется подписанный URL-адрес (SAS), в том числе неудачные и успешные запросы. |Ошибки времени ожидания для клиента и сервера. |
|   Запросы данных tooanalytics |    Неудачные запросы GET с кодом ошибки 304 (не изменено). |
| Запросы, выполненные в самой аналитике хранилища, такие как запросы на создание или удаление журнала, не регистрируются. Полный список hello в журнал данных описаны в hello [операций ведения журнала аналитики хранилища и сообщения о состоянии](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) и [формат журнала аналитики хранилища](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) разделы. | Остальные неудачные анонимные запросы не регистрируются. Полный список hello в журнал данных описаны в hello [операций ведения журнала аналитики хранилища и сообщения о состоянии](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) и [формат журнала аналитики хранилища](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Журналы сетей Azure
Мониторинг и ведение журнала сетей в Azure выполняется комплексно и охватывает две обширные категории.

-   [Наблюдатель сети](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -сценариям сетевого мониторинга входит в состав функции hello в Наблюдатель сети. Эта служба включает в себя запись пакетов, определение следующего прыжка, проверку IP-потока, представление групп безопасности и журналы потоков NSG. Мониторинг на уровне сценария обеспечивает представление tooend конечных сетевых ресурсов в ресурс контрастность tooindividual сетевого мониторинга.

-   [Мониторинг ресурсов](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring). Мониторинг на уровне ресурса базируется на четырех компонентах. Это журналы диагностики, метрики, устранение неполадок и работоспособность ресурсов. Все эти возможности построены на уровне ресурсов сети hello.

![Журналы сетей Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Наблюдатель сети региональные служба, которая позволяет вам toomonitor и диагностики условий уровнем сети сценарий в, чтобы и из Azure. Диагностика сети и средств визуализации, доступных в Наблюдатель сети помогают понять, диагностики и получить аналитики tooyour сети в Azure.

**Ведение журнала потока NSG** -журналы потока для групп безопасности сети включить связанные tootraffic журналы toocapture, разрешенных или запрещенных правилами безопасности hello в группе hello. Эти потока журналы записываются в формате JSON и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.

### <a name="network-security-group-flow-logging"></a>Ведение журнала потоков для групп безопасности сети

[Сетевая группа безопасности потока журналы](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) являются компонентом Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети. Эти потока журналы записываются в формате JSON и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.

Хотя поток входит в целевые группы безопасности сети, они не отображаются hello же, как hello другие журналы. Журналы потоков хранятся только в учетной записи хранения.

Здравствуйте же политики хранения, как показано на другие журналы применить tooflow журналы. Журналы имеют политики хранения, может принимать значения от 1 дня too365 дней. Если политика хранения не задано, журналы hello сохраняются навсегда.

**Журналы диагностики**

События периодических и достаточную гибкость созданные сетевым ресурсам и войти в учетных записях хранения, отправляемых tooan концентратора событий или анализа журналов. Эти журналы получить представление о работоспособности hello ресурса. Их можно просматривать в таких инструментах, как Power BI и Log Analytics. как tooview журналы диагностики, посетите toolearn [анализа журналов.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Журналы диагностики](./media/azure-log-audit/azure-log-audit-fig5.png)

Доступны журналы диагностики для [подсистемы балансировки нагрузки](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [групп безопасности сети](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), маршрутов и [шлюза приложений](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Наблюдатель за сетями содержит представление журналов диагностики. Оно содержит все сетевые ресурсы, поддерживающие ведение журналов диагностики. В этом представлении можно удобно и быстро включать и отключать сетевые ресурсы.


В дополнение toopreceding протоколирования Наблюдатель сети в настоящее время имеет hello следующие возможности:
- [Топология](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -предоставляет hello отображение представление уровня сети различных взаимосвязями и ассоциации между сетевым ресурсам в группе ресурсов.

- [Изменяемая запись пакетов](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview). Позволяет записывать входящие и исходящие пакеты данных для виртуальной машины. Дополнительные параметры фильтрации и тонкой настройки элементов управления, например, может tooset ограничения по времени и размер предоставляют versatility.hello пакетные данные могут храниться в хранилище BLOB-объектов или на локальном диске hello в формате .cap.

-   [Проверка IP-потока](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview). Позволяет проверить, разрешен или запрещен пакет, на основе информации о пакете, указанной в пяти кортежах (IP-адрес назначения, исходный IP-адрес, порт назначения, исходный порт и протокол). Если пакет приветствия запрещен группой безопасности, hello правил и групп, которым отказано в пакет приветствия возвращается.

-   [Следующий прыжок](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -определяет hello следующего прыжка для пакетов, направляется в сетевой инфраструктуре Azure, позволяя toodiagnose любое неправильно настроенных определяемых пользователем маршрутов hello.

-   [Представление "Группа безопасности"](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -возвращает hello безопасности эффективный и примененные правила, которые применяются на виртуальной Машине.

-   [Шлюз виртуальной сети и устранение неполадок при подключении](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -предоставляет возможность tootroubleshoot hello шлюзах виртуальной сети и подключения.

-   [Сетевые ограничения подписки](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -позволяет tooview использование ресурсов сети с ограничениями.

### <a name="application-insight"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) — это расширяемая служба управления производительностью приложений (APM) для веб-разработчиков на нескольких платформах. Используйте его toomonitor динамической веб-приложения. Она автоматически обнаруживает аномалии производительности. Он включает toohelp средств гибкой аналитической диагностировать проблемы и toounderstand, какие пользователи фактически выполняют вместе с приложением.

 Он разработан toohelp постоянно повысить производительность и удобство использования.

 Он работает для приложений на различных платформах, включая .NET, Node.js и J2EE, размещенные локально или в облаке hello. Интегрируется с процесс devOps и средства разработки toovarious точек подключения.

![Application Insights](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights предназначен для команды разработчиков hello, toohelp понять, как работает приложение, и как он используется. Она отслеживает следующее:

-   **Частота запросов, время отклика и частота сбоев.** Узнайте, какие страницы наиболее популярны, в какое время дня их посещают чаще всего, а также узнайте о расположении пользователей. Узнайте, какие страницы работают лучше всего. Если при увеличении количества запросов повышается время отклика и частота сбоев, возможно, возникла проблема с ресурсами.

-   **Частота зависимостей, время отклика и частота сбоев.** Узнайте, замедляют ли внешние службы вашу работу.

-   **Исключения** — анализ статистики суммарный hello, или выбрать конкретные экземпляры и можно перейти к трассировке стека hello и связанные запросы. Исключения сервера и браузера регистрируются.

-   **Просмотры страниц и производительность загрузки.** Эти сведения сообщаются через браузеры пользователей.

-   **Вызовы AJAX** с веб-страницы. Скорость, время отклика и частота сбоев.

-   **Количество пользователей и сеансов.**

-   **Счетчики производительности** с компьютеров с сервером Windows или Linux, такие как ЦП, память и использование сети.

-   **Размещение диагностики** из Docker или Azure.

-   **Журналы диагностики трассировки** из вашего приложения. Предназначены для сопоставления событий трассировки с запросами.

-   **Пользовательские события и метрики** создавать самостоятельно в hello клиента или сервера кода, tootrack бизнес-события, такие как элементы продаж или игр реализовано.

**Список сценариев интеграции и их описание**

| Сценарии интеграции | Описание |
| --------------------- | :---------- |
|[Сопоставление приложений](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|компоненты приложения, оповещения и ключевые показатели Hello.||
|[Поиск данных экземпляра в системе диагностики](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| Поиск и фильтрация событий, таких как запросы, исключения, вызовы зависимостей, журналы трассировки и просмотры страниц.||
|[Обозреватель метрик для статистических данных](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Просмотр, фильтрация и сегментирование объединенных данных, таких как частоты запросов, ошибок и исключений, время отклика и время загрузки страницы.||
|[Панели мониторинга](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Объединение разнородных данных из нескольких ресурсов и их совместное использование с другими пользователями. Идеальное решение для многокомпонентные приложений, а также для непрерывного отображения в комнату команды hello.||
|[Динамический поток метрик](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|При развертывании новой сборки, просмотрите эти toomake индикаторы производительности рядом реального времени, убедиться, что все работает правильно.||
|[Аналитика](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Получите ответы на сложные вопросы о производительности и использовании приложения с помощью этого мощного языка запросов.||
|[Автоматические и ручные оповещения](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Автоматические оповещения адаптировать tooyour приложения обычных шаблонов, телеметрии и триггер когда что-нибудь за пределами hello стандартный подход. Также можно настроить оповещения для определенных уровней пользовательских или стандартных метрик.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Просмотреть данные производительности в коде hello. Toocode перейти из трассировки стека.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Интегрируйте метрики использования с другими метриками бизнес-аналитики.||
|[REST API](https://dev.applicationinsights.io/)|Напишите код, toorun запросы через метрики и необработанных данных.||
|[непрерывный экспорт.](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Массовый экспорт toostorage необработанные данные, при его поступлении.||

### <a name="azure-security-center-alerts"></a>Оповещения центра безопасности Azure
[Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) автоматически собирает, анализирует и интегрирует данных журнала из ресурсов Azure, сети hello и решения подключенных партнеров, как брандмауэр и конечной точки решения по защите, toodetect реальными угрозами и уменьшить ложные положительные результаты. Список оповещений системы безопасности упорядоченный отображается в центре безопасности вместе с hello информацию, необходимую tooquickly исследовать проблему hello и рекомендаций по их атаки tooremediate.

Центр обеспечения безопасности для обнаружения угроз работает автоматически собирает сведения о безопасности с ресурсы Azure, сети hello и решения партнеров подключенной. Данная программа анализирует эти данные часто корреляции данных из нескольких источников, tooidentify угроз. Приоритет предупреждения системы безопасности в центре безопасности вместе с рекомендации о том, как tooremediate hello угроз.

![Центр безопасности Azure](./media/azure-log-audit/azure-log-audit-fig7.png)

В центре безопасности используется расширенная аналитика безопасности, возможности которой значительно превышают возможности подходов, основанных на сигнатурах. Успехов в больших объемов данных и [машинное Обучение](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) технологии являются примененных tooevaluate событий для hello всей облака — обнаружение угроз, которые были бы невозможным tooidentify способами вручную и прогнозирование hello развитие атак. Вот что входит в аналитику по вопросам безопасности:

-   **Интегрированные анализ угроз:** выглядит для известных недобросовестных сторон, применяя анализ глобальных угроз из продуктов и служб, Майкрософт hello Microsoft цифровой преступлений единицы (DCU), hello Microsoft Security Response Center (MSRC) и внешние веб-каналы.

-   **Аналитику поведения:** применяется известные шаблоны toodiscover вредоносным действиям.

-   **Обнаружение аномалий:** использует статистические профилирование toobuild исторических базового плана. Выводит предупреждение о отклонения от установленных базовые показатели, которые соответствуют tooa потенциальных атак.


Многие операции безопасности и группами реагирования на события полагаться на это решение сведения о безопасности и управления событий (SIEM) как hello, начальная точка для рассмотрения и исследование предупреждений системы безопасности. С помощью интеграции журналов Azure клиенты могут синхронизировать оповещения центра безопасности, а также события безопасности виртуальных машин, собранные системой диагностики Azure и журналами аудита Azure, с решением Log Analytics или SIEM в режиме, близком к реальному времени.


## <a name="log-analytics"></a>Служба Log Analytics

Log Analytics — это служба в [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview), которая помогает собирать и анализировать данные, создаваемые ресурсами в облачных и локальных средах. Он предоставляет аналитики в реальном времени, с помощью интегрированной возможности поиска и настраиваемых панелей мониторинга tooreadily анализа миллионов записей во всех рабочих нагрузках и серверах независимо от их физического расположения.

![Служба Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Hello центр аналитика журналов является репозиторием hello OMS, размещаемой в облаке Azure hello. Данные собираются в репозиторий hello из подключенных источников по настройке источников данных и Добавление подписки tooyour решения. Источники данных и решений каждого создаст записей различных типов, которые имеют свой собственный набор свойств, но может по-прежнему проанализировать вместе в репозиторий toohello запросов. Это позволяет toouse hello же toowork средств и методов с разными типами данных, собираемых различных источников.

Подключенные источники являются hello компьютерам и другим ресурсам, которые создают данные, собранные службой аналитики журналов. К этим источникам относятся агенты, установленные на компьютеры [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) и [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents), подключенные напрямую, или агенты в [подключенной группе управления System Center Operations Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents). Log Analytics может также собирать данные из [службы хранилища Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage).

[Источники данных](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) hello разных типов данных, собранных из каждого подключенного источника. Это включает в себя события и [данные о производительности](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) из [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) агентов и Linux в toosources сложения, например [журналы IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), и [настраиваемые текстовые журналы.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Можно настроить каждый источник данных, что требуется toocollect и конфигурации hello автоматически доставленный tooeach подключенного источника.

[Сбор журналов и метрик для служб Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) можно выполнить четырьмя разными способами:
1.  Прямой tooLog диагностики Azure Analytics (диагностики в следующей таблице hello)

2.  Диагностика Azure tooAzure хранения tooLog аналитика (хранилище в следующей таблице hello)

3.  Соединители для служб Azure (соединителей в следующей таблице hello)

4.  Сценарии toocollect, а затем данные post в службе анализа журналов (в следующей таблице hello и для служб, которые не указаны, то пустые)

| служба | Тип ресурса | Журналы | Метрики | Решение |
| :------ | :------------ | :--- | :------ | :------- |
|Шлюзы приложений|  Microsoft.Network/<br>applicationGateways|  Диагностика|Диагностика|    [Анализ шлюзов](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [приложений Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application Insights||     Соединитель|  Соединитель|  [Соединитель Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [(предварительная версия)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Учетные записи службы автоматизации|   Microsoft.Automation/<br>AutomationAccounts|    Диагностика||       [Дополнительные сведения](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Учетные записи пакетной службы|    Microsoft.Batch/<br>batchAccounts|  Диагностика|    Диагностика||
|Классические облачные службы||       Хранилище||       [Дополнительные сведения](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Cognitive Services|    Microsoft.CognitiveServices/<br>accounts|       Диагностика|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Диагностика|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>accounts|   Диагностика|||
|пространство имен концентратора событий;|   Microsoft.EventHub/<br>namespaces|  Диагностика|    Диагностика||
|Центры Интернета вещей;|  Microsoft.Devices/<br>IotHubs||     Диагностика||
|хранилище ключей;| Microsoft.KeyVault/<br>vaults|  Диагностика  || [Анализ Key Vault](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Балансировщики нагрузки|    Microsoft.Network/<br>loadBalancers|    Диагностика|||
|Приложения логики|    Microsoft.Logic/<br>workflows|  Диагностика|    Диагностика||
||Microsoft.Logic/<br>integrationAccounts||||
|группы сетевой безопасности;|   Microsoft.Network/<br>networksecuritygroups|Диагностика||   [Анализ групп безопасности сети Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Хранилища восстановления|   Microsoft.RecoveryServices/<br>vaults|||[Служба анализа служб восстановления Azure (предварительная версия)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Службы поиска|   Microsoft.Search/<br>searchServices|    Диагностика|    Диагностика||
|Пространство имен служебной шины| Microsoft.ServiceBus/<br>namespaces|    Диагностика|Диагностика|    [Служба анализа служебной шины (предварительная версия)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Хранилище||    [Анализ Service Fabric (предварительная версия)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (версия 12)| Microsoft.Sql/<br>servers/<br>databases||       Диагностика||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|Хранилище|||         Скрипт| [Служба анализа службы хранилища Azure (предварительная версия)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Виртуальные машины|  Microsoft.Compute/<br>virtualMachines|  Добавочный номер|  Добавочный номер||
||||Диагностика||
|Масштабируемые наборы виртуальных машин|   Microsoft.Compute/<br>virtualMachines    ||Диагностика||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Фермы веб-серверов|Microsoft.Web/<br>serverfarms||   Диагностика
|Веб-сайты| Microsoft.Web/<br>sites ||      Диагностика|    [Дополнительные сведения](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Интеграция журналов с локальными системами SIEM
[Интеграция журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324) позволяет toointegrate необработанные журналы по вашим ресурсам Azure в tooyour локальной **системы сведения о безопасности и управления событий (SIEM)**.

![Интеграция журналов](./media/azure-log-audit/azure-log-audit-fig9.png)

Она собирает данные системы диагностики Azure из виртуальных машин Windows (WAD), журналов действий Azure, оповещений центра безопасности Azure и журналов поставщика ресурсов Azure. Такая интеграция обеспечивает единый панели мониторинга для каждого из ОС, локально или в облаке hello, чтобы статистической обработки, сопоставлять, анализировать и предупреждения для событий безопасности.



Служба интеграции журналов Azure сейчас поддерживает интеграцию журналов действий Azure, журналов событий Windows для виртуальной машины Windows в подписке Azure, оповещений центра безопасности Azure, журналов диагностики Azure и журналов аудита Azure Active Directory.

| Тип журнала | Log Analytics с поддержкой JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|Журналы аудита AAD|    Да|
|Журналы действий| Да|
|Оповещения ASC |Да|
|Журналы диагностики (журналы ресурсов)|  Да|
|Журналы виртуальных машин|   Да, но посредством перенаправления событий, а не с помощью JSON.|


Hello следующей таблице описаны категории журналов hello и подробности интеграции SIEM.

[Приступая к работе со службой интеграции журналов Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) — в этом руководстве рассматривается установка службы интеграции журналов Azure и интеграция журналов из хранилища WAD в Azure, журналов действий Azure, оповещений центра безопасности Azure и журналов аудита Azure Active Directory.

Сценарии интеграции

-   [Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — в этой записи блога показано, как tooconfigure Azure журнала toowork интеграция с решениями партнеров Splunk и разработанное HP, IBM QRadar.

-   [Azure log integration frequently asked questions (FAQ)](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) (Служба интеграции журналов Azure: часто задаваемые вопросы) — эта статья содержит ответы на часто задаваемые вопросы об интеграции журналов Azure.

-   [Интеграция центра обеспечения безопасности интеграции журнала предупреждений с помощью Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) — в этом документе показано, как оповещения центра обеспечения безопасности toosync, вместе с событиями безопасности виртуальной машины, собранные диагностики Azure и журналы аудита Azure, с помощью аналитики журналов или Решения SIEM.

## <a name="next-steps"></a>Дальнейшие действия

- [Аудит и ведение журнала](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Защита данных с обслуживание видимость и быстро отвечать tootimely оповещений системы безопасности

- [Security Logging and Audit Log Collection within Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/) (Ведение журнала безопасности и сбор журналов аудита в Azure)

Какие параметры, которые необходимы tooenforce toomake убедиться, что экземпляры Azure собираются hello безопасности и журналы аудита.

- [Настройка параметров аудита для семейства веб-сайтов](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Как администратор семейства сайтов один можно получить журнал hello действия, производимые конкретного пользователя и можно также получать hello журнал действий во время диапазона определенной даты. 

- [Журнал аудита hello поиска в центр соответствия и hello безопасностью Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Hello безопасностью Office 365 & Центр соответствия toosearch hello единой аудита журнала tooview пользователя и администратора действия можно использовать в организации Office 365.


