---
title: "aaaMove данных из MySQL, с помощью фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как toomove данных из MySQL базы данных с помощью фабрики данных Azure."
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
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="efbd6-103">Перемещение данных из MySQL с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="efbd6-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="efbd6-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данных из базы данных MySQL в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="efbd6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="efbd6-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="efbd6-106">Можно скопировать данные из локальной MySQL хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="efbd6-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="efbd6-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="efbd6-108">Фабрика данных в настоящее время поддерживает только при перемещении данных MySQL хранения tooother хранилищ данных, но не для переноса данных из другого хранилища данных сохраняет tooan данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="efbd6-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="efbd6-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="efbd6-109">Prerequisites</span></span>
<span data-ttu-id="efbd6-110">Служба фабрики данных поддерживает подключения MySQL tooon локальные источники, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="efbd6-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="efbd6-111">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="efbd6-112">Требуется использовать шлюз, даже если база данных MySQL hello размещается в Azure IaaS виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="efbd6-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="efbd6-113">Hello шлюз можно установить на hello одной виртуальной Машины как данные hello хранения или же в другой виртуальной Машине, при условии, что шлюз hello могут подключаться toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="efbd6-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="efbd6-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="efbd6-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="efbd6-115">Supported versions and installation</span></span>
<span data-ttu-id="efbd6-116">Для toohello tooconnect шлюз управления данными базы данных MySQL, необходимо tooinstall hello [MySQL Connector/Net Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (версия 6.6.5 или более поздней версии) на hello же системы как hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="efbd6-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="efbd6-117">Поддерживается MySQL версии 5.1 и более.</span><span class="sxs-lookup"><span data-stu-id="efbd6-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="efbd6-118">Если ошибка попадания в «Проверка подлинности не пройдена из-за hello удаленная сторона закрыла hello транспортного потока.», рекомендуется hello tooupgrade toohigher версии MySQL Connector/Net.</span><span class="sxs-lookup"><span data-stu-id="efbd6-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="efbd6-119">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="efbd6-119">Getting started</span></span>
<span data-ttu-id="efbd6-120">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="efbd6-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="efbd6-121">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="efbd6-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="efbd6-122">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="efbd6-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="efbd6-123">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="efbd6-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="efbd6-124">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="efbd6-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="efbd6-125">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="efbd6-126">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="efbd6-127">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="efbd6-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="efbd6-128">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="efbd6-129">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="efbd6-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="efbd6-130">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="efbd6-131">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных MySQL в разделе [пример JSON: копирования данных из MySQL tooAzure больших двоичных объектов](#json-example-copy-data-from-mysql-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="efbd6-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="efbd6-132">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa MySQL хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="efbd6-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="efbd6-133">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="efbd6-133">Linked service properties</span></span>
<span data-ttu-id="efbd6-134">Hello в следующей таблице приводится описание службы конкретных tooMySQL связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="efbd6-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="efbd6-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="efbd6-135">Property</span></span> | <span data-ttu-id="efbd6-136">Описание</span><span class="sxs-lookup"><span data-stu-id="efbd6-136">Description</span></span> | <span data-ttu-id="efbd6-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efbd6-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efbd6-138">type</span><span class="sxs-lookup"><span data-stu-id="efbd6-138">type</span></span> |<span data-ttu-id="efbd6-139">свойство типа Hello должно быть присвоено: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="efbd6-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="efbd6-140">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-140">Yes</span></span> |
| <span data-ttu-id="efbd6-141">server</span><span class="sxs-lookup"><span data-stu-id="efbd6-141">server</span></span> |<span data-ttu-id="efbd6-142">Имя сервера MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="efbd6-143">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-143">Yes</span></span> |
| <span data-ttu-id="efbd6-144">database</span><span class="sxs-lookup"><span data-stu-id="efbd6-144">database</span></span> |<span data-ttu-id="efbd6-145">Имя базы данных MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="efbd6-146">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-146">Yes</span></span> |
| <span data-ttu-id="efbd6-147">schema</span><span class="sxs-lookup"><span data-stu-id="efbd6-147">schema</span></span> |<span data-ttu-id="efbd6-148">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="efbd6-149">Нет</span><span class="sxs-lookup"><span data-stu-id="efbd6-149">No</span></span> |
| <span data-ttu-id="efbd6-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="efbd6-150">authenticationType</span></span> |<span data-ttu-id="efbd6-151">Тип проверки подлинности используется база данных MySQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="efbd6-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="efbd6-152">Возможные значения: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="efbd6-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="efbd6-153">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-153">Yes</span></span> |
| <span data-ttu-id="efbd6-154">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="efbd6-154">username</span></span> |<span data-ttu-id="efbd6-155">Укажите базу данных MySQL toohello tooconnect имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="efbd6-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="efbd6-156">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-156">Yes</span></span> |
| <span data-ttu-id="efbd6-157">пароль</span><span class="sxs-lookup"><span data-stu-id="efbd6-157">password</span></span> |<span data-ttu-id="efbd6-158">Укажите пароль для учетной записи пользователя hello указанное.</span><span class="sxs-lookup"><span data-stu-id="efbd6-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="efbd6-159">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-159">Yes</span></span> |
| <span data-ttu-id="efbd6-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="efbd6-160">gatewayName</span></span> |<span data-ttu-id="efbd6-161">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="efbd6-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="efbd6-162">Да</span><span class="sxs-lookup"><span data-stu-id="efbd6-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="efbd6-163">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="efbd6-163">Dataset properties</span></span>
<span data-ttu-id="efbd6-164">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="efbd6-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="efbd6-165">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="efbd6-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="efbd6-166">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="efbd6-167">Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных MySQL) имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="efbd6-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="efbd6-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="efbd6-168">Property</span></span> | <span data-ttu-id="efbd6-169">Описание</span><span class="sxs-lookup"><span data-stu-id="efbd6-169">Description</span></span> | <span data-ttu-id="efbd6-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efbd6-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efbd6-171">tableName</span><span class="sxs-lookup"><span data-stu-id="efbd6-171">tableName</span></span> |<span data-ttu-id="efbd6-172">Имя таблицы hello в экземпляр базы данных MySQL, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="efbd6-173">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="efbd6-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="efbd6-174">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="efbd6-174">Copy activity properties</span></span>
<span data-ttu-id="efbd6-175">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="efbd6-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="efbd6-176">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="efbd6-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="efbd6-177">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="efbd6-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="efbd6-178">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="efbd6-179">Если источник в действии копирования имеет тип **RelationalSource** (включает MySQL), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="efbd6-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="efbd6-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="efbd6-180">Property</span></span> | <span data-ttu-id="efbd6-181">Описание</span><span class="sxs-lookup"><span data-stu-id="efbd6-181">Description</span></span> | <span data-ttu-id="efbd6-182">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="efbd6-182">Allowed values</span></span> | <span data-ttu-id="efbd6-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efbd6-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="efbd6-184">query</span><span class="sxs-lookup"><span data-stu-id="efbd6-184">query</span></span> |<span data-ttu-id="efbd6-185">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="efbd6-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="efbd6-186">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="efbd6-186">SQL query string.</span></span> <span data-ttu-id="efbd6-187">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="efbd6-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="efbd6-188">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="efbd6-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="efbd6-189">Пример JSON: копирование данных из MySQL tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="efbd6-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="efbd6-190">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="efbd6-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="efbd6-191">В нем показано, как toocopy данных из MySQL локальной базы данных tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="efbd6-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="efbd6-192">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="efbd6-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efbd6-193">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="efbd6-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="efbd6-194">Он не включает пошаговые инструкции по созданию фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="efbd6-195">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="efbd6-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="efbd6-196">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="efbd6-197">Связанная служба типа [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efbd6-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="efbd6-198">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efbd6-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="efbd6-199">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efbd6-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="efbd6-200">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efbd6-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="efbd6-201">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efbd6-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="efbd6-202">Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных MySQL каждый час.</span><span class="sxs-lookup"><span data-stu-id="efbd6-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="efbd6-203">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="efbd6-204">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="efbd6-205">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="efbd6-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="efbd6-206">**Связанная служба MySQL:**</span><span class="sxs-lookup"><span data-stu-id="efbd6-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="efbd6-207">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="efbd6-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="efbd6-208">**Входной набор данных MySQL:**</span><span class="sxs-lookup"><span data-stu-id="efbd6-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="efbd6-209">Образец Hello предполагается создания таблицы «MyTable» в MySQL и она содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="efbd6-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="efbd6-210">Параметр «external»: «true» уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="efbd6-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="efbd6-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="efbd6-212">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="efbd6-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="efbd6-213">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="efbd6-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="efbd6-214">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="efbd6-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="efbd6-215">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="efbd6-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="efbd6-216">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="efbd6-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="efbd6-217">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="efbd6-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="efbd6-218">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="efbd6-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="efbd6-219">Сопоставление типов для MySQL</span><span class="sxs-lookup"><span data-stu-id="efbd6-219">Type mapping for MySQL</span></span>
<span data-ttu-id="efbd6-220">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:</span><span class="sxs-lookup"><span data-stu-id="efbd6-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="efbd6-221">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="efbd6-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="efbd6-222">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="efbd6-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="efbd6-223">При перемещении данных tooMySQL, hello следующие сопоставления используются типы too.NET типы MySQL.</span><span class="sxs-lookup"><span data-stu-id="efbd6-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="efbd6-224">Тип базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="efbd6-224">MySQL Database type</span></span> | <span data-ttu-id="efbd6-225">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="efbd6-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="efbd6-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-226">bigint unsigned</span></span> |<span data-ttu-id="efbd6-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="efbd6-227">Decimal</span></span> |
| <span data-ttu-id="efbd6-228">bigint</span><span class="sxs-lookup"><span data-stu-id="efbd6-228">bigint</span></span> |<span data-ttu-id="efbd6-229">Int64</span><span class="sxs-lookup"><span data-stu-id="efbd6-229">Int64</span></span> |
| <span data-ttu-id="efbd6-230">bit</span><span class="sxs-lookup"><span data-stu-id="efbd6-230">bit</span></span> |<span data-ttu-id="efbd6-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="efbd6-231">Decimal</span></span> |
| <span data-ttu-id="efbd6-232">blob-объект</span><span class="sxs-lookup"><span data-stu-id="efbd6-232">blob</span></span> |<span data-ttu-id="efbd6-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efbd6-233">Byte[]</span></span> |
| <span data-ttu-id="efbd6-234">bool</span><span class="sxs-lookup"><span data-stu-id="efbd6-234">bool</span></span> |<span data-ttu-id="efbd6-235">Логический</span><span class="sxs-lookup"><span data-stu-id="efbd6-235">Boolean</span></span> |
| <span data-ttu-id="efbd6-236">char;</span><span class="sxs-lookup"><span data-stu-id="efbd6-236">char</span></span> |<span data-ttu-id="efbd6-237">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-237">String</span></span> |
| <span data-ttu-id="efbd6-238">дата</span><span class="sxs-lookup"><span data-stu-id="efbd6-238">date</span></span> |<span data-ttu-id="efbd6-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="efbd6-239">Datetime</span></span> |
| <span data-ttu-id="efbd6-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="efbd6-240">datetime</span></span> |<span data-ttu-id="efbd6-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="efbd6-241">Datetime</span></span> |
| <span data-ttu-id="efbd6-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="efbd6-242">decimal</span></span> |<span data-ttu-id="efbd6-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="efbd6-243">Decimal</span></span> |
| <span data-ttu-id="efbd6-244">double precision</span><span class="sxs-lookup"><span data-stu-id="efbd6-244">double precision</span></span> |<span data-ttu-id="efbd6-245">Double</span><span class="sxs-lookup"><span data-stu-id="efbd6-245">Double</span></span> |
| <span data-ttu-id="efbd6-246">Double</span><span class="sxs-lookup"><span data-stu-id="efbd6-246">double</span></span> |<span data-ttu-id="efbd6-247">Double</span><span class="sxs-lookup"><span data-stu-id="efbd6-247">Double</span></span> |
| <span data-ttu-id="efbd6-248">enum</span><span class="sxs-lookup"><span data-stu-id="efbd6-248">enum</span></span> |<span data-ttu-id="efbd6-249">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-249">String</span></span> |
| <span data-ttu-id="efbd6-250">float;</span><span class="sxs-lookup"><span data-stu-id="efbd6-250">float</span></span> |<span data-ttu-id="efbd6-251">Single</span><span class="sxs-lookup"><span data-stu-id="efbd6-251">Single</span></span> |
| <span data-ttu-id="efbd6-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-252">int unsigned</span></span> |<span data-ttu-id="efbd6-253">Int64</span><span class="sxs-lookup"><span data-stu-id="efbd6-253">Int64</span></span> |
| <span data-ttu-id="efbd6-254">int</span><span class="sxs-lookup"><span data-stu-id="efbd6-254">int</span></span> |<span data-ttu-id="efbd6-255">Int32</span><span class="sxs-lookup"><span data-stu-id="efbd6-255">Int32</span></span> |
| <span data-ttu-id="efbd6-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-256">integer unsigned</span></span> |<span data-ttu-id="efbd6-257">Int64</span><span class="sxs-lookup"><span data-stu-id="efbd6-257">Int64</span></span> |
| <span data-ttu-id="efbd6-258">целое число</span><span class="sxs-lookup"><span data-stu-id="efbd6-258">integer</span></span> |<span data-ttu-id="efbd6-259">Int32</span><span class="sxs-lookup"><span data-stu-id="efbd6-259">Int32</span></span> |
| <span data-ttu-id="efbd6-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="efbd6-260">long varbinary</span></span> |<span data-ttu-id="efbd6-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efbd6-261">Byte[]</span></span> |
| <span data-ttu-id="efbd6-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="efbd6-262">long varchar</span></span> |<span data-ttu-id="efbd6-263">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-263">String</span></span> |
| <span data-ttu-id="efbd6-264">longblob</span><span class="sxs-lookup"><span data-stu-id="efbd6-264">longblob</span></span> |<span data-ttu-id="efbd6-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efbd6-265">Byte[]</span></span> |
| <span data-ttu-id="efbd6-266">longtext</span><span class="sxs-lookup"><span data-stu-id="efbd6-266">longtext</span></span> |<span data-ttu-id="efbd6-267">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-267">String</span></span> |
| <span data-ttu-id="efbd6-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="efbd6-268">mediumblob</span></span> |<span data-ttu-id="efbd6-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efbd6-269">Byte[]</span></span> |
| <span data-ttu-id="efbd6-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-270">mediumint unsigned</span></span> |<span data-ttu-id="efbd6-271">Int64</span><span class="sxs-lookup"><span data-stu-id="efbd6-271">Int64</span></span> |
| <span data-ttu-id="efbd6-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="efbd6-272">mediumint</span></span> |<span data-ttu-id="efbd6-273">Int32</span><span class="sxs-lookup"><span data-stu-id="efbd6-273">Int32</span></span> |
| <span data-ttu-id="efbd6-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="efbd6-274">mediumtext</span></span> |<span data-ttu-id="efbd6-275">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-275">String</span></span> |
| <span data-ttu-id="efbd6-276">numeric</span><span class="sxs-lookup"><span data-stu-id="efbd6-276">numeric</span></span> |<span data-ttu-id="efbd6-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="efbd6-277">Decimal</span></span> |
| <span data-ttu-id="efbd6-278">real;</span><span class="sxs-lookup"><span data-stu-id="efbd6-278">real</span></span> |<span data-ttu-id="efbd6-279">Double</span><span class="sxs-lookup"><span data-stu-id="efbd6-279">Double</span></span> |
| <span data-ttu-id="efbd6-280">set</span><span class="sxs-lookup"><span data-stu-id="efbd6-280">set</span></span> |<span data-ttu-id="efbd6-281">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-281">String</span></span> |
| <span data-ttu-id="efbd6-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-282">smallint unsigned</span></span> |<span data-ttu-id="efbd6-283">Int32</span><span class="sxs-lookup"><span data-stu-id="efbd6-283">Int32</span></span> |
| <span data-ttu-id="efbd6-284">smallint;</span><span class="sxs-lookup"><span data-stu-id="efbd6-284">smallint</span></span> |<span data-ttu-id="efbd6-285">Int16</span><span class="sxs-lookup"><span data-stu-id="efbd6-285">Int16</span></span> |
| <span data-ttu-id="efbd6-286">text</span><span class="sxs-lookup"><span data-stu-id="efbd6-286">text</span></span> |<span data-ttu-id="efbd6-287">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-287">String</span></span> |
| <span data-ttu-id="efbd6-288">time</span><span class="sxs-lookup"><span data-stu-id="efbd6-288">time</span></span> |<span data-ttu-id="efbd6-289">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="efbd6-289">TimeSpan</span></span> |
| <span data-ttu-id="efbd6-290">Timestamp</span><span class="sxs-lookup"><span data-stu-id="efbd6-290">timestamp</span></span> |<span data-ttu-id="efbd6-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="efbd6-291">Datetime</span></span> |
| <span data-ttu-id="efbd6-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="efbd6-292">tinyblob</span></span> |<span data-ttu-id="efbd6-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="efbd6-293">Byte[]</span></span> |
| <span data-ttu-id="efbd6-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="efbd6-294">tinyint unsigned</span></span> |<span data-ttu-id="efbd6-295">Int16</span><span class="sxs-lookup"><span data-stu-id="efbd6-295">Int16</span></span> |
| <span data-ttu-id="efbd6-296">tinyint;</span><span class="sxs-lookup"><span data-stu-id="efbd6-296">tinyint</span></span> |<span data-ttu-id="efbd6-297">Int16</span><span class="sxs-lookup"><span data-stu-id="efbd6-297">Int16</span></span> |
| <span data-ttu-id="efbd6-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="efbd6-298">tinytext</span></span> |<span data-ttu-id="efbd6-299">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-299">String</span></span> |
| <span data-ttu-id="efbd6-300">varchar.</span><span class="sxs-lookup"><span data-stu-id="efbd6-300">varchar</span></span> |<span data-ttu-id="efbd6-301">Строка</span><span class="sxs-lookup"><span data-stu-id="efbd6-301">String</span></span> |
| <span data-ttu-id="efbd6-302">year</span><span class="sxs-lookup"><span data-stu-id="efbd6-302">year</span></span> |<span data-ttu-id="efbd6-303">int</span><span class="sxs-lookup"><span data-stu-id="efbd6-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="efbd6-304">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="efbd6-304">Map source toosink columns</span></span>
<span data-ttu-id="efbd6-305">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="efbd6-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="efbd6-306">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="efbd6-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="efbd6-307">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="efbd6-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="efbd6-308">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="efbd6-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="efbd6-309">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="efbd6-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="efbd6-310">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="efbd6-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="efbd6-311">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="efbd6-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="efbd6-312">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="efbd6-312">Performance and Tuning</span></span>
<span data-ttu-id="efbd6-313">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="efbd6-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
