---
title: "Перемещение данных из базы данных Cassandra с помощью фабрики данных | Документация Майкрософт"
description: "Узнайте, как перемещать данные из локальной базы данных Cassandra с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="41486-103">Перемещение данных из локальной базы данных Cassandra с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="41486-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="41486-104">В этой статье объясняется, как с помощью действия копирования в фабрике данных Azure перемещать данные из локальной базы данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="41486-105">Этот документ является продолжением статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="41486-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="41486-106">Вы можете скопировать данные из локальной базы данных Cassandra в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="41486-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="41486-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, см. в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="41486-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="41486-108">Сейчас фабрика данных поддерживает только перемещение данных из локального хранилища данных Cassandra в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="41486-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="41486-109">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="41486-109">Supported versions</span></span>
<span data-ttu-id="41486-110">Соединитель Cassandra поддерживает следующие версии Cassandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="41486-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41486-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41486-111">Prerequisites</span></span>
<span data-ttu-id="41486-112">Чтобы служба фабрики данных Azure могла подключаться к локальной базе данных Cassandra, необходимо установить шлюз управления данными на том же компьютере, на котором размещена база данных, или на отдельном компьютере во избежание конкуренции за ресурсы с базой данных.</span><span class="sxs-lookup"><span data-stu-id="41486-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="41486-113">Шлюз управления данными — это компонент, который обеспечивает безопасное и управляемое подключение локальных источников данных к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="41486-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="41486-114">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="41486-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="41486-115">Пошаговые инструкции по настройке шлюза для перемещения данных с помощью конвейера см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="41486-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="41486-116">Для подключения к базе данных Cassandra необходимо использовать шлюз, даже если база данных размещается в облаке, например на виртуальной машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="41486-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="41486-117">Шлюз можно установить на той же виртуальной машине, на которой размещается база данных, или на отдельной виртуальной машине. Самое главное, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="41486-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="41486-118">Вместе со шлюзом автоматически устанавливается драйвер ODBC Microsoft Cassandra, который используется для подключения к базе данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="41486-119">Поэтому вам не нужно вручную устанавливать драйверы на компьютере шлюза при копировании данных из базы данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="41486-120">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="41486-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="41486-121">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="41486-121">Getting started</span></span>
<span data-ttu-id="41486-122">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="41486-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="41486-123">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="41486-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="41486-124">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="41486-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="41486-125">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="41486-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="41486-126">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41486-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="41486-127">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="41486-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="41486-128">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41486-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="41486-129">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="41486-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="41486-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="41486-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="41486-131">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="41486-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="41486-132">При использовании средств и API-интерфейсов (за исключением .NET API) эти сущности фабрики данных определяются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="41486-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="41486-133">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных Cassandra, вы найдете в разделе [Пример JSON. Копирование данных из базы данных Cassandra в хранилище BLOB-объектов Azure](#json-example-copy-data-from-cassandra-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="41486-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="41486-134">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="41486-135">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="41486-135">Linked service properties</span></span>
<span data-ttu-id="41486-136">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="41486-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="41486-137">Property</span></span> | <span data-ttu-id="41486-138">Описание</span><span class="sxs-lookup"><span data-stu-id="41486-138">Description</span></span> | <span data-ttu-id="41486-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="41486-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41486-140">type</span><span class="sxs-lookup"><span data-stu-id="41486-140">type</span></span> |<span data-ttu-id="41486-141">Для свойства type необходимо задать значение **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="41486-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="41486-142">Да</span><span class="sxs-lookup"><span data-stu-id="41486-142">Yes</span></span> |
| <span data-ttu-id="41486-143">host</span><span class="sxs-lookup"><span data-stu-id="41486-143">host</span></span> |<span data-ttu-id="41486-144">Один или несколько IP-адресов или имен узлов серверов Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="41486-145">Укажите через запятую список IP-адресов или имен узлов для одновременного подключения ко всем серверам.</span><span class="sxs-lookup"><span data-stu-id="41486-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="41486-146">Да</span><span class="sxs-lookup"><span data-stu-id="41486-146">Yes</span></span> |
| <span data-ttu-id="41486-147">порт</span><span class="sxs-lookup"><span data-stu-id="41486-147">port</span></span> |<span data-ttu-id="41486-148">TCP-порт, используемый сервером Cassandra для прослушивания клиентских подключений</span><span class="sxs-lookup"><span data-stu-id="41486-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="41486-149">Нет. Значение по умолчанию — 9042</span><span class="sxs-lookup"><span data-stu-id="41486-149">No, default value: 9042</span></span> |
| <span data-ttu-id="41486-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="41486-150">authenticationType</span></span> |<span data-ttu-id="41486-151">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="41486-151">Basic, or Anonymous</span></span> |<span data-ttu-id="41486-152">Да</span><span class="sxs-lookup"><span data-stu-id="41486-152">Yes</span></span> |
| <span data-ttu-id="41486-153">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="41486-153">username</span></span> |<span data-ttu-id="41486-154">Укажите имя пользователя для учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="41486-154">Specify user name for the user account.</span></span> |<span data-ttu-id="41486-155">Да (если для свойства authenticationType задано значение Basic)</span><span class="sxs-lookup"><span data-stu-id="41486-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="41486-156">пароль</span><span class="sxs-lookup"><span data-stu-id="41486-156">password</span></span> |<span data-ttu-id="41486-157">Укажите пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="41486-157">Specify password for the user account.</span></span> |<span data-ttu-id="41486-158">Да (если для свойства authenticationType задано значение Basic)</span><span class="sxs-lookup"><span data-stu-id="41486-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="41486-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="41486-159">gatewayName</span></span> |<span data-ttu-id="41486-160">Имя шлюза, который используется для подключения к локальной базе данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="41486-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="41486-161">Да</span><span class="sxs-lookup"><span data-stu-id="41486-161">Yes</span></span> |
| <span data-ttu-id="41486-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="41486-162">encryptedCredential</span></span> |<span data-ttu-id="41486-163">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="41486-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="41486-164">Нет</span><span class="sxs-lookup"><span data-stu-id="41486-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="41486-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="41486-165">Dataset properties</span></span>
<span data-ttu-id="41486-166">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="41486-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="41486-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="41486-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="41486-168">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="41486-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="41486-169">Раздел typeProperties набора данных типа **CassandraTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="41486-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="41486-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="41486-170">Property</span></span> | <span data-ttu-id="41486-171">Описание</span><span class="sxs-lookup"><span data-stu-id="41486-171">Description</span></span> | <span data-ttu-id="41486-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="41486-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41486-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="41486-173">keyspace</span></span> |<span data-ttu-id="41486-174">Имя пространства ключей или схемы в базе данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="41486-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="41486-175">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="41486-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="41486-176">tableName</span><span class="sxs-lookup"><span data-stu-id="41486-176">tableName</span></span> |<span data-ttu-id="41486-177">Имя таблицы в базе данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="41486-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="41486-178">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="41486-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="41486-179">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="41486-179">Copy activity properties</span></span>
<span data-ttu-id="41486-180">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="41486-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="41486-181">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="41486-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="41486-182">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="41486-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="41486-183">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="41486-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="41486-184">Если источник относится к типу **CassandraSource**, в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="41486-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="41486-185">Свойство</span><span class="sxs-lookup"><span data-stu-id="41486-185">Property</span></span> | <span data-ttu-id="41486-186">Описание</span><span class="sxs-lookup"><span data-stu-id="41486-186">Description</span></span> | <span data-ttu-id="41486-187">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="41486-187">Allowed values</span></span> | <span data-ttu-id="41486-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="41486-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="41486-189">query</span><span class="sxs-lookup"><span data-stu-id="41486-189">query</span></span> |<span data-ttu-id="41486-190">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="41486-190">Use the custom query to read data.</span></span> |<span data-ttu-id="41486-191">Запрос SQL-92 или CQL.</span><span class="sxs-lookup"><span data-stu-id="41486-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="41486-192">Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="41486-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="41486-193">Если используется SQL-запрос, то таблицу, к которой необходимо отправить запрос, укажите в формате **имя_пространства_ключей.имя_таблицы**.</span><span class="sxs-lookup"><span data-stu-id="41486-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="41486-194">Нет (если в наборе данных определены свойства tableName и keyspace)</span><span class="sxs-lookup"><span data-stu-id="41486-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="41486-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="41486-195">consistencyLevel</span></span> |<span data-ttu-id="41486-196">Определяет количество реплик, которые должны ответить на запрос на чтение перед возвращением данных в клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="41486-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="41486-197">Чтобы выполнить запрос на чтение, база данных Cassandra проверяет наличие указанного количества реплик для данных</span><span class="sxs-lookup"><span data-stu-id="41486-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="41486-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="41486-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="41486-199">Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных).</span><span class="sxs-lookup"><span data-stu-id="41486-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="41486-200">Нет.</span><span class="sxs-lookup"><span data-stu-id="41486-200">No.</span></span> <span data-ttu-id="41486-201">Значение по умолчанию — ONE</span><span class="sxs-lookup"><span data-stu-id="41486-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="41486-202">Пример JSON. Копирование данных из базы данных Cassandra в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="41486-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="41486-203">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="41486-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="41486-204">В этом примере показано, как скопировать данные из локальной базы данных Cassandra в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="41486-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="41486-205">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="41486-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41486-206">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="41486-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="41486-207">Он не включает в себя пошаговые инструкции по созданию фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41486-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="41486-208">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="41486-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="41486-209">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41486-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="41486-210">Связанная служба типа [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="41486-211">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="41486-212">Входной [набор данных](data-factory-create-datasets.md) типа [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="41486-213">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="41486-214">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [CassandraSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="41486-215">**Связанная служба Cassandra**</span><span class="sxs-lookup"><span data-stu-id="41486-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="41486-216">В этом примере используется связанная служба **Cassandra** .</span><span class="sxs-lookup"><span data-stu-id="41486-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="41486-217">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Свойства связанной службы OnPremisesCassandra](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="41486-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="41486-218">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="41486-218">**Azure Storage linked service:**</span></span>

