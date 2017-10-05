---
title: "Перемещение данных из MySQL с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как перемещать данные из базы данных MySQL с использованием фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="6afc5-103">Перемещение данных из MySQL с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="6afc5-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="6afc5-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локальной базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="6afc5-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="6afc5-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6afc5-106">Вы можете скопировать данные из локального хранилища данных MySQL в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="6afc5-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6afc5-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6afc5-108">Сейчас фабрика данных поддерживает только перемещение данных из локального хранилища данных MySQL в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="6afc5-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6afc5-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6afc5-109">Prerequisites</span></span>
<span data-ttu-id="6afc5-110">Служба фабрики данных поддерживает подключение к локальным источникам MySQL с помощью шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="6afc5-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="6afc5-111">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="6afc5-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="6afc5-112">Шлюз является обязательным, даже если база данных MySQL размещается на виртуальной машине (ВМ) Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="6afc5-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="6afc5-113">Шлюз можно установить на той же ВМ, на которой размещается хранилище данных, или на другой ВМ. Важно, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="6afc5-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="6afc5-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6afc5-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="6afc5-115">Supported versions and installation</span></span>
<span data-ttu-id="6afc5-116">Чтобы подключить шлюз управления данными к базе данных MySQL, соединитель [MySQL Connector/Net для Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (версии 6.6.5 или более поздней) необходимо установить на тот же компьютер, что и шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="6afc5-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="6afc5-117">Поддерживается MySQL версии 5.1 и более.</span><span class="sxs-lookup"><span data-stu-id="6afc5-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="6afc5-118">Если произошла ошибка "Аутентификация не пройдена из-за закрытия транспортного потока удаленной стороной", то рекомендуется обновить соединитель MySQL Connector/Net до более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6afc5-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6afc5-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="6afc5-119">Getting started</span></span>
<span data-ttu-id="6afc5-120">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="6afc5-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6afc5-121">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="6afc5-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6afc5-122">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="6afc5-123">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6afc5-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6afc5-124">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6afc5-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6afc5-125">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6afc5-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6afc5-126">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6afc5-127">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="6afc5-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6afc5-128">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6afc5-129">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="6afc5-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6afc5-130">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="6afc5-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6afc5-131">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных MySQL, вы найдете в разделе [Пример JSON. Копирование данных из MySQL в большой двоичный объект Azure](#json-example-copy-data-from-mysql-to-azure-blob) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6afc5-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6afc5-132">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6afc5-133">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="6afc5-133">Linked service properties</span></span>
<span data-ttu-id="6afc5-134">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="6afc5-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="6afc5-135">Property</span></span> | <span data-ttu-id="6afc5-136">Описание</span><span class="sxs-lookup"><span data-stu-id="6afc5-136">Description</span></span> | <span data-ttu-id="6afc5-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6afc5-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6afc5-138">type</span><span class="sxs-lookup"><span data-stu-id="6afc5-138">type</span></span> |<span data-ttu-id="6afc5-139">Для свойства type необходимо задать значение **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="6afc5-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="6afc5-140">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-140">Yes</span></span> |
| <span data-ttu-id="6afc5-141">server</span><span class="sxs-lookup"><span data-stu-id="6afc5-141">server</span></span> |<span data-ttu-id="6afc5-142">Имя сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-142">Name of the MySQL server.</span></span> |<span data-ttu-id="6afc5-143">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-143">Yes</span></span> |
| <span data-ttu-id="6afc5-144">database</span><span class="sxs-lookup"><span data-stu-id="6afc5-144">database</span></span> |<span data-ttu-id="6afc5-145">Имя базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-145">Name of the MySQL database.</span></span> |<span data-ttu-id="6afc5-146">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-146">Yes</span></span> |
| <span data-ttu-id="6afc5-147">schema</span><span class="sxs-lookup"><span data-stu-id="6afc5-147">schema</span></span> |<span data-ttu-id="6afc5-148">Имя схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-148">Name of the schema in the database.</span></span> |<span data-ttu-id="6afc5-149">Нет</span><span class="sxs-lookup"><span data-stu-id="6afc5-149">No</span></span> |
| <span data-ttu-id="6afc5-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6afc5-150">authenticationType</span></span> |<span data-ttu-id="6afc5-151">Тип проверки подлинности, используемый для подключения к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="6afc5-152">Возможные значения: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="6afc5-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="6afc5-153">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-153">Yes</span></span> |
| <span data-ttu-id="6afc5-154">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="6afc5-154">username</span></span> |<span data-ttu-id="6afc5-155">Укажите имя пользователя для подключения к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="6afc5-156">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-156">Yes</span></span> |
| <span data-ttu-id="6afc5-157">password</span><span class="sxs-lookup"><span data-stu-id="6afc5-157">password</span></span> |<span data-ttu-id="6afc5-158">Введите пароль для указанной вами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6afc5-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="6afc5-159">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-159">Yes</span></span> |
| <span data-ttu-id="6afc5-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6afc5-160">gatewayName</span></span> |<span data-ttu-id="6afc5-161">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="6afc5-162">Да</span><span class="sxs-lookup"><span data-stu-id="6afc5-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="6afc5-163">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="6afc5-163">Dataset properties</span></span>
<span data-ttu-id="6afc5-164">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6afc5-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6afc5-165">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="6afc5-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6afc5-166">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6afc5-167">Раздел typeProperties набора данных с типом **RelationalTable** (который включает набор данных MySQL) содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="6afc5-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="6afc5-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="6afc5-168">Property</span></span> | <span data-ttu-id="6afc5-169">Описание</span><span class="sxs-lookup"><span data-stu-id="6afc5-169">Description</span></span> | <span data-ttu-id="6afc5-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6afc5-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6afc5-171">tableName</span><span class="sxs-lookup"><span data-stu-id="6afc5-171">tableName</span></span> |<span data-ttu-id="6afc5-172">Имя таблицы в экземпляре базы данных MySQL, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="6afc5-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="6afc5-173">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="6afc5-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6afc5-174">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="6afc5-174">Copy activity properties</span></span>
<span data-ttu-id="6afc5-175">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6afc5-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6afc5-176">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="6afc5-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="6afc5-177">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="6afc5-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="6afc5-178">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="6afc5-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6afc5-179">Если источник действия копирования относится к типу **RelationalSource** (который содержит MySQL), то в разделе typeProperties доступны следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="6afc5-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6afc5-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="6afc5-180">Property</span></span> | <span data-ttu-id="6afc5-181">Описание</span><span class="sxs-lookup"><span data-stu-id="6afc5-181">Description</span></span> | <span data-ttu-id="6afc5-182">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="6afc5-182">Allowed values</span></span> | <span data-ttu-id="6afc5-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6afc5-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6afc5-184">query</span><span class="sxs-lookup"><span data-stu-id="6afc5-184">query</span></span> |<span data-ttu-id="6afc5-185">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-185">Use the custom query to read data.</span></span> |<span data-ttu-id="6afc5-186">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="6afc5-186">SQL query string.</span></span> <span data-ttu-id="6afc5-187">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6afc5-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="6afc5-188">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="6afc5-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="6afc5-189">Пример JSON. Копирование данных из MySQL в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="6afc5-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="6afc5-190">Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6afc5-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6afc5-191">В нем показано, как скопировать данные из локальной базы данных MySQL в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6afc5-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="6afc5-192">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="6afc5-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6afc5-193">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="6afc5-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="6afc5-194">Он не включает в себя пошаговые инструкции по созданию фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="6afc5-195">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="6afc5-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="6afc5-196">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="6afc5-197">Связанная служба типа [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6afc5-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6afc5-198">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6afc5-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6afc5-199">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6afc5-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6afc5-200">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6afc5-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6afc5-201">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6afc5-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6afc5-202">В примере данные из результата выполнения запроса к базе данных MySQL каждый час копируются в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="6afc5-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="6afc5-203">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="6afc5-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6afc5-204">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="6afc5-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="6afc5-205">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="6afc5-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6afc5-206">**Связанная служба MySQL:**</span><span class="sxs-lookup"><span data-stu-id="6afc5-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="6afc5-207">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="6afc5-207">**Azure Storage linked service:**</span></span>

```JSON
    {
      "name": "AzureStorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
      }
    }
```

<span data-ttu-id="6afc5-208">**Входной набор данных MySQL:**</span><span class="sxs-lookup"><span data-stu-id="6afc5-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="6afc5-209">В примере предполагается, что таблица MyTable уже создана в MySQL и содержит столбец с именем timestampcolumn для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="6afc5-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6afc5-210">Если для параметра external задать значение true, то фабрика данных воспримет эту таблицу как внешнюю, которая создана не каким-либо действием в этой фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="6afc5-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true,
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
```

<span data-ttu-id="6afc5-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="6afc5-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6afc5-212">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6afc5-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6afc5-213">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="6afc5-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6afc5-214">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="6afc5-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
                "format": {
                    "type": "TextFormat",
                    "rowDelimiter": "\n",
                    "columnDelimiter": "\t"
                },
                "partitionedBy": [
                    {
                        "name": "Year",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy"
                        }
                    },
                    {
                        "name": "Month",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "MM"
                        }
                    },
                    {
                        "name": "Day",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "dd"
                        }
                    },
                    {
                        "name": "Hour",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
```

<span data-ttu-id="6afc5-215">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="6afc5-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6afc5-216">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="6afc5-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6afc5-217">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6afc5-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6afc5-218">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="6afc5-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="6afc5-219">Сопоставление типов для MySQL</span><span class="sxs-lookup"><span data-stu-id="6afc5-219">Type mapping for MySQL</span></span>
<span data-ttu-id="6afc5-220">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="6afc5-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="6afc5-221">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="6afc5-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6afc5-222">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="6afc5-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6afc5-223">Когда данные перемещаются в MySQL, для преобразования типа MySQL в тип .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="6afc5-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="6afc5-224">Тип базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="6afc5-224">MySQL Database type</span></span> | <span data-ttu-id="6afc5-225">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6afc5-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6afc5-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-226">bigint unsigned</span></span> |<span data-ttu-id="6afc5-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="6afc5-227">Decimal</span></span> |
| <span data-ttu-id="6afc5-228">bigint</span><span class="sxs-lookup"><span data-stu-id="6afc5-228">bigint</span></span> |<span data-ttu-id="6afc5-229">Int64</span><span class="sxs-lookup"><span data-stu-id="6afc5-229">Int64</span></span> |
| <span data-ttu-id="6afc5-230">bit</span><span class="sxs-lookup"><span data-stu-id="6afc5-230">bit</span></span> |<span data-ttu-id="6afc5-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="6afc5-231">Decimal</span></span> |
| <span data-ttu-id="6afc5-232">blob-объект</span><span class="sxs-lookup"><span data-stu-id="6afc5-232">blob</span></span> |<span data-ttu-id="6afc5-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6afc5-233">Byte[]</span></span> |
| <span data-ttu-id="6afc5-234">bool</span><span class="sxs-lookup"><span data-stu-id="6afc5-234">bool</span></span> |<span data-ttu-id="6afc5-235">Логический</span><span class="sxs-lookup"><span data-stu-id="6afc5-235">Boolean</span></span> |
| <span data-ttu-id="6afc5-236">char;</span><span class="sxs-lookup"><span data-stu-id="6afc5-236">char</span></span> |<span data-ttu-id="6afc5-237">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-237">String</span></span> |
| <span data-ttu-id="6afc5-238">дата</span><span class="sxs-lookup"><span data-stu-id="6afc5-238">date</span></span> |<span data-ttu-id="6afc5-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="6afc5-239">Datetime</span></span> |
| <span data-ttu-id="6afc5-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="6afc5-240">datetime</span></span> |<span data-ttu-id="6afc5-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="6afc5-241">Datetime</span></span> |
| <span data-ttu-id="6afc5-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="6afc5-242">decimal</span></span> |<span data-ttu-id="6afc5-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="6afc5-243">Decimal</span></span> |
| <span data-ttu-id="6afc5-244">double precision</span><span class="sxs-lookup"><span data-stu-id="6afc5-244">double precision</span></span> |<span data-ttu-id="6afc5-245">Double</span><span class="sxs-lookup"><span data-stu-id="6afc5-245">Double</span></span> |
| <span data-ttu-id="6afc5-246">Double</span><span class="sxs-lookup"><span data-stu-id="6afc5-246">double</span></span> |<span data-ttu-id="6afc5-247">Double</span><span class="sxs-lookup"><span data-stu-id="6afc5-247">Double</span></span> |
| <span data-ttu-id="6afc5-248">enum</span><span class="sxs-lookup"><span data-stu-id="6afc5-248">enum</span></span> |<span data-ttu-id="6afc5-249">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-249">String</span></span> |
| <span data-ttu-id="6afc5-250">float;</span><span class="sxs-lookup"><span data-stu-id="6afc5-250">float</span></span> |<span data-ttu-id="6afc5-251">Single</span><span class="sxs-lookup"><span data-stu-id="6afc5-251">Single</span></span> |
| <span data-ttu-id="6afc5-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-252">int unsigned</span></span> |<span data-ttu-id="6afc5-253">Int64</span><span class="sxs-lookup"><span data-stu-id="6afc5-253">Int64</span></span> |
| <span data-ttu-id="6afc5-254">int</span><span class="sxs-lookup"><span data-stu-id="6afc5-254">int</span></span> |<span data-ttu-id="6afc5-255">Int32</span><span class="sxs-lookup"><span data-stu-id="6afc5-255">Int32</span></span> |
| <span data-ttu-id="6afc5-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-256">integer unsigned</span></span> |<span data-ttu-id="6afc5-257">Int64</span><span class="sxs-lookup"><span data-stu-id="6afc5-257">Int64</span></span> |
| <span data-ttu-id="6afc5-258">целое число</span><span class="sxs-lookup"><span data-stu-id="6afc5-258">integer</span></span> |<span data-ttu-id="6afc5-259">Int32</span><span class="sxs-lookup"><span data-stu-id="6afc5-259">Int32</span></span> |
| <span data-ttu-id="6afc5-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="6afc5-260">long varbinary</span></span> |<span data-ttu-id="6afc5-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6afc5-261">Byte[]</span></span> |
| <span data-ttu-id="6afc5-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="6afc5-262">long varchar</span></span> |<span data-ttu-id="6afc5-263">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-263">String</span></span> |
| <span data-ttu-id="6afc5-264">longblob</span><span class="sxs-lookup"><span data-stu-id="6afc5-264">longblob</span></span> |<span data-ttu-id="6afc5-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6afc5-265">Byte[]</span></span> |
| <span data-ttu-id="6afc5-266">longtext</span><span class="sxs-lookup"><span data-stu-id="6afc5-266">longtext</span></span> |<span data-ttu-id="6afc5-267">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-267">String</span></span> |
| <span data-ttu-id="6afc5-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="6afc5-268">mediumblob</span></span> |<span data-ttu-id="6afc5-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6afc5-269">Byte[]</span></span> |
| <span data-ttu-id="6afc5-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-270">mediumint unsigned</span></span> |<span data-ttu-id="6afc5-271">Int64</span><span class="sxs-lookup"><span data-stu-id="6afc5-271">Int64</span></span> |
| <span data-ttu-id="6afc5-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="6afc5-272">mediumint</span></span> |<span data-ttu-id="6afc5-273">Int32</span><span class="sxs-lookup"><span data-stu-id="6afc5-273">Int32</span></span> |
| <span data-ttu-id="6afc5-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="6afc5-274">mediumtext</span></span> |<span data-ttu-id="6afc5-275">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-275">String</span></span> |
| <span data-ttu-id="6afc5-276">numeric</span><span class="sxs-lookup"><span data-stu-id="6afc5-276">numeric</span></span> |<span data-ttu-id="6afc5-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="6afc5-277">Decimal</span></span> |
| <span data-ttu-id="6afc5-278">real;</span><span class="sxs-lookup"><span data-stu-id="6afc5-278">real</span></span> |<span data-ttu-id="6afc5-279">Double</span><span class="sxs-lookup"><span data-stu-id="6afc5-279">Double</span></span> |
| <span data-ttu-id="6afc5-280">set</span><span class="sxs-lookup"><span data-stu-id="6afc5-280">set</span></span> |<span data-ttu-id="6afc5-281">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-281">String</span></span> |
| <span data-ttu-id="6afc5-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-282">smallint unsigned</span></span> |<span data-ttu-id="6afc5-283">Int32</span><span class="sxs-lookup"><span data-stu-id="6afc5-283">Int32</span></span> |
| <span data-ttu-id="6afc5-284">smallint;</span><span class="sxs-lookup"><span data-stu-id="6afc5-284">smallint</span></span> |<span data-ttu-id="6afc5-285">Int16</span><span class="sxs-lookup"><span data-stu-id="6afc5-285">Int16</span></span> |
| <span data-ttu-id="6afc5-286">text</span><span class="sxs-lookup"><span data-stu-id="6afc5-286">text</span></span> |<span data-ttu-id="6afc5-287">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-287">String</span></span> |
| <span data-ttu-id="6afc5-288">time</span><span class="sxs-lookup"><span data-stu-id="6afc5-288">time</span></span> |<span data-ttu-id="6afc5-289">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="6afc5-289">TimeSpan</span></span> |
| <span data-ttu-id="6afc5-290">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6afc5-290">timestamp</span></span> |<span data-ttu-id="6afc5-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="6afc5-291">Datetime</span></span> |
| <span data-ttu-id="6afc5-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="6afc5-292">tinyblob</span></span> |<span data-ttu-id="6afc5-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6afc5-293">Byte[]</span></span> |
| <span data-ttu-id="6afc5-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="6afc5-294">tinyint unsigned</span></span> |<span data-ttu-id="6afc5-295">Int16</span><span class="sxs-lookup"><span data-stu-id="6afc5-295">Int16</span></span> |
| <span data-ttu-id="6afc5-296">tinyint;</span><span class="sxs-lookup"><span data-stu-id="6afc5-296">tinyint</span></span> |<span data-ttu-id="6afc5-297">Int16</span><span class="sxs-lookup"><span data-stu-id="6afc5-297">Int16</span></span> |
| <span data-ttu-id="6afc5-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="6afc5-298">tinytext</span></span> |<span data-ttu-id="6afc5-299">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-299">String</span></span> |
| <span data-ttu-id="6afc5-300">varchar.</span><span class="sxs-lookup"><span data-stu-id="6afc5-300">varchar</span></span> |<span data-ttu-id="6afc5-301">Строка</span><span class="sxs-lookup"><span data-stu-id="6afc5-301">String</span></span> |
| <span data-ttu-id="6afc5-302">year</span><span class="sxs-lookup"><span data-stu-id="6afc5-302">year</span></span> |<span data-ttu-id="6afc5-303">int</span><span class="sxs-lookup"><span data-stu-id="6afc5-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6afc5-304">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="6afc5-304">Map source to sink columns</span></span>
<span data-ttu-id="6afc5-305">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6afc5-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6afc5-306">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="6afc5-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="6afc5-307">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="6afc5-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6afc5-308">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="6afc5-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6afc5-309">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="6afc5-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6afc5-310">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="6afc5-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6afc5-311">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6afc5-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6afc5-312">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="6afc5-312">Performance and Tuning</span></span>
<span data-ttu-id="6afc5-313">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="6afc5-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
