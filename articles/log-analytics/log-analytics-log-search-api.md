---
title: "REST API поиска журналов аналитики aaaLog | Документы Microsoft"
description: "Данное руководство содержит базовые знания о об использовании hello анализа журналов поиска REST API в hello Operations Management Suite (OMS) и содержит примеры, показывающие, как команды toouse hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>API REST поиска по журналам Log Analytics
Это руководство дает базовые знания, включая примеры того, как можно использовать REST API поиска аналитики журналов hello. Служба аналитики журналов является частью hello Operations Management Suite (OMS).

> [!NOTE]
> Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то toouse hello устаревших запросов языка с API поиска журналов hello продолжать, как описано в этой статье.  Новый API будет выпущена для обновленных рабочих областей и hello документация будет обновляться в это время. 

> [!NOTE]
> Служба аналитики журналов был вызван ранее оперативной аналитики, поэтому это hello имя, используемое в поставщике ресурсов hello.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Общие сведения о REST API поиска журналов hello
Hello REST API поиска аналитики журналов относится к категории RESTful и может запускаться через API диспетчера ресурсов Azure hello. В этой статье приведены примеры доступа к API hello через [ARMClient](https://github.com/projectkudu/ARMClient), Здравствуйте, средство командной строки открытым исходным кодом, который упрощает вызов API диспетчера ресурсов Azure. Использование ARMClient Hello является одним из многих параметров tooaccess hello API поиска аналитики журналов. Другой вариант — модуля Azure PowerShell hello toouse для OperationalInsights, в который входят командлеты для доступа к поиска. С помощью этих средств можно использовать рабочие области tooOMS вызовы toomake API диспетчера ресурсов Azure hello и выполнения команд поиска в них. Hello API выводит результаты поиска в формате JSON, позволяя результаты поиска hello toouse различными способами программными средствами.

Hello диспетчера ресурсов Azure можно использовать через [библиотека для .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) и hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn более, просмотрите hello связаны веб-страницы.

> [!NOTE]
> При использовании статистической обработки команды `|measure count()` или `distinct`, каждый вызов toosearch может возвращать не более 500 000 записей. Операции поиска, в которых не используется команда агрегирования, возвращают не более 5000 записей.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Учебник по основам API REST поиска по службе Log Analytics
### <a name="toouse-armclient"></a>toouse ARMClient
1. Установите [Chocolatey](https://chocolatey.org/), который является диспетчером пакетов с открытым исходным кодом для Windows. Откройте окно командной строки от имени администратора и выполните следующую команду hello:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Установите ARMClient, выполнив следующую команду hello:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform поиска с помощью ARMClient
1. Войдите в учетную запись Майкрософт или в рабочую или учебную учетную запись:

    ```
    armclient login
    ```

    Успешного входа появится список всех подписок, привязанных toohello, учитывая учетной записи:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Получение рабочих областей Operations Management Suite hello:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    При успешном вызове Get отобразятся, все рабочие области привязан toohello подписки:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Создание своей переменной поиска:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Поиск с помощью новой переменной поиска:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Примеры API REST поиска по службе Log Analytics
Hello в следующих примерах показано, как можно использовать API поиска hello.

### <a name="search---actionread"></a>Поиск — Действие/Чтение
**Пример URL:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Запрос:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Hello в следующей таблице описаны доступные свойства hello.

| **Свойство** | **Описание** |
| --- | --- |
| top |Максимальное количество результатов tooreturn Hello. |
| highlight |Содержит параметры pre и post, которые обычно используются для выделения соответствующих запросу полей |
| pre |Префиксы hello в строковые поля tooyour соответствует заданному. |
| post |Добавляет заданного поля соответствует tooyour строку hello. |
| query |запрос поиска Hello используется toocollect и возвращать результаты. |
| start |Начало Hello hello временное окно, необходимо найти toobe результаты. |
| end |конец Hello hello временное окно, необходимо найти toobe результаты. |

**Ответ.**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Поиск/{ID} - Действие/Чтение
**Запрос содержимого сохраненных результатов поиска hello:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Если hello поиска возвращает со статусом «Ожидание», hello обновить результаты опроса можно сделать с помощью этого API. Через 6 минут результат поиска hello hello, будут удалены из кэша hello и HTTP больше не будут возвращены. Если hello первоначального поискового запроса немедленно возвращает состояние «Успешно», результаты hello не добавляются toohello кэша, причиной этого tooreturn API HTTP Gone при запросе. содержимое результатов HTTP 200 Hello находятся в том же формате, что hello первоначального поискового запроса, но с обновленными значениями hello.
>
>

### <a name="saved-searches"></a>Сохраненные поисковые запросы
**Запрос списка сохраненных поисковых запросов:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Поддерживаемые методы: GET, PUT и DELETE.

Поддерживаемые методы сбора данных: GET

Hello в следующей таблице описаны доступные свойства hello.

| Свойство | Описание |
| --- | --- |
| Идентификатор |Уникальный идентификатор Hello. |
| Etag |**Необходимо для обновления**. Обновляется сервером при каждой операции записи. Значение должно быть равно toohello текущее сохраненное значение или "*" tooupdate. Для старых или недопустимых значений возвращается 409. |
| properties.query |**Обязательный**. Hello поисковый запрос. |
| properties.displayName |**Обязательный**. Hello определяемых пользователем отображаемое имя запроса hello. |
| properties.category |**Обязательный**. Hello определяемая пользователем Категория запроса hello. |

> [!NOTE]
> Hello API поиска аналитики журналов в настоящее время возвращает созданные пользователем сохраненные поисковые запросы, когда запрашиваются сохраненные поисковые запросы в рабочей области. Hello API не возвращает сохраненные поисковые запросы, предоставляемых решениями.
>
>

### <a name="create-saved-searches"></a>Создание сохраненных поисковых запросов
**Запрос:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.

### <a name="delete-saved-searches"></a>Удаление сохраненных поисковых запросов
**Запрос:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Изменение сохраненных поисковых запросов
 **Запрос:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Метаданные (только JSON)
Вот способ toosee hello полей для всех типов журналов hello данных, собранных в рабочей области. Например если вы хотите узнать, если hello тип события содержит поле с именем компьютера, этот запрос является одним из способов toocheck.

**Запрос полей**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Ответ.**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Hello в следующей таблице описаны доступные свойства hello.

| **Свойство** | **Описание** |
| --- | --- |
| name |Имя поля. |
| displayName |Hello отображаемое имя поля hello. |
| type |Здравствуйте, тип значения поля hello. |
| facetable |Сочетание текущих свойств indexed, stored и facet. |
| display |Текущее свойство display. Если поле отображается при поиске, используется значение true. |
| ownerType |Снижение tooonly типы, принадлежащие tooonboarded IP. |

## <a name="optional-parameters"></a>Необязательные параметры
Hello следующую информацию описывает доступные необязательные параметры.

### <a name="highlighting"></a>Выделение
параметр «Highlight» Hello является необязательным параметром можно использовать подсистемы поиска toorequest hello в ответ, добавить набор маркеров.

Эти маркеры указывают hello начало и окончание выделяемого текста, который сопоставляет термины hello, указанный в запросе поиска.
Можно указать начало hello и конечный маркеры, используемые выделенной hello toowrap поисковому запросу.

**Пример поискового запроса**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Пример результата:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Обратите внимание, что hello предыдущий результат содержит сообщение об ошибке, префиксом и постфиксом.

## <a name="computer-groups"></a>Группы компьютеров
Группы компьютеров — специальные сохраненные поисковые запросы, возвращающие набор компьютеров.  Группы компьютеров можно использовать на других компьютерах запросы toolimit hello результаты toohello в группе hello.  Группа компьютеров реализуется как сохраненный поисковый запрос с тегом Group (Группа) и значением Computer (Компьютер).

Ниже представлен пример ответа для группы компьютеров.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Извлечение группы компьютеров
группы компьютеров, используйте hello метод Get с группой hello tooretrieve по идентификатору.

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Создание или обновление группы компьютеров
toocreate группы компьютеров, используйте hello метода Put с идентификатором уникальный сохраненные условия поиска. Если используется существующий идентификатор группы компьютеров, он будет изменен. При создании группы компьютеров на портале службы анализа журналов hello идентификатор hello создается из группы hello и имени.

Hello запрос, используемый для определения группы hello должен возвращать набор компьютеров для группы toofunction hello должным образом.  Рекомендуется завершении запроса с `| Distinct Computer` tooensure hello правильные данные возвращаются.

Определение Hello hello сохраненного поиска необходимо включить тег с именем группы со значением компьютера для поиска toobe hello, классифицируются как группы компьютеров.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Удаление группы компьютеров
группы компьютеров, используйте hello метода Delete с группой hello toodelete по идентификатору.

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) toobuild запросы, использующие настраиваемые поля для критериев.