```json
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

<span data-ttu-id="41486-219">**Входной набор данных Cassandra**</span><span class="sxs-lookup"><span data-stu-id="41486-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
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

<span data-ttu-id="41486-220">Если для параметра **external** задать значение **true**, то фабрика данных воспримет этот набор данных как внешний, который создан не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="41486-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="41486-221">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="41486-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="41486-222">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="41486-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="41486-223">**Действие копирования в конвейере с базой данных Cassandra в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="41486-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="41486-224">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="41486-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="41486-225">В определении JSON конвейера для типа **source** установлено значение **CassandraSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="41486-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="41486-226">Список свойств, поддерживаемых CassandraSource, см. в разделе [Свойства типа CassandraSource](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="41486-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]    
    }
}
```

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="41486-227">Сопоставление типов для Cassandra</span><span class="sxs-lookup"><span data-stu-id="41486-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="41486-228">Тип данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="41486-228">Cassandra Type</span></span> | <span data-ttu-id="41486-229">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="41486-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="41486-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="41486-230">ASCII</span></span> |<span data-ttu-id="41486-231">Строка</span><span class="sxs-lookup"><span data-stu-id="41486-231">String</span></span> |
| <span data-ttu-id="41486-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="41486-232">BIGINT</span></span> |<span data-ttu-id="41486-233">Int64</span><span class="sxs-lookup"><span data-stu-id="41486-233">Int64</span></span> |
| <span data-ttu-id="41486-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="41486-234">BLOB</span></span> |<span data-ttu-id="41486-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41486-235">Byte[]</span></span> |
| <span data-ttu-id="41486-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="41486-236">BOOLEAN</span></span> |<span data-ttu-id="41486-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="41486-237">Boolean</span></span> |
| <span data-ttu-id="41486-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="41486-238">DECIMAL</span></span> |<span data-ttu-id="41486-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="41486-239">Decimal</span></span> |
| <span data-ttu-id="41486-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="41486-240">DOUBLE</span></span> |<span data-ttu-id="41486-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="41486-241">Double</span></span> |
| <span data-ttu-id="41486-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="41486-242">FLOAT</span></span> |<span data-ttu-id="41486-243">Single</span><span class="sxs-lookup"><span data-stu-id="41486-243">Single</span></span> |
| <span data-ttu-id="41486-244">INET</span><span class="sxs-lookup"><span data-stu-id="41486-244">INET</span></span> |<span data-ttu-id="41486-245">Строка</span><span class="sxs-lookup"><span data-stu-id="41486-245">String</span></span> |
| <span data-ttu-id="41486-246">INT</span><span class="sxs-lookup"><span data-stu-id="41486-246">INT</span></span> |<span data-ttu-id="41486-247">Int32</span><span class="sxs-lookup"><span data-stu-id="41486-247">Int32</span></span> |
| <span data-ttu-id="41486-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="41486-248">TEXT</span></span> |<span data-ttu-id="41486-249">Строка</span><span class="sxs-lookup"><span data-stu-id="41486-249">String</span></span> |
| <span data-ttu-id="41486-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="41486-250">TIMESTAMP</span></span> |<span data-ttu-id="41486-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="41486-251">DateTime</span></span> |
| <span data-ttu-id="41486-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="41486-252">TIMEUUID</span></span> |<span data-ttu-id="41486-253">Guid</span><span class="sxs-lookup"><span data-stu-id="41486-253">Guid</span></span> |
| <span data-ttu-id="41486-254">UUID</span><span class="sxs-lookup"><span data-stu-id="41486-254">UUID</span></span> |<span data-ttu-id="41486-255">Guid</span><span class="sxs-lookup"><span data-stu-id="41486-255">Guid</span></span> |
| <span data-ttu-id="41486-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="41486-256">VARCHAR</span></span> |<span data-ttu-id="41486-257">Строка</span><span class="sxs-lookup"><span data-stu-id="41486-257">String</span></span> |
| <span data-ttu-id="41486-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="41486-258">VARINT</span></span> |<span data-ttu-id="41486-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="41486-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="41486-260">Дополнительные сведения о типах коллекций (сопоставлениях, наборах, списках и т. д.) см. в разделе [Работа с коллекциями с использованием виртуальной таблицы](#work-with-collections-using-virtual-table).</span><span class="sxs-lookup"><span data-stu-id="41486-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="41486-261">Пользовательские типы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="41486-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="41486-262">Длина столбца двоичного кода и столбца строки не может превышать 4000 знаков.</span><span class="sxs-lookup"><span data-stu-id="41486-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="41486-263">Работа с коллекциями с использованием виртуальной таблицы</span><span class="sxs-lookup"><span data-stu-id="41486-263">Work with collections using virtual table</span></span>
<span data-ttu-id="41486-264">В фабрике данных Azure используется встроенный драйвер ODBC, который позволяет подключаться к базе данных Cassandra и копировать из нее данные.</span><span class="sxs-lookup"><span data-stu-id="41486-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="41486-265">Для типов коллекций, в том числе сопоставлений, наборов и списков, драйвер ренормализует данные в соответствующие виртуальные таблицы.</span><span class="sxs-lookup"><span data-stu-id="41486-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="41486-266">В частности, если таблица содержит столбцы с данными типа коллекции, драйвер создает следующие виртуальные таблицы.</span><span class="sxs-lookup"><span data-stu-id="41486-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="41486-267">**Базовая таблица**. В ней содержатся те же данные, что и в исходной таблице, кроме столбцов данных типа коллекции.</span><span class="sxs-lookup"><span data-stu-id="41486-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="41486-268">Имена базовой таблицы и таблицы, которую она представляет, совпадают.</span><span class="sxs-lookup"><span data-stu-id="41486-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="41486-269">**Виртуальная таблица**. Эта таблица создается для каждого столбца с данными типа коллекции. В ней представлены вложенные данные в развернутом виде.</span><span class="sxs-lookup"><span data-stu-id="41486-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="41486-270">Виртуальным таблицам, представляющим коллекции, присваиваются имена в следующем формате: "имя_исходной_таблицы*_vt_*имя_столбца".</span><span class="sxs-lookup"><span data-stu-id="41486-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="41486-271">Виртуальные таблицы ссылаются на данные в исходной таблице, что позволяет драйверу подключаться к денормализованным данным.</span><span class="sxs-lookup"><span data-stu-id="41486-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="41486-272">Дополнительные сведения см. в разделе "Пример".</span><span class="sxs-lookup"><span data-stu-id="41486-272">See Example section for details.</span></span> <span data-ttu-id="41486-273">Доступ к содержимому коллекций Cassandra можно получить при помощи отправки запроса и соединения виртуальных таблиц.</span><span class="sxs-lookup"><span data-stu-id="41486-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="41486-274">Список таблиц, в том числе виртуальных, в базе данных Cassandra и содержащиеся в них данные можно просмотреть с помощью [мастера копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity).</span><span class="sxs-lookup"><span data-stu-id="41486-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="41486-275">Он также позволяет создать запрос и просмотреть результат выполнения.</span><span class="sxs-lookup"><span data-stu-id="41486-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="41486-276">Пример</span><span class="sxs-lookup"><span data-stu-id="41486-276">Example</span></span>
<span data-ttu-id="41486-277">Ниже приведен пример таблицы ExampleTable в базе данных Cassandra. В этой таблице содержатся такие столбцы: столбец первичного ключа pk_int (целое число), текстовый столбец "Значение", столбец "Список", "Сопоставление" и StringSet.</span><span class="sxs-lookup"><span data-stu-id="41486-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="41486-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="41486-278">pk_int</span></span> | <span data-ttu-id="41486-279">Значение</span><span class="sxs-lookup"><span data-stu-id="41486-279">Value</span></span> | <span data-ttu-id="41486-280">список</span><span class="sxs-lookup"><span data-stu-id="41486-280">List</span></span> | <span data-ttu-id="41486-281">Сопоставление</span><span class="sxs-lookup"><span data-stu-id="41486-281">Map</span></span> | <span data-ttu-id="41486-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="41486-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="41486-283">1</span><span class="sxs-lookup"><span data-stu-id="41486-283">1</span></span> |<span data-ttu-id="41486-284">"пример значения 1"</span><span class="sxs-lookup"><span data-stu-id="41486-284">"sample value 1"</span></span> |<span data-ttu-id="41486-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="41486-285">["1", "2", "3"]</span></span> |<span data-ttu-id="41486-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="41486-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="41486-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="41486-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="41486-288">3</span><span class="sxs-lookup"><span data-stu-id="41486-288">3</span></span> |<span data-ttu-id="41486-289">"пример значения 3"</span><span class="sxs-lookup"><span data-stu-id="41486-289">"sample value 3"</span></span> |<span data-ttu-id="41486-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="41486-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="41486-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="41486-291">{"S1": "t"}</span></span> |<span data-ttu-id="41486-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="41486-292">{"A", "E"}</span></span> |

