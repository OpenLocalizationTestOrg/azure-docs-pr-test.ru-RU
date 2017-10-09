---
title: "aaaArchive журналы диагностики Azure | Документы Microsoft"
description: "Узнайте, как tooarchive вашей Azure журналы диагностики для долгосрочного хранения в учетную запись хранилища."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Архивация журналов диагностики Azure
В этой статье показано, как использовать hello портал Azure, командлеты PowerShell, CLI, или REST API tooarchive вашей [Azure журналам диагностики](monitoring-overview-of-diagnostic-logs.md) в учетной записи хранения. Этот параметр полезен, если вы хотите tooretain журналы вашей диагностики с политикой хранения необязательно для аудита, статического анализа или резервной копии. Учетная запись хранения Hello не имеет toobe в hello той же подписке, hello ресурсов выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать, вам потребуется слишком[создать учетную запись хранилища](../storage/storage-create-storage-account.md) toowhich, вы можете архивировать вашим журналам диагностики. Настоятельно рекомендуется не использовать существующую учетную запись хранения с других, отличных от наблюдения за данными, хранимыми в нем, чтобы лучше управлять toomonitoring доступа к данным. Тем не менее если ваш журнал действий и учетной записи хранения метрики диагностики tooa архивация также выполняется, может быть toouse смысле этой учетной записи хранения для вашей журналы диагностики также tookeep все данные наблюдения в центральном расположении. Hello учетной записи хранилища, используемого должна быть учетной записью хранения общего назначения, не учетную запись хранилища больших двоичных объектов.

## <a name="diagnostic-settings"></a>Параметры диагностики
задать tooarchive журналы вашей диагностики с помощью приведенных ниже способов hello, **параметра диагностики** к определенному ресурсу. Параметра диагностики для ресурса определяет категории hello журналов и данных метрики отправляются tooa назначения (учетной записи хранилища, пространство имен концентраторов событий или служба аналитики журналов). Он также определяет политику хранения hello (количество дней tooretain) для событий по каждой категории журнала и метрик данные, хранящиеся в учетной записи хранилища. Если политика хранения toozero, события для этой категории журнала хранятся бесконечно (то есть, toosay, бесконечно). Для политики хранения можно задать любое значение от 1 до 2 147 483 647. [Подробные сведения о параметрах диагностики см. здесь](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политики хранения будут удалены. Например если политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Журналы диагностики архив с помощью портала hello
1. На портале hello перейдите tooAzure монитор и нажмите на **параметров диагностики**

    ![Раздел мониторинга Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. При необходимости фильтровать список hello по группе ресурсов или тип ресурса, а затем щелкните hello ресурсов, для которого вы хотите tooset параметра диагностики.

3. Если параметры не существует в hello ресурс, который вы выбрали, не запрошенные toocreate параметр. Щелкните Turn on diagnostics (Включить диагностику).

   ![Добавление параметра диагностики — имеющиеся параметры отсутствуют](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Если имеются существующие параметры ресурсов hello, вы увидите список параметров, уже настроен на этом ресурсе. Нажмите Add diagnostic setting (Добавить параметр диагностики).

   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Введите имя параметра и установите флажок "hello" для **Экспорт tooStorage учетной записи**, затем выберите учетную запись хранилища. При необходимости задайте количество дней tooretain эти журналы с помощью hello **хранения (в днях)** ползунки. Хранение 0 дней хранит журналы hello бесконечно.
   
   ![Добавление параметра диагностики — имеющиеся параметры](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Щелкните **Сохранить**.

Через несколько секунд появится новый параметр hello в списке параметров для данного ресурса и журналы диагностики, хранения архивных toothat учетной записи, как только создается новый данные события.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Архивация журналов диагностики с помощью Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Свойство | Обязательно | Описание |
| --- | --- | --- |
| ResourceId |Да |Идентификатор ресурса hello ресурса, на котором будет tooset параметра диагностики. |
| StorageAccountId |Нет |Идентификатор ресурса toowhich hello учетной записи хранения журналов диагностики должен быть сохранен. |
| Категории |Нет |Список разделенных запятыми tooenable категории журнала. |
| Включено |Да |Логическое значение, определяющее включение и отключение диагностики на этом ресурсе. |
| RetentionEnabled |Нет |Логическое значение, определяющее включение политики хранения на этом ресурсе. |
| RetentionInDays |Нет |Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647. Нулевое значение хранятся журналы hello бесконечно. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Журналы диагностики архив через hello кросс-платформенных CLI
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Свойство | Обязательно | Описание |
| --- | --- | --- |
| ResourceId |Да |Идентификатор ресурса hello ресурса, на котором будет tooset параметра диагностики. |
| storageId |Нет |Журналы диагностики toowhich учетной записи хранилища hello идентификатор ресурса должен быть сохранен. |
| Категории |Нет |Список разделенных запятыми tooenable категории журнала. |
| Включено |Да |Логическое значение, определяющее включение и отключение диагностики на этом ресурсе. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Журналы диагностики архив через API-Интерфейс REST hello
[См. в этом документе](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) сведения на как можно настроить параметра диагностики, с помощью API REST Azure монитор hello.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Схема в журналах диагностики в учетной записи хранилища hello
После настройки архивации, как только событие происходит в одну из категорий hello журнала, которые вы выбрали контейнер хранилища создается в учетной записи хранения hello. Hello большие двоичные объекты в контейнере hello следуйте hello в том же формате, в журналы диагностики и hello журнал действий. Эти большие двоичные объекты Hello структура выглядит:

> insights-logs-{имя категории журнала}/resourceId=/SUBSCRIPTIONS/{код подписки}/RESOURCEGROUPS/{имя группы ресурсов}/PROVIDERS/{имя поставщика ресурсов}/{тип ресурса}/{имя ресурса}/y={год цифрами, 4 цифры}/m={месяц цифрами, 2 цифры}/d={день цифрами, 2 цифры}/h={время цифрами, 2 цифры, 24-часовой формат}/m=00/PT1H.json
> 
> 

Или даже еще проще:

> insights-logs-{имя категории журнала}/resourceId=/{resource Id}/y={год цифрами, 4 цифры}/m={месяц цифрами, 2 цифры}/d={день цифрами, 2 цифры}/h={время цифрами, 2 цифры, 24-часовой формат}/m=00/PT1H.json
> 
> 

Например, большой двоичный объект может иметь такое имя:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Каждый BLOB-объект PT1H.json содержит большой двоичный объект JSON, событий, произошедших в течение часа hello, указанный в URL-адрес hello больших двоичных объектов (например, h = 12). Во время hello присутствует час события, добавленных toohello PT1H.json файл, как только они происходят. Здравствуйте, значение минуты (m = 00) всегда равно 00, так как события журнала диагностики разбиваются на отдельные большие двоичные объекты в час.

В файле PT1H.json hello каждое событие хранится в массиве записей «hello», в следующем формате:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| Имя элемента | Описание |
| --- | --- |
| Twitter в режиме реального |Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello. |
| resourceId |Идентификатор ресурса hello влияния ресурсов. |
| operationName |Имя операции hello. |
| category |Категории журнала событий hello. |
| properties |Набор `<Key, Value>` пары (т. е. словарь), описывающий hello подробных сведениях события hello. |

> [!NOTE]
> свойства Hello и использовании этих свойств зависит от ресурса hello.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* [Скачивание больших двоичных объектов для анализа](../storage/storage-dotnet-how-to-use-blobs.md)
* [Stream диагностических журналов пространство имен tooan концентраторов событий](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Сбор и использование данных журнала из ресурсов Azure](monitoring-overview-of-diagnostic-logs.md)
