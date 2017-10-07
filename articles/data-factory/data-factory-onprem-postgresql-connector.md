---
title: "aaaMove данных PostgreSQL с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из базы данных PostgreSQL, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="59bfc-103">Перемещение данных из PostgreSQL с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="59bfc-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="59bfc-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="59bfc-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="59bfc-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="59bfc-106">Можно скопировать данные из локальной PostgreSQL хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="59bfc-107">Список хранилищ данных, поддерживаемые действием копирования hello как приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="59bfc-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="59bfc-108">Фабрика данных в настоящее время поддерживает перемещение данных из PostgreSQL баз данных хранилища данных tooother, но не для перемещения данных из других данных хранит tooan база данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="59bfc-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="59bfc-109">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="59bfc-109">prerequisites</span></span>

<span data-ttu-id="59bfc-110">Служба фабрики данных поддерживает подключения PostgreSQL tooon локальные источники, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="59bfc-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="59bfc-111">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="59bfc-112">Даже если база данных PostgreSQL hello размещается на виртуальной Машине Azure IaaS требуется шлюз.</span><span class="sxs-lookup"><span data-stu-id="59bfc-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="59bfc-113">Можно установить шлюз на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="59bfc-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="59bfc-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="59bfc-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="59bfc-115">Supported versions and installation</span></span>
<span data-ttu-id="59bfc-116">Шлюз управления данными tooconnect toohello базы данных PostgreSQL, установите hello [Ngpsql поставщик данных для PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 или выше на hello же системы как hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="59bfc-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="59bfc-117">Поддерживается PostgreSQL версии 7.4 и более.</span><span class="sxs-lookup"><span data-stu-id="59bfc-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="59bfc-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="59bfc-118">Getting started</span></span>
<span data-ttu-id="59bfc-119">Создать конвейер с действием копирования, который перемещает данные из локального хранилища данных PostgreSQL, можно с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="59bfc-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="59bfc-120">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="59bfc-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="59bfc-121">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="59bfc-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="59bfc-122">Можно также использовать следующие средства toocreate конвейера hello:</span><span class="sxs-lookup"><span data-stu-id="59bfc-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="59bfc-123">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="59bfc-123">Azure portal</span></span>
    - <span data-ttu-id="59bfc-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59bfc-124">Visual Studio</span></span>
    - <span data-ttu-id="59bfc-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="59bfc-125">Azure PowerShell</span></span>
    - <span data-ttu-id="59bfc-126">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="59bfc-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="59bfc-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="59bfc-127">.NET API</span></span>
    - <span data-ttu-id="59bfc-128">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="59bfc-128">REST API</span></span>

     <span data-ttu-id="59bfc-129">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="59bfc-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="59bfc-130">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="59bfc-131">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="59bfc-132">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="59bfc-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="59bfc-133">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="59bfc-134">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="59bfc-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="59bfc-135">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="59bfc-136">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных PostgreSQL см [пример JSON: копирования данных из PostgreSQL tooAzure больших двоичных объектов](#json-example-copy-data-from-postgresql-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="59bfc-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="59bfc-137">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa PostgreSQL хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="59bfc-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="59bfc-138">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="59bfc-138">Linked service properties</span></span>
<span data-ttu-id="59bfc-139">Hello в следующей таблице приводится описание службы конкретных tooPostgreSQL связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="59bfc-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="59bfc-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="59bfc-140">Property</span></span> | <span data-ttu-id="59bfc-141">Описание</span><span class="sxs-lookup"><span data-stu-id="59bfc-141">Description</span></span> | <span data-ttu-id="59bfc-142">Обязательно</span><span class="sxs-lookup"><span data-stu-id="59bfc-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59bfc-143">type</span><span class="sxs-lookup"><span data-stu-id="59bfc-143">type</span></span> |<span data-ttu-id="59bfc-144">свойство типа Hello должно быть присвоено: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="59bfc-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="59bfc-145">Да</span><span class="sxs-lookup"><span data-stu-id="59bfc-145">Yes</span></span> |
| <span data-ttu-id="59bfc-146">server</span><span class="sxs-lookup"><span data-stu-id="59bfc-146">server</span></span> |<span data-ttu-id="59bfc-147">Имя сервера PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="59bfc-148">Да</span><span class="sxs-lookup"><span data-stu-id="59bfc-148">Yes</span></span> |
| <span data-ttu-id="59bfc-149">database</span><span class="sxs-lookup"><span data-stu-id="59bfc-149">database</span></span> |<span data-ttu-id="59bfc-150">Имя базы данных PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="59bfc-151">Да</span><span class="sxs-lookup"><span data-stu-id="59bfc-151">Yes</span></span> |
| <span data-ttu-id="59bfc-152">schema</span><span class="sxs-lookup"><span data-stu-id="59bfc-152">schema</span></span> |<span data-ttu-id="59bfc-153">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="59bfc-154">Имя схемы Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="59bfc-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="59bfc-155">Нет</span><span class="sxs-lookup"><span data-stu-id="59bfc-155">No</span></span> |
| <span data-ttu-id="59bfc-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="59bfc-156">authenticationType</span></span> |<span data-ttu-id="59bfc-157">Тип проверки подлинности используется база данных PostgreSQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="59bfc-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="59bfc-158">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="59bfc-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="59bfc-159">Да</span><span class="sxs-lookup"><span data-stu-id="59bfc-159">Yes</span></span> |
| <span data-ttu-id="59bfc-160">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="59bfc-160">username</span></span> |<span data-ttu-id="59bfc-161">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="59bfc-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="59bfc-162">Нет</span><span class="sxs-lookup"><span data-stu-id="59bfc-162">No</span></span> |
| <span data-ttu-id="59bfc-163">пароль</span><span class="sxs-lookup"><span data-stu-id="59bfc-163">password</span></span> |<span data-ttu-id="59bfc-164">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="59bfc-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="59bfc-165">Нет</span><span class="sxs-lookup"><span data-stu-id="59bfc-165">No</span></span> |
| <span data-ttu-id="59bfc-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="59bfc-166">gatewayName</span></span> |<span data-ttu-id="59bfc-167">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальная база данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="59bfc-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="59bfc-168">Да</span><span class="sxs-lookup"><span data-stu-id="59bfc-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="59bfc-169">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="59bfc-169">Dataset properties</span></span>
<span data-ttu-id="59bfc-170">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="59bfc-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="59bfc-171">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="59bfc-172">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="59bfc-173">Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных PostgreSQL) имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="59bfc-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="59bfc-174">Свойство</span><span class="sxs-lookup"><span data-stu-id="59bfc-174">Property</span></span> | <span data-ttu-id="59bfc-175">Описание</span><span class="sxs-lookup"><span data-stu-id="59bfc-175">Description</span></span> | <span data-ttu-id="59bfc-176">Обязательно</span><span class="sxs-lookup"><span data-stu-id="59bfc-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59bfc-177">tableName</span><span class="sxs-lookup"><span data-stu-id="59bfc-177">tableName</span></span> |<span data-ttu-id="59bfc-178">Имя таблицы hello в экземпляр базы данных PostgreSQL, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="59bfc-179">Hello tableName учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="59bfc-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="59bfc-180">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="59bfc-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="59bfc-181">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="59bfc-181">Copy activity properties</span></span>
<span data-ttu-id="59bfc-182">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="59bfc-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="59bfc-183">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="59bfc-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="59bfc-184">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="59bfc-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="59bfc-185">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="59bfc-186">Если источник имеет тип **RelationalSource** (включая PostgreSQL), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="59bfc-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="59bfc-187">Свойство</span><span class="sxs-lookup"><span data-stu-id="59bfc-187">Property</span></span> | <span data-ttu-id="59bfc-188">Описание</span><span class="sxs-lookup"><span data-stu-id="59bfc-188">Description</span></span> | <span data-ttu-id="59bfc-189">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="59bfc-189">Allowed values</span></span> | <span data-ttu-id="59bfc-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="59bfc-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59bfc-191">query</span><span class="sxs-lookup"><span data-stu-id="59bfc-191">query</span></span> |<span data-ttu-id="59bfc-192">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="59bfc-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="59bfc-193">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="59bfc-193">SQL query string.</span></span> <span data-ttu-id="59bfc-194">Например, "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="59bfc-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="59bfc-195">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="59bfc-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="59bfc-196">В именах схем и таблиц учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="59bfc-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="59bfc-197">Заключайте их в `""` (двойные кавычки) в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="59bfc-198">**Пример**</span><span class="sxs-lookup"><span data-stu-id="59bfc-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="59bfc-199">Пример JSON: копирование данных из PostgreSQL tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="59bfc-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="59bfc-200">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="59bfc-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="59bfc-201">Они показывают, как данные toocopy из PostgreSQL базы данных tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="59bfc-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="59bfc-202">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="59bfc-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="59bfc-203">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="59bfc-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="59bfc-204">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="59bfc-205">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="59bfc-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="59bfc-206">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="59bfc-207">Связанная служба типа [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59bfc-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="59bfc-208">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59bfc-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="59bfc-209">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="59bfc-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="59bfc-210">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="59bfc-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="59bfc-211">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="59bfc-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="59bfc-212">Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных PostgreSQL каждый час.</span><span class="sxs-lookup"><span data-stu-id="59bfc-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="59bfc-213">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="59bfc-214">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="59bfc-215">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="59bfc-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="59bfc-216">**Связанная служба PostgreSQL**</span><span class="sxs-lookup"><span data-stu-id="59bfc-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="59bfc-217">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="59bfc-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="59bfc-218">**Входной набор данных PostgreSQL**</span><span class="sxs-lookup"><span data-stu-id="59bfc-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="59bfc-219">Образец Hello предполагается создания таблицы «MyTable» в PostgreSQL, и она содержит столбец с именем «timestamp» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="59bfc-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="59bfc-220">Параметр `"external": true` информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="59bfc-221">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="59bfc-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="59bfc-222">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="59bfc-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="59bfc-223">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="59bfc-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="59bfc-224">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="59bfc-225">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="59bfc-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="59bfc-226">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="59bfc-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="59bfc-227">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="59bfc-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="59bfc-228">запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello данные из таблицы public.usstates hello в базе данных PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="59bfc-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="59bfc-229">Сопоставление типов для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="59bfc-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="59bfc-230">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="59bfc-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="59bfc-231">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="59bfc-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="59bfc-232">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="59bfc-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="59bfc-233">При перемещении данных tooPostgreSQL, hello следующие сопоставления используются из типа too.NET PostgreSQL типа.</span><span class="sxs-lookup"><span data-stu-id="59bfc-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="59bfc-234">Тип базы данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="59bfc-234">PostgreSQL Database type</span></span> | <span data-ttu-id="59bfc-235">Псевдонимы PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="59bfc-235">PostgresSQL aliases</span></span> | <span data-ttu-id="59bfc-236">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="59bfc-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59bfc-237">abstime</span><span class="sxs-lookup"><span data-stu-id="59bfc-237">abstime</span></span> | |<span data-ttu-id="59bfc-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="59bfc-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="59bfc-239">bigint</span><span class="sxs-lookup"><span data-stu-id="59bfc-239">bigint</span></span> |<span data-ttu-id="59bfc-240">int8</span><span class="sxs-lookup"><span data-stu-id="59bfc-240">int8</span></span> |<span data-ttu-id="59bfc-241">Int64</span><span class="sxs-lookup"><span data-stu-id="59bfc-241">Int64</span></span> |
| <span data-ttu-id="59bfc-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="59bfc-242">bigserial</span></span> |<span data-ttu-id="59bfc-243">serial8</span><span class="sxs-lookup"><span data-stu-id="59bfc-243">serial8</span></span> |<span data-ttu-id="59bfc-244">Int64</span><span class="sxs-lookup"><span data-stu-id="59bfc-244">Int64</span></span> |
| <span data-ttu-id="59bfc-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-245">bit [ (n) ]</span></span> | |<span data-ttu-id="59bfc-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="59bfc-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="59bfc-248">varbit</span><span class="sxs-lookup"><span data-stu-id="59bfc-248">varbit</span></span> |<span data-ttu-id="59bfc-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-249">Byte[], String</span></span> |
| <span data-ttu-id="59bfc-250">Логическое</span><span class="sxs-lookup"><span data-stu-id="59bfc-250">boolean</span></span> |<span data-ttu-id="59bfc-251">bool</span><span class="sxs-lookup"><span data-stu-id="59bfc-251">bool</span></span> |<span data-ttu-id="59bfc-252">Логическое</span><span class="sxs-lookup"><span data-stu-id="59bfc-252">Boolean</span></span> |
| <span data-ttu-id="59bfc-253">box</span><span class="sxs-lookup"><span data-stu-id="59bfc-253">box</span></span> | |<span data-ttu-id="59bfc-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-255">bytea</span><span class="sxs-lookup"><span data-stu-id="59bfc-255">bytea</span></span> | |<span data-ttu-id="59bfc-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-257">character [ (n) ]</span></span> |<span data-ttu-id="59bfc-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-258">char [ (n) ]</span></span> |<span data-ttu-id="59bfc-259">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-259">String</span></span> |
| <span data-ttu-id="59bfc-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-260">character varying [ (n) ]</span></span> |<span data-ttu-id="59bfc-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-261">varchar [ (n) ]</span></span> |<span data-ttu-id="59bfc-262">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-262">String</span></span> |
| <span data-ttu-id="59bfc-263">cid</span><span class="sxs-lookup"><span data-stu-id="59bfc-263">cid</span></span> | |<span data-ttu-id="59bfc-264">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-264">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-265">cidr</span><span class="sxs-lookup"><span data-stu-id="59bfc-265">cidr</span></span> | |<span data-ttu-id="59bfc-266">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-266">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-267">circle</span><span class="sxs-lookup"><span data-stu-id="59bfc-267">circle</span></span> | |<span data-ttu-id="59bfc-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-269">дата</span><span class="sxs-lookup"><span data-stu-id="59bfc-269">date</span></span> | |<span data-ttu-id="59bfc-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="59bfc-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="59bfc-271">daterange</span><span class="sxs-lookup"><span data-stu-id="59bfc-271">daterange</span></span> | |<span data-ttu-id="59bfc-272">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-272">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-273">double precision</span><span class="sxs-lookup"><span data-stu-id="59bfc-273">double precision</span></span> |<span data-ttu-id="59bfc-274">float8</span><span class="sxs-lookup"><span data-stu-id="59bfc-274">float8</span></span> |<span data-ttu-id="59bfc-275">Double</span><span class="sxs-lookup"><span data-stu-id="59bfc-275">Double</span></span> |
| <span data-ttu-id="59bfc-276">inet</span><span class="sxs-lookup"><span data-stu-id="59bfc-276">inet</span></span> | |<span data-ttu-id="59bfc-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-278">intarry</span><span class="sxs-lookup"><span data-stu-id="59bfc-278">intarry</span></span> | |<span data-ttu-id="59bfc-279">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-279">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-280">int4range</span><span class="sxs-lookup"><span data-stu-id="59bfc-280">int4range</span></span> | |<span data-ttu-id="59bfc-281">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-281">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-282">int8range</span><span class="sxs-lookup"><span data-stu-id="59bfc-282">int8range</span></span> | |<span data-ttu-id="59bfc-283">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-283">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-284">целое число</span><span class="sxs-lookup"><span data-stu-id="59bfc-284">integer</span></span> |<span data-ttu-id="59bfc-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="59bfc-285">int, int4</span></span> |<span data-ttu-id="59bfc-286">Int32</span><span class="sxs-lookup"><span data-stu-id="59bfc-286">Int32</span></span> |
| <span data-ttu-id="59bfc-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="59bfc-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="59bfc-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="59bfc-289">json</span><span class="sxs-lookup"><span data-stu-id="59bfc-289">json</span></span> | |<span data-ttu-id="59bfc-290">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-290">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="59bfc-291">jsonb</span></span> | |<span data-ttu-id="59bfc-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="59bfc-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="59bfc-293">line</span><span class="sxs-lookup"><span data-stu-id="59bfc-293">line</span></span> | |<span data-ttu-id="59bfc-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-295">lseg</span><span class="sxs-lookup"><span data-stu-id="59bfc-295">lseg</span></span> | |<span data-ttu-id="59bfc-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="59bfc-297">macaddr</span></span> | |<span data-ttu-id="59bfc-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-299">money;</span><span class="sxs-lookup"><span data-stu-id="59bfc-299">money</span></span> | |<span data-ttu-id="59bfc-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="59bfc-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="59bfc-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="59bfc-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="59bfc-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="59bfc-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="59bfc-303">Decimal</span></span> |
| <span data-ttu-id="59bfc-304">numrange</span><span class="sxs-lookup"><span data-stu-id="59bfc-304">numrange</span></span> | |<span data-ttu-id="59bfc-305">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-305">String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-306">oid</span><span class="sxs-lookup"><span data-stu-id="59bfc-306">oid</span></span> | |<span data-ttu-id="59bfc-307">Int32</span><span class="sxs-lookup"><span data-stu-id="59bfc-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="59bfc-308">path</span><span class="sxs-lookup"><span data-stu-id="59bfc-308">path</span></span> | |<span data-ttu-id="59bfc-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="59bfc-310">pg_lsn</span></span> | |<span data-ttu-id="59bfc-311">Int64</span><span class="sxs-lookup"><span data-stu-id="59bfc-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="59bfc-312">point</span><span class="sxs-lookup"><span data-stu-id="59bfc-312">point</span></span> | |<span data-ttu-id="59bfc-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-314">polygon</span><span class="sxs-lookup"><span data-stu-id="59bfc-314">polygon</span></span> | |<span data-ttu-id="59bfc-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="59bfc-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="59bfc-316">real;</span><span class="sxs-lookup"><span data-stu-id="59bfc-316">real</span></span> |<span data-ttu-id="59bfc-317">float4</span><span class="sxs-lookup"><span data-stu-id="59bfc-317">float4</span></span> |<span data-ttu-id="59bfc-318">Single</span><span class="sxs-lookup"><span data-stu-id="59bfc-318">Single</span></span> |
| <span data-ttu-id="59bfc-319">smallint;</span><span class="sxs-lookup"><span data-stu-id="59bfc-319">smallint</span></span> |<span data-ttu-id="59bfc-320">int2</span><span class="sxs-lookup"><span data-stu-id="59bfc-320">int2</span></span> |<span data-ttu-id="59bfc-321">Int16</span><span class="sxs-lookup"><span data-stu-id="59bfc-321">Int16</span></span> |
| <span data-ttu-id="59bfc-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="59bfc-322">smallserial</span></span> |<span data-ttu-id="59bfc-323">serial2</span><span class="sxs-lookup"><span data-stu-id="59bfc-323">serial2</span></span> |<span data-ttu-id="59bfc-324">Int16</span><span class="sxs-lookup"><span data-stu-id="59bfc-324">Int16</span></span> |
| <span data-ttu-id="59bfc-325">serial</span><span class="sxs-lookup"><span data-stu-id="59bfc-325">serial</span></span> |<span data-ttu-id="59bfc-326">serial4</span><span class="sxs-lookup"><span data-stu-id="59bfc-326">serial4</span></span> |<span data-ttu-id="59bfc-327">Int32</span><span class="sxs-lookup"><span data-stu-id="59bfc-327">Int32</span></span> |
| <span data-ttu-id="59bfc-328">text</span><span class="sxs-lookup"><span data-stu-id="59bfc-328">text</span></span> | |<span data-ttu-id="59bfc-329">Строка</span><span class="sxs-lookup"><span data-stu-id="59bfc-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="59bfc-330">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="59bfc-330">Map source toosink columns</span></span>
<span data-ttu-id="59bfc-331">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="59bfc-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="59bfc-332">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="59bfc-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="59bfc-333">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="59bfc-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="59bfc-334">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="59bfc-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="59bfc-335">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="59bfc-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="59bfc-336">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="59bfc-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="59bfc-337">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="59bfc-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="59bfc-338">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="59bfc-338">Performance and Tuning</span></span>
<span data-ttu-id="59bfc-339">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="59bfc-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