<span data-ttu-id="41486-293">Для представления такой одной таблицы драйвер создает несколько виртуальных таблиц.</span><span class="sxs-lookup"><span data-stu-id="41486-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="41486-294">Столбцы внешнего ключа в виртуальных таблицах ссылаются на столбцы первичного ключа в исходных таблицах и указывают, какая строка исходной таблицы соответствует строке виртуальной таблицы.</span><span class="sxs-lookup"><span data-stu-id="41486-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="41486-295">Ниже приведен пример первой базовой виртуальной таблицы ExampleTable.</span><span class="sxs-lookup"><span data-stu-id="41486-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="41486-296">В этой таблице содержатся те же данные, что и в исходной, но без коллекций. Они развернуты в других виртуальных таблицах.</span><span class="sxs-lookup"><span data-stu-id="41486-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="41486-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="41486-297">pk_int</span></span> | <span data-ttu-id="41486-298">Значение</span><span class="sxs-lookup"><span data-stu-id="41486-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="41486-299">1</span><span class="sxs-lookup"><span data-stu-id="41486-299">1</span></span> |<span data-ttu-id="41486-300">"пример значения 1"</span><span class="sxs-lookup"><span data-stu-id="41486-300">"sample value 1"</span></span> |
| <span data-ttu-id="41486-301">3</span><span class="sxs-lookup"><span data-stu-id="41486-301">3</span></span> |<span data-ttu-id="41486-302">"пример значения 3"</span><span class="sxs-lookup"><span data-stu-id="41486-302">"sample value 3"</span></span> |

