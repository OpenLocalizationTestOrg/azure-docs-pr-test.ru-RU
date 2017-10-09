---
title: "решения для анализа SQL в службе анализа журналов aaaAzure | Документы Microsoft"
description: "Hello решения для анализа SQL Azure позволяет управлять базами данных Azure SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Мониторинг базы данных SQL Azure с помощью служб анализа SQL Azure (предварительная версия) в Log Analytics

![Символ службы "Аналитика SQL Azure"](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hello решения для анализа SQL Azure в службе анализа журналов Azure собирает и отображает важные показатели производительности SQL Azure. С помощью hello показателей, собираемых с решением hello, можно создать пользовательские правила наблюдения и оповещения. Вы можете отслеживать метрики базы данных SQL Azure и эластичных пулов в нескольких подписках Azure и эластичных пулах, а также визуализировать их. Hello решение также помогает tooidentify проблемы на каждом уровне стека вашего приложения.  Она использует [метрики диагностики Azure](log-analytics-azure-storage.md) вместе с анализа журналов представления toopresent данные обо всех базах данных Azure SQL и пулах эластичных БД в одной рабочей области аналитики журналов.

В настоящее время это решение Предварительная версия поддерживает до too150 000 баз данных SQL Azure и 5000 пулов эластичных SQL каждой рабочей области.

Hello решения для анализа SQL Azure, как и другие доступные для анализа журналов позволяет отслеживать и получать уведомления о работоспособности hello ресурсам Azure — в данном случае база данных SQL Azure. База данных SQL Microsoft Azure является масштабируемой реляционной базы данных служба, предоставляющая знакомы tooapplications возможности SQL Server подобные, работающих в облаке Azure hello. Аналитика журналов позволяет toocollect, корреляции и визуализировать структурированные и неструктурированные данные.

## <a name="connected-sources"></a>Подключенные источники

Hello решения для анализа SQL Azure не использует агенты tooconnect toohello службы анализа журналов.

Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.

| Подключенный источник | Поддержка | Описание |
| --- | --- | --- |
| [Агенты Windows](log-analytics-windows-agents.md) | Нет | Прямой агентов Windows hello решения не используются. |
| [Агенты Linux](log-analytics-linux-agents.md) | Нет | Прямой агенты Linux не используются решением hello. |
| [Группы управления SCOM](log-analytics-om-agents.md) | Нет | Прямое подключение от tooLog агент SCOM hello Analytics решением hello не используется. |
| [Учетная запись хранения Azure](log-analytics-azure-storage.md) | Нет | Служба аналитики журналов не прочитать hello данные из учетной записи хранения. |
| [Настройка системы диагностики Azure для входа в Application Insights](log-analytics-azure-storage.md) | Да | Azure метрики данные отправляются tooLog Analytics непосредственно в Azure. |

## <a name="prerequisites"></a>Предварительные требования

- Подписка Azure. Если у вас ее нет, вы можете создать ее [бесплатно](https://azure.microsoft.com/free/).
- Рабочая область Log Analytics. Вы можете использовать имеющуюся рабочую область или же [создать ее](log-analytics-get-started.md), прежде чем начать использовать это решение.
- Включение диагностики Azure для баз данных Azure SQL и эластичные пулы и [настроить их toosend их tooLog данных аналитики](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Конфигурация

Выполните следующие шаги tooadd hello Azure SQL решения tooyour рабочей областью аналитики hello.

1. Добавление hello SQL Azure Analytics решения tooyour рабочей области из [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. В hello портал Azure, щелкните **New** (hello символу "+"), hello выберите в списке ресурсов, **мониторинг + управления**.  
    ![Мониторинг и управление](./media/log-analytics-azure-sql/monitoring-management.png)
3. В hello **мониторинг + управления** выберите **все**.
4. В hello **рекомендуется** выберите **дополнительные** и в новый список hello, найдите **аналитики SQL Azure (Предварительная версия)** и выберите его.  
    ![Решение служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. В hello **аналитики SQL Azure (Предварительная версия)** колонка, щелкните **создать**.  
    ![Создание](./media/log-analytics-azure-sql/portal-create.png)
6. В hello **Создание нового решения** колонки, рабочей области выберите hello, необходимо решение tooand tooadd hello, нажмите кнопку '' **создать**.  
    ![добавить tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure несколько подписок Azure

toosupport несколько подписок, использовать сценарий PowerShell hello из [Azure включить ведение журнала метрики ресурсов с помощью PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Предоставить идентификатор ресурса hello рабочей области в качестве параметра при выполнении hello сценария toosend диагностических данных из ресурсов в рабочей области tooa одной подписки Azure в другой подписке Azure.

**Пример**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>С помощью решения hello

При добавлении рабочей области tooyour решения hello SQL Azure Analytics плитки приветствия добавляется tooyour рабочей области, и он отображается в обзоре. Hello отражает количество hello баз данных Azure SQL и пулах эластичных БД Azure SQL, к которой подключен hello решения.

![Элемент служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Просмотр данных службы "Аналитика SQL Azure"

Щелкните hello **SQL Azure Analytics** панель мониторинга для SQL Azure Analytics hello tooopen плитки. панель мониторинга Hello включает колонках hello, описанные ниже. Каждой колонки список ресурсов too15 (подписки, сервер, эластичного пула и базы данных). Щелкните любой мониторинга hello tooopen hello ресурсы для конкретного ресурса. Эластичный пул или база данных содержит hello диаграммы с метрик для выбранного ресурса. Щелкните диалоговое окно поиска журналов hello tooopen диаграммы.

| Колонка | Описание |
|---|---|
| Подписки | Список подписок с количеством подключенных серверов, пулов и баз данных. |
| Серверы | Список серверов с количеством подключенных пулов и баз данных. |
| Эластичные пулы | Список подключенных эластичные пулы с максимальной ГБ и eDTU в hello наблюдается периода. |
|Базы данных | Список подключенных баз данных с максимальной ГБ и DTU в hello окончание периода.|


### <a name="analyze-data-and-create-alerts"></a>Анализ данных и создание оповещений

Можно легко создать предупреждения с hello данные поступают из ресурсов базы данных SQL Azure. Вот несколько полезных запросов для [поиска по журналам](log-analytics-log-searches.md), которые можно использовать для предупреждений.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Высокий уровень DTU в базе данных SQL Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Высокий уровень DTU в эластичном пуле базы данных SQL Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Можно использовать эти запросы на основе оповещения tooalert на определенные пороговые значения для базы данных SQL Azure и эластичные пулы. tooconfigure оповещение для рабочей области OMS:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure оповещение для рабочей области

1. Go toohello [портал OMS](http://mms.microsoft.com/) и выполните вход.
2. Откройте рабочую область hello, настроенное для решения hello.
3. На странице приветствия Обзор щелкните hello **аналитики SQL Azure (Предварительная версия)** плитки.
4. Выполните одну из hello примеров запросов.
5. В поиске по журналам щелкните **Оповещение**.  
![Создание оповещения в поиске](./media/log-analytics-azure-sql/create-alert01.png)
6. На hello **добавить правило оповещения** задайте соответствующие свойства hello и hello определенных пороговых значений и нажмите кнопку **Сохранить**.  
![Добавление правила оповещения](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Выполнение действий над данными службы "Аналитика SQL Azure"

Например одна из hello самые полезные запросы, которые можно выполнять — toocompare hello DTU использования для всех пулов эластичных SQL Azure во всех подписках Azure. Единица пропускной способности базы данных (DTU) предоставляет toodescribe способом hello относительную емкость уровня производительности баз данных Basic, Standard и Premium и пулы. Единицы DTU получают на основе показателей ЦП, памяти, операций чтения и записи. При увеличении количества Dtu, hello возможности, предлагаемые уровня увеличения производительности hello. Например, уровень производительности с 5 единицами DTU в пять раз выше уровня производительности с 1 единицей DTU. Максимальная квота DTU применяется tooeach сервера и переменной ширины пула.

Выполняя следующий запрос поиска журнала hello, можно легко отличить недостаточно или более использование пулов эластичных SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запрос изменится toohello следующее.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

В следующем примере hello, можно видно, один эластичный пул имеет высокую загруженность близка к 100% DTU, тогда как другие содержат очень мало использования. В среде с помощью журналов действий Azure можно изучить tootroubleshoot потенциальных последние изменения.

![Результаты поиска по журналам. Высокая загрузка](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>См. также

- Используйте [запросов поиска журналов](log-analytics-log-searches.md) в службе анализа журналов tooview подробных данных Azure SQL.
- [Создавайте пользовательские панели мониторинга](log-analytics-dashboards.md), отображающие данные SQL Azure.
- [Создавайте оповещения](log-analytics-alerts.md), предупреждающие о возникновении определенных событий SQL Azure.
