---
title: "Привязка внешних таблиц в Функциях Azure (предварительная версия) | Документация Майкрософт"
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
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="1be21-103">Привязка внешних таблиц в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="1be21-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="1be21-104">В этой статье показано, как управлять табличными данными для поставщиков SaaS (например, Sharepoint, Dynamics) внутри функции со встроенными привязками.</span><span class="sxs-lookup"><span data-stu-id="1be21-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="1be21-105">Функции Azure поддерживают входные и выходные привязки для внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="1be21-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="1be21-106">Подключения API</span><span class="sxs-lookup"><span data-stu-id="1be21-106">API Connections</span></span>

<span data-ttu-id="1be21-107">Привязки таблиц используют внешние подключения API для проверки подлинности у сторонних поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="1be21-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="1be21-108">При назначении привязки можно создать новое подключение API или использовать существующее подключение API в той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1be21-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="1be21-109">Поддерживаемые подключения API (таблица)</span><span class="sxs-lookup"><span data-stu-id="1be21-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="1be21-110">Соединитель</span><span class="sxs-lookup"><span data-stu-id="1be21-110">Connector</span></span>|<span data-ttu-id="1be21-111">Триггер</span><span class="sxs-lookup"><span data-stu-id="1be21-111">Trigger</span></span>|<span data-ttu-id="1be21-112">Входные данные</span><span class="sxs-lookup"><span data-stu-id="1be21-112">Input</span></span>|<span data-ttu-id="1be21-113">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="1be21-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="1be21-114">DB2</span><span class="sxs-lookup"><span data-stu-id="1be21-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="1be21-115">x</span><span class="sxs-lookup"><span data-stu-id="1be21-115">x</span></span>|<span data-ttu-id="1be21-116">x</span><span class="sxs-lookup"><span data-stu-id="1be21-116">x</span></span>
|[<span data-ttu-id="1be21-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="1be21-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="1be21-118">x</span><span class="sxs-lookup"><span data-stu-id="1be21-118">x</span></span>|<span data-ttu-id="1be21-119">x</span><span class="sxs-lookup"><span data-stu-id="1be21-119">x</span></span>
|[<span data-ttu-id="1be21-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="1be21-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="1be21-121">x</span><span class="sxs-lookup"><span data-stu-id="1be21-121">x</span></span>|<span data-ttu-id="1be21-122">x</span><span class="sxs-lookup"><span data-stu-id="1be21-122">x</span></span>
|[<span data-ttu-id="1be21-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="1be21-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="1be21-124">x</span><span class="sxs-lookup"><span data-stu-id="1be21-124">x</span></span>|<span data-ttu-id="1be21-125">x</span><span class="sxs-lookup"><span data-stu-id="1be21-125">x</span></span>
|[<span data-ttu-id="1be21-126">Таблицы Google</span><span class="sxs-lookup"><span data-stu-id="1be21-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="1be21-127">x</span><span class="sxs-lookup"><span data-stu-id="1be21-127">x</span></span>|<span data-ttu-id="1be21-128">x</span><span class="sxs-lookup"><span data-stu-id="1be21-128">x</span></span>
|[<span data-ttu-id="1be21-129">Informix</span><span class="sxs-lookup"><span data-stu-id="1be21-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="1be21-130">x</span><span class="sxs-lookup"><span data-stu-id="1be21-130">x</span></span>|<span data-ttu-id="1be21-131">x</span><span class="sxs-lookup"><span data-stu-id="1be21-131">x</span></span>
|[<span data-ttu-id="1be21-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="1be21-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="1be21-133">x</span><span class="sxs-lookup"><span data-stu-id="1be21-133">x</span></span>|<span data-ttu-id="1be21-134">x</span><span class="sxs-lookup"><span data-stu-id="1be21-134">x</span></span>
|[<span data-ttu-id="1be21-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="1be21-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="1be21-136">x</span><span class="sxs-lookup"><span data-stu-id="1be21-136">x</span></span>|<span data-ttu-id="1be21-137">x</span><span class="sxs-lookup"><span data-stu-id="1be21-137">x</span></span>
|[<span data-ttu-id="1be21-138">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="1be21-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="1be21-139">x</span><span class="sxs-lookup"><span data-stu-id="1be21-139">x</span></span>|<span data-ttu-id="1be21-140">x</span><span class="sxs-lookup"><span data-stu-id="1be21-140">x</span></span>
|[<span data-ttu-id="1be21-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="1be21-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="1be21-142">x</span><span class="sxs-lookup"><span data-stu-id="1be21-142">x</span></span>|<span data-ttu-id="1be21-143">x</span><span class="sxs-lookup"><span data-stu-id="1be21-143">x</span></span>
|[<span data-ttu-id="1be21-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="1be21-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="1be21-145">x</span><span class="sxs-lookup"><span data-stu-id="1be21-145">x</span></span>|<span data-ttu-id="1be21-146">x</span><span class="sxs-lookup"><span data-stu-id="1be21-146">x</span></span>
|[<span data-ttu-id="1be21-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="1be21-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="1be21-148">x</span><span class="sxs-lookup"><span data-stu-id="1be21-148">x</span></span>|<span data-ttu-id="1be21-149">x</span><span class="sxs-lookup"><span data-stu-id="1be21-149">x</span></span>
|[<span data-ttu-id="1be21-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1be21-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="1be21-151">x</span><span class="sxs-lookup"><span data-stu-id="1be21-151">x</span></span>|<span data-ttu-id="1be21-152">x</span><span class="sxs-lookup"><span data-stu-id="1be21-152">x</span></span>
|[<span data-ttu-id="1be21-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="1be21-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="1be21-154">x</span><span class="sxs-lookup"><span data-stu-id="1be21-154">x</span></span>|<span data-ttu-id="1be21-155">x</span><span class="sxs-lookup"><span data-stu-id="1be21-155">x</span></span>
|<span data-ttu-id="1be21-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="1be21-156">UserVoice</span></span>||<span data-ttu-id="1be21-157">x</span><span class="sxs-lookup"><span data-stu-id="1be21-157">x</span></span>|<span data-ttu-id="1be21-158">x</span><span class="sxs-lookup"><span data-stu-id="1be21-158">x</span></span>
|<span data-ttu-id="1be21-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="1be21-159">Zendesk</span></span>||<span data-ttu-id="1be21-160">x</span><span class="sxs-lookup"><span data-stu-id="1be21-160">x</span></span>|<span data-ttu-id="1be21-161">x</span><span class="sxs-lookup"><span data-stu-id="1be21-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="1be21-162">В [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) могут также использоваться подключения к внешним таблицам.</span><span class="sxs-lookup"><span data-stu-id="1be21-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="1be21-163">Пошаговые инструкции по созданию подключения API</span><span class="sxs-lookup"><span data-stu-id="1be21-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="1be21-164">Create a function (Создать функцию) > Пользовательская функция ![Создание пользовательской функции](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="1be21-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="1be21-165">Сценарий `Experimental`  >  Шаблон `ExternalTable-CSharp` > Создать новое подключение `External Table connection` 
 ![Выбор шаблона входных данных для таблицы](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="1be21-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="1be21-166">Выберите поставщика SaaS > Выберите или создайте подключение ![Настройка подключения SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="1be21-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="1be21-167">Выберите подключение API > Создайте функцию ![Создание табличной функции](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="1be21-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="1be21-168">Выберите `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="1be21-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="1be21-169">Настройте подключение так, чтобы использовать в нем целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="1be21-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="1be21-170">Эти параметры варьируются у разных поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="1be21-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="1be21-171">Они описаны ниже в разделе [Параметры источника данных](#datasourcesettings).
![Настройка таблицы](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="1be21-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="1be21-172">Использование</span><span class="sxs-lookup"><span data-stu-id="1be21-172">Usage</span></span>

<span data-ttu-id="1be21-173">В этом примере мы установим подключение к таблице Contact со столбцами Id, LastName и FirstName.</span><span class="sxs-lookup"><span data-stu-id="1be21-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="1be21-174">В коде перечислены сущности таблицы Contact, а также записаны имена и фамилии.</span><span class="sxs-lookup"><span data-stu-id="1be21-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="1be21-175">Привязки</span><span class="sxs-lookup"><span data-stu-id="1be21-175">Bindings</span></span>
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
<span data-ttu-id="1be21-176">Параметр `entityId` должен быть пустым для привязок таблиц.</span><span class="sxs-lookup"><span data-stu-id="1be21-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="1be21-177">`ConnectionAppSettingsKey` определяет параметр приложения, в котором хранится строка подключения API.</span><span class="sxs-lookup"><span data-stu-id="1be21-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="1be21-178">Параметр приложения создается автоматически при добавлении подключения API в интерфейсе интеграции.</span><span class="sxs-lookup"><span data-stu-id="1be21-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="1be21-179">Табличный соединитель предоставляет наборы данных, и каждый набор данных содержит таблицы.</span><span class="sxs-lookup"><span data-stu-id="1be21-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="1be21-180">По умолчанию задано имя набора данных default.</span><span class="sxs-lookup"><span data-stu-id="1be21-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="1be21-181">Ниже перечислены заголовки для набора данных и таблицы у различных поставщиков SaaS.</span><span class="sxs-lookup"><span data-stu-id="1be21-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="1be21-182">Соединитель</span><span class="sxs-lookup"><span data-stu-id="1be21-182">Connector</span></span>|<span data-ttu-id="1be21-183">Выборка</span><span class="sxs-lookup"><span data-stu-id="1be21-183">Dataset</span></span>|<span data-ttu-id="1be21-184">Таблица</span><span class="sxs-lookup"><span data-stu-id="1be21-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="1be21-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="1be21-185">**SharePoint**</span></span>|<span data-ttu-id="1be21-186">Сайт</span><span class="sxs-lookup"><span data-stu-id="1be21-186">Site</span></span>|<span data-ttu-id="1be21-187">Список SharePoint</span><span class="sxs-lookup"><span data-stu-id="1be21-187">SharePoint List</span></span>
|<span data-ttu-id="1be21-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="1be21-188">**SQL**</span></span>|<span data-ttu-id="1be21-189">База данных</span><span class="sxs-lookup"><span data-stu-id="1be21-189">Database</span></span>|<span data-ttu-id="1be21-190">Таблица</span><span class="sxs-lookup"><span data-stu-id="1be21-190">Table</span></span> 
|<span data-ttu-id="1be21-191">**Таблица Google**</span><span class="sxs-lookup"><span data-stu-id="1be21-191">**Google Sheet**</span></span>|<span data-ttu-id="1be21-192">Электронная таблица</span><span class="sxs-lookup"><span data-stu-id="1be21-192">Spreadsheet</span></span>|<span data-ttu-id="1be21-193">Лист</span><span class="sxs-lookup"><span data-stu-id="1be21-193">Worksheet</span></span> 
|<span data-ttu-id="1be21-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="1be21-194">**Excel**</span></span>|<span data-ttu-id="1be21-195">Файл Excel</span><span class="sxs-lookup"><span data-stu-id="1be21-195">Excel file</span></span>|<span data-ttu-id="1be21-196">Лист</span><span class="sxs-lookup"><span data-stu-id="1be21-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="1be21-197">Использование в языке C#</span><span class="sxs-lookup"><span data-stu-id="1be21-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
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

<span data-ttu-id="1be21-198"><!--
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
## Параметры источника данных</span><span class="sxs-lookup"><span data-stu-id="1be21-198"><!--
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

### <a name="sql-server"></a><span data-ttu-id="1be21-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1be21-199">SQL Server</span></span>

<span data-ttu-id="1be21-200">Скрипт для создания и заполнения таблицы Contact приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="1be21-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="1be21-201">Имя dataSetName — default.</span><span class="sxs-lookup"><span data-stu-id="1be21-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="1be21-202">Таблицы Google</span><span class="sxs-lookup"><span data-stu-id="1be21-202">Google Sheets</span></span>
<span data-ttu-id="1be21-203">В Документах Google создайте таблицу с листом `Contact`.</span><span class="sxs-lookup"><span data-stu-id="1be21-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="1be21-204">Соединитель не может использовать отображаемое имя листа.</span><span class="sxs-lookup"><span data-stu-id="1be21-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="1be21-205">В качестве dataSetName необходимо использовать внутреннее имя (выделено полужирным шрифтом), например: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**. Добавьте имена столбцов `Id`, `LastName`, `FirstName` в первую строку, а затем заполните данные в последующих строках.</span><span class="sxs-lookup"><span data-stu-id="1be21-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="1be21-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="1be21-206">Salesforce</span></span>
<span data-ttu-id="1be21-207">Имя dataSetName — default.</span><span class="sxs-lookup"><span data-stu-id="1be21-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="1be21-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1be21-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