<span data-ttu-id="41486-303">Ниже приведены виртуальные таблицы, в которых ренормализированы данные из столбцов "Список", "Сопоставление" и StringSet.</span><span class="sxs-lookup"><span data-stu-id="41486-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="41486-304">Столбцы, имена которых заканчиваются на _index или _key, указывают на позицию данных в исходном списке или сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="41486-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="41486-305">Столбцы, имена которых заканчиваются на _value, содержат развернутые данные из коллекции.</span><span class="sxs-lookup"><span data-stu-id="41486-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="41486-306">Таблица ExampleTable_vt_List</span><span class="sxs-lookup"><span data-stu-id="41486-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="41486-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="41486-307">pk_int</span></span> | <span data-ttu-id="41486-308">List_index</span><span class="sxs-lookup"><span data-stu-id="41486-308">List_index</span></span> | <span data-ttu-id="41486-309">List_value</span><span class="sxs-lookup"><span data-stu-id="41486-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41486-310">1</span><span class="sxs-lookup"><span data-stu-id="41486-310">1</span></span> |<span data-ttu-id="41486-311">0</span><span class="sxs-lookup"><span data-stu-id="41486-311">0</span></span> |<span data-ttu-id="41486-312">1</span><span class="sxs-lookup"><span data-stu-id="41486-312">1</span></span> |
| <span data-ttu-id="41486-313">1</span><span class="sxs-lookup"><span data-stu-id="41486-313">1</span></span> |<span data-ttu-id="41486-314">1</span><span class="sxs-lookup"><span data-stu-id="41486-314">1</span></span> |<span data-ttu-id="41486-315">2</span><span class="sxs-lookup"><span data-stu-id="41486-315">2</span></span> |
| <span data-ttu-id="41486-316">1</span><span class="sxs-lookup"><span data-stu-id="41486-316">1</span></span> |<span data-ttu-id="41486-317">2</span><span class="sxs-lookup"><span data-stu-id="41486-317">2</span></span> |<span data-ttu-id="41486-318">3</span><span class="sxs-lookup"><span data-stu-id="41486-318">3</span></span> |
| <span data-ttu-id="41486-319">3</span><span class="sxs-lookup"><span data-stu-id="41486-319">3</span></span> |<span data-ttu-id="41486-320">0</span><span class="sxs-lookup"><span data-stu-id="41486-320">0</span></span> |<span data-ttu-id="41486-321">100</span><span class="sxs-lookup"><span data-stu-id="41486-321">100</span></span> |
| <span data-ttu-id="41486-322">3</span><span class="sxs-lookup"><span data-stu-id="41486-322">3</span></span> |<span data-ttu-id="41486-323">1</span><span class="sxs-lookup"><span data-stu-id="41486-323">1</span></span> |<span data-ttu-id="41486-324">101</span><span class="sxs-lookup"><span data-stu-id="41486-324">101</span></span> |
| <span data-ttu-id="41486-325">3</span><span class="sxs-lookup"><span data-stu-id="41486-325">3</span></span> |<span data-ttu-id="41486-326">2</span><span class="sxs-lookup"><span data-stu-id="41486-326">2</span></span> |<span data-ttu-id="41486-327">102</span><span class="sxs-lookup"><span data-stu-id="41486-327">102</span></span> |
| <span data-ttu-id="41486-328">3</span><span class="sxs-lookup"><span data-stu-id="41486-328">3</span></span> |<span data-ttu-id="41486-329">3</span><span class="sxs-lookup"><span data-stu-id="41486-329">3</span></span> |<span data-ttu-id="41486-330">103</span><span class="sxs-lookup"><span data-stu-id="41486-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="41486-331">Таблица ExampleTable_vt_Map</span><span class="sxs-lookup"><span data-stu-id="41486-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="41486-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="41486-332">pk_int</span></span> | <span data-ttu-id="41486-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="41486-333">Map_key</span></span> | <span data-ttu-id="41486-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="41486-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41486-335">1</span><span class="sxs-lookup"><span data-stu-id="41486-335">1</span></span> |<span data-ttu-id="41486-336">S1</span><span class="sxs-lookup"><span data-stu-id="41486-336">S1</span></span> |<span data-ttu-id="41486-337">Файл ,</span><span class="sxs-lookup"><span data-stu-id="41486-337">A</span></span> |
| <span data-ttu-id="41486-338">1</span><span class="sxs-lookup"><span data-stu-id="41486-338">1</span></span> |<span data-ttu-id="41486-339">S2</span><span class="sxs-lookup"><span data-stu-id="41486-339">S2</span></span> |<span data-ttu-id="41486-340">b</span><span class="sxs-lookup"><span data-stu-id="41486-340">b</span></span> |
| <span data-ttu-id="41486-341">3</span><span class="sxs-lookup"><span data-stu-id="41486-341">3</span></span> |<span data-ttu-id="41486-342">S1</span><span class="sxs-lookup"><span data-stu-id="41486-342">S1</span></span> |<span data-ttu-id="41486-343">t</span><span class="sxs-lookup"><span data-stu-id="41486-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="41486-344">Таблица ExampleTable_vt_StringSet:</span><span class="sxs-lookup"><span data-stu-id="41486-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="41486-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="41486-345">pk_int</span></span> | <span data-ttu-id="41486-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="41486-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="41486-347">1</span><span class="sxs-lookup"><span data-stu-id="41486-347">1</span></span> |<span data-ttu-id="41486-348">Файл ,</span><span class="sxs-lookup"><span data-stu-id="41486-348">A</span></span> |
| <span data-ttu-id="41486-349">1</span><span class="sxs-lookup"><span data-stu-id="41486-349">1</span></span> |<span data-ttu-id="41486-350">b</span><span class="sxs-lookup"><span data-stu-id="41486-350">B</span></span> |
| <span data-ttu-id="41486-351">1</span><span class="sxs-lookup"><span data-stu-id="41486-351">1</span></span> |<span data-ttu-id="41486-352">C</span><span class="sxs-lookup"><span data-stu-id="41486-352">C</span></span> |
| <span data-ttu-id="41486-353">3</span><span class="sxs-lookup"><span data-stu-id="41486-353">3</span></span> |<span data-ttu-id="41486-354">Файл ,</span><span class="sxs-lookup"><span data-stu-id="41486-354">A</span></span> |
| <span data-ttu-id="41486-355">3</span><span class="sxs-lookup"><span data-stu-id="41486-355">3</span></span> |<span data-ttu-id="41486-356">E</span><span class="sxs-lookup"><span data-stu-id="41486-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="41486-357">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="41486-357">Map source to sink columns</span></span>
<span data-ttu-id="41486-358">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="41486-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="41486-359">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="41486-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="41486-360">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="41486-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="41486-361">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="41486-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="41486-362">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="41486-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="41486-363">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="41486-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="41486-364">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="41486-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="41486-365">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="41486-365">Performance and Tuning</span></span>
<span data-ttu-id="41486-366">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="41486-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
