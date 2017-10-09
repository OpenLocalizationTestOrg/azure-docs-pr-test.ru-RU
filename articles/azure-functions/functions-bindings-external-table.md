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
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="02343-103">Привязка внешних таблиц в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="02343-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="02343-104">В этой статье показано, как toomanipulate табличных данных для поставщиков SaaS (например, Sharepoint, Dynamics) внутри функции со встроенными привязками.</span><span class="sxs-lookup"><span data-stu-id="02343-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="02343-105">Функции Azure поддерживают входные и выходные привязки для внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="02343-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="02343-106">Подключения API</span><span class="sxs-lookup"><span data-stu-id="02343-106">API Connections</span></span>

<span data-ttu-id="02343-107">Привязки таблицы использовать внешние tooauthenticate подключений API с помощью сторонних поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="02343-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="02343-108">При назначении привязки можно создать новое соединение API или использовать существующее соединение API в пределах hello одну группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="02343-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="02343-109">Поддерживаемые подключения API (таблица)</span><span class="sxs-lookup"><span data-stu-id="02343-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="02343-110">Соединитель</span><span class="sxs-lookup"><span data-stu-id="02343-110">Connector</span></span>|<span data-ttu-id="02343-111">Триггер</span><span class="sxs-lookup"><span data-stu-id="02343-111">Trigger</span></span>|<span data-ttu-id="02343-112">Входные данные</span><span class="sxs-lookup"><span data-stu-id="02343-112">Input</span></span>|<span data-ttu-id="02343-113">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="02343-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="02343-114">DB2</span><span class="sxs-lookup"><span data-stu-id="02343-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="02343-115">x</span><span class="sxs-lookup"><span data-stu-id="02343-115">x</span></span>|<span data-ttu-id="02343-116">x</span><span class="sxs-lookup"><span data-stu-id="02343-116">x</span></span>
|[<span data-ttu-id="02343-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="02343-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="02343-118">x</span><span class="sxs-lookup"><span data-stu-id="02343-118">x</span></span>|<span data-ttu-id="02343-119">x</span><span class="sxs-lookup"><span data-stu-id="02343-119">x</span></span>
|[<span data-ttu-id="02343-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="02343-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="02343-121">x</span><span class="sxs-lookup"><span data-stu-id="02343-121">x</span></span>|<span data-ttu-id="02343-122">x</span><span class="sxs-lookup"><span data-stu-id="02343-122">x</span></span>
|[<span data-ttu-id="02343-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="02343-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="02343-124">x</span><span class="sxs-lookup"><span data-stu-id="02343-124">x</span></span>|<span data-ttu-id="02343-125">x</span><span class="sxs-lookup"><span data-stu-id="02343-125">x</span></span>
|[<span data-ttu-id="02343-126">Таблицы Google</span><span class="sxs-lookup"><span data-stu-id="02343-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="02343-127">x</span><span class="sxs-lookup"><span data-stu-id="02343-127">x</span></span>|<span data-ttu-id="02343-128">x</span><span class="sxs-lookup"><span data-stu-id="02343-128">x</span></span>
|[<span data-ttu-id="02343-129">Informix</span><span class="sxs-lookup"><span data-stu-id="02343-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="02343-130">x</span><span class="sxs-lookup"><span data-stu-id="02343-130">x</span></span>|<span data-ttu-id="02343-131">x</span><span class="sxs-lookup"><span data-stu-id="02343-131">x</span></span>
|[<span data-ttu-id="02343-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="02343-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="02343-133">x</span><span class="sxs-lookup"><span data-stu-id="02343-133">x</span></span>|<span data-ttu-id="02343-134">x</span><span class="sxs-lookup"><span data-stu-id="02343-134">x</span></span>
|[<span data-ttu-id="02343-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="02343-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="02343-136">x</span><span class="sxs-lookup"><span data-stu-id="02343-136">x</span></span>|<span data-ttu-id="02343-137">x</span><span class="sxs-lookup"><span data-stu-id="02343-137">x</span></span>
|[<span data-ttu-id="02343-138">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="02343-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="02343-139">x</span><span class="sxs-lookup"><span data-stu-id="02343-139">x</span></span>|<span data-ttu-id="02343-140">x</span><span class="sxs-lookup"><span data-stu-id="02343-140">x</span></span>
|[<span data-ttu-id="02343-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="02343-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="02343-142">x</span><span class="sxs-lookup"><span data-stu-id="02343-142">x</span></span>|<span data-ttu-id="02343-143">x</span><span class="sxs-lookup"><span data-stu-id="02343-143">x</span></span>
|[<span data-ttu-id="02343-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="02343-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="02343-145">x</span><span class="sxs-lookup"><span data-stu-id="02343-145">x</span></span>|<span data-ttu-id="02343-146">x</span><span class="sxs-lookup"><span data-stu-id="02343-146">x</span></span>
|[<span data-ttu-id="02343-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="02343-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="02343-148">x</span><span class="sxs-lookup"><span data-stu-id="02343-148">x</span></span>|<span data-ttu-id="02343-149">x</span><span class="sxs-lookup"><span data-stu-id="02343-149">x</span></span>
|[<span data-ttu-id="02343-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="02343-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="02343-151">x</span><span class="sxs-lookup"><span data-stu-id="02343-151">x</span></span>|<span data-ttu-id="02343-152">x</span><span class="sxs-lookup"><span data-stu-id="02343-152">x</span></span>
|[<span data-ttu-id="02343-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="02343-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="02343-154">x</span><span class="sxs-lookup"><span data-stu-id="02343-154">x</span></span>|<span data-ttu-id="02343-155">x</span><span class="sxs-lookup"><span data-stu-id="02343-155">x</span></span>
|<span data-ttu-id="02343-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="02343-156">UserVoice</span></span>||<span data-ttu-id="02343-157">x</span><span class="sxs-lookup"><span data-stu-id="02343-157">x</span></span>|<span data-ttu-id="02343-158">x</span><span class="sxs-lookup"><span data-stu-id="02343-158">x</span></span>
|<span data-ttu-id="02343-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="02343-159">Zendesk</span></span>||<span data-ttu-id="02343-160">x</span><span class="sxs-lookup"><span data-stu-id="02343-160">x</span></span>|<span data-ttu-id="02343-161">x</span><span class="sxs-lookup"><span data-stu-id="02343-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="02343-162">В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним таблицам.</span><span class="sxs-lookup"><span data-stu-id="02343-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="02343-163">Пошаговые инструкции по созданию подключения API</span><span class="sxs-lookup"><span data-stu-id="02343-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="02343-164">Create a function (Создать функцию) > Пользовательская функция ![Создание пользовательской функции](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="02343-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="02343-165">Сценарий `Experimental`  >  Шаблон `ExternalTable-CSharp` > Создать новое подключение `External Table connection` 
 ![Выбор шаблона входных данных для таблицы](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="02343-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="02343-166">Выберите поставщика SaaS > Выберите или создайте подключение ![Настройка подключения SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="02343-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="02343-167">Выберите подключение к API > создать функции hello ![создать табличную функцию](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="02343-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="02343-168">Выберите `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="02343-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="02343-169">Настройка подключения toouse hello целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="02343-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="02343-170">Эти параметры варьируются у разных поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="02343-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="02343-171">Они описаны ниже в разделе [Параметры источника данных](#datasourcesettings).
![Настройка таблицы](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="02343-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="02343-172">Использование</span><span class="sxs-lookup"><span data-stu-id="02343-172">Usage</span></span>

<span data-ttu-id="02343-173">В этом примере подключается tooa таблицу с именем «Contact» столбцами Id, FirstName и LastName.</span><span class="sxs-lookup"><span data-stu-id="02343-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="02343-174">Код Hello перечислены сущности контакта hello в таблице hello и журналы hello имена и фамилии.</span><span class="sxs-lookup"><span data-stu-id="02343-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="02343-175">Привязки</span><span class="sxs-lookup"><span data-stu-id="02343-175">Bindings</span></span>
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
<span data-ttu-id="02343-176">Параметр `entityId` должен быть пустым для привязок таблиц.</span><span class="sxs-lookup"><span data-stu-id="02343-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="02343-177">`ConnectionAppSettingsKey`Определяет параметр приложения hello, который хранит строку соединения hello API.</span><span class="sxs-lookup"><span data-stu-id="02343-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="02343-178">Hello параметр приложения создается автоматически при добавлении API соединения в hello интеграции пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="02343-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="02343-179">Табличный соединитель предоставляет наборы данных, и каждый набор данных содержит таблицы.</span><span class="sxs-lookup"><span data-stu-id="02343-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="02343-180">Имя набора данных по умолчанию hello Hello — «default».</span><span class="sxs-lookup"><span data-stu-id="02343-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="02343-181">Ниже перечислены названия Hello для набора данных и таблицы в различных поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="02343-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="02343-182">Соединитель</span><span class="sxs-lookup"><span data-stu-id="02343-182">Connector</span></span>|<span data-ttu-id="02343-183">Выборка</span><span class="sxs-lookup"><span data-stu-id="02343-183">Dataset</span></span>|<span data-ttu-id="02343-184">Таблица</span><span class="sxs-lookup"><span data-stu-id="02343-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="02343-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="02343-185">**SharePoint**</span></span>|<span data-ttu-id="02343-186">Сайт</span><span class="sxs-lookup"><span data-stu-id="02343-186">Site</span></span>|<span data-ttu-id="02343-187">Список SharePoint</span><span class="sxs-lookup"><span data-stu-id="02343-187">SharePoint List</span></span>
|<span data-ttu-id="02343-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="02343-188">**SQL**</span></span>|<span data-ttu-id="02343-189">База данных</span><span class="sxs-lookup"><span data-stu-id="02343-189">Database</span></span>|<span data-ttu-id="02343-190">Таблица</span><span class="sxs-lookup"><span data-stu-id="02343-190">Table</span></span> 
|<span data-ttu-id="02343-191">**Таблица Google**</span><span class="sxs-lookup"><span data-stu-id="02343-191">**Google Sheet**</span></span>|<span data-ttu-id="02343-192">Электронная таблица</span><span class="sxs-lookup"><span data-stu-id="02343-192">Spreadsheet</span></span>|<span data-ttu-id="02343-193">Лист</span><span class="sxs-lookup"><span data-stu-id="02343-193">Worksheet</span></span> 
|<span data-ttu-id="02343-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="02343-194">**Excel**</span></span>|<span data-ttu-id="02343-195">Файл Excel</span><span class="sxs-lookup"><span data-stu-id="02343-195">Excel file</span></span>|<span data-ttu-id="02343-196">Лист</span><span class="sxs-lookup"><span data-stu-id="02343-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="02343-197">Использование в языке C#</span><span class="sxs-lookup"><span data-stu-id="02343-197">Usage in C#</span></span> #

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

<span data-ttu-id="02343-198"><!--
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
## Параметры источника данных</span><span class="sxs-lookup"><span data-stu-id="02343-198"><!--
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
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="02343-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="02343-199">SQL Server</span></span>

<span data-ttu-id="02343-200">Здравствуйте toocreate скрипта и заполнения таблицы Contact hello меньше.</span><span class="sxs-lookup"><span data-stu-id="02343-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="02343-201">Имя dataSetName — default.</span><span class="sxs-lookup"><span data-stu-id="02343-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="02343-202">Таблицы Google</span><span class="sxs-lookup"><span data-stu-id="02343-202">Google Sheets</span></span>
<span data-ttu-id="02343-203">В Документах Google создайте таблицу с листом `Contact`.</span><span class="sxs-lookup"><span data-stu-id="02343-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="02343-204">Соединитель Hello нельзя использовать отображаемое имя листа hello.</span><span class="sxs-lookup"><span data-stu-id="02343-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="02343-205">внутреннее имя Hello (полужирным шрифтом) должен использовать в качестве dataSetName, например toobe: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  добавить имена столбцов hello `Id`, `LastName`, `FirstName` toohello сначала строку, а затем заполнить данные на последующие строки.</span><span class="sxs-lookup"><span data-stu-id="02343-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="02343-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="02343-206">Salesforce</span></span>
<span data-ttu-id="02343-207">Имя dataSetName — default.</span><span class="sxs-lookup"><span data-stu-id="02343-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="02343-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02343-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
