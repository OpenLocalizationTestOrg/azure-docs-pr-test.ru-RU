---
title: "Привязка внешней таблицы функции aaaAzure (Предварительная версия) | Документы Microsoft"
description: "Использование привязок внешних таблиц в Функциях Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Привязка внешних таблиц в Функциях Azure (предварительная версия)
В этой статье показано, как toomanipulate табличных данных для поставщиков SaaS (например, Sharepoint, Dynamics) внутри функции со встроенными привязками. Функции Azure поддерживают входные и выходные привязки для внешних таблиц.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>Подключения API

Привязки таблицы использовать внешние tooauthenticate подключений API с помощью сторонних поставщиков SaaS. 

При назначении привязки можно создать новое соединение API или использовать существующее соединение API в пределах hello одну группу ресурсов

### <a name="supported-api-connections-tables"></a>Поддерживаемые подключения API (таблица)

|Соединитель|Триггер|Входные данные|Выходные данные|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 for Operations](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Таблицы Google](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 for Financials](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[База данных Oracle](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним таблицам.

### <a name="creating-an-api-connection-step-by-step"></a>Пошаговые инструкции по созданию подключения API

1. Create a function (Создать функцию) > Пользовательская функция ![Создание пользовательской функции](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Сценарий `Experimental`  >  Шаблон `ExternalTable-CSharp` > Создать новое подключение `External Table connection` 
 ![Выбор шаблона входных данных для таблицы](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Выберите поставщика SaaS > Выберите или создайте подключение ![Настройка подключения SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Выберите подключение к API > создать функции hello ![создать табличную функцию](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Выберите `Integrate` > `External Table`
    1. Настройка подключения toouse hello целевой таблицы. Эти параметры варьируются у разных поставщиков SaaS. Они описаны ниже в разделе [Параметры источника данных](#datasourcesettings).
![Настройка таблицы](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Использование

В этом примере подключается tooa таблицу с именем «Contact» столбцами Id, FirstName и LastName. Код Hello перечислены сущности контакта hello в таблице hello и журналы hello имена и фамилии.

### <a name="bindings"></a>Привязки
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
Параметр `entityId` должен быть пустым для привязок таблиц.

`ConnectionAppSettingsKey`Определяет параметр приложения hello, который хранит строку соединения hello API. Hello параметр приложения создается автоматически при добавлении API соединения в hello интеграции пользовательского интерфейса.

Табличный соединитель предоставляет наборы данных, и каждый набор данных содержит таблицы. Имя набора данных по умолчанию hello Hello — «default». Ниже перечислены названия Hello для набора данных и таблицы в различных поставщиков SaaS.

|Соединитель|Выборка|Таблица|
|:-----|:---|:---| 
|**SharePoint**|Сайт|Список SharePoint
|**SQL**|База данных|Таблица 
|**Таблица Google**|Электронная таблица|Лист 
|**Excel**|Файл Excel|Лист 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Использование в языке C# #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Параметры источника данных

### <a name="sql-server"></a>SQL Server

Здравствуйте toocreate скрипта и заполнения таблицы Contact hello меньше. Имя dataSetName — default.

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Таблицы Google
В Документах Google создайте таблицу с листом `Contact`. Соединитель Hello нельзя использовать отображаемое имя листа hello. внутреннее имя Hello (полужирным шрифтом) должен использовать в качестве dataSetName, например toobe: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  добавить имена столбцов hello `Id`, `LastName`, `FirstName` toohello сначала строку, а затем заполнить данные на последующие строки.

### <a name="salesforce"></a>Salesforce
Имя dataSetName — default.

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
