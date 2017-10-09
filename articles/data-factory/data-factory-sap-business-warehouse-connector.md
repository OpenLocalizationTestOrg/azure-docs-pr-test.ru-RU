---
title: "aaaMove данных из SAP Business Warehouse, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данных из SAP Business Warehouse, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="90d76-103">Перемещение данных из SAP Business Warehouse с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="90d76-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="90d76-104">В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из локального SAP Business хранилища (BW).</span><span class="sxs-lookup"><span data-stu-id="90d76-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="90d76-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="90d76-106">Можно скопировать данные из локальной SAP Business Warehouse хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="90d76-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="90d76-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="90d76-108">Фабрика данных в настоящее время поддерживает только для перемещения данных из объекта данных SAP Business Warehouse tooother хранятся, но не для перемещения данных из других данных хранит tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="90d76-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="90d76-109">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="90d76-109">Supported versions and installation</span></span>
<span data-ttu-id="90d76-110">Этот соединитель поддерживает SAP Business Warehouse версии 7.x.</span><span class="sxs-lookup"><span data-stu-id="90d76-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="90d76-111">Он поддерживает копирование данных из InfoCube и QueryCubes (включая запросы BEx) с помощью запросов многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="90d76-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="90d76-112">tooenable hello подключения toohello экземпляра SAP BW, установите hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="90d76-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="90d76-113">**Шлюз управления данными**: подключение локальной tooon данных поддерживает службы фабрики данных хранилища (включая SAP Business Warehouse) с помощью компонента вызывается шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="90d76-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="90d76-114">toolearn о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. в разделе [перемещение данных между локальными данными хранения хранилища данных toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="90d76-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="90d76-115">Требуется использовать шлюз, даже если hello SAP Business Warehouse размещается в Azure IaaS виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="90d76-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="90d76-116">Hello шлюз можно установить на hello одной виртуальной Машины как данные hello хранения или же в другой виртуальной Машине, при условии, что шлюз hello могут подключаться toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="90d76-117">**Библиотека SAP NetWeaver** на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="90d76-118">Библиотека SAP Netweaver hello можно получить у администратора SAP или непосредственно из hello [центра загрузки программного обеспечения SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="90d76-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="90d76-119">Поиск hello **&#1025361; Примечание SAP** расположения загрузки hello tooget hello самой последней версии.</span><span class="sxs-lookup"><span data-stu-id="90d76-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="90d76-120">Убедитесь, что что hello архитектура для библиотеки SAP NetWeaver hello (32-разрядной или 64-разрядной) соответствует установку шлюза.</span><span class="sxs-lookup"><span data-stu-id="90d76-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="90d76-121">Установите все файлы, включенные в hello SAP NetWeaver RFC SDK соответствующим toohello Примечание SAP.</span><span class="sxs-lookup"><span data-stu-id="90d76-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="90d76-122">Библиотека SAP NetWeaver Hello также включается в hello установки клиентских средств SAP.</span><span class="sxs-lookup"><span data-stu-id="90d76-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="90d76-123">Поместите hello библиотек DLL, извлеченных из hello NetWeaver RFC SDK в папку system32.</span><span class="sxs-lookup"><span data-stu-id="90d76-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="90d76-124">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="90d76-124">Getting started</span></span>
<span data-ttu-id="90d76-125">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="90d76-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="90d76-126">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="90d76-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="90d76-127">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="90d76-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="90d76-128">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="90d76-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="90d76-129">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="90d76-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="90d76-130">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="90d76-131">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="90d76-132">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="90d76-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="90d76-133">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="90d76-134">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="90d76-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="90d76-135">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="90d76-136">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной SAP Business Warehouse см. в разделе [JSON пример: копирование данных из SAP Business Warehouse tooAzure большого двоичного объекта](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="90d76-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="90d76-137">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooan SAP BW хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="90d76-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="90d76-138">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="90d76-138">Linked service properties</span></span>
<span data-ttu-id="90d76-139">Привет, в следующей таблице приводится описание tooSAP службы хранилища предприятия (BW) связаны определенные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="90d76-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="90d76-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="90d76-140">Property</span></span> | <span data-ttu-id="90d76-141">Описание</span><span class="sxs-lookup"><span data-stu-id="90d76-141">Description</span></span> | <span data-ttu-id="90d76-142">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="90d76-142">Allowed values</span></span> | <span data-ttu-id="90d76-143">Обязательно</span><span class="sxs-lookup"><span data-stu-id="90d76-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="90d76-144">server</span><span class="sxs-lookup"><span data-stu-id="90d76-144">server</span></span> | <span data-ttu-id="90d76-145">Имя сервера hello, на какие hello SAP BW расположен экземпляр.</span><span class="sxs-lookup"><span data-stu-id="90d76-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="90d76-146">string</span><span class="sxs-lookup"><span data-stu-id="90d76-146">string</span></span> | <span data-ttu-id="90d76-147">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-147">Yes</span></span>
<span data-ttu-id="90d76-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="90d76-148">systemNumber</span></span> | <span data-ttu-id="90d76-149">Номер системы hello системы SAP BW.</span><span class="sxs-lookup"><span data-stu-id="90d76-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="90d76-150">Двузначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="90d76-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="90d76-151">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-151">Yes</span></span>
<span data-ttu-id="90d76-152">clientid</span><span class="sxs-lookup"><span data-stu-id="90d76-152">clientId</span></span> | <span data-ttu-id="90d76-153">Идентификатор клиента для клиента hello в hello системы SAP-W.</span><span class="sxs-lookup"><span data-stu-id="90d76-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="90d76-154">Трехзначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="90d76-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="90d76-155">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-155">Yes</span></span>
<span data-ttu-id="90d76-156">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="90d76-156">username</span></span> | <span data-ttu-id="90d76-157">Имя пользователя hello с сервера SAP toohello доступа</span><span class="sxs-lookup"><span data-stu-id="90d76-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="90d76-158">string</span><span class="sxs-lookup"><span data-stu-id="90d76-158">string</span></span> | <span data-ttu-id="90d76-159">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-159">Yes</span></span>
<span data-ttu-id="90d76-160">пароль</span><span class="sxs-lookup"><span data-stu-id="90d76-160">password</span></span> | <span data-ttu-id="90d76-161">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-161">Password for hello user.</span></span> | <span data-ttu-id="90d76-162">string</span><span class="sxs-lookup"><span data-stu-id="90d76-162">string</span></span> | <span data-ttu-id="90d76-163">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-163">Yes</span></span>
<span data-ttu-id="90d76-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="90d76-164">gatewayName</span></span> | <span data-ttu-id="90d76-165">Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP BW экземпляр.</span><span class="sxs-lookup"><span data-stu-id="90d76-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="90d76-166">string</span><span class="sxs-lookup"><span data-stu-id="90d76-166">string</span></span> | <span data-ttu-id="90d76-167">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-167">Yes</span></span>
<span data-ttu-id="90d76-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="90d76-168">encryptedCredential</span></span> | <span data-ttu-id="90d76-169">Строка Hello шифрования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-169">hello encrypted credential string.</span></span> | <span data-ttu-id="90d76-170">string</span><span class="sxs-lookup"><span data-stu-id="90d76-170">string</span></span> | <span data-ttu-id="90d76-171">Нет</span><span class="sxs-lookup"><span data-stu-id="90d76-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="90d76-172">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="90d76-172">Dataset properties</span></span>
<span data-ttu-id="90d76-173">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="90d76-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="90d76-174">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="90d76-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="90d76-175">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="90d76-176">Свойства определенного типа, не поддерживается для набора данных SAP BW hello типа **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="90d76-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="90d76-177">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="90d76-177">Copy activity properties</span></span>
<span data-ttu-id="90d76-178">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="90d76-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="90d76-179">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="90d76-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="90d76-180">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="90d76-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="90d76-181">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="90d76-182">Если источник в действии копирования имеет тип **RelationalSource** (включает SAP BW), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="90d76-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="90d76-183">Свойство</span><span class="sxs-lookup"><span data-stu-id="90d76-183">Property</span></span> | <span data-ttu-id="90d76-184">Описание</span><span class="sxs-lookup"><span data-stu-id="90d76-184">Description</span></span> | <span data-ttu-id="90d76-185">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="90d76-185">Allowed values</span></span> | <span data-ttu-id="90d76-186">Обязательно</span><span class="sxs-lookup"><span data-stu-id="90d76-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90d76-187">query</span><span class="sxs-lookup"><span data-stu-id="90d76-187">query</span></span> | <span data-ttu-id="90d76-188">Указывает tooread hello многомерных Выражений запроса данных из экземпляра SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="90d76-189">Запрос многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="90d76-189">MDX query.</span></span> | <span data-ttu-id="90d76-190">Да</span><span class="sxs-lookup"><span data-stu-id="90d76-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="90d76-191">Пример JSON: копирование данных из SAP Business Warehouse tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="90d76-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="90d76-192">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="90d76-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="90d76-193">В этом примере показано, как данные toocopy из tooan SAP Business Warehouse локального хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="90d76-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="90d76-194">Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="90d76-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="90d76-195">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="90d76-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="90d76-196">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="90d76-197">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="90d76-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="90d76-198">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="90d76-199">Связанная служба типа [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="90d76-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="90d76-200">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="90d76-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="90d76-201">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="90d76-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="90d76-202">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="90d76-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="90d76-203">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="90d76-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="90d76-204">Образец Hello копирует данные из tooan экземпляра SAP Business Warehouse BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="90d76-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="90d76-205">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="90d76-206">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="90d76-207">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="90d76-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="90d76-208">Связанная служба SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="90d76-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="90d76-209">Ссылки на службы связаны toohello данных SAP BW экземпляр фабрики.</span><span class="sxs-lookup"><span data-stu-id="90d76-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="90d76-210">Hello свойство type установлено слишком**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="90d76-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="90d76-211">Hello typeProperties раздел содержит сведения о соединении для экземпляра SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="90d76-212">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="90d76-212">Azure Storage linked service</span></span>
<span data-ttu-id="90d76-213">Ссылки на службы связаны фабрики данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="90d76-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="90d76-214">Hello свойство type установлено слишком**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="90d76-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="90d76-215">Hello typeProperties раздел содержит сведения о соединении для hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="90d76-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="90d76-216">Входной набор данных SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="90d76-216">SAP BW input dataset</span></span>
<span data-ttu-id="90d76-217">Этот набор данных определяет набор данных SAP Business Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="90d76-218">Задание типа hello фабрики данных набора данных hello слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="90d76-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="90d76-219">В настоящее время какие-либо свойства типа для набора данных SAP Business Warehouse не указываются пользователем.</span><span class="sxs-lookup"><span data-stu-id="90d76-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="90d76-220">запрос Hello в hello определение действия копирования указывает, какие tooread данных из экземпляра SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="90d76-221">Установка значения внешнего свойства tootrue сообщает hello служба фабрики данных, этой таблицы hello является фабрикой toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="90d76-222">Свойства частоту и интервал определяет расписание hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="90d76-223">В этом случае hello считывании данных из экземпляра SAP BW hello каждый час.</span><span class="sxs-lookup"><span data-stu-id="90d76-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="90d76-224">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="90d76-224">Azure Blob output dataset</span></span>
<span data-ttu-id="90d76-225">Этот набор данных определяет hello выходной BLOB-объектов Azure, набор данных.</span><span class="sxs-lookup"><span data-stu-id="90d76-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="90d76-226">свойство типа Hello задается tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="90d76-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="90d76-227">раздел typeProperties Hello содержит, где хранятся данные hello, скопированные из экземпляра SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="90d76-228">Hello записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="90d76-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="90d76-229">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="90d76-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="90d76-230">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="90d76-231">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="90d76-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="90d76-232">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="90d76-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="90d76-233">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** (для источника SAP BW) и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="90d76-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="90d76-234">Hello запрос, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="90d76-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="90d76-235">Сопоставление типов для SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="90d76-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="90d76-236">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:</span><span class="sxs-lookup"><span data-stu-id="90d76-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="90d76-237">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="90d76-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="90d76-238">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="90d76-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="90d76-239">При перемещении данных из SAP BW из SAP BW типы too.NET типы используются следующие сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="90d76-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="90d76-240">Тип данных в словаре ABAP hello</span><span class="sxs-lookup"><span data-stu-id="90d76-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="90d76-241">Тип данных .NET</span><span class="sxs-lookup"><span data-stu-id="90d76-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="90d76-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="90d76-242">ACCP</span></span> |  <span data-ttu-id="90d76-243">int</span><span class="sxs-lookup"><span data-stu-id="90d76-243">Int</span></span>
<span data-ttu-id="90d76-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="90d76-244">CHAR</span></span> | <span data-ttu-id="90d76-245">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-245">String</span></span>
<span data-ttu-id="90d76-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="90d76-246">CLNT</span></span> | <span data-ttu-id="90d76-247">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-247">String</span></span>
<span data-ttu-id="90d76-248">CURR</span><span class="sxs-lookup"><span data-stu-id="90d76-248">CURR</span></span> | <span data-ttu-id="90d76-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="90d76-249">Decimal</span></span>
<span data-ttu-id="90d76-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="90d76-250">CUKY</span></span> | <span data-ttu-id="90d76-251">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-251">String</span></span>
<span data-ttu-id="90d76-252">DEC</span><span class="sxs-lookup"><span data-stu-id="90d76-252">DEC</span></span> | <span data-ttu-id="90d76-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="90d76-253">Decimal</span></span>
<span data-ttu-id="90d76-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="90d76-254">FLTP</span></span> | <span data-ttu-id="90d76-255">Double</span><span class="sxs-lookup"><span data-stu-id="90d76-255">Double</span></span>
<span data-ttu-id="90d76-256">INT1</span><span class="sxs-lookup"><span data-stu-id="90d76-256">INT1</span></span> | <span data-ttu-id="90d76-257">Byte</span><span class="sxs-lookup"><span data-stu-id="90d76-257">Byte</span></span>
<span data-ttu-id="90d76-258">INT2</span><span class="sxs-lookup"><span data-stu-id="90d76-258">INT2</span></span> | <span data-ttu-id="90d76-259">Int16</span><span class="sxs-lookup"><span data-stu-id="90d76-259">Int16</span></span>
<span data-ttu-id="90d76-260">INT4</span><span class="sxs-lookup"><span data-stu-id="90d76-260">INT4</span></span> | <span data-ttu-id="90d76-261">int</span><span class="sxs-lookup"><span data-stu-id="90d76-261">Int</span></span>
<span data-ttu-id="90d76-262">LANG</span><span class="sxs-lookup"><span data-stu-id="90d76-262">LANG</span></span> | <span data-ttu-id="90d76-263">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-263">String</span></span>
<span data-ttu-id="90d76-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="90d76-264">LCHR</span></span> | <span data-ttu-id="90d76-265">string</span><span class="sxs-lookup"><span data-stu-id="90d76-265">String</span></span>
<span data-ttu-id="90d76-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="90d76-266">LRAW</span></span> | <span data-ttu-id="90d76-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="90d76-267">Byte[]</span></span>
<span data-ttu-id="90d76-268">PREC</span><span class="sxs-lookup"><span data-stu-id="90d76-268">PREC</span></span> | <span data-ttu-id="90d76-269">Int16</span><span class="sxs-lookup"><span data-stu-id="90d76-269">Int16</span></span>
<span data-ttu-id="90d76-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="90d76-270">QUAN</span></span> | <span data-ttu-id="90d76-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="90d76-271">Decimal</span></span>
<span data-ttu-id="90d76-272">RAW</span><span class="sxs-lookup"><span data-stu-id="90d76-272">RAW</span></span> | <span data-ttu-id="90d76-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="90d76-273">Byte[]</span></span>
<span data-ttu-id="90d76-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="90d76-274">RAWSTRING</span></span> | <span data-ttu-id="90d76-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="90d76-275">Byte[]</span></span>
<span data-ttu-id="90d76-276">STRING</span><span class="sxs-lookup"><span data-stu-id="90d76-276">STRING</span></span> | <span data-ttu-id="90d76-277">string</span><span class="sxs-lookup"><span data-stu-id="90d76-277">String</span></span>
<span data-ttu-id="90d76-278">ЕДИНИЦА ИЗМЕРЕНИЯ</span><span class="sxs-lookup"><span data-stu-id="90d76-278">UNIT</span></span> | <span data-ttu-id="90d76-279">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-279">String</span></span>
<span data-ttu-id="90d76-280">DATS</span><span class="sxs-lookup"><span data-stu-id="90d76-280">DATS</span></span> | <span data-ttu-id="90d76-281">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-281">String</span></span>
<span data-ttu-id="90d76-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="90d76-282">NUMC</span></span> | <span data-ttu-id="90d76-283">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-283">String</span></span>
<span data-ttu-id="90d76-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="90d76-284">TIMS</span></span> | <span data-ttu-id="90d76-285">Строка</span><span class="sxs-lookup"><span data-stu-id="90d76-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="90d76-286">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="90d76-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="90d76-287">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="90d76-287">Map source toosink columns</span></span>
<span data-ttu-id="90d76-288">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="90d76-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="90d76-289">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="90d76-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="90d76-290">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="90d76-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="90d76-291">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="90d76-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="90d76-292">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="90d76-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="90d76-293">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="90d76-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="90d76-294">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="90d76-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="90d76-295">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="90d76-295">Performance and Tuning</span></span>
<span data-ttu-id="90d76-296">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="90d76-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
