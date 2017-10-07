---
title: "aaaAzure SQL базы данных метрик и ведения журнала диагностики | Документы Microsoft"
description: "Сведения о настройке использования ресурсов toostore ресурсов базы данных SQL Azure, подключение и статистику выполнения запросов."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Метрики и журналы диагностики базы данных SQL Azure 
База данных SQL Azure может выдавать значения метрик и журналы диагностики для упрощения мониторинга. Можно настроить использование ресурсов toostore базы данных SQL Azure, сотрудников и сеансы и соединения до одного из этих ресурсов Azure:
- **Служба хранилища Azure**: для архивации больших объемов телеметрии по оптимальной стоимости.
- **Концентратор событий Azure**: для интеграции телеметрии базы данных SQL Azure с настраиваемым решением для мониторинга или горячими конвейерами.
- **Azure Log Analytics**: для стандартной hello решением с отчетов, предупреждения и устранения возможности для мониторинга 

    ![архитектура](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>Включение ведения журналов

Метрики и журналы диагностики не включены по умолчанию. Можно включить и управлять метрик и ведения журнала диагностики с помощью одного из следующих методов hello:
- Портал Azure
- PowerShell
- Инфраструктура CLI Azure
- Интерфейс REST API 
- Шаблон Resource Manager

При включении метрик и ведения журнала диагностики, необходимо toospecify hello ресурсов Azure, где собираются выбранных данных. Доступны следующие варианты:
- Служба Log Analytics
- Концентратор событий
- Хранилище Azure 

Вы можете подготовить новый ресурс Azure или выбрать имеющийся. После выбора hello ресурса хранилища, необходимо toospecify какие toocollect данных. Доступны следующие варианты.

- **[Метрики 1 минуты](sql-database-metrics-diag-logging.md#1-minute-metrics)** содержат сведения о проценте использования DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте успешных, неудачных или заблокированных подключений брандмауэра, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, проценте хранилища XTP.

Если указать учетную запись AzureStorage или концентратор событий, можно указать toospecify политики хранения данных, которые старше выбранного периода времени удаляется. При указании анализа журналов hello политики хранения зависит от hello выбранная Ценовая категория. Узнайте больше о [ценах на Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/). 

Рекомендуется прочитать обоих hello [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) и [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи, посвященные toogain понимание не только как tooenable ведения журналов, но hello метрики и журнала категории поддерживается hello различных служб Azure.

### <a name="azure-portal"></a>Портал Azure

метрики tooenable и журналы диагностики в hello портал Azure перейдите базы данных Azure SQL tooyour или эластичный пул страниц и нажмите кнопку **параметров диагностики**.

   ![включить в hello портал Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable метрик и ведения журнала диагностики с помощью PowerShell, используйте hello, следующие команды:

- хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   Hello идентификатор учетной записи хранилища — идентификатор ресурса hello, для журналов toowhich учетной записи хранилища hello, требуется toosend hello.

- tooenable потоковую передачу журналов диагностики tooan концентратора событий, используйте следующую команду:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   Hello ИД правила Service Bus представляет собой строку следующего формата:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- Вы можете получить идентификатор ресурса hello рабочей области аналитики журналов с помощью hello следующую команду:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

Эти параметры tooenable можно объединить несколько параметров вывода.

### <a name="cli"></a>Интерфейс командной строки

метрики tooenable и с помощью ведения журнала диагностики hello Azure CLI, hello используйте следующие команды:

- хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   Hello идентификатор учетной записи хранилища — идентификатор ресурса hello, для журналов toowhich учетной записи хранилища hello, требуется toosend hello.

- tooenable потоковую передачу журналов диагностики tooan концентратора событий, используйте следующую команду:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   Hello ИД правила Service Bus представляет собой строку следующего формата:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

Эти параметры tooenable можно объединить несколько параметров вывода.

### <a name="rest-api"></a>Интерфейс REST API

Дополнительные сведения см. слишком[изменения параметров диагностики с помощью API REST Azure монитор hello](https://msdn.microsoft.com/library/azure/dn931931.aspx). 

### <a name="resource-manager-template"></a>Шаблон Resource Manager

Дополнительные сведения см. слишком[Включение параметров диагностики при создании ресурса, с помощью шаблона диспетчера ресурсов](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Поток в службе Log Analytics 
Azure метрики базы данных SQL и журналы диагностики может передаваться в службе анализа журналов с помощью параметра встроенных «отправить tooLog аналитика» hello, портале hello, или путем включения аналитики журналов в параметрах диагностики через командлеты Azure PowerShell, Azure CLI или монитор REST Azure API-ИНТЕРФЕЙС.

### <a name="installation-overview"></a>Обзор установки

Мониторинг транспортной карты базы данных SQL Azure упрощен благодаря службе Log Analytics. Необходимо выполнить три шага:

1.  Создание ресурса Log Analytics
2.  Настройка метрики toorecord баз данных и журналов диагностики в hello создана служба аналитики журналов
3.  Установить решение **Аналитика SQL Azure** из коллекции в Log Analytics.

### <a name="create-log-analytics-resource"></a>Создание ресурса Log Analytics

1. Нажмите кнопку **New** в левом меню hello.
2. Щелкните **Monitoring + Management** (Мониторинг и управление).
3. Щелкните **Log Analytics**.
4. Заполнить hello Дополнительные сведения, необходимые в форме аналитики журналов hello: имя рабочей области, подписки, группы ресурсов, расположение и ценовой категории.

   ![Служба Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>Настройка метрик toorecord баз данных и журналов диагностики

простым способом tooconfigure Hello где баз данных записать их показатели выполняется с помощью hello портал Azure. В hello портал Azure, перейдите tooyour ресурсов базы данных SQL Azure и нажмите кнопку **параметры диагностики**. 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>Установка решения hello аналитики SQL Azure из коллекции  

1. После hello ресурсов анализа журналов и данных передается ее установки решения для анализа SQL Azure. Это можно сделать с помощью hello **коллекции решений** , можно найти на домашней странице OMS hello и в боковом меню hello. В галерее hello, найдите и щелкните **SQL Azure Analytics** решения и нажмите кнопку **добавить**.

   ![решение мониторинга](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. На домашней странице OMS появится новая плитка под названием **Аналитика SQL Azure**. При выборе этой плитки откроется панель SQL Azure Analytics hello.

### <a name="using-azure-sql-analytics-solution"></a>Использование решения "Аналитика SQL Azure"

Аналитика SQL Azure имеет иерархическую панель мониторинга, которая позволяет вам toonavigate через иерархию hello ресурсов базы данных SQL Azure. Эта возможность позволяет вам toodo высокого уровня мониторинга но он также позволяет tooscope вашей мониторинга toojust hello правый набор ресурсов.
Панель мониторинга содержит списки hello разных ресурсов в рамках hello выбранного ресурса. Например, для выбранной подписки можно увидеть hello все серверы, эластичные пулы и базы данных, принадлежащие toohello выбранной подписки. Кроме того для пулов эластичных и баз данных, можно просмотреть метрики использования ресурсов hello этого ресурса. Сюда входят диаграммы для DTU, ЦП, операций ввода-вывода, операций записи в журнал, сеансов, рабочих ролей, подключений и объема хранилища в ГБ.

## <a name="stream-into-azure-event-hub"></a>Потоковая передача в концентратор событий Azure

Azure метрики базы данных SQL и журналы диагностики может передаваться в концентратор событий с помощью параметра встроенных «поток tooan концентратор событий» hello, hello портала или включив ИД правила Service Bus в параметрах диагностики через командлеты PowerShell Azure, Azure CLI или монитор REST Azure API-ИНТЕРФЕЙС. 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>Какие toodo с показателями и в журналах диагностики в концентратор событий?
После hello выбранных данных поступает в концентратор событий, существует один подробный tooenabling шаг сложных сценариях мониторинга. Концентраторов событий действует как hello «дверью» для конвейера событий и сбора данных в концентратор событий, он может преобразовываться и сохраненных с помощью любого поставщика аналитика в реальном времени или адаптеры пакетной обработки хранилища. Концентраторы событий отделяет hello рабочего потока событий из hello использования этих событий, чтобы потребители событий можно получать доступ к событиям hello по собственному расписанию. Дополнительные сведения о концентраторе событий см. в статьях:

- [Что такое концентраторы событий Azure?](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Приступая к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Вот лишь несколько способов, которые можно использовать возможность потоковой передачи hello.

-   Служба работоспособности при потоковой передаче данных «Горячий путь» tooPowerBI - с помощью концентраторов событий, Stream Analytics и PowerBI, можно легко преобразовать метрики и диагностики данных почти в реальном времени аналитики для служб Azure. Обзор как tooset копирование концентраторов событий обработки данных с Stream Analytics и использовать PowerBI в качестве выходных данных. в разделе [Stream Analytics и Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).
-   Поток журналы сторонних toothird ведение журнала и телеметрии потоки — концентраторов событий с помощью потоковой передачи, вы можно получить метрики и журналы диагностики в toodifferent аналитические решения сторонних мониторинга и журнала. 
-   Построение пользовательского телеметрии и платформ ведения журнала — платформа пользовательские телеметрии или уже являются мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема журналы диагностики. В разделе [toousing руководство Dan Rosanova концентраторов событий на платформе телеметрии масштабе](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-azure-storage"></a>Потоковая передача в службу хранилища Azure

Azure метрики базы данных SQL и журналы диагностики могут храниться в хранилище Azure с помощью hello встроенный параметр «Архивировать tooa учетной записи хранения» в hello портал Azure или путем включения хранилища Azure в параметрах диагностики через командлеты PowerShell Azure, Azure или Azure CLI Монитор API REST.

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>Схема метрик и в журналах диагностики в учетной записи хранилища hello

После настройки метрики и журналы диагностики, контейнер хранилища создается в учетной записи хранения hello, заданные при hello первой строки данных недоступны. Эти большие двоичные объекты Hello структура выглядит:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
Или даже еще проще:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Например, большой двоичный объект метрики 1 минуты может иметь такое имя:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

В случае, если вам нужны данные hello toorecord из hello эластичного пула, имя BLOB-объекта немного отличается.

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>Загрузка метрик и журналов из службы хранилища Azure

Ознакомьтесь с разделом [Скачивание больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).

## <a name="1-minute-metrics"></a>Метрики 1 минуты

| |  |
|---|---|
|**Ресурс**|**Метрики**|
|База данных|Сведения о проценте использования DTU, используемых единицах DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте успешных, неудачных или заблокированных подключений брандмауэра, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, проценте хранилища XTP, взаимоблокировках |
|Эластичный пул|Сведения о проценте использования DTU, используемых единицах DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, ограничении хранилища, проценте хранилища XTP |
|||

## <a name="next-steps"></a>Дальнейшие действия

- Чтение обоих hello [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) и [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи, посвященные toogain понимание не только как tooenable ведения журнала, но hello метрик и журнала категорий поддерживается hello различных служб Azure.
- Прочтите эти toolearn статьи о концентраторах событий:
   - [Что такое концентраторы событий Azure?](../event-hubs/event-hubs-what-is-event-hubs.md)
   - [Начало работы с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Ознакомьтесь с разделом [Скачивание больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).
