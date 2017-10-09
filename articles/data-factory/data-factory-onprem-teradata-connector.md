---
title: "aaaMove данных Teradata, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о соединителя для Teradata для hello служба фабрики данных, которая позволяет перемещать данные из базы данных Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="2463f-103">Перемещение данных из Teradata с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="2463f-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="2463f-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="2463f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="2463f-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2463f-106">Можно скопировать данные из локальной Teradata хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="2463f-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="2463f-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2463f-108">Фабрика данных в настоящее время поддерживает только при перемещении данных Teradata хранения tooother хранилищ данных, но не для перемещения данных из других данных Teradata tooa хранилищ данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="2463f-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2463f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2463f-109">Prerequisites</span></span>
<span data-ttu-id="2463f-110">Фабрики данных поддерживает подключения источники Teradata tooon организациями через hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="2463f-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="2463f-111">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="2463f-112">Даже если hello Teradata размещается на виртуальной Машине Azure IaaS требуется шлюз.</span><span class="sxs-lookup"><span data-stu-id="2463f-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="2463f-113">Hello шлюз можно установить на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="2463f-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="2463f-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="2463f-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="2463f-115">Supported versions and installation</span></span>
<span data-ttu-id="2463f-116">Для toohello tooconnect шлюз управления данными базы данных Teradata, необходимо tooinstall hello [поставщик данных .NET для Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) версии 14 или выше на hello же системы как hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="2463f-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="2463f-117">Поддерживается Teradata версии 12 и более.</span><span class="sxs-lookup"><span data-stu-id="2463f-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2463f-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="2463f-118">Getting started</span></span>
<span data-ttu-id="2463f-119">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="2463f-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2463f-120">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="2463f-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2463f-121">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="2463f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2463f-122">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="2463f-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2463f-123">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="2463f-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2463f-124">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2463f-125">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2463f-126">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="2463f-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2463f-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2463f-128">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="2463f-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2463f-129">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2463f-130">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных Teradata см. в разделе [JSON пример: копирование данных из tooAzure Teradata большого двоичного объекта](#json-example-copy-data-from-teradata-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="2463f-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2463f-131">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa Teradata хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="2463f-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2463f-132">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="2463f-132">Linked service properties</span></span>
<span data-ttu-id="2463f-133">Hello в следующей таблице приводится описание службы конкретных tooTeradata связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="2463f-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="2463f-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="2463f-134">Property</span></span> | <span data-ttu-id="2463f-135">Описание</span><span class="sxs-lookup"><span data-stu-id="2463f-135">Description</span></span> | <span data-ttu-id="2463f-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2463f-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2463f-137">type</span><span class="sxs-lookup"><span data-stu-id="2463f-137">type</span></span> |<span data-ttu-id="2463f-138">свойство типа Hello должно быть присвоено: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="2463f-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="2463f-139">Да</span><span class="sxs-lookup"><span data-stu-id="2463f-139">Yes</span></span> |
| <span data-ttu-id="2463f-140">server</span><span class="sxs-lookup"><span data-stu-id="2463f-140">server</span></span> |<span data-ttu-id="2463f-141">Имя сервера Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="2463f-142">Да</span><span class="sxs-lookup"><span data-stu-id="2463f-142">Yes</span></span> |
| <span data-ttu-id="2463f-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2463f-143">authenticationType</span></span> |<span data-ttu-id="2463f-144">Тип проверки подлинности используется база данных Teradata toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2463f-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="2463f-145">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="2463f-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2463f-146">Да</span><span class="sxs-lookup"><span data-stu-id="2463f-146">Yes</span></span> |
| <span data-ttu-id="2463f-147">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="2463f-147">username</span></span> |<span data-ttu-id="2463f-148">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="2463f-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="2463f-149">Нет</span><span class="sxs-lookup"><span data-stu-id="2463f-149">No</span></span> |
| <span data-ttu-id="2463f-150">пароль</span><span class="sxs-lookup"><span data-stu-id="2463f-150">password</span></span> |<span data-ttu-id="2463f-151">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="2463f-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="2463f-152">Нет</span><span class="sxs-lookup"><span data-stu-id="2463f-152">No</span></span> |
| <span data-ttu-id="2463f-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2463f-153">gatewayName</span></span> |<span data-ttu-id="2463f-154">Имя шлюза hello, hello служба фабрики данных следует использовать базы данных Teradata tooconnect toohello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="2463f-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="2463f-155">Да</span><span class="sxs-lookup"><span data-stu-id="2463f-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2463f-156">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="2463f-156">Dataset properties</span></span>
<span data-ttu-id="2463f-157">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="2463f-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2463f-158">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2463f-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2463f-159">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2463f-160">В настоящее время нет свойств типа поддерживается для набора данных Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="2463f-161">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="2463f-161">Copy activity properties</span></span>
<span data-ttu-id="2463f-162">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="2463f-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2463f-163">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="2463f-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="2463f-164">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="2463f-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2463f-165">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2463f-166">Если источник hello имеет тип **RelationalSource** (включает Teradata), hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="2463f-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="2463f-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="2463f-167">Property</span></span> | <span data-ttu-id="2463f-168">Описание</span><span class="sxs-lookup"><span data-stu-id="2463f-168">Description</span></span> | <span data-ttu-id="2463f-169">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2463f-169">Allowed values</span></span> | <span data-ttu-id="2463f-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2463f-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2463f-171">query</span><span class="sxs-lookup"><span data-stu-id="2463f-171">query</span></span> |<span data-ttu-id="2463f-172">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="2463f-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2463f-173">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="2463f-173">SQL query string.</span></span> <span data-ttu-id="2463f-174">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="2463f-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="2463f-175">Да</span><span class="sxs-lookup"><span data-stu-id="2463f-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="2463f-176">Пример JSON: копирование данных из tooAzure Teradata больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="2463f-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="2463f-177">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2463f-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2463f-178">Они показывают как toocopy данные из tooAzure Teradata хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2463f-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="2463f-179">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2463f-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="2463f-180">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="2463f-181">Связанная служба типа [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2463f-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="2463f-182">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2463f-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2463f-183">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2463f-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2463f-184">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2463f-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2463f-185">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2463f-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2463f-186">Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных Teradata каждый час.</span><span class="sxs-lookup"><span data-stu-id="2463f-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="2463f-187">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2463f-188">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="2463f-189">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="2463f-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2463f-190">**Связанная служба Teradata**</span><span class="sxs-lookup"><span data-stu-id="2463f-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="2463f-191">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="2463f-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="2463f-192">**Входной набор данных Teradata**</span><span class="sxs-lookup"><span data-stu-id="2463f-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="2463f-193">Образец Hello предполагается создания таблицы «MyTable» в Teradata, и она содержит столбец с именем «timestamp» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="2463f-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="2463f-194">Параметр «external»: true уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="2463f-195">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="2463f-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2463f-196">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="2463f-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2463f-197">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="2463f-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2463f-198">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="2463f-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="2463f-199">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="2463f-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="2463f-200">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="2463f-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="2463f-201">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2463f-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2463f-202">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="2463f-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="2463f-203">Сопоставление типов для Teradata</span><span class="sxs-lookup"><span data-stu-id="2463f-203">Type mapping for Teradata</span></span>
<span data-ttu-id="2463f-204">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статья hello действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="2463f-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="2463f-205">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="2463f-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2463f-206">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="2463f-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2463f-207">При перемещении данных tooTeradata, hello следующие сопоставления используются из типа too.NET типа Teradata.</span><span class="sxs-lookup"><span data-stu-id="2463f-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="2463f-208">Тип базы данных Teradata</span><span class="sxs-lookup"><span data-stu-id="2463f-208">Teradata Database type</span></span> | <span data-ttu-id="2463f-209">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2463f-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="2463f-210">Char</span><span class="sxs-lookup"><span data-stu-id="2463f-210">Char</span></span> |<span data-ttu-id="2463f-211">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-211">String</span></span> |
| <span data-ttu-id="2463f-212">Clob</span><span class="sxs-lookup"><span data-stu-id="2463f-212">Clob</span></span> |<span data-ttu-id="2463f-213">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-213">String</span></span> |
| <span data-ttu-id="2463f-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="2463f-214">Graphic</span></span> |<span data-ttu-id="2463f-215">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-215">String</span></span> |
| <span data-ttu-id="2463f-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="2463f-216">VarChar</span></span> |<span data-ttu-id="2463f-217">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-217">String</span></span> |
| <span data-ttu-id="2463f-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="2463f-218">VarGraphic</span></span> |<span data-ttu-id="2463f-219">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-219">String</span></span> |
| <span data-ttu-id="2463f-220">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="2463f-220">Blob</span></span> |<span data-ttu-id="2463f-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2463f-221">Byte[]</span></span> |
| <span data-ttu-id="2463f-222">Byte</span><span class="sxs-lookup"><span data-stu-id="2463f-222">Byte</span></span> |<span data-ttu-id="2463f-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2463f-223">Byte[]</span></span> |
| <span data-ttu-id="2463f-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="2463f-224">VarByte</span></span> |<span data-ttu-id="2463f-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2463f-225">Byte[]</span></span> |
| <span data-ttu-id="2463f-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="2463f-226">BigInt</span></span> |<span data-ttu-id="2463f-227">Int64</span><span class="sxs-lookup"><span data-stu-id="2463f-227">Int64</span></span> |
| <span data-ttu-id="2463f-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="2463f-228">ByteInt</span></span> |<span data-ttu-id="2463f-229">Int16</span><span class="sxs-lookup"><span data-stu-id="2463f-229">Int16</span></span> |
| <span data-ttu-id="2463f-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="2463f-230">Decimal</span></span> |<span data-ttu-id="2463f-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="2463f-231">Decimal</span></span> |
| <span data-ttu-id="2463f-232">Double</span><span class="sxs-lookup"><span data-stu-id="2463f-232">Double</span></span> |<span data-ttu-id="2463f-233">Double</span><span class="sxs-lookup"><span data-stu-id="2463f-233">Double</span></span> |
| <span data-ttu-id="2463f-234">Число</span><span class="sxs-lookup"><span data-stu-id="2463f-234">Integer</span></span> |<span data-ttu-id="2463f-235">Int32</span><span class="sxs-lookup"><span data-stu-id="2463f-235">Int32</span></span> |
| <span data-ttu-id="2463f-236">Число</span><span class="sxs-lookup"><span data-stu-id="2463f-236">Number</span></span> |<span data-ttu-id="2463f-237">Double</span><span class="sxs-lookup"><span data-stu-id="2463f-237">Double</span></span> |
| <span data-ttu-id="2463f-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2463f-238">SmallInt</span></span> |<span data-ttu-id="2463f-239">Int16</span><span class="sxs-lookup"><span data-stu-id="2463f-239">Int16</span></span> |
| <span data-ttu-id="2463f-240">Дата</span><span class="sxs-lookup"><span data-stu-id="2463f-240">Date</span></span> |<span data-ttu-id="2463f-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="2463f-241">DateTime</span></span> |
| <span data-ttu-id="2463f-242">Время</span><span class="sxs-lookup"><span data-stu-id="2463f-242">Time</span></span> |<span data-ttu-id="2463f-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-243">TimeSpan</span></span> |
| <span data-ttu-id="2463f-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="2463f-244">Time With Time Zone</span></span> |<span data-ttu-id="2463f-245">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-245">String</span></span> |
| <span data-ttu-id="2463f-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2463f-246">Timestamp</span></span> |<span data-ttu-id="2463f-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="2463f-247">DateTime</span></span> |
| <span data-ttu-id="2463f-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="2463f-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="2463f-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="2463f-249">DateTimeOffset</span></span> |
| <span data-ttu-id="2463f-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="2463f-250">Interval Day</span></span> |<span data-ttu-id="2463f-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-251">TimeSpan</span></span> |
| <span data-ttu-id="2463f-252">День tooHour интервал</span><span class="sxs-lookup"><span data-stu-id="2463f-252">Interval Day tooHour</span></span> |<span data-ttu-id="2463f-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-253">TimeSpan</span></span> |
| <span data-ttu-id="2463f-254">День tooMinute интервал</span><span class="sxs-lookup"><span data-stu-id="2463f-254">Interval Day tooMinute</span></span> |<span data-ttu-id="2463f-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-255">TimeSpan</span></span> |
| <span data-ttu-id="2463f-256">День tooSecond интервал</span><span class="sxs-lookup"><span data-stu-id="2463f-256">Interval Day tooSecond</span></span> |<span data-ttu-id="2463f-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-257">TimeSpan</span></span> |
| <span data-ttu-id="2463f-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="2463f-258">Interval Hour</span></span> |<span data-ttu-id="2463f-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-259">TimeSpan</span></span> |
| <span data-ttu-id="2463f-260">Интервал tooMinute час</span><span class="sxs-lookup"><span data-stu-id="2463f-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="2463f-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-261">TimeSpan</span></span> |
| <span data-ttu-id="2463f-262">Интервал tooSecond час</span><span class="sxs-lookup"><span data-stu-id="2463f-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="2463f-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-263">TimeSpan</span></span> |
| <span data-ttu-id="2463f-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="2463f-264">Interval Minute</span></span> |<span data-ttu-id="2463f-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-265">TimeSpan</span></span> |
| <span data-ttu-id="2463f-266">Минуты tooSecond интервал</span><span class="sxs-lookup"><span data-stu-id="2463f-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="2463f-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-267">TimeSpan</span></span> |
| <span data-ttu-id="2463f-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="2463f-268">Interval Second</span></span> |<span data-ttu-id="2463f-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2463f-269">TimeSpan</span></span> |
| <span data-ttu-id="2463f-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="2463f-270">Interval Year</span></span> |<span data-ttu-id="2463f-271">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-271">String</span></span> |
| <span data-ttu-id="2463f-272">Интервал tooMonth год</span><span class="sxs-lookup"><span data-stu-id="2463f-272">Interval Year tooMonth</span></span> |<span data-ttu-id="2463f-273">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-273">String</span></span> |
| <span data-ttu-id="2463f-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="2463f-274">Interval Month</span></span> |<span data-ttu-id="2463f-275">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-275">String</span></span> |
| <span data-ttu-id="2463f-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="2463f-276">Period(Date)</span></span> |<span data-ttu-id="2463f-277">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-277">String</span></span> |
| <span data-ttu-id="2463f-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="2463f-278">Period(Time)</span></span> |<span data-ttu-id="2463f-279">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-279">String</span></span> |
| <span data-ttu-id="2463f-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="2463f-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="2463f-281">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-281">String</span></span> |
| <span data-ttu-id="2463f-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="2463f-282">Period(Timestamp)</span></span> |<span data-ttu-id="2463f-283">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-283">String</span></span> |
| <span data-ttu-id="2463f-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="2463f-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="2463f-285">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-285">String</span></span> |
| <span data-ttu-id="2463f-286">Xml</span><span class="sxs-lookup"><span data-stu-id="2463f-286">Xml</span></span> |<span data-ttu-id="2463f-287">Строка</span><span class="sxs-lookup"><span data-stu-id="2463f-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2463f-288">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="2463f-288">Map source toosink columns</span></span>
<span data-ttu-id="2463f-289">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2463f-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2463f-290">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="2463f-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="2463f-291">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="2463f-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2463f-292">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="2463f-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2463f-293">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="2463f-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2463f-294">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="2463f-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2463f-295">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2463f-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2463f-296">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="2463f-296">Performance and Tuning</span></span>
<span data-ttu-id="2463f-297">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="2463f-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
