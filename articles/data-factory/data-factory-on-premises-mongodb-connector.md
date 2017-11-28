---
title: "Перемещение данных из базы данных MongoDB с помощью фабрики данных | Документация Майкрософт"
description: "Узнайте, как перемещать данные из базы данных MongoDB с использованием фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="c85e1-103">Перемещение данных из MongoDB с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="c85e1-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="c85e1-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локальной базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c85e1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="c85e1-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c85e1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c85e1-106">Вы можете скопировать данные из локального хранилища данных MongoDB в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="c85e1-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c85e1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c85e1-108">Сейчас фабрика данных поддерживает только перемещение данных из хранилища данных MongoDB в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="c85e1-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c85e1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c85e1-109">Prerequisites</span></span>
<span data-ttu-id="c85e1-110">Чтобы служба фабрики данных Azure могла подключаться к локальной базе данных MongoDB, необходимо установить следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="c85e1-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="c85e1-111">Поддерживаемые версии MongoDB: 2.4, 2.6, 3.0 и 3.2.</span><span class="sxs-lookup"><span data-stu-id="c85e1-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="c85e1-112">Шлюз управления данными на том же компьютере, на котором размещена база данных, или на отдельном компьютере во избежание конкуренции за ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c85e1-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="c85e1-113">Шлюз управления данными — это программное обеспечение, которое обеспечивает безопасное и управляемое подключение локальных источников данных к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="c85e1-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="c85e1-114">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="c85e1-115">Пошаговые инструкции по настройке шлюза для перемещения данных с помощью конвейера см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="c85e1-116">Вместе со шлюзом автоматически устанавливается драйвер ODBC Microsoft MongoDB, который используется для подключения к базе данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c85e1-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c85e1-117">Шлюз используется для подключения к источнику MongoDB, даже если он размещен на виртуальных машинах IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="c85e1-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="c85e1-118">Если вы подключаетесь к экземпляру MongoDB, размещенному в облаке, экземпляр шлюза можно тоже установить на виртуальную машину IaaS.</span><span class="sxs-lookup"><span data-stu-id="c85e1-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c85e1-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c85e1-119">Getting started</span></span>
<span data-ttu-id="c85e1-120">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных MongoDB, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="c85e1-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="c85e1-121">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="c85e1-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c85e1-122">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c85e1-123">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c85e1-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c85e1-124">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c85e1-125">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c85e1-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="c85e1-126">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c85e1-127">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="c85e1-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c85e1-128">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c85e1-129">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="c85e1-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c85e1-130">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c85e1-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c85e1-131">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных MongoDB, приведен в разделе [Пример JSON. Копирование данных из MongoDB в большой двоичный объект Azure](#json-example-copy-data-from-mongodb-to-azure-blob) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c85e1-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c85e1-132">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к источнику MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c85e1-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c85e1-133">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="c85e1-133">Linked service properties</span></span>
<span data-ttu-id="c85e1-134">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе **OnPremisesMongoDB** .</span><span class="sxs-lookup"><span data-stu-id="c85e1-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="c85e1-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="c85e1-135">Property</span></span> | <span data-ttu-id="c85e1-136">Описание</span><span class="sxs-lookup"><span data-stu-id="c85e1-136">Description</span></span> | <span data-ttu-id="c85e1-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c85e1-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c85e1-138">type</span><span class="sxs-lookup"><span data-stu-id="c85e1-138">type</span></span> |<span data-ttu-id="c85e1-139">Для свойства type необходимо задать значение **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="c85e1-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="c85e1-140">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-140">Yes</span></span> |
| <span data-ttu-id="c85e1-141">server</span><span class="sxs-lookup"><span data-stu-id="c85e1-141">server</span></span> |<span data-ttu-id="c85e1-142">IP-адрес или имя узла сервера MongoDB</span><span class="sxs-lookup"><span data-stu-id="c85e1-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="c85e1-143">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-143">Yes</span></span> |
| <span data-ttu-id="c85e1-144">порт</span><span class="sxs-lookup"><span data-stu-id="c85e1-144">port</span></span> |<span data-ttu-id="c85e1-145">TCP-порт, используемый сервером MongoDB для прослушивания клиентских подключений</span><span class="sxs-lookup"><span data-stu-id="c85e1-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="c85e1-146">Значение по умолчанию — 27017 (необязательно)</span><span class="sxs-lookup"><span data-stu-id="c85e1-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="c85e1-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c85e1-147">authenticationType</span></span> |<span data-ttu-id="c85e1-148">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="c85e1-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="c85e1-149">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-149">Yes</span></span> |
| <span data-ttu-id="c85e1-150">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="c85e1-150">username</span></span> |<span data-ttu-id="c85e1-151">Учетная запись пользователя для доступа к MongoDB</span><span class="sxs-lookup"><span data-stu-id="c85e1-151">User account to access MongoDB.</span></span> |<span data-ttu-id="c85e1-152">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="c85e1-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="c85e1-153">пароль</span><span class="sxs-lookup"><span data-stu-id="c85e1-153">password</span></span> |<span data-ttu-id="c85e1-154">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="c85e1-154">Password for the user.</span></span> |<span data-ttu-id="c85e1-155">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="c85e1-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="c85e1-156">authSource</span><span class="sxs-lookup"><span data-stu-id="c85e1-156">authSource</span></span> |<span data-ttu-id="c85e1-157">Имя базы данных MongoDB, которое будет использоваться для проверки учетных данных при проверке подлинности</span><span class="sxs-lookup"><span data-stu-id="c85e1-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="c85e1-158">Необязательно (если используется обычная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="c85e1-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="c85e1-159">По умолчанию используется учетная запись администратора и база данных, указанная с помощью свойства databaseName</span><span class="sxs-lookup"><span data-stu-id="c85e1-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="c85e1-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="c85e1-160">databaseName</span></span> |<span data-ttu-id="c85e1-161">Имя базы данных MongoDB, к которой необходимо получить доступ</span><span class="sxs-lookup"><span data-stu-id="c85e1-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="c85e1-162">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-162">Yes</span></span> |
| <span data-ttu-id="c85e1-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c85e1-163">gatewayName</span></span> |<span data-ttu-id="c85e1-164">Имя шлюза, который обращается к хранилищу данных</span><span class="sxs-lookup"><span data-stu-id="c85e1-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="c85e1-165">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-165">Yes</span></span> |
| <span data-ttu-id="c85e1-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c85e1-166">encryptedCredential</span></span> |<span data-ttu-id="c85e1-167">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="c85e1-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="c85e1-168">Необязательно</span><span class="sxs-lookup"><span data-stu-id="c85e1-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c85e1-169">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="c85e1-169">Dataset properties</span></span>
<span data-ttu-id="c85e1-170">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c85e1-171">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c85e1-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c85e1-172">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c85e1-173">Раздел typeProperties набора данных типа **MongoDbCollection** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="c85e1-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="c85e1-174">Свойство</span><span class="sxs-lookup"><span data-stu-id="c85e1-174">Property</span></span> | <span data-ttu-id="c85e1-175">Описание</span><span class="sxs-lookup"><span data-stu-id="c85e1-175">Description</span></span> | <span data-ttu-id="c85e1-176">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c85e1-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c85e1-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="c85e1-177">collectionName</span></span> |<span data-ttu-id="c85e1-178">Имя коллекции в базе данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="c85e1-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="c85e1-179">Да</span><span class="sxs-lookup"><span data-stu-id="c85e1-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c85e1-180">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="c85e1-180">Copy activity properties</span></span>
<span data-ttu-id="c85e1-181">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c85e1-182">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="c85e1-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c85e1-183">С другой стороны, свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="c85e1-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="c85e1-184">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="c85e1-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c85e1-185">Если источник относится к типу **MongoDbSource** , в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="c85e1-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c85e1-186">Свойство</span><span class="sxs-lookup"><span data-stu-id="c85e1-186">Property</span></span> | <span data-ttu-id="c85e1-187">Описание</span><span class="sxs-lookup"><span data-stu-id="c85e1-187">Description</span></span> | <span data-ttu-id="c85e1-188">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="c85e1-188">Allowed values</span></span> | <span data-ttu-id="c85e1-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c85e1-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c85e1-190">query</span><span class="sxs-lookup"><span data-stu-id="c85e1-190">query</span></span> |<span data-ttu-id="c85e1-191">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-191">Use the custom query to read data.</span></span> |<span data-ttu-id="c85e1-192">Строка запроса SQL-92.</span><span class="sxs-lookup"><span data-stu-id="c85e1-192">SQL-92 query string.</span></span> <span data-ttu-id="c85e1-193">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="c85e1-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="c85e1-194">Нет (если для свойства **collectionName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="c85e1-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="c85e1-195">Пример JSON. Копирование данных из MongoDB в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="c85e1-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="c85e1-196">Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c85e1-197">В нем показано, как скопировать данные из локального хранилища данных MongoDB в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c85e1-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="c85e1-198">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c85e1-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="c85e1-199">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c85e1-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c85e1-200">Связанная служба типа [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c85e1-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="c85e1-201">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c85e1-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c85e1-202">Входной [набор данных](data-factory-create-datasets.md) типа [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c85e1-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="c85e1-203">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c85e1-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c85e1-204">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [MongoDbSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c85e1-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c85e1-205">В примере данные из результата выполнения запроса к базе данных MongoDB каждый час копируются в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="c85e1-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="c85e1-206">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="c85e1-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c85e1-207">Сначала настройте шлюз управления данными. Необходимые инструкции представлены в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="c85e1-208">**Связанная служба MongoDB**</span><span class="sxs-lookup"><span data-stu-id="c85e1-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="c85e1-209">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="c85e1-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="c85e1-210">**Входной набор данных MongoDB**. Если для параметра external задать значение true, то фабрика данных воспримет эту таблицу как внешнюю таблицу, которая создана не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="c85e1-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="c85e1-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="c85e1-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c85e1-212">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c85e1-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c85e1-213">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="c85e1-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c85e1-214">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="c85e1-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c85e1-215">**Действие копирования в конвейере с MongoDB в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="c85e1-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="c85e1-216">Конвейер содержит действие копирования (Copy), которое использует входной и выходной наборы данных (см. выше) и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="c85e1-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c85e1-217">В определении JSON конвейера для типа **source** установлено значение **MongoDbSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c85e1-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c85e1-218">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="c85e1-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="c85e1-219">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c85e1-219">Schema by Data Factory</span></span>
<span data-ttu-id="c85e1-220">Служба фабрики данных Azure определяет схему для коллекции MongoDB, используя последние 100 документов в коллекции.</span><span class="sxs-lookup"><span data-stu-id="c85e1-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="c85e1-221">Если эти 100 документов не содержат полной схемы, во время копирования некоторые столбцы могут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="c85e1-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="c85e1-222">Сопоставление типов для MongoDB</span><span class="sxs-lookup"><span data-stu-id="c85e1-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="c85e1-223">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа.</span><span class="sxs-lookup"><span data-stu-id="c85e1-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="c85e1-224">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="c85e1-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c85e1-225">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="c85e1-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c85e1-226">Когда данные перемещаются в MongoDB, для преобразования типов MongoDB в типы .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="c85e1-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="c85e1-227">Тип MongoDB</span><span class="sxs-lookup"><span data-stu-id="c85e1-227">MongoDB type</span></span> | <span data-ttu-id="c85e1-228">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c85e1-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c85e1-229">Binary</span><span class="sxs-lookup"><span data-stu-id="c85e1-229">Binary</span></span> |<span data-ttu-id="c85e1-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c85e1-230">Byte[]</span></span> |
| <span data-ttu-id="c85e1-231">Логический</span><span class="sxs-lookup"><span data-stu-id="c85e1-231">Boolean</span></span> |<span data-ttu-id="c85e1-232">Логический</span><span class="sxs-lookup"><span data-stu-id="c85e1-232">Boolean</span></span> |
| <span data-ttu-id="c85e1-233">Дата</span><span class="sxs-lookup"><span data-stu-id="c85e1-233">Date</span></span> |<span data-ttu-id="c85e1-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="c85e1-234">DateTime</span></span> |
| <span data-ttu-id="c85e1-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="c85e1-235">NumberDouble</span></span> |<span data-ttu-id="c85e1-236">Double</span><span class="sxs-lookup"><span data-stu-id="c85e1-236">Double</span></span> |
| <span data-ttu-id="c85e1-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="c85e1-237">NumberInt</span></span> |<span data-ttu-id="c85e1-238">Int32</span><span class="sxs-lookup"><span data-stu-id="c85e1-238">Int32</span></span> |
| <span data-ttu-id="c85e1-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="c85e1-239">NumberLong</span></span> |<span data-ttu-id="c85e1-240">Int64</span><span class="sxs-lookup"><span data-stu-id="c85e1-240">Int64</span></span> |
| <span data-ttu-id="c85e1-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="c85e1-241">ObjectID</span></span> |<span data-ttu-id="c85e1-242">Строковый</span><span class="sxs-lookup"><span data-stu-id="c85e1-242">String</span></span> |
| <span data-ttu-id="c85e1-243">Строковый</span><span class="sxs-lookup"><span data-stu-id="c85e1-243">String</span></span> |<span data-ttu-id="c85e1-244">Строковый</span><span class="sxs-lookup"><span data-stu-id="c85e1-244">String</span></span> |
| <span data-ttu-id="c85e1-245">UUID</span><span class="sxs-lookup"><span data-stu-id="c85e1-245">UUID</span></span> |<span data-ttu-id="c85e1-246">Guid</span><span class="sxs-lookup"><span data-stu-id="c85e1-246">Guid</span></span> |
| <span data-ttu-id="c85e1-247">Объект</span><span class="sxs-lookup"><span data-stu-id="c85e1-247">Object</span></span> |<span data-ttu-id="c85e1-248">Преобразованный в плоские столбцы с "_" в качестве вложенного разделителя</span><span class="sxs-lookup"><span data-stu-id="c85e1-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="c85e1-249">Дополнительные сведения о поддержке массивов с помощью виртуальных таблиц см. в разделе [Поддержка сложных типов с помощью виртуальных таблиц](#support-for-complex-types-using-virtual-tables) ниже.</span><span class="sxs-lookup"><span data-stu-id="c85e1-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="c85e1-250">В настоящее время не поддерживаются следующие типы MongoDB: DBPointer, JavaScript, мин. и макс. значение ключей, регулярное выражение, символ, метка времени, не определенный.</span><span class="sxs-lookup"><span data-stu-id="c85e1-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="c85e1-251">Поддержка сложных типов с помощью виртуальных таблиц</span><span class="sxs-lookup"><span data-stu-id="c85e1-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="c85e1-252">В фабрике данных Azure используется встроенный драйвер ODBC, который позволяет подключаться к базе данных MongoDB и копировать из нее данные.</span><span class="sxs-lookup"><span data-stu-id="c85e1-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="c85e1-253">Для сложных типов, таких как массивы или объекты с различными типами данных в документах, драйвер ренормализует данные в соответствующие виртуальные таблицы.</span><span class="sxs-lookup"><span data-stu-id="c85e1-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="c85e1-254">В частности, если таблица содержит такие столбцы, драйвер создает следующие виртуальные таблицы.</span><span class="sxs-lookup"><span data-stu-id="c85e1-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="c85e1-255">**Базовая таблица**, в которой содержатся те же данные, что и в исходной таблице, кроме столбцов сложного типа.</span><span class="sxs-lookup"><span data-stu-id="c85e1-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="c85e1-256">Имена базовой таблицы и таблицы, которую она представляет, совпадают.</span><span class="sxs-lookup"><span data-stu-id="c85e1-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="c85e1-257">**Виртуальная таблица** для каждого столбца сложного типа, в которой представлены вложенные данные в развернутом виде.</span><span class="sxs-lookup"><span data-stu-id="c85e1-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="c85e1-258">Виртуальным таблицам присваиваются имена в следующем формате: имя исходной таблицы, разделитель "_", имя массива или объекта.</span><span class="sxs-lookup"><span data-stu-id="c85e1-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="c85e1-259">Виртуальные таблицы ссылаются на данные в исходной таблице, что позволяет драйверу подключаться к денормализованным данным.</span><span class="sxs-lookup"><span data-stu-id="c85e1-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="c85e1-260">Дополнительные сведения см. в разделе "Примеры".</span><span class="sxs-lookup"><span data-stu-id="c85e1-260">See Example section below details.</span></span> <span data-ttu-id="c85e1-261">Доступ к содержимому массивов MongoDB можно получить при помощи отправки запроса и соединения виртуальных таблиц.</span><span class="sxs-lookup"><span data-stu-id="c85e1-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="c85e1-262">Просмотреть список таблиц, в том числе виртуальных, в базе данных MongoDB и содержащихся в них данных можно с помощью [мастера копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) .</span><span class="sxs-lookup"><span data-stu-id="c85e1-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="c85e1-263">Он также позволяет создать запрос и просмотреть результат выполнения.</span><span class="sxs-lookup"><span data-stu-id="c85e1-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="c85e1-264">Пример</span><span class="sxs-lookup"><span data-stu-id="c85e1-264">Example</span></span>
<span data-ttu-id="c85e1-265">Ниже приведен пример таблицы ExampleTable в базе данных MongoDB, содержащей столбец ("Счета") с массивом объектов в каждой ячейке и столбец с массивом данных скалярных типов ("Оценки").</span><span class="sxs-lookup"><span data-stu-id="c85e1-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="c85e1-266">_№</span><span class="sxs-lookup"><span data-stu-id="c85e1-266">_id</span></span> | <span data-ttu-id="c85e1-267">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="c85e1-267">Customer Name</span></span> | <span data-ttu-id="c85e1-268">Счета</span><span class="sxs-lookup"><span data-stu-id="c85e1-268">Invoices</span></span> | <span data-ttu-id="c85e1-269">Уровень обслуживания</span><span class="sxs-lookup"><span data-stu-id="c85e1-269">Service Level</span></span> | <span data-ttu-id="c85e1-270">Оценки</span><span class="sxs-lookup"><span data-stu-id="c85e1-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c85e1-271">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-271">1111</span></span> |<span data-ttu-id="c85e1-272">ABC</span><span class="sxs-lookup"><span data-stu-id="c85e1-272">ABC</span></span> |<span data-ttu-id="c85e1-273">[{счет_№:"123", товар:"тостер", цена:"456", скидка:"0,2"}, {счет_№:"124", товар:"печь", цена: "1235", скидка: "0,2"}]</span><span class="sxs-lookup"><span data-stu-id="c85e1-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="c85e1-274">Silver</span><span class="sxs-lookup"><span data-stu-id="c85e1-274">Silver</span></span> |<span data-ttu-id="c85e1-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="c85e1-275">[5,6]</span></span> |
| <span data-ttu-id="c85e1-276">2222</span><span class="sxs-lookup"><span data-stu-id="c85e1-276">2222</span></span> |<span data-ttu-id="c85e1-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="c85e1-277">XYZ</span></span> |<span data-ttu-id="c85e1-278">[{счет_№: "135", товар: "холодильник", цена: "12543", скидка: "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="c85e1-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="c85e1-279">Gold</span><span class="sxs-lookup"><span data-stu-id="c85e1-279">Gold</span></span> |<span data-ttu-id="c85e1-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="c85e1-280">[1,2]</span></span> |

<span data-ttu-id="c85e1-281">Для представления такой одной таблицы драйвер создает несколько виртуальных таблиц.</span><span class="sxs-lookup"><span data-stu-id="c85e1-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="c85e1-282">Ниже приведен пример первой базовой виртуальной таблицы ExampleTable.</span><span class="sxs-lookup"><span data-stu-id="c85e1-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="c85e1-283">Базовая таблица содержит все данные из исходной таблицы, но данные массивов опущены и развернуты в виртуальных таблицах.</span><span class="sxs-lookup"><span data-stu-id="c85e1-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="c85e1-284">_№</span><span class="sxs-lookup"><span data-stu-id="c85e1-284">_id</span></span> | <span data-ttu-id="c85e1-285">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="c85e1-285">Customer Name</span></span> | <span data-ttu-id="c85e1-286">Уровень обслуживания</span><span class="sxs-lookup"><span data-stu-id="c85e1-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c85e1-287">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-287">1111</span></span> |<span data-ttu-id="c85e1-288">ABC</span><span class="sxs-lookup"><span data-stu-id="c85e1-288">ABC</span></span> |<span data-ttu-id="c85e1-289">Silver</span><span class="sxs-lookup"><span data-stu-id="c85e1-289">Silver</span></span> |
| <span data-ttu-id="c85e1-290">2222</span><span class="sxs-lookup"><span data-stu-id="c85e1-290">2222</span></span> |<span data-ttu-id="c85e1-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="c85e1-291">XYZ</span></span> |<span data-ttu-id="c85e1-292">Gold</span><span class="sxs-lookup"><span data-stu-id="c85e1-292">Gold</span></span> |

<span data-ttu-id="c85e1-293">В следующих таблицах представлены виртуальные таблицы, соответствующие исходным массивам в примере.</span><span class="sxs-lookup"><span data-stu-id="c85e1-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="c85e1-294">Каждая из этих таблиц содержит следующее:</span><span class="sxs-lookup"><span data-stu-id="c85e1-294">These tables contain the following:</span></span>

* <span data-ttu-id="c85e1-295">обратную ссылку на исходный ключевой столбец, соответствующий строке исходного массива (с помощью столбца _№);</span><span class="sxs-lookup"><span data-stu-id="c85e1-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="c85e1-296">указание на позицию данных в исходном массиве;</span><span class="sxs-lookup"><span data-stu-id="c85e1-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="c85e1-297">развернутые данные для каждого элемента в массиве.</span><span class="sxs-lookup"><span data-stu-id="c85e1-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="c85e1-298">Таблица ExampleTable_Invoices:</span><span class="sxs-lookup"><span data-stu-id="c85e1-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="c85e1-299">_№</span><span class="sxs-lookup"><span data-stu-id="c85e1-299">_id</span></span> | <span data-ttu-id="c85e1-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="c85e1-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="c85e1-301">счет_№</span><span class="sxs-lookup"><span data-stu-id="c85e1-301">invoice_id</span></span> | <span data-ttu-id="c85e1-302">item</span><span class="sxs-lookup"><span data-stu-id="c85e1-302">item</span></span> | <span data-ttu-id="c85e1-303">price</span><span class="sxs-lookup"><span data-stu-id="c85e1-303">price</span></span> | <span data-ttu-id="c85e1-304">Скидка</span><span class="sxs-lookup"><span data-stu-id="c85e1-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c85e1-305">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-305">1111</span></span> |<span data-ttu-id="c85e1-306">0</span><span class="sxs-lookup"><span data-stu-id="c85e1-306">0</span></span> |<span data-ttu-id="c85e1-307">123</span><span class="sxs-lookup"><span data-stu-id="c85e1-307">123</span></span> |<span data-ttu-id="c85e1-308">тостер</span><span class="sxs-lookup"><span data-stu-id="c85e1-308">toaster</span></span> |<span data-ttu-id="c85e1-309">456</span><span class="sxs-lookup"><span data-stu-id="c85e1-309">456</span></span> |<span data-ttu-id="c85e1-310">0,2</span><span class="sxs-lookup"><span data-stu-id="c85e1-310">0.2</span></span> |
| <span data-ttu-id="c85e1-311">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-311">1111</span></span> |<span data-ttu-id="c85e1-312">1</span><span class="sxs-lookup"><span data-stu-id="c85e1-312">1</span></span> |<span data-ttu-id="c85e1-313">124</span><span class="sxs-lookup"><span data-stu-id="c85e1-313">124</span></span> |<span data-ttu-id="c85e1-314">печь</span><span class="sxs-lookup"><span data-stu-id="c85e1-314">oven</span></span> |<span data-ttu-id="c85e1-315">1235</span><span class="sxs-lookup"><span data-stu-id="c85e1-315">1235</span></span> |<span data-ttu-id="c85e1-316">0,2</span><span class="sxs-lookup"><span data-stu-id="c85e1-316">0.2</span></span> |
| <span data-ttu-id="c85e1-317">2222</span><span class="sxs-lookup"><span data-stu-id="c85e1-317">2222</span></span> |<span data-ttu-id="c85e1-318">0</span><span class="sxs-lookup"><span data-stu-id="c85e1-318">0</span></span> |<span data-ttu-id="c85e1-319">135</span><span class="sxs-lookup"><span data-stu-id="c85e1-319">135</span></span> |<span data-ttu-id="c85e1-320">холодильник</span><span class="sxs-lookup"><span data-stu-id="c85e1-320">fridge</span></span> |<span data-ttu-id="c85e1-321">12543</span><span class="sxs-lookup"><span data-stu-id="c85e1-321">12543</span></span> |<span data-ttu-id="c85e1-322">0,0</span><span class="sxs-lookup"><span data-stu-id="c85e1-322">0.0</span></span> |

<span data-ttu-id="c85e1-323">Таблица ExampleTable_Ratings:</span><span class="sxs-lookup"><span data-stu-id="c85e1-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="c85e1-324">_№</span><span class="sxs-lookup"><span data-stu-id="c85e1-324">_id</span></span> | <span data-ttu-id="c85e1-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="c85e1-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="c85e1-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="c85e1-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c85e1-327">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-327">1111</span></span> |<span data-ttu-id="c85e1-328">0</span><span class="sxs-lookup"><span data-stu-id="c85e1-328">0</span></span> |<span data-ttu-id="c85e1-329">5</span><span class="sxs-lookup"><span data-stu-id="c85e1-329">5</span></span> |
| <span data-ttu-id="c85e1-330">1111</span><span class="sxs-lookup"><span data-stu-id="c85e1-330">1111</span></span> |<span data-ttu-id="c85e1-331">1</span><span class="sxs-lookup"><span data-stu-id="c85e1-331">1</span></span> |<span data-ttu-id="c85e1-332">6</span><span class="sxs-lookup"><span data-stu-id="c85e1-332">6</span></span> |
| <span data-ttu-id="c85e1-333">2222</span><span class="sxs-lookup"><span data-stu-id="c85e1-333">2222</span></span> |<span data-ttu-id="c85e1-334">0</span><span class="sxs-lookup"><span data-stu-id="c85e1-334">0</span></span> |<span data-ttu-id="c85e1-335">1</span><span class="sxs-lookup"><span data-stu-id="c85e1-335">1</span></span> |
| <span data-ttu-id="c85e1-336">2222</span><span class="sxs-lookup"><span data-stu-id="c85e1-336">2222</span></span> |<span data-ttu-id="c85e1-337">1</span><span class="sxs-lookup"><span data-stu-id="c85e1-337">1</span></span> |<span data-ttu-id="c85e1-338">2</span><span class="sxs-lookup"><span data-stu-id="c85e1-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c85e1-339">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="c85e1-339">Map source to sink columns</span></span>
<span data-ttu-id="c85e1-340">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c85e1-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c85e1-341">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="c85e1-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="c85e1-342">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="c85e1-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c85e1-343">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="c85e1-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c85e1-344">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="c85e1-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c85e1-345">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="c85e1-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c85e1-346">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c85e1-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c85e1-347">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="c85e1-347">Performance and Tuning</span></span>
<span data-ttu-id="c85e1-348">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="c85e1-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c85e1-349">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c85e1-349">Next Steps</span></span>
<span data-ttu-id="c85e1-350">Ознакомьтесь со статьей [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md), в которой представлены пошаговые инструкции по созданию конвейера данных, который перемещает данные из локального хранилища в хранилище данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c85e1-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
