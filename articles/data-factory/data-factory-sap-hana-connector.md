---
title: "aaaMove данных из SAP HANA, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данных из SAP HANA, с помощью фабрики данных Azure."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="0941c-103">Перемещение данных из SAP HANA с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="0941c-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="0941c-104">В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure с локальным SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0941c-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="0941c-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="0941c-106">Можно скопировать данные из локальной SAP HANA хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="0941c-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="0941c-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0941c-108">Фабрика данных в настоящее время поддерживает только для перемещения хранятся данные из объекта данных SAP HANA tooother, но не для перемещения данных из других данных хранит tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0941c-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0941c-109">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="0941c-109">Supported versions and installation</span></span>
<span data-ttu-id="0941c-110">Этот соединитель поддерживает все версии базы данных SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0941c-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="0941c-111">Он поддерживает копирование данных из информационных моделей HANA (например, представлений Analytic и Calculation) и таблиц со строками и столбцами с помощью SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="0941c-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="0941c-112">tooenable hello подключения toohello экземпляра SAP HANA, установите hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="0941c-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="0941c-113">**Шлюз управления данными**: подключение локальной tooon данных поддерживает службы фабрики данных хранилища (включая SAP HANA) с помощью компонента вызывается шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="0941c-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="0941c-114">toolearn о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. в разделе [перемещение данных между локальными данными хранения хранилища данных toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0941c-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0941c-115">Требуется использовать шлюз, даже если hello SAP HANA размещается в Azure IaaS виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="0941c-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="0941c-116">Hello шлюз можно установить на hello одной виртуальной Машины как данные hello хранения или же в другой виртуальной Машине, при условии, что шлюз hello могут подключаться toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="0941c-117">**Драйвер SAP HANA ODBC** на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="0941c-118">Можно загрузить драйвер SAP HANA ODBC hello hello [центра загрузки программного обеспечения SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="0941c-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="0941c-119">Поиска с ключевым словом hello **SAP HANA КЛИЕНТА для Windows**.</span><span class="sxs-lookup"><span data-stu-id="0941c-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="0941c-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="0941c-120">Getting started</span></span>
<span data-ttu-id="0941c-121">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="0941c-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0941c-122">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="0941c-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0941c-123">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="0941c-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="0941c-124">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="0941c-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0941c-125">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="0941c-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0941c-126">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="0941c-127">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="0941c-128">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="0941c-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="0941c-129">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0941c-130">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="0941c-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0941c-131">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0941c-132">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из SAP HANA в локальной среде, см. [пример JSON: копирование данных из SAP HANA tooAzure больших двоичных объектов](#json-example-copy-data-from-sap-hana-to-azure-blob) данной статьи.</span><span class="sxs-lookup"><span data-stu-id="0941c-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0941c-133">Hello в следующих разделах подробно свойства JSON, хранилище данных SAP HANA tooan определенных сущностей используется toodefine фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="0941c-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0941c-134">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="0941c-134">Linked service properties</span></span>
<span data-ttu-id="0941c-135">в следующей таблице Hello предоставляет описание tooSAP HANA определенные элементы JSON связанной службы.</span><span class="sxs-lookup"><span data-stu-id="0941c-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="0941c-136">Свойство</span><span class="sxs-lookup"><span data-stu-id="0941c-136">Property</span></span> | <span data-ttu-id="0941c-137">Описание</span><span class="sxs-lookup"><span data-stu-id="0941c-137">Description</span></span> | <span data-ttu-id="0941c-138">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="0941c-138">Allowed values</span></span> | <span data-ttu-id="0941c-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0941c-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0941c-140">server</span><span class="sxs-lookup"><span data-stu-id="0941c-140">server</span></span> | <span data-ttu-id="0941c-141">Имя сервера hello, на какие hello SAP HANA расположен экземпляр.</span><span class="sxs-lookup"><span data-stu-id="0941c-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="0941c-142">Если ваш сервер использует настроенный порт, укажите `server:port`.</span><span class="sxs-lookup"><span data-stu-id="0941c-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="0941c-143">строка</span><span class="sxs-lookup"><span data-stu-id="0941c-143">string</span></span> | <span data-ttu-id="0941c-144">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-144">Yes</span></span>
<span data-ttu-id="0941c-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0941c-145">authenticationType</span></span> | <span data-ttu-id="0941c-146">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0941c-146">Type of authentication.</span></span> | <span data-ttu-id="0941c-147">string.</span><span class="sxs-lookup"><span data-stu-id="0941c-147">string.</span></span> <span data-ttu-id="0941c-148">Basic или Windows.</span><span class="sxs-lookup"><span data-stu-id="0941c-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="0941c-149">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-149">Yes</span></span> 
<span data-ttu-id="0941c-150">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="0941c-150">username</span></span> | <span data-ttu-id="0941c-151">Имя пользователя hello с сервера SAP toohello доступа</span><span class="sxs-lookup"><span data-stu-id="0941c-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="0941c-152">string</span><span class="sxs-lookup"><span data-stu-id="0941c-152">string</span></span> | <span data-ttu-id="0941c-153">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-153">Yes</span></span>
<span data-ttu-id="0941c-154">пароль</span><span class="sxs-lookup"><span data-stu-id="0941c-154">password</span></span> | <span data-ttu-id="0941c-155">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-155">Password for hello user.</span></span> | <span data-ttu-id="0941c-156">string</span><span class="sxs-lookup"><span data-stu-id="0941c-156">string</span></span> | <span data-ttu-id="0941c-157">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-157">Yes</span></span>
<span data-ttu-id="0941c-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0941c-158">gatewayName</span></span> | <span data-ttu-id="0941c-159">Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP HANA экземпляр.</span><span class="sxs-lookup"><span data-stu-id="0941c-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="0941c-160">string</span><span class="sxs-lookup"><span data-stu-id="0941c-160">string</span></span> | <span data-ttu-id="0941c-161">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-161">Yes</span></span>
<span data-ttu-id="0941c-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0941c-162">encryptedCredential</span></span> | <span data-ttu-id="0941c-163">Строка Hello шифрования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-163">hello encrypted credential string.</span></span> | <span data-ttu-id="0941c-164">string</span><span class="sxs-lookup"><span data-stu-id="0941c-164">string</span></span> | <span data-ttu-id="0941c-165">Нет</span><span class="sxs-lookup"><span data-stu-id="0941c-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="0941c-166">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="0941c-166">Dataset properties</span></span>
<span data-ttu-id="0941c-167">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0941c-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0941c-168">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0941c-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0941c-169">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0941c-170">Свойства конкретного типа, не поддерживается для набора данных SAP HANA hello типа **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0941c-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="0941c-171">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="0941c-171">Copy activity properties</span></span>
<span data-ttu-id="0941c-172">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0941c-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0941c-173">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="0941c-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="0941c-174">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="0941c-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0941c-175">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="0941c-176">Если источник в действии копирования имеет тип **RelationalSource** (включает SAP HANA), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="0941c-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0941c-177">Свойство</span><span class="sxs-lookup"><span data-stu-id="0941c-177">Property</span></span> | <span data-ttu-id="0941c-178">Описание</span><span class="sxs-lookup"><span data-stu-id="0941c-178">Description</span></span> | <span data-ttu-id="0941c-179">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="0941c-179">Allowed values</span></span> | <span data-ttu-id="0941c-180">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0941c-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0941c-181">query</span><span class="sxs-lookup"><span data-stu-id="0941c-181">query</span></span> | <span data-ttu-id="0941c-182">Указывает tooread hello SQL запроса данных из экземпляра SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="0941c-183">SQL-запрос.</span><span class="sxs-lookup"><span data-stu-id="0941c-183">SQL query.</span></span> | <span data-ttu-id="0941c-184">Да</span><span class="sxs-lookup"><span data-stu-id="0941c-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="0941c-185">Пример JSON: копирование данных из SAP HANA tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="0941c-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="0941c-186">Hello следующий пример предоставляет образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0941c-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0941c-187">В этом примере показано, как данные toocopy из tooan SAP HANA локального хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0941c-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="0941c-188">Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello в списке [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0941c-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0941c-189">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="0941c-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="0941c-190">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="0941c-191">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="0941c-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="0941c-192">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="0941c-193">Связанная служба типа [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0941c-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="0941c-194">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0941c-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0941c-195">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0941c-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0941c-196">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0941c-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0941c-197">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0941c-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0941c-198">Образец Hello копирует данные из tooan экземпляра SAP HANA BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="0941c-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="0941c-199">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="0941c-200">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="0941c-201">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0941c-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="0941c-202">Связанная служба SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0941c-202">SAP HANA linked service</span></span>
<span data-ttu-id="0941c-203">Ссылки на службы связаны toohello данных SAP HANA экземпляр фабрики.</span><span class="sxs-lookup"><span data-stu-id="0941c-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="0941c-204">Hello свойство type установлено слишком**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="0941c-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="0941c-205">Hello typeProperties раздел содержит сведения о соединении для экземпляра SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="0941c-206">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="0941c-206">Azure Storage linked service</span></span>
<span data-ttu-id="0941c-207">Ссылки на службы связаны фабрики данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0941c-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="0941c-208">Hello свойство type установлено слишком**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0941c-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="0941c-209">Hello typeProperties раздел содержит сведения о соединении для hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0941c-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="0941c-210">Входной набор данных SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0941c-210">SAP HANA input dataset</span></span>

<span data-ttu-id="0941c-211">Этот набор данных определяет набор данных SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="0941c-212">Задание типа hello фабрики данных набора данных hello слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0941c-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="0941c-213">В настоящее время какие-либо свойства типа для набора данных SAP HANA не указываются пользователем.</span><span class="sxs-lookup"><span data-stu-id="0941c-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="0941c-214">запрос Hello в hello определение действия копирования указывает, какие tooread данных из экземпляра SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="0941c-215">Установка значения внешнего свойства tootrue сообщает hello служба фабрики данных, этой таблицы hello является фабрикой toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="0941c-216">Свойства частоту и интервал определяет расписание hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="0941c-217">В этом случае hello считывании данных из экземпляра SAP HANA hello каждый час.</span><span class="sxs-lookup"><span data-stu-id="0941c-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0941c-218">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="0941c-218">Azure Blob output dataset</span></span>
<span data-ttu-id="0941c-219">Этот набор данных определяет hello выходной BLOB-объектов Azure, набор данных.</span><span class="sxs-lookup"><span data-stu-id="0941c-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="0941c-220">свойство типа Hello задается tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="0941c-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="0941c-221">раздел typeProperties Hello содержит, где хранятся данные hello, скопированные из экземпляра SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="0941c-222">Hello записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="0941c-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0941c-223">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="0941c-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0941c-224">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="0941c-225">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="0941c-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="0941c-226">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="0941c-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0941c-227">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** (для источника SAP HANA) и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0941c-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="0941c-228">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="0941c-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="0941c-229">Сопоставление типов для SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0941c-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="0941c-230">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:</span><span class="sxs-lookup"><span data-stu-id="0941c-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="0941c-231">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="0941c-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="0941c-232">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="0941c-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="0941c-233">При перемещении данных из SAP HANA из SAP HANA типы too.NET типы используются следующие сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="0941c-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="0941c-234">Тип SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0941c-234">SAP HANA Type</span></span> | <span data-ttu-id="0941c-235">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="0941c-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="0941c-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="0941c-236">TINYINT</span></span> | <span data-ttu-id="0941c-237">Byte</span><span class="sxs-lookup"><span data-stu-id="0941c-237">Byte</span></span>
<span data-ttu-id="0941c-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="0941c-238">SMALLINT</span></span> | <span data-ttu-id="0941c-239">Int16</span><span class="sxs-lookup"><span data-stu-id="0941c-239">Int16</span></span>
<span data-ttu-id="0941c-240">INT</span><span class="sxs-lookup"><span data-stu-id="0941c-240">INT</span></span> | <span data-ttu-id="0941c-241">Int32</span><span class="sxs-lookup"><span data-stu-id="0941c-241">Int32</span></span>
<span data-ttu-id="0941c-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="0941c-242">BIGINT</span></span> | <span data-ttu-id="0941c-243">Int64</span><span class="sxs-lookup"><span data-stu-id="0941c-243">Int64</span></span>
<span data-ttu-id="0941c-244">REAL</span><span class="sxs-lookup"><span data-stu-id="0941c-244">REAL</span></span> | <span data-ttu-id="0941c-245">Single</span><span class="sxs-lookup"><span data-stu-id="0941c-245">Single</span></span>
<span data-ttu-id="0941c-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="0941c-246">DOUBLE</span></span> | <span data-ttu-id="0941c-247">Single</span><span class="sxs-lookup"><span data-stu-id="0941c-247">Single</span></span>
<span data-ttu-id="0941c-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0941c-248">DECIMAL</span></span> | <span data-ttu-id="0941c-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="0941c-249">Decimal</span></span>
<span data-ttu-id="0941c-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="0941c-250">BOOLEAN</span></span> | <span data-ttu-id="0941c-251">Byte</span><span class="sxs-lookup"><span data-stu-id="0941c-251">Byte</span></span>
<span data-ttu-id="0941c-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="0941c-252">VARCHAR</span></span> | <span data-ttu-id="0941c-253">string</span><span class="sxs-lookup"><span data-stu-id="0941c-253">String</span></span>
<span data-ttu-id="0941c-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="0941c-254">NVARCHAR</span></span> | <span data-ttu-id="0941c-255">Строка</span><span class="sxs-lookup"><span data-stu-id="0941c-255">String</span></span>
<span data-ttu-id="0941c-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="0941c-256">CLOB</span></span> | <span data-ttu-id="0941c-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0941c-257">Byte[]</span></span>
<span data-ttu-id="0941c-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="0941c-258">ALPHANUM</span></span> | <span data-ttu-id="0941c-259">string</span><span class="sxs-lookup"><span data-stu-id="0941c-259">String</span></span>
<span data-ttu-id="0941c-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="0941c-260">BLOB</span></span> | <span data-ttu-id="0941c-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0941c-261">Byte[]</span></span>
<span data-ttu-id="0941c-262">DATE</span><span class="sxs-lookup"><span data-stu-id="0941c-262">DATE</span></span> | <span data-ttu-id="0941c-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="0941c-263">DateTime</span></span>
<span data-ttu-id="0941c-264">TIME</span><span class="sxs-lookup"><span data-stu-id="0941c-264">TIME</span></span> | <span data-ttu-id="0941c-265">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="0941c-265">TimeSpan</span></span>
<span data-ttu-id="0941c-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="0941c-266">TIMESTAMP</span></span> | <span data-ttu-id="0941c-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="0941c-267">DateTime</span></span>
<span data-ttu-id="0941c-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="0941c-268">SECONDDATE</span></span> | <span data-ttu-id="0941c-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="0941c-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="0941c-270">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="0941c-270">Known limitations</span></span>
<span data-ttu-id="0941c-271">Существует несколько известных ограничений, действующих при копировании данных из SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0941c-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="0941c-272">Строки NVARCHAR, усеченных toomaximum длиной 4000 символов Юникода</span><span class="sxs-lookup"><span data-stu-id="0941c-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="0941c-273">SMALLDECIMAL не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0941c-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="0941c-274">VARBINARY не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0941c-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="0941c-275">Допустимый диапазон дат: 30.12.1899–31.12.9999.</span><span class="sxs-lookup"><span data-stu-id="0941c-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="0941c-276">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="0941c-276">Map source toosink columns</span></span>
<span data-ttu-id="0941c-277">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0941c-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0941c-278">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="0941c-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="0941c-279">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="0941c-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="0941c-280">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="0941c-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0941c-281">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="0941c-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0941c-282">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="0941c-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0941c-283">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="0941c-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0941c-284">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="0941c-284">Performance and Tuning</span></span>
<span data-ttu-id="0941c-285">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="0941c-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
