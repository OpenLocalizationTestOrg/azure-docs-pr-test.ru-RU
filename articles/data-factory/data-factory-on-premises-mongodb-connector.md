---
title: "aaaMove данных с помощью фабрики данных MongoDB | Документы Microsoft"
description: "Узнайте, как базы данных MongoDB toomove данные с помощью фабрики данных Azure."
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="bd636-103">Перемещение данных из MongoDB с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="bd636-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="bd636-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd636-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="bd636-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="bd636-106">Можно скопировать данные из локальной MongoDB хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="bd636-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="bd636-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="bd636-108">Фабрика данных в настоящее время поддерживает только при перемещении данных MongoDB хранения tooother хранилищ данных, но не для перемещения данных из хранилища данных MongoDB хранилищ tooan других данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bd636-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bd636-109">Prerequisites</span></span>
<span data-ttu-id="bd636-110">Для hello фабрики данных Azure toobe может tooconnect tooyour локальной MongoDB базы данных службы необходимо установить следующие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="bd636-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="bd636-111">Поддерживаемые версии MongoDB: 2.4, 2.6, 3.0 и 3.2.</span><span class="sxs-lookup"><span data-stu-id="bd636-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="bd636-112">Шлюз управления данными на hello компьютере hello узлов базы данных или на отдельный компьютер tooavoid, конкурирующие за ресурсы с базой данных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="bd636-113">Шлюз управления данными — это программное обеспечение, который подключается образом безопасности и управления локальными службами toocloud источники данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="bd636-114">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="bd636-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="bd636-115">В разделе [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello toomove конвейера данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="bd636-116">При установке шлюза hello автоматически устанавливает tooMongoDB tooconnect используется драйвер Microsoft MongoDB ODBC.</span><span class="sxs-lookup"><span data-stu-id="bd636-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd636-117">Необходимо toouse hello шлюза tooconnect tooMongoDB, даже если она размещается в виртуальных машинах IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="bd636-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="bd636-118">Если вы пытаетесь экземпляр tooan tooconnect MongoDB, размещенной в облаке, также можно устанавливать экземпляр шлюза hello на hello ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="bd636-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd636-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="bd636-119">Getting started</span></span>
<span data-ttu-id="bd636-120">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных MongoDB, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="bd636-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="bd636-121">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="bd636-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="bd636-122">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="bd636-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="bd636-123">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="bd636-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bd636-124">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="bd636-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="bd636-125">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="bd636-126">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="bd636-127">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="bd636-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="bd636-128">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="bd636-129">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="bd636-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="bd636-130">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="bd636-131">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных MongoDB см [пример JSON: копирования данных из tooAzure MongoDB больших двоичных объектов](#json-example-copy-data-from-mongodb-to-azure-blob) данной статьи.</span><span class="sxs-lookup"><span data-stu-id="bd636-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="bd636-132">Hello в следующих разделах содержатся сведения о свойствах JSON, которые являются источником tooMongoDB определенных сущностей фабрики данных используется toodefine:</span><span class="sxs-lookup"><span data-stu-id="bd636-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bd636-133">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="bd636-133">Linked service properties</span></span>
<span data-ttu-id="bd636-134">Hello Следующая таблица содержит описание для конкретных элементов JSON слишком**OnPremisesMongoDB** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="bd636-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="bd636-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="bd636-135">Property</span></span> | <span data-ttu-id="bd636-136">Описание</span><span class="sxs-lookup"><span data-stu-id="bd636-136">Description</span></span> | <span data-ttu-id="bd636-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bd636-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd636-138">type</span><span class="sxs-lookup"><span data-stu-id="bd636-138">type</span></span> |<span data-ttu-id="bd636-139">свойство типа Hello должно быть присвоено: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="bd636-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="bd636-140">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-140">Yes</span></span> |
| <span data-ttu-id="bd636-141">server</span><span class="sxs-lookup"><span data-stu-id="bd636-141">server</span></span> |<span data-ttu-id="bd636-142">IP-адрес или имя сервера hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd636-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="bd636-143">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-143">Yes</span></span> |
| <span data-ttu-id="bd636-144">порт</span><span class="sxs-lookup"><span data-stu-id="bd636-144">port</span></span> |<span data-ttu-id="bd636-145">TCP-порт, который hello MongoDB server использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="bd636-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="bd636-146">Значение по умолчанию — 27017 (необязательно)</span><span class="sxs-lookup"><span data-stu-id="bd636-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="bd636-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="bd636-147">authenticationType</span></span> |<span data-ttu-id="bd636-148">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="bd636-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="bd636-149">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-149">Yes</span></span> |
| <span data-ttu-id="bd636-150">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="bd636-150">username</span></span> |<span data-ttu-id="bd636-151">Учетная запись пользователя, tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd636-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="bd636-152">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="bd636-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="bd636-153">пароль</span><span class="sxs-lookup"><span data-stu-id="bd636-153">password</span></span> |<span data-ttu-id="bd636-154">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-154">Password for hello user.</span></span> |<span data-ttu-id="bd636-155">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="bd636-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="bd636-156">authSource</span><span class="sxs-lookup"><span data-stu-id="bd636-156">authSource</span></span> |<span data-ttu-id="bd636-157">Имя базы данных MongoDB hello, что требуется toouse toocheck учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bd636-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="bd636-158">Необязательно (если используется обычная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="bd636-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="bd636-159">по умолчанию: используется учетная запись администратора hello и hello базы данных, указанный с помощью свойства databaseName.</span><span class="sxs-lookup"><span data-stu-id="bd636-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="bd636-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="bd636-160">databaseName</span></span> |<span data-ttu-id="bd636-161">Имя базы данных MongoDB hello, которое следует tooaccess.</span><span class="sxs-lookup"><span data-stu-id="bd636-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="bd636-162">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-162">Yes</span></span> |
| <span data-ttu-id="bd636-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="bd636-163">gatewayName</span></span> |<span data-ttu-id="bd636-164">Имя шлюза hello, который обращается к хранилищу данных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="bd636-165">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-165">Yes</span></span> |
| <span data-ttu-id="bd636-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="bd636-166">encryptedCredential</span></span> |<span data-ttu-id="bd636-167">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="bd636-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="bd636-168">Необязательно</span><span class="sxs-lookup"><span data-stu-id="bd636-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="bd636-169">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="bd636-169">Dataset properties</span></span>
<span data-ttu-id="bd636-170">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="bd636-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bd636-171">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="bd636-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bd636-172">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="bd636-173">Hello typeProperties статьи для набора данных типа **MongoDbCollection** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="bd636-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="bd636-174">Свойство</span><span class="sxs-lookup"><span data-stu-id="bd636-174">Property</span></span> | <span data-ttu-id="bd636-175">Описание</span><span class="sxs-lookup"><span data-stu-id="bd636-175">Description</span></span> | <span data-ttu-id="bd636-176">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bd636-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd636-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="bd636-177">collectionName</span></span> |<span data-ttu-id="bd636-178">Имя коллекции hello базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd636-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="bd636-179">Да</span><span class="sxs-lookup"><span data-stu-id="bd636-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bd636-180">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="bd636-180">Copy activity properties</span></span>
<span data-ttu-id="bd636-181">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="bd636-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bd636-182">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="bd636-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="bd636-183">Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="bd636-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="bd636-184">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="bd636-185">Если источник hello имеет тип **MongoDbSource** hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="bd636-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="bd636-186">Свойство</span><span class="sxs-lookup"><span data-stu-id="bd636-186">Property</span></span> | <span data-ttu-id="bd636-187">Описание</span><span class="sxs-lookup"><span data-stu-id="bd636-187">Description</span></span> | <span data-ttu-id="bd636-188">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="bd636-188">Allowed values</span></span> | <span data-ttu-id="bd636-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="bd636-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd636-190">query</span><span class="sxs-lookup"><span data-stu-id="bd636-190">query</span></span> |<span data-ttu-id="bd636-191">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="bd636-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="bd636-192">Строка запроса SQL-92.</span><span class="sxs-lookup"><span data-stu-id="bd636-192">SQL-92 query string.</span></span> <span data-ttu-id="bd636-193">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="bd636-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="bd636-194">Нет (если для свойства **collectionName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="bd636-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="bd636-195">Пример JSON: копирование данных из tooAzure MongoDB больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="bd636-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="bd636-196">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd636-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bd636-197">Здесь показано, как данные toocopy из tooan MongoDB локального хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="bd636-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="bd636-198">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="bd636-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="bd636-199">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="bd636-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="bd636-200">Связанная служба типа [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd636-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd636-201">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd636-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd636-202">Входной [набор данных](data-factory-create-datasets.md) типа [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd636-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="bd636-203">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd636-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bd636-204">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [MongoDbSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bd636-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bd636-205">Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных MongoDB каждый час.</span><span class="sxs-lookup"><span data-stu-id="bd636-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="bd636-206">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bd636-207">В качестве первого шага установки шлюза управления данными hello согласно инструкциям hello hello [шлюз управления данными](data-factory-data-management-gateway.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="bd636-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="bd636-208">**Связанная служба MongoDB**</span><span class="sxs-lookup"><span data-stu-id="bd636-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="bd636-209">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="bd636-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="bd636-210">**Входной набор данных MongoDB:** параметра «external»: «true» уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="bd636-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="bd636-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bd636-212">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="bd636-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd636-213">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="bd636-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="bd636-214">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="bd636-215">**Действие копирования в конвейере с MongoDB в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="bd636-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="bd636-216">конвейер Hello содержит операции копирования, настроенные toouse hello выше входные и выходные наборы данных и запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="bd636-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="bd636-217">В определении JSON конвейера hello, hello **источника** тип установлен слишком**MongoDbSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bd636-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="bd636-218">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="bd636-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="bd636-219">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="bd636-219">Schema by Data Factory</span></span>
<span data-ttu-id="bd636-220">Служба фабрики данных Azure выводит схему из коллекции MongoDB с использованием hello 100 последних документов в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="bd636-221">Если эти 100 документы не содержат полную схему, некоторые столбцы могут игнорироваться во время операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="bd636-222">Сопоставление типов для MongoDB</span><span class="sxs-lookup"><span data-stu-id="bd636-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="bd636-223">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="bd636-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="bd636-224">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="bd636-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="bd636-225">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="bd636-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="bd636-226">При перемещении данных tooMongoDB hello следующие сопоставления используются из MongoDB типы too.NET типы.</span><span class="sxs-lookup"><span data-stu-id="bd636-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="bd636-227">Тип MongoDB</span><span class="sxs-lookup"><span data-stu-id="bd636-227">MongoDB type</span></span> | <span data-ttu-id="bd636-228">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="bd636-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="bd636-229">Binary</span><span class="sxs-lookup"><span data-stu-id="bd636-229">Binary</span></span> |<span data-ttu-id="bd636-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="bd636-230">Byte[]</span></span> |
| <span data-ttu-id="bd636-231">Логический</span><span class="sxs-lookup"><span data-stu-id="bd636-231">Boolean</span></span> |<span data-ttu-id="bd636-232">Логический</span><span class="sxs-lookup"><span data-stu-id="bd636-232">Boolean</span></span> |
| <span data-ttu-id="bd636-233">Дата</span><span class="sxs-lookup"><span data-stu-id="bd636-233">Date</span></span> |<span data-ttu-id="bd636-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="bd636-234">DateTime</span></span> |
| <span data-ttu-id="bd636-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="bd636-235">NumberDouble</span></span> |<span data-ttu-id="bd636-236">Double</span><span class="sxs-lookup"><span data-stu-id="bd636-236">Double</span></span> |
| <span data-ttu-id="bd636-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="bd636-237">NumberInt</span></span> |<span data-ttu-id="bd636-238">Int32</span><span class="sxs-lookup"><span data-stu-id="bd636-238">Int32</span></span> |
| <span data-ttu-id="bd636-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="bd636-239">NumberLong</span></span> |<span data-ttu-id="bd636-240">Int64</span><span class="sxs-lookup"><span data-stu-id="bd636-240">Int64</span></span> |
| <span data-ttu-id="bd636-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="bd636-241">ObjectID</span></span> |<span data-ttu-id="bd636-242">Строковый</span><span class="sxs-lookup"><span data-stu-id="bd636-242">String</span></span> |
| <span data-ttu-id="bd636-243">Строковый</span><span class="sxs-lookup"><span data-stu-id="bd636-243">String</span></span> |<span data-ttu-id="bd636-244">Строковый</span><span class="sxs-lookup"><span data-stu-id="bd636-244">String</span></span> |
| <span data-ttu-id="bd636-245">UUID</span><span class="sxs-lookup"><span data-stu-id="bd636-245">UUID</span></span> |<span data-ttu-id="bd636-246">Guid</span><span class="sxs-lookup"><span data-stu-id="bd636-246">Guid</span></span> |
| <span data-ttu-id="bd636-247">Объект</span><span class="sxs-lookup"><span data-stu-id="bd636-247">Object</span></span> |<span data-ttu-id="bd636-248">Преобразованный в плоские столбцы с "_" в качестве вложенного разделителя</span><span class="sxs-lookup"><span data-stu-id="bd636-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="bd636-249">toolearn о поддержке массивов с помощью виртуальной таблицы ссылаться слишком[поддержка сложных типов с помощью виртуальной таблицы](#support-for-complex-types-using-virtual-tables) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="bd636-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="bd636-250">В настоящее время не поддерживаются следующие типы данных MongoDB hello: DBPointer, JavaScript, Max и Min ключа регулярного выражения, символ, Timestamp, не определено</span><span class="sxs-lookup"><span data-stu-id="bd636-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="bd636-251">Поддержка сложных типов с помощью виртуальных таблиц</span><span class="sxs-lookup"><span data-stu-id="bd636-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="bd636-252">Фабрика данных Azure использует встроенные ODBC драйвера tooconnect tooand копирования данных из базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd636-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="bd636-253">Для сложных типов, таких как массивы и объекты с различными типами в документах hello драйвер hello повторно нормализует данных в соответствующей виртуальной таблицы.</span><span class="sxs-lookup"><span data-stu-id="bd636-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="bd636-254">В частности Если таблица содержит такие столбцы, hello драйвер создает следующие виртуальные таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="bd636-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="bd636-255">Объект **базовой таблицы**, который содержит hello и тех же данных как hello Настоящая таблица, за исключением столбцов сложного типа hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="bd636-256">Hello базовая таблица использует hello точно такое же имя в качестве hello реальную таблицу, который он представляет.</span><span class="sxs-lookup"><span data-stu-id="bd636-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="bd636-257">Объект **виртуальную таблицу** для каждого столбца сложный тип, который расширяет hello вложенные данные.</span><span class="sxs-lookup"><span data-stu-id="bd636-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="bd636-258">Виртуальные таблицы Hello именуются hello имя реальную таблицу hello, разделитель «_», имя hello hello массива или объекта.</span><span class="sxs-lookup"><span data-stu-id="bd636-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="bd636-259">Виртуальные таблицы ссылки toohello данные реальном таблицы hello, включение tooaccess драйвер hello hello денормализованные данные.</span><span class="sxs-lookup"><span data-stu-id="bd636-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="bd636-260">Дополнительные сведения см. в разделе "Примеры".</span><span class="sxs-lookup"><span data-stu-id="bd636-260">See Example section below details.</span></span> <span data-ttu-id="bd636-261">Можно открыть содержимое hello MongoDB массивов, запрашивая и соединение таблиц виртуальных hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="bd636-262">Можно использовать hello [мастер копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively представление hello список таблиц в базе данных MongoDB, включая виртуальные таблицы hello и предварительного просмотра данных hello внутри.</span><span class="sxs-lookup"><span data-stu-id="bd636-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="bd636-263">Можно также создать запрос в приветствия мастера копирования и toosee hello результат проверки.</span><span class="sxs-lookup"><span data-stu-id="bd636-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="bd636-264">Пример</span><span class="sxs-lookup"><span data-stu-id="bd636-264">Example</span></span>
<span data-ttu-id="bd636-265">Ниже приведен пример таблицы ExampleTable в базе данных MongoDB, содержащей столбец ("Счета") с массивом объектов в каждой ячейке и столбец с массивом данных скалярных типов ("Оценки").</span><span class="sxs-lookup"><span data-stu-id="bd636-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="bd636-266">_№</span><span class="sxs-lookup"><span data-stu-id="bd636-266">_id</span></span> | <span data-ttu-id="bd636-267">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="bd636-267">Customer Name</span></span> | <span data-ttu-id="bd636-268">Счета</span><span class="sxs-lookup"><span data-stu-id="bd636-268">Invoices</span></span> | <span data-ttu-id="bd636-269">Уровень обслуживания</span><span class="sxs-lookup"><span data-stu-id="bd636-269">Service Level</span></span> | <span data-ttu-id="bd636-270">Оценки</span><span class="sxs-lookup"><span data-stu-id="bd636-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bd636-271">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-271">1111</span></span> |<span data-ttu-id="bd636-272">ABC</span><span class="sxs-lookup"><span data-stu-id="bd636-272">ABC</span></span> |<span data-ttu-id="bd636-273">[{счет_№:"123", товар:"тостер", цена:"456", скидка:"0,2"}, {счет_№:"124", товар:"печь", цена: "1235", скидка: "0,2"}]</span><span class="sxs-lookup"><span data-stu-id="bd636-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="bd636-274">Silver</span><span class="sxs-lookup"><span data-stu-id="bd636-274">Silver</span></span> |<span data-ttu-id="bd636-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="bd636-275">[5,6]</span></span> |
| <span data-ttu-id="bd636-276">2222</span><span class="sxs-lookup"><span data-stu-id="bd636-276">2222</span></span> |<span data-ttu-id="bd636-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="bd636-277">XYZ</span></span> |<span data-ttu-id="bd636-278">[{счет_№: "135", товар: "холодильник", цена: "12543", скидка: "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="bd636-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="bd636-279">Gold</span><span class="sxs-lookup"><span data-stu-id="bd636-279">Gold</span></span> |<span data-ttu-id="bd636-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="bd636-280">[1,2]</span></span> |

<span data-ttu-id="bd636-281">драйвер Hello, создает несколько toorepresent виртуальные таблицы этой таблице.</span><span class="sxs-lookup"><span data-stu-id="bd636-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="bd636-282">первая виртуальная таблица Hello — hello базовой таблицы с именем «ExampleTable», показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bd636-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="bd636-283">Hello базовая таблица содержит все данные hello hello исходной таблицы, но hello данных из массивов hello включен и развернуты в виртуальной таблице hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="bd636-284">_№</span><span class="sxs-lookup"><span data-stu-id="bd636-284">_id</span></span> | <span data-ttu-id="bd636-285">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="bd636-285">Customer Name</span></span> | <span data-ttu-id="bd636-286">Уровень обслуживания</span><span class="sxs-lookup"><span data-stu-id="bd636-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd636-287">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-287">1111</span></span> |<span data-ttu-id="bd636-288">ABC</span><span class="sxs-lookup"><span data-stu-id="bd636-288">ABC</span></span> |<span data-ttu-id="bd636-289">Silver</span><span class="sxs-lookup"><span data-stu-id="bd636-289">Silver</span></span> |
| <span data-ttu-id="bd636-290">2222</span><span class="sxs-lookup"><span data-stu-id="bd636-290">2222</span></span> |<span data-ttu-id="bd636-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="bd636-291">XYZ</span></span> |<span data-ttu-id="bd636-292">Gold</span><span class="sxs-lookup"><span data-stu-id="bd636-292">Gold</span></span> |

<span data-ttu-id="bd636-293">Hello следующих таблицах показаны hello виртуальные таблицы, представляющих исходные массивы hello в примере hello.</span><span class="sxs-lookup"><span data-stu-id="bd636-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="bd636-294">Эти таблицы содержат следующие hello:</span><span class="sxs-lookup"><span data-stu-id="bd636-294">These tables contain hello following:</span></span>

* <span data-ttu-id="bd636-295">Обратная ссылка toohello исходный столбец первичного ключа соответствующей toohello строке исходного массива hello (с помощью hello _id столбец)</span><span class="sxs-lookup"><span data-stu-id="bd636-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="bd636-296">Значение, указывающее положение hello hello данных в пределах исходного массива hello</span><span class="sxs-lookup"><span data-stu-id="bd636-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="bd636-297">данные для каждого элемента в массиве hello развернут Hello</span><span class="sxs-lookup"><span data-stu-id="bd636-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="bd636-298">Таблица ExampleTable_Invoices:</span><span class="sxs-lookup"><span data-stu-id="bd636-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="bd636-299">_№</span><span class="sxs-lookup"><span data-stu-id="bd636-299">_id</span></span> | <span data-ttu-id="bd636-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="bd636-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="bd636-301">счет_№</span><span class="sxs-lookup"><span data-stu-id="bd636-301">invoice_id</span></span> | <span data-ttu-id="bd636-302">item</span><span class="sxs-lookup"><span data-stu-id="bd636-302">item</span></span> | <span data-ttu-id="bd636-303">price</span><span class="sxs-lookup"><span data-stu-id="bd636-303">price</span></span> | <span data-ttu-id="bd636-304">Скидка</span><span class="sxs-lookup"><span data-stu-id="bd636-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="bd636-305">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-305">1111</span></span> |<span data-ttu-id="bd636-306">0</span><span class="sxs-lookup"><span data-stu-id="bd636-306">0</span></span> |<span data-ttu-id="bd636-307">123</span><span class="sxs-lookup"><span data-stu-id="bd636-307">123</span></span> |<span data-ttu-id="bd636-308">тостер</span><span class="sxs-lookup"><span data-stu-id="bd636-308">toaster</span></span> |<span data-ttu-id="bd636-309">456</span><span class="sxs-lookup"><span data-stu-id="bd636-309">456</span></span> |<span data-ttu-id="bd636-310">0,2</span><span class="sxs-lookup"><span data-stu-id="bd636-310">0.2</span></span> |
| <span data-ttu-id="bd636-311">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-311">1111</span></span> |<span data-ttu-id="bd636-312">1</span><span class="sxs-lookup"><span data-stu-id="bd636-312">1</span></span> |<span data-ttu-id="bd636-313">124</span><span class="sxs-lookup"><span data-stu-id="bd636-313">124</span></span> |<span data-ttu-id="bd636-314">печь</span><span class="sxs-lookup"><span data-stu-id="bd636-314">oven</span></span> |<span data-ttu-id="bd636-315">1235</span><span class="sxs-lookup"><span data-stu-id="bd636-315">1235</span></span> |<span data-ttu-id="bd636-316">0,2</span><span class="sxs-lookup"><span data-stu-id="bd636-316">0.2</span></span> |
| <span data-ttu-id="bd636-317">2222</span><span class="sxs-lookup"><span data-stu-id="bd636-317">2222</span></span> |<span data-ttu-id="bd636-318">0</span><span class="sxs-lookup"><span data-stu-id="bd636-318">0</span></span> |<span data-ttu-id="bd636-319">135</span><span class="sxs-lookup"><span data-stu-id="bd636-319">135</span></span> |<span data-ttu-id="bd636-320">холодильник</span><span class="sxs-lookup"><span data-stu-id="bd636-320">fridge</span></span> |<span data-ttu-id="bd636-321">12543</span><span class="sxs-lookup"><span data-stu-id="bd636-321">12543</span></span> |<span data-ttu-id="bd636-322">0,0</span><span class="sxs-lookup"><span data-stu-id="bd636-322">0.0</span></span> |

<span data-ttu-id="bd636-323">Таблица ExampleTable_Ratings:</span><span class="sxs-lookup"><span data-stu-id="bd636-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="bd636-324">_№</span><span class="sxs-lookup"><span data-stu-id="bd636-324">_id</span></span> | <span data-ttu-id="bd636-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="bd636-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="bd636-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="bd636-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd636-327">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-327">1111</span></span> |<span data-ttu-id="bd636-328">0</span><span class="sxs-lookup"><span data-stu-id="bd636-328">0</span></span> |<span data-ttu-id="bd636-329">5</span><span class="sxs-lookup"><span data-stu-id="bd636-329">5</span></span> |
| <span data-ttu-id="bd636-330">1111</span><span class="sxs-lookup"><span data-stu-id="bd636-330">1111</span></span> |<span data-ttu-id="bd636-331">1</span><span class="sxs-lookup"><span data-stu-id="bd636-331">1</span></span> |<span data-ttu-id="bd636-332">6</span><span class="sxs-lookup"><span data-stu-id="bd636-332">6</span></span> |
| <span data-ttu-id="bd636-333">2222</span><span class="sxs-lookup"><span data-stu-id="bd636-333">2222</span></span> |<span data-ttu-id="bd636-334">0</span><span class="sxs-lookup"><span data-stu-id="bd636-334">0</span></span> |<span data-ttu-id="bd636-335">1</span><span class="sxs-lookup"><span data-stu-id="bd636-335">1</span></span> |
| <span data-ttu-id="bd636-336">2222</span><span class="sxs-lookup"><span data-stu-id="bd636-336">2222</span></span> |<span data-ttu-id="bd636-337">1</span><span class="sxs-lookup"><span data-stu-id="bd636-337">1</span></span> |<span data-ttu-id="bd636-338">2</span><span class="sxs-lookup"><span data-stu-id="bd636-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="bd636-339">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="bd636-339">Map source toosink columns</span></span>
<span data-ttu-id="bd636-340">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bd636-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="bd636-341">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="bd636-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="bd636-342">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="bd636-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="bd636-343">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="bd636-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="bd636-344">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="bd636-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="bd636-345">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="bd636-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="bd636-346">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="bd636-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bd636-347">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="bd636-347">Performance and Tuning</span></span>
<span data-ttu-id="bd636-348">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="bd636-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd636-349">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd636-349">Next Steps</span></span>
<span data-ttu-id="bd636-350">В разделе [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статью пошаговые инструкции для создания конвейера данных, перемещает данные из локальных данных хранилище tooan данных Azure.</span><span class="sxs-lookup"><span data-stu-id="bd636-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
