---
title: "aaaMove данных из Sybase, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из базы данных Sybase, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="4a5f7-103">Перемещение данных из Sybase с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="4a5f7-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="4a5f7-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="4a5f7-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4a5f7-106">Можно скопировать данные из локальной Sybase хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="4a5f7-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4a5f7-108">Фабрика данных в настоящее время поддерживает только при перемещении данных Sybase хранения tooother хранилищ данных, но не для перемещения данных из других данных Sybase tooa хранилищ данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4a5f7-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4a5f7-109">Prerequisites</span></span>
<span data-ttu-id="4a5f7-110">Служба фабрики данных поддерживает подключения Sybase tooon локальные источники, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="4a5f7-111">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="4a5f7-112">Даже если база данных Sybase hello размещается на виртуальной Машине Azure IaaS требуется шлюз.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="4a5f7-113">Hello шлюз можно установить на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="4a5f7-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="4a5f7-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="4a5f7-115">Supported versions and installation</span></span>
<span data-ttu-id="4a5f7-116">Для toohello tooconnect шлюз управления данными базы данных Sybase, необходим tooinstall hello [поставщик данных для Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 или выше на hello же системы как hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="4a5f7-117">Поддерживается Sybase версии 16 и более.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4a5f7-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4a5f7-118">Getting started</span></span>
<span data-ttu-id="4a5f7-119">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="4a5f7-120">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4a5f7-121">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="4a5f7-122">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4a5f7-123">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4a5f7-124">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4a5f7-125">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4a5f7-126">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="4a5f7-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4a5f7-128">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4a5f7-129">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4a5f7-130">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных Sybase в разделе [пример JSON: копирования данных из Sybase tooAzure больших двоичных объектов](#json-example-copy-data-from-sybase-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4a5f7-131">Hello в следующих разделах подробно свойства JSON, хранилище данных Sybase tooa определенных сущностей используется toodefine фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="4a5f7-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4a5f7-132">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="4a5f7-132">Linked service properties</span></span>
<span data-ttu-id="4a5f7-133">Hello в следующей таблице приводится описание службы конкретных tooSybase связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="4a5f7-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="4a5f7-134">Property</span></span> | <span data-ttu-id="4a5f7-135">Описание</span><span class="sxs-lookup"><span data-stu-id="4a5f7-135">Description</span></span> | <span data-ttu-id="4a5f7-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a5f7-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a5f7-137">type</span><span class="sxs-lookup"><span data-stu-id="4a5f7-137">type</span></span> |<span data-ttu-id="4a5f7-138">свойство типа Hello должно быть присвоено: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="4a5f7-139">Да</span><span class="sxs-lookup"><span data-stu-id="4a5f7-139">Yes</span></span> |
| <span data-ttu-id="4a5f7-140">server</span><span class="sxs-lookup"><span data-stu-id="4a5f7-140">server</span></span> |<span data-ttu-id="4a5f7-141">Имя сервера Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="4a5f7-142">Да</span><span class="sxs-lookup"><span data-stu-id="4a5f7-142">Yes</span></span> |
| <span data-ttu-id="4a5f7-143">database</span><span class="sxs-lookup"><span data-stu-id="4a5f7-143">database</span></span> |<span data-ttu-id="4a5f7-144">Имя базы данных Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="4a5f7-145">Да</span><span class="sxs-lookup"><span data-stu-id="4a5f7-145">Yes</span></span> |
| <span data-ttu-id="4a5f7-146">schema</span><span class="sxs-lookup"><span data-stu-id="4a5f7-146">schema</span></span> |<span data-ttu-id="4a5f7-147">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="4a5f7-148">Нет</span><span class="sxs-lookup"><span data-stu-id="4a5f7-148">No</span></span> |
| <span data-ttu-id="4a5f7-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4a5f7-149">authenticationType</span></span> |<span data-ttu-id="4a5f7-150">Тип проверки подлинности используется база данных Sybase toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="4a5f7-151">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="4a5f7-152">Да</span><span class="sxs-lookup"><span data-stu-id="4a5f7-152">Yes</span></span> |
| <span data-ttu-id="4a5f7-153">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="4a5f7-153">username</span></span> |<span data-ttu-id="4a5f7-154">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="4a5f7-155">Нет</span><span class="sxs-lookup"><span data-stu-id="4a5f7-155">No</span></span> |
| <span data-ttu-id="4a5f7-156">пароль</span><span class="sxs-lookup"><span data-stu-id="4a5f7-156">password</span></span> |<span data-ttu-id="4a5f7-157">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="4a5f7-158">Нет</span><span class="sxs-lookup"><span data-stu-id="4a5f7-158">No</span></span> |
| <span data-ttu-id="4a5f7-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4a5f7-159">gatewayName</span></span> |<span data-ttu-id="4a5f7-160">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="4a5f7-161">Да</span><span class="sxs-lookup"><span data-stu-id="4a5f7-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4a5f7-162">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="4a5f7-162">Dataset properties</span></span>
<span data-ttu-id="4a5f7-163">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4a5f7-164">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4a5f7-165">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4a5f7-166">Hello **typeProperties** раздел для набора данных типа **RelationalTable** (включает набор данных Sybase) имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="4a5f7-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="4a5f7-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="4a5f7-167">Property</span></span> | <span data-ttu-id="4a5f7-168">Описание</span><span class="sxs-lookup"><span data-stu-id="4a5f7-168">Description</span></span> | <span data-ttu-id="4a5f7-169">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a5f7-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a5f7-170">tableName</span><span class="sxs-lookup"><span data-stu-id="4a5f7-170">tableName</span></span> |<span data-ttu-id="4a5f7-171">Имя таблицы hello в экземпляр базы данных Sybase, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="4a5f7-172">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4a5f7-173">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="4a5f7-173">Copy activity properties</span></span>
<span data-ttu-id="4a5f7-174">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4a5f7-175">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4a5f7-176">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="4a5f7-177">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4a5f7-178">Если источник hello имеет тип **RelationalSource** (включает Sybase), hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="4a5f7-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="4a5f7-179">Свойство</span><span class="sxs-lookup"><span data-stu-id="4a5f7-179">Property</span></span> | <span data-ttu-id="4a5f7-180">Описание</span><span class="sxs-lookup"><span data-stu-id="4a5f7-180">Description</span></span> | <span data-ttu-id="4a5f7-181">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="4a5f7-181">Allowed values</span></span> | <span data-ttu-id="4a5f7-182">Обязательно</span><span class="sxs-lookup"><span data-stu-id="4a5f7-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a5f7-183">query</span><span class="sxs-lookup"><span data-stu-id="4a5f7-183">query</span></span> |<span data-ttu-id="4a5f7-184">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="4a5f7-185">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-185">SQL query string.</span></span> <span data-ttu-id="4a5f7-186">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="4a5f7-187">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="4a5f7-188">Пример JSON: копирование данных из Sybase tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="4a5f7-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="4a5f7-189">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4a5f7-190">Они показывают, как toocopy данных из Sybase базы данных tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="4a5f7-191">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="4a5f7-192">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="4a5f7-193">Связанная служба типа [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4a5f7-194">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4a5f7-195">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4a5f7-196">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4a5f7-197">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4a5f7-198">Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных Sybase каждый час.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="4a5f7-199">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="4a5f7-200">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="4a5f7-201">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="4a5f7-202">**Связанная служба Sybase**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="4a5f7-203">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="4a5f7-204">**Входной набор данных Sybase**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="4a5f7-205">Образец Hello предполагается создания таблицы «MyTable» в Sybase и она содержит столбец с именем «timestamp» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="4a5f7-206">Параметр «external»: true уведомляет службу hello фабрики данных, что этот набор данных фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="4a5f7-207">Обратите внимание, что hello **тип** hello связанной службы задано значение: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="4a5f7-208">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4a5f7-209">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4a5f7-210">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4a5f7-211">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="4a5f7-212">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="4a5f7-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4a5f7-213">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="4a5f7-214">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="4a5f7-215">запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello данные из hello администратор базы данных. Таблицы Orders в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="4a5f7-216">Сопоставление типов для Sybase</span><span class="sxs-lookup"><span data-stu-id="4a5f7-216">Type mapping for Sybase</span></span>
<span data-ttu-id="4a5f7-217">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статья hello действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="4a5f7-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="4a5f7-218">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="4a5f7-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4a5f7-219">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="4a5f7-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4a5f7-220">Sybase поддерживает T-SQL и типы T-SQL.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="4a5f7-221">Таблицу сопоставления из типа too.NET типов sql. в разделе [соединитель SQL Azure](data-factory-azure-sql-connector.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="4a5f7-222">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="4a5f7-222">Map source toosink columns</span></span>
<span data-ttu-id="4a5f7-223">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4a5f7-224">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="4a5f7-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="4a5f7-225">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="4a5f7-226">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4a5f7-227">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4a5f7-228">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4a5f7-229">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="4a5f7-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4a5f7-230">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="4a5f7-230">Performance and Tuning</span></span>
<span data-ttu-id="4a5f7-231">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="4a5f7-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
