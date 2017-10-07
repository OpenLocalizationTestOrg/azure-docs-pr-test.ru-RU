---
title: "aaaMove данные из фабрики данных с помощью Cassandra | Документы Microsoft"
description: "Узнайте, как данные toomove из Cassandra локальной базы данных с помощью фабрики данных Azure."
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
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="72b86-103">Перемещение данных из локальной базы данных Cassandra с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="72b86-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="72b86-104">В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из Cassandra локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="72b86-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="72b86-106">Можно скопировать данные из локальной Cassandra хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="72b86-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="72b86-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="72b86-108">Фабрика данных в настоящее время поддерживает только при перемещении данных из данных Cassandra хранения tooother хранилищ данных, но не для перемещения данных из других данных Cassandra tooa хранилищ данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="72b86-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="72b86-109">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="72b86-109">Supported versions</span></span>
<span data-ttu-id="72b86-110">Hello Cassandra соединитель поддерживает следующие версии Cassandra hello: 2.X.</span><span class="sxs-lookup"><span data-stu-id="72b86-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b86-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="72b86-111">Prerequisites</span></span>
<span data-ttu-id="72b86-112">Для hello фабрики данных Azure toobe может tooconnect tooyour локальной Cassandra базы данных службы, необходимо установить шлюз управления данными на hello же машины, hello размещение базы данных или на отдельном компьютере tooavoid, конкурировать за ресурсы с hello База данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="72b86-113">Шлюз управления данными — это компонент, который подключается образом безопасности и управления локальными службами toocloud источники данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="72b86-114">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="72b86-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="72b86-115">В разделе [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello toomove конвейера данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="72b86-116">Необходимо использовать hello шлюза tooconnect tooa Cassandra базы данных, даже если hello база данных размещается в облаке hello, например, на виртуальной Машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="72b86-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="72b86-117">Y которых имеются hello шлюза на hello одной виртуальной Машины, hello размещение базы данных или на отдельной виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="72b86-118">При установке шлюза hello автоматически устанавливает Microsoft Cassandra ODBC tooconnect драйвер, используемый tooCassandra базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="72b86-119">Таким образом, не требуется toomanually установить любой драйвер на компьютере шлюза hello при копировании данных из базы данных Cassandra hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="72b86-120">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="72b86-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="72b86-121">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="72b86-121">Getting started</span></span>
<span data-ttu-id="72b86-122">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="72b86-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="72b86-123">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="72b86-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="72b86-124">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="72b86-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="72b86-125">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="72b86-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="72b86-126">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="72b86-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="72b86-127">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="72b86-128">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="72b86-129">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="72b86-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="72b86-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="72b86-131">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="72b86-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="72b86-132">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="72b86-133">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных в локальной Cassandra см [пример JSON: копирования данных из Cassandra tooAzure большого двоичного объекта](#json-example-copy-data-from-cassandra-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="72b86-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="72b86-134">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa Cassandra хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="72b86-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="72b86-135">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="72b86-135">Linked service properties</span></span>
<span data-ttu-id="72b86-136">Hello в следующей таблице приводится описание службы конкретных tooCassandra связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="72b86-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="72b86-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="72b86-137">Property</span></span> | <span data-ttu-id="72b86-138">Описание</span><span class="sxs-lookup"><span data-stu-id="72b86-138">Description</span></span> | <span data-ttu-id="72b86-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="72b86-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72b86-140">type</span><span class="sxs-lookup"><span data-stu-id="72b86-140">type</span></span> |<span data-ttu-id="72b86-141">свойство типа Hello должно быть присвоено: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="72b86-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="72b86-142">Да</span><span class="sxs-lookup"><span data-stu-id="72b86-142">Yes</span></span> |
| <span data-ttu-id="72b86-143">host</span><span class="sxs-lookup"><span data-stu-id="72b86-143">host</span></span> |<span data-ttu-id="72b86-144">Один или несколько IP-адресов или имен узлов серверов Cassandra.</span><span class="sxs-lookup"><span data-stu-id="72b86-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="72b86-145">Укажите список разделенных запятой IP-адреса или имена серверов tooall tooconnect одновременно.</span><span class="sxs-lookup"><span data-stu-id="72b86-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="72b86-146">Да</span><span class="sxs-lookup"><span data-stu-id="72b86-146">Yes</span></span> |
| <span data-ttu-id="72b86-147">порт</span><span class="sxs-lookup"><span data-stu-id="72b86-147">port</span></span> |<span data-ttu-id="72b86-148">TCP-порт, который hello Cassandra server Hello использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="72b86-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="72b86-149">Нет. Значение по умолчанию — 9042</span><span class="sxs-lookup"><span data-stu-id="72b86-149">No, default value: 9042</span></span> |
| <span data-ttu-id="72b86-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="72b86-150">authenticationType</span></span> |<span data-ttu-id="72b86-151">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="72b86-151">Basic, or Anonymous</span></span> |<span data-ttu-id="72b86-152">Да</span><span class="sxs-lookup"><span data-stu-id="72b86-152">Yes</span></span> |
| <span data-ttu-id="72b86-153">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="72b86-153">username</span></span> |<span data-ttu-id="72b86-154">Укажите имя пользователя для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="72b86-155">Да, если tooBasic authenticationType.</span><span class="sxs-lookup"><span data-stu-id="72b86-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="72b86-156">пароль</span><span class="sxs-lookup"><span data-stu-id="72b86-156">password</span></span> |<span data-ttu-id="72b86-157">Укажите пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-157">Specify password for hello user account.</span></span> |<span data-ttu-id="72b86-158">Да, если tooBasic authenticationType.</span><span class="sxs-lookup"><span data-stu-id="72b86-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="72b86-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="72b86-159">gatewayName</span></span> |<span data-ttu-id="72b86-160">имя шлюза hello, используемые tooconnect toohello Hello локальной Cassandra базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="72b86-161">Да</span><span class="sxs-lookup"><span data-stu-id="72b86-161">Yes</span></span> |
| <span data-ttu-id="72b86-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="72b86-162">encryptedCredential</span></span> |<span data-ttu-id="72b86-163">Учетные данные, зашифрованные шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="72b86-164">Нет</span><span class="sxs-lookup"><span data-stu-id="72b86-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="72b86-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="72b86-165">Dataset properties</span></span>
<span data-ttu-id="72b86-166">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="72b86-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="72b86-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="72b86-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="72b86-168">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="72b86-169">Hello typeProperties статьи для набора данных типа **CassandraTable** имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="72b86-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="72b86-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="72b86-170">Property</span></span> | <span data-ttu-id="72b86-171">Описание</span><span class="sxs-lookup"><span data-stu-id="72b86-171">Description</span></span> | <span data-ttu-id="72b86-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="72b86-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72b86-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="72b86-173">keyspace</span></span> |<span data-ttu-id="72b86-174">Имя hello пространство ключей или схемы в базе данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="72b86-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="72b86-175">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="72b86-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="72b86-176">tableName</span><span class="sxs-lookup"><span data-stu-id="72b86-176">tableName</span></span> |<span data-ttu-id="72b86-177">Имя таблицы hello Cassandra базы данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="72b86-178">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="72b86-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="72b86-179">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="72b86-179">Copy activity properties</span></span>
<span data-ttu-id="72b86-180">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="72b86-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="72b86-181">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="72b86-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="72b86-182">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="72b86-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="72b86-183">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="72b86-184">Если источник имеет тип **CassandraSource**, hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="72b86-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="72b86-185">Свойство</span><span class="sxs-lookup"><span data-stu-id="72b86-185">Property</span></span> | <span data-ttu-id="72b86-186">Описание</span><span class="sxs-lookup"><span data-stu-id="72b86-186">Description</span></span> | <span data-ttu-id="72b86-187">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="72b86-187">Allowed values</span></span> | <span data-ttu-id="72b86-188">Обязательно</span><span class="sxs-lookup"><span data-stu-id="72b86-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72b86-189">query</span><span class="sxs-lookup"><span data-stu-id="72b86-189">query</span></span> |<span data-ttu-id="72b86-190">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="72b86-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="72b86-191">Запрос SQL-92 или CQL.</span><span class="sxs-lookup"><span data-stu-id="72b86-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="72b86-192">Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="72b86-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="72b86-193">При использовании SQL-запрос, укажите **keyspace name.table имя** toorepresent hello таблицу tooquery.</span><span class="sxs-lookup"><span data-stu-id="72b86-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="72b86-194">Нет (если в наборе данных определены свойства tableName и keyspace)</span><span class="sxs-lookup"><span data-stu-id="72b86-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="72b86-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="72b86-195">consistencyLevel</span></span> |<span data-ttu-id="72b86-196">уровень согласованности Hello указывает, сколько реплик должен вернуть запрос чтения tooa до возвращения данных toohello клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="72b86-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="72b86-197">Проверяет Cassandra hello указанное число реплик, для запроса на чтение данных toosatisfy hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="72b86-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="72b86-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="72b86-199">Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных).</span><span class="sxs-lookup"><span data-stu-id="72b86-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="72b86-200">Нет.</span><span class="sxs-lookup"><span data-stu-id="72b86-200">No.</span></span> <span data-ttu-id="72b86-201">Значение по умолчанию — ONE</span><span class="sxs-lookup"><span data-stu-id="72b86-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="72b86-202">Пример JSON: копирование данных из Cassandra tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="72b86-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="72b86-203">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="72b86-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="72b86-204">В нем показано, как данные toocopy из Cassandra локальной базы данных tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="72b86-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="72b86-205">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="72b86-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72b86-206">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="72b86-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="72b86-207">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="72b86-208">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="72b86-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="72b86-209">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="72b86-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="72b86-210">Связанная служба типа [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="72b86-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="72b86-211">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="72b86-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="72b86-212">Входной [набор данных](data-factory-create-datasets.md) типа [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="72b86-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="72b86-213">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="72b86-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="72b86-214">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [CassandraSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="72b86-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="72b86-215">**Связанная служба Cassandra**</span><span class="sxs-lookup"><span data-stu-id="72b86-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="72b86-216">В этом примере используется hello **Cassandra** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="72b86-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="72b86-217">В разделе [Cassandra связанная служба](#linked-service-properties) раздел для hello свойства, поддерживаемые этой связанной службы.</span><span class="sxs-lookup"><span data-stu-id="72b86-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

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

<span data-ttu-id="72b86-218">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="72b86-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="72b86-219">**Входной набор данных Cassandra**</span><span class="sxs-lookup"><span data-stu-id="72b86-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="72b86-220">Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="72b86-221">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="72b86-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="72b86-222">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="72b86-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="72b86-223">**Действие копирования в конвейере с базой данных Cassandra в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="72b86-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="72b86-224">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="72b86-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="72b86-225">В определении JSON конвейера hello, hello **источника** тип установлен слишком**CassandraSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="72b86-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="72b86-226">В разделе [свойства типа RelationalSource](#copy-activity-properties) список свойств, поддерживаемых hello RelationalSource hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Cassandra tooan Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="72b86-227">Сопоставление типов для Cassandra</span><span class="sxs-lookup"><span data-stu-id="72b86-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="72b86-228">Тип данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="72b86-228">Cassandra Type</span></span> | <span data-ttu-id="72b86-229">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="72b86-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="72b86-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="72b86-230">ASCII</span></span> |<span data-ttu-id="72b86-231">Строка</span><span class="sxs-lookup"><span data-stu-id="72b86-231">String</span></span> |
| <span data-ttu-id="72b86-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="72b86-232">BIGINT</span></span> |<span data-ttu-id="72b86-233">Int64</span><span class="sxs-lookup"><span data-stu-id="72b86-233">Int64</span></span> |
| <span data-ttu-id="72b86-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="72b86-234">BLOB</span></span> |<span data-ttu-id="72b86-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="72b86-235">Byte[]</span></span> |
| <span data-ttu-id="72b86-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="72b86-236">BOOLEAN</span></span> |<span data-ttu-id="72b86-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="72b86-237">Boolean</span></span> |
| <span data-ttu-id="72b86-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="72b86-238">DECIMAL</span></span> |<span data-ttu-id="72b86-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="72b86-239">Decimal</span></span> |
| <span data-ttu-id="72b86-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="72b86-240">DOUBLE</span></span> |<span data-ttu-id="72b86-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="72b86-241">Double</span></span> |
| <span data-ttu-id="72b86-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="72b86-242">FLOAT</span></span> |<span data-ttu-id="72b86-243">Single</span><span class="sxs-lookup"><span data-stu-id="72b86-243">Single</span></span> |
| <span data-ttu-id="72b86-244">INET</span><span class="sxs-lookup"><span data-stu-id="72b86-244">INET</span></span> |<span data-ttu-id="72b86-245">Строка</span><span class="sxs-lookup"><span data-stu-id="72b86-245">String</span></span> |
| <span data-ttu-id="72b86-246">INT</span><span class="sxs-lookup"><span data-stu-id="72b86-246">INT</span></span> |<span data-ttu-id="72b86-247">Int32</span><span class="sxs-lookup"><span data-stu-id="72b86-247">Int32</span></span> |
| <span data-ttu-id="72b86-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="72b86-248">TEXT</span></span> |<span data-ttu-id="72b86-249">Строка</span><span class="sxs-lookup"><span data-stu-id="72b86-249">String</span></span> |
| <span data-ttu-id="72b86-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="72b86-250">TIMESTAMP</span></span> |<span data-ttu-id="72b86-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="72b86-251">DateTime</span></span> |
| <span data-ttu-id="72b86-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="72b86-252">TIMEUUID</span></span> |<span data-ttu-id="72b86-253">Guid</span><span class="sxs-lookup"><span data-stu-id="72b86-253">Guid</span></span> |
| <span data-ttu-id="72b86-254">UUID</span><span class="sxs-lookup"><span data-stu-id="72b86-254">UUID</span></span> |<span data-ttu-id="72b86-255">Guid</span><span class="sxs-lookup"><span data-stu-id="72b86-255">Guid</span></span> |
| <span data-ttu-id="72b86-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="72b86-256">VARCHAR</span></span> |<span data-ttu-id="72b86-257">Строка</span><span class="sxs-lookup"><span data-stu-id="72b86-257">String</span></span> |
| <span data-ttu-id="72b86-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="72b86-258">VARINT</span></span> |<span data-ttu-id="72b86-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="72b86-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="72b86-260">Коллекция типов (карты, набор, список, т. д.), см. в разделе слишком[работать с Cassandra типов коллекций, с помощью виртуальной таблицы](#work-with-collections-using-virtual-table) раздела.</span><span class="sxs-lookup"><span data-stu-id="72b86-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="72b86-261">Пользовательские типы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="72b86-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="72b86-262">Длина Hello длины двоичного столбца и строки столбцов не может превышать 4000.</span><span class="sxs-lookup"><span data-stu-id="72b86-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="72b86-263">Работа с коллекциями с использованием виртуальной таблицы</span><span class="sxs-lookup"><span data-stu-id="72b86-263">Work with collections using virtual table</span></span>
<span data-ttu-id="72b86-264">Фабрика данных Azure использует встроенные ODBC драйвера tooconnect tooand копирования данных из базы данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="72b86-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="72b86-265">Для типов коллекций, включая карты, набор и список драйвер hello сопряженный hello данных в соответствующей виртуальной таблицы.</span><span class="sxs-lookup"><span data-stu-id="72b86-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="72b86-266">В частности Если таблица содержит коллекцию столбцов, hello драйвер создает следующие виртуальные таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="72b86-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="72b86-267">Объект **базовой таблицы**, который содержит hello и тех же данных как hello реальную таблицу за исключением hello коллекции столбцов.</span><span class="sxs-lookup"><span data-stu-id="72b86-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="72b86-268">Hello базовая таблица использует hello точно такое же имя в качестве hello реальную таблицу, который он представляет.</span><span class="sxs-lookup"><span data-stu-id="72b86-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="72b86-269">Объект **виртуальную таблицу** для каждого столбца в коллекции, который расширяет hello вложенные данные.</span><span class="sxs-lookup"><span data-stu-id="72b86-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="72b86-270">Hello виртуальные таблицы, которые представляют собой коллекции именуются с использованием имени hello hello реальную таблицу с разделителем "*vt*» и hello имя столбца hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="72b86-271">Виртуальные таблицы ссылки toohello данные реальном таблицы hello, включение tooaccess драйвер hello hello денормализованные данные.</span><span class="sxs-lookup"><span data-stu-id="72b86-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="72b86-272">Дополнительные сведения см. в разделе "Пример".</span><span class="sxs-lookup"><span data-stu-id="72b86-272">See Example section for details.</span></span> <span data-ttu-id="72b86-273">Можно получить доступ к hello содержимое коллекций Cassandra, запрашивая и соединение таблиц виртуальных hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="72b86-274">Можно использовать hello [мастер копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively представление hello список таблиц в базе данных Cassandra, включая виртуальные таблицы hello и предварительного просмотра данных hello внутри.</span><span class="sxs-lookup"><span data-stu-id="72b86-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="72b86-275">Можно также создать запрос в приветствия мастера копирования и toosee hello результат проверки.</span><span class="sxs-lookup"><span data-stu-id="72b86-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="72b86-276">Пример</span><span class="sxs-lookup"><span data-stu-id="72b86-276">Example</span></span>
<span data-ttu-id="72b86-277">Например hello следующие «ExampleTable» является Cassandra таблицу базы данных, содержащую целочисленный столбец первичного ключа с именем «pk_int», текстовый столбец с именем value, столбца списка, столбец карты и представляющий собой набор столбцов (с именем «StringSet»).</span><span class="sxs-lookup"><span data-stu-id="72b86-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="72b86-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="72b86-278">pk_int</span></span> | <span data-ttu-id="72b86-279">Значение</span><span class="sxs-lookup"><span data-stu-id="72b86-279">Value</span></span> | <span data-ttu-id="72b86-280">список</span><span class="sxs-lookup"><span data-stu-id="72b86-280">List</span></span> | <span data-ttu-id="72b86-281">Сопоставление</span><span class="sxs-lookup"><span data-stu-id="72b86-281">Map</span></span> | <span data-ttu-id="72b86-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="72b86-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="72b86-283">1</span><span class="sxs-lookup"><span data-stu-id="72b86-283">1</span></span> |<span data-ttu-id="72b86-284">"пример значения 1"</span><span class="sxs-lookup"><span data-stu-id="72b86-284">"sample value 1"</span></span> |<span data-ttu-id="72b86-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="72b86-285">["1", "2", "3"]</span></span> |<span data-ttu-id="72b86-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="72b86-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="72b86-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="72b86-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="72b86-288">3</span><span class="sxs-lookup"><span data-stu-id="72b86-288">3</span></span> |<span data-ttu-id="72b86-289">"пример значения 3"</span><span class="sxs-lookup"><span data-stu-id="72b86-289">"sample value 3"</span></span> |<span data-ttu-id="72b86-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="72b86-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="72b86-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="72b86-291">{"S1": "t"}</span></span> |<span data-ttu-id="72b86-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="72b86-292">{"A", "E"}</span></span> |

<span data-ttu-id="72b86-293">драйвер Hello, создает несколько toorepresent виртуальные таблицы этой таблице.</span><span class="sxs-lookup"><span data-stu-id="72b86-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="72b86-294">Hello столбцы внешних ключей в таблицах виртуального hello ссылаться hello столбцы первичного ключа в таблице реальные hello и указать, какие реального соответствует таблице строки hello виртуальную таблицу, в строке.</span><span class="sxs-lookup"><span data-stu-id="72b86-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="72b86-295">первая виртуальная таблица Hello — hello базовой таблицы с именем «ExampleTable» отображается в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="72b86-296">Hello базовая таблица содержит hello и тех же данных как hello исходной таблицы базы данных, за исключением hello коллекции, которые исключаются из этой таблицы, которые развернуты в других виртуальные таблицы.</span><span class="sxs-lookup"><span data-stu-id="72b86-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="72b86-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="72b86-297">pk_int</span></span> | <span data-ttu-id="72b86-298">Значение</span><span class="sxs-lookup"><span data-stu-id="72b86-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="72b86-299">1</span><span class="sxs-lookup"><span data-stu-id="72b86-299">1</span></span> |<span data-ttu-id="72b86-300">"пример значения 1"</span><span class="sxs-lookup"><span data-stu-id="72b86-300">"sample value 1"</span></span> |
| <span data-ttu-id="72b86-301">3</span><span class="sxs-lookup"><span data-stu-id="72b86-301">3</span></span> |<span data-ttu-id="72b86-302">"пример значения 3"</span><span class="sxs-lookup"><span data-stu-id="72b86-302">"sample value 3"</span></span> |

<span data-ttu-id="72b86-303">Hello следующих таблицах показаны hello виртуальные таблицы, которые renormalize hello данные из столбцов списка, карты и StringSet hello.</span><span class="sxs-lookup"><span data-stu-id="72b86-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="72b86-304">Hello столбцы с именами, которые заканчиваются на «_index» или «сер_вера» укажите позицию hello hello данные в исходном списке hello или карты.</span><span class="sxs-lookup"><span data-stu-id="72b86-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="72b86-305">Hello столбцы с именами, которые заканчиваются на «_value» содержат данные hello развернут hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="72b86-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="72b86-306">Таблица ExampleTable_vt_List</span><span class="sxs-lookup"><span data-stu-id="72b86-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="72b86-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="72b86-307">pk_int</span></span> | <span data-ttu-id="72b86-308">List_index</span><span class="sxs-lookup"><span data-stu-id="72b86-308">List_index</span></span> | <span data-ttu-id="72b86-309">List_value</span><span class="sxs-lookup"><span data-stu-id="72b86-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72b86-310">1</span><span class="sxs-lookup"><span data-stu-id="72b86-310">1</span></span> |<span data-ttu-id="72b86-311">0</span><span class="sxs-lookup"><span data-stu-id="72b86-311">0</span></span> |<span data-ttu-id="72b86-312">1</span><span class="sxs-lookup"><span data-stu-id="72b86-312">1</span></span> |
| <span data-ttu-id="72b86-313">1</span><span class="sxs-lookup"><span data-stu-id="72b86-313">1</span></span> |<span data-ttu-id="72b86-314">1</span><span class="sxs-lookup"><span data-stu-id="72b86-314">1</span></span> |<span data-ttu-id="72b86-315">2</span><span class="sxs-lookup"><span data-stu-id="72b86-315">2</span></span> |
| <span data-ttu-id="72b86-316">1</span><span class="sxs-lookup"><span data-stu-id="72b86-316">1</span></span> |<span data-ttu-id="72b86-317">2</span><span class="sxs-lookup"><span data-stu-id="72b86-317">2</span></span> |<span data-ttu-id="72b86-318">3</span><span class="sxs-lookup"><span data-stu-id="72b86-318">3</span></span> |
| <span data-ttu-id="72b86-319">3</span><span class="sxs-lookup"><span data-stu-id="72b86-319">3</span></span> |<span data-ttu-id="72b86-320">0</span><span class="sxs-lookup"><span data-stu-id="72b86-320">0</span></span> |<span data-ttu-id="72b86-321">100</span><span class="sxs-lookup"><span data-stu-id="72b86-321">100</span></span> |
| <span data-ttu-id="72b86-322">3</span><span class="sxs-lookup"><span data-stu-id="72b86-322">3</span></span> |<span data-ttu-id="72b86-323">1</span><span class="sxs-lookup"><span data-stu-id="72b86-323">1</span></span> |<span data-ttu-id="72b86-324">101</span><span class="sxs-lookup"><span data-stu-id="72b86-324">101</span></span> |
| <span data-ttu-id="72b86-325">3</span><span class="sxs-lookup"><span data-stu-id="72b86-325">3</span></span> |<span data-ttu-id="72b86-326">2</span><span class="sxs-lookup"><span data-stu-id="72b86-326">2</span></span> |<span data-ttu-id="72b86-327">102</span><span class="sxs-lookup"><span data-stu-id="72b86-327">102</span></span> |
| <span data-ttu-id="72b86-328">3</span><span class="sxs-lookup"><span data-stu-id="72b86-328">3</span></span> |<span data-ttu-id="72b86-329">3</span><span class="sxs-lookup"><span data-stu-id="72b86-329">3</span></span> |<span data-ttu-id="72b86-330">103</span><span class="sxs-lookup"><span data-stu-id="72b86-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="72b86-331">Таблица ExampleTable_vt_Map</span><span class="sxs-lookup"><span data-stu-id="72b86-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="72b86-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="72b86-332">pk_int</span></span> | <span data-ttu-id="72b86-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="72b86-333">Map_key</span></span> | <span data-ttu-id="72b86-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="72b86-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72b86-335">1</span><span class="sxs-lookup"><span data-stu-id="72b86-335">1</span></span> |<span data-ttu-id="72b86-336">S1</span><span class="sxs-lookup"><span data-stu-id="72b86-336">S1</span></span> |<span data-ttu-id="72b86-337">Файл ,</span><span class="sxs-lookup"><span data-stu-id="72b86-337">A</span></span> |
| <span data-ttu-id="72b86-338">1</span><span class="sxs-lookup"><span data-stu-id="72b86-338">1</span></span> |<span data-ttu-id="72b86-339">S2</span><span class="sxs-lookup"><span data-stu-id="72b86-339">S2</span></span> |<span data-ttu-id="72b86-340">b</span><span class="sxs-lookup"><span data-stu-id="72b86-340">b</span></span> |
| <span data-ttu-id="72b86-341">3</span><span class="sxs-lookup"><span data-stu-id="72b86-341">3</span></span> |<span data-ttu-id="72b86-342">S1</span><span class="sxs-lookup"><span data-stu-id="72b86-342">S1</span></span> |<span data-ttu-id="72b86-343">t</span><span class="sxs-lookup"><span data-stu-id="72b86-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="72b86-344">Таблица ExampleTable_vt_StringSet:</span><span class="sxs-lookup"><span data-stu-id="72b86-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="72b86-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="72b86-345">pk_int</span></span> | <span data-ttu-id="72b86-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="72b86-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="72b86-347">1</span><span class="sxs-lookup"><span data-stu-id="72b86-347">1</span></span> |<span data-ttu-id="72b86-348">Файл ,</span><span class="sxs-lookup"><span data-stu-id="72b86-348">A</span></span> |
| <span data-ttu-id="72b86-349">1</span><span class="sxs-lookup"><span data-stu-id="72b86-349">1</span></span> |<span data-ttu-id="72b86-350">b</span><span class="sxs-lookup"><span data-stu-id="72b86-350">B</span></span> |
| <span data-ttu-id="72b86-351">1</span><span class="sxs-lookup"><span data-stu-id="72b86-351">1</span></span> |<span data-ttu-id="72b86-352">C</span><span class="sxs-lookup"><span data-stu-id="72b86-352">C</span></span> |
| <span data-ttu-id="72b86-353">3</span><span class="sxs-lookup"><span data-stu-id="72b86-353">3</span></span> |<span data-ttu-id="72b86-354">Файл ,</span><span class="sxs-lookup"><span data-stu-id="72b86-354">A</span></span> |
| <span data-ttu-id="72b86-355">3</span><span class="sxs-lookup"><span data-stu-id="72b86-355">3</span></span> |<span data-ttu-id="72b86-356">E</span><span class="sxs-lookup"><span data-stu-id="72b86-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="72b86-357">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="72b86-357">Map source toosink columns</span></span>
<span data-ttu-id="72b86-358">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="72b86-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="72b86-359">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="72b86-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="72b86-360">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="72b86-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="72b86-361">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="72b86-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="72b86-362">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="72b86-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="72b86-363">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="72b86-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="72b86-364">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="72b86-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="72b86-365">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="72b86-365">Performance and Tuning</span></span>
<span data-ttu-id="72b86-366">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="72b86-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
