---
title: "Перемещение данных из Teradata с помощью фабрики данных Azure | Документация Майкрософт"
description: "Сведения о соединителе Teradata для службы фабрики данных, с помощью которого можно перемещать данные из базы данных Teradata."
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
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="61170-103">Перемещение данных из Teradata с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="61170-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="61170-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локальной базы данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="61170-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="61170-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="61170-106">Вы можете скопировать данные из локального хранилища данных Teradata в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="61170-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="61170-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="61170-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="61170-108">Сейчас фабрика данных поддерживает только перемещение данных из локального хранилища данных Teradata в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="61170-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="61170-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="61170-109">Prerequisites</span></span>
<span data-ttu-id="61170-110">Фабрика данных поддерживает подключение к локальным источникам Teradata с помощью шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="61170-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="61170-111">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="61170-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="61170-112">Шлюз является обязательным, даже если база данных Teradata размещается на виртуальной машине (ВМ) Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="61170-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="61170-113">Шлюз можно установить на той же ВМ IaaS, на которой размещается хранилище данных, или на другой ВМ. Важно, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="61170-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="61170-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="61170-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="61170-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="61170-115">Supported versions and installation</span></span>
<span data-ttu-id="61170-116">Для подключения шлюза управления данными к базе данных Teradata необходимо установить [поставщик данных .NET для Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) версии 14 и более в одной системе со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="61170-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="61170-117">Поддерживается Teradata версии 12 и более.</span><span class="sxs-lookup"><span data-stu-id="61170-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="61170-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="61170-118">Getting started</span></span>
<span data-ttu-id="61170-119">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="61170-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="61170-120">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="61170-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="61170-121">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="61170-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="61170-122">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="61170-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="61170-123">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="61170-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="61170-124">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="61170-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="61170-125">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="61170-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="61170-126">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="61170-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="61170-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="61170-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="61170-128">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="61170-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="61170-129">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="61170-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="61170-130">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных Teradata, вы найдете в разделе [Пример JSON. Копирование данных из Teradata в большой двоичный объект Azure](#json-example-copy-data-from-teradata-to-azure-blob) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="61170-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="61170-131">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="61170-132">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="61170-132">Linked service properties</span></span>
<span data-ttu-id="61170-133">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="61170-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="61170-134">Property</span></span> | <span data-ttu-id="61170-135">Описание</span><span class="sxs-lookup"><span data-stu-id="61170-135">Description</span></span> | <span data-ttu-id="61170-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61170-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61170-137">type</span><span class="sxs-lookup"><span data-stu-id="61170-137">type</span></span> |<span data-ttu-id="61170-138">Для свойства type необходимо задать значение **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="61170-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="61170-139">Да</span><span class="sxs-lookup"><span data-stu-id="61170-139">Yes</span></span> |
| <span data-ttu-id="61170-140">server</span><span class="sxs-lookup"><span data-stu-id="61170-140">server</span></span> |<span data-ttu-id="61170-141">Имя сервера Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-141">Name of the Teradata server.</span></span> |<span data-ttu-id="61170-142">Да</span><span class="sxs-lookup"><span data-stu-id="61170-142">Yes</span></span> |
| <span data-ttu-id="61170-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="61170-143">authenticationType</span></span> |<span data-ttu-id="61170-144">Тип проверки подлинности, используемый для подключения к базе данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="61170-145">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="61170-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="61170-146">Да</span><span class="sxs-lookup"><span data-stu-id="61170-146">Yes</span></span> |
| <span data-ttu-id="61170-147">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="61170-147">username</span></span> |<span data-ttu-id="61170-148">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="61170-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="61170-149">Нет</span><span class="sxs-lookup"><span data-stu-id="61170-149">No</span></span> |
| <span data-ttu-id="61170-150">пароль</span><span class="sxs-lookup"><span data-stu-id="61170-150">password</span></span> |<span data-ttu-id="61170-151">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="61170-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="61170-152">Нет</span><span class="sxs-lookup"><span data-stu-id="61170-152">No</span></span> |
| <span data-ttu-id="61170-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="61170-153">gatewayName</span></span> |<span data-ttu-id="61170-154">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="61170-155">Да</span><span class="sxs-lookup"><span data-stu-id="61170-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="61170-156">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="61170-156">Dataset properties</span></span>
<span data-ttu-id="61170-157">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="61170-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="61170-158">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="61170-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="61170-159">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="61170-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="61170-160">Сейчас нет каких-либо свойств типа, поддерживаемых для набора данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="61170-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="61170-161">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="61170-161">Copy activity properties</span></span>
<span data-ttu-id="61170-162">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="61170-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="61170-163">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="61170-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="61170-164">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="61170-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="61170-165">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="61170-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="61170-166">Если источник относится к типу **RelationalSource** (который содержит Teradata), то в разделе **typeProperties** доступны следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="61170-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="61170-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="61170-167">Property</span></span> | <span data-ttu-id="61170-168">Описание</span><span class="sxs-lookup"><span data-stu-id="61170-168">Description</span></span> | <span data-ttu-id="61170-169">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="61170-169">Allowed values</span></span> | <span data-ttu-id="61170-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61170-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="61170-171">query</span><span class="sxs-lookup"><span data-stu-id="61170-171">query</span></span> |<span data-ttu-id="61170-172">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="61170-172">Use the custom query to read data.</span></span> |<span data-ttu-id="61170-173">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="61170-173">SQL query string.</span></span> <span data-ttu-id="61170-174">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="61170-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="61170-175">Да</span><span class="sxs-lookup"><span data-stu-id="61170-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="61170-176">Пример JSON. Копирование данных из Teradata в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="61170-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="61170-177">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="61170-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="61170-178">Вы узнаете, как копировать данные из Teradata в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="61170-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="61170-179">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="61170-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="61170-180">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="61170-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="61170-181">Связанная служба типа [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="61170-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="61170-182">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="61170-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="61170-183">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="61170-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="61170-184">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="61170-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="61170-185">[Конвейер](data-factory-create-pipelines.md) с действием копирования, которое использует [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="61170-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="61170-186">В примере данные из результата выполнения запроса к базе данных Teradata каждый час копируются в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="61170-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="61170-187">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="61170-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="61170-188">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="61170-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="61170-189">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="61170-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="61170-190">**Связанная служба Teradata**</span><span class="sxs-lookup"><span data-stu-id="61170-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="61170-191">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="61170-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="61170-192">**Входной набор данных Teradata**</span><span class="sxs-lookup"><span data-stu-id="61170-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="61170-193">В примере предполагается, что вы уже создали таблицу MyTable в Teradata и она содержит столбец с именем timestamp для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="61170-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="61170-194">Если для параметра external задать значение true, то фабрика данных воспримет эту таблицу как внешнюю, которая создана не каким-либо действием в этой фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="61170-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="61170-195">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="61170-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="61170-196">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="61170-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="61170-197">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="61170-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="61170-198">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="61170-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="61170-199">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="61170-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="61170-200">Конвейер содержит действие копирования, которое использует входные и выходные наборы данных и выполняется ежечасно.</span><span class="sxs-lookup"><span data-stu-id="61170-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="61170-201">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="61170-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="61170-202">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="61170-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="61170-203">Сопоставление типов для Teradata</span><span class="sxs-lookup"><span data-stu-id="61170-203">Type mapping for Teradata</span></span>
<span data-ttu-id="61170-204">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в 2 этапа:</span><span class="sxs-lookup"><span data-stu-id="61170-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="61170-205">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="61170-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="61170-206">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="61170-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="61170-207">При перемещении данных в Teradata используются следующие сопоставления из типов Teradata в типы .NET.</span><span class="sxs-lookup"><span data-stu-id="61170-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="61170-208">Тип базы данных Teradata</span><span class="sxs-lookup"><span data-stu-id="61170-208">Teradata Database type</span></span> | <span data-ttu-id="61170-209">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="61170-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="61170-210">Char</span><span class="sxs-lookup"><span data-stu-id="61170-210">Char</span></span> |<span data-ttu-id="61170-211">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-211">String</span></span> |
| <span data-ttu-id="61170-212">Clob</span><span class="sxs-lookup"><span data-stu-id="61170-212">Clob</span></span> |<span data-ttu-id="61170-213">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-213">String</span></span> |
| <span data-ttu-id="61170-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="61170-214">Graphic</span></span> |<span data-ttu-id="61170-215">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-215">String</span></span> |
| <span data-ttu-id="61170-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="61170-216">VarChar</span></span> |<span data-ttu-id="61170-217">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-217">String</span></span> |
| <span data-ttu-id="61170-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="61170-218">VarGraphic</span></span> |<span data-ttu-id="61170-219">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-219">String</span></span> |
| <span data-ttu-id="61170-220">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="61170-220">Blob</span></span> |<span data-ttu-id="61170-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="61170-221">Byte[]</span></span> |
| <span data-ttu-id="61170-222">Byte</span><span class="sxs-lookup"><span data-stu-id="61170-222">Byte</span></span> |<span data-ttu-id="61170-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="61170-223">Byte[]</span></span> |
| <span data-ttu-id="61170-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="61170-224">VarByte</span></span> |<span data-ttu-id="61170-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="61170-225">Byte[]</span></span> |
| <span data-ttu-id="61170-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="61170-226">BigInt</span></span> |<span data-ttu-id="61170-227">Int64</span><span class="sxs-lookup"><span data-stu-id="61170-227">Int64</span></span> |
| <span data-ttu-id="61170-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="61170-228">ByteInt</span></span> |<span data-ttu-id="61170-229">Int16</span><span class="sxs-lookup"><span data-stu-id="61170-229">Int16</span></span> |
| <span data-ttu-id="61170-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="61170-230">Decimal</span></span> |<span data-ttu-id="61170-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="61170-231">Decimal</span></span> |
| <span data-ttu-id="61170-232">Double</span><span class="sxs-lookup"><span data-stu-id="61170-232">Double</span></span> |<span data-ttu-id="61170-233">Double</span><span class="sxs-lookup"><span data-stu-id="61170-233">Double</span></span> |
| <span data-ttu-id="61170-234">Число</span><span class="sxs-lookup"><span data-stu-id="61170-234">Integer</span></span> |<span data-ttu-id="61170-235">Int32</span><span class="sxs-lookup"><span data-stu-id="61170-235">Int32</span></span> |
| <span data-ttu-id="61170-236">Число</span><span class="sxs-lookup"><span data-stu-id="61170-236">Number</span></span> |<span data-ttu-id="61170-237">Double</span><span class="sxs-lookup"><span data-stu-id="61170-237">Double</span></span> |
| <span data-ttu-id="61170-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="61170-238">SmallInt</span></span> |<span data-ttu-id="61170-239">Int16</span><span class="sxs-lookup"><span data-stu-id="61170-239">Int16</span></span> |
| <span data-ttu-id="61170-240">Дата</span><span class="sxs-lookup"><span data-stu-id="61170-240">Date</span></span> |<span data-ttu-id="61170-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="61170-241">DateTime</span></span> |
| <span data-ttu-id="61170-242">Время</span><span class="sxs-lookup"><span data-stu-id="61170-242">Time</span></span> |<span data-ttu-id="61170-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-243">TimeSpan</span></span> |
| <span data-ttu-id="61170-244">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="61170-244">Time With Time Zone</span></span> |<span data-ttu-id="61170-245">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-245">String</span></span> |
| <span data-ttu-id="61170-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="61170-246">Timestamp</span></span> |<span data-ttu-id="61170-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="61170-247">DateTime</span></span> |
| <span data-ttu-id="61170-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="61170-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="61170-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="61170-249">DateTimeOffset</span></span> |
| <span data-ttu-id="61170-250">Interval Day</span><span class="sxs-lookup"><span data-stu-id="61170-250">Interval Day</span></span> |<span data-ttu-id="61170-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-251">TimeSpan</span></span> |
| <span data-ttu-id="61170-252">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="61170-252">Interval Day To Hour</span></span> |<span data-ttu-id="61170-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-253">TimeSpan</span></span> |
| <span data-ttu-id="61170-254">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="61170-254">Interval Day To Minute</span></span> |<span data-ttu-id="61170-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-255">TimeSpan</span></span> |
| <span data-ttu-id="61170-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="61170-256">Interval Day To Second</span></span> |<span data-ttu-id="61170-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-257">TimeSpan</span></span> |
| <span data-ttu-id="61170-258">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="61170-258">Interval Hour</span></span> |<span data-ttu-id="61170-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-259">TimeSpan</span></span> |
| <span data-ttu-id="61170-260">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="61170-260">Interval Hour To Minute</span></span> |<span data-ttu-id="61170-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-261">TimeSpan</span></span> |
| <span data-ttu-id="61170-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="61170-262">Interval Hour To Second</span></span> |<span data-ttu-id="61170-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-263">TimeSpan</span></span> |
| <span data-ttu-id="61170-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="61170-264">Interval Minute</span></span> |<span data-ttu-id="61170-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-265">TimeSpan</span></span> |
| <span data-ttu-id="61170-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="61170-266">Interval Minute To Second</span></span> |<span data-ttu-id="61170-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-267">TimeSpan</span></span> |
| <span data-ttu-id="61170-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="61170-268">Interval Second</span></span> |<span data-ttu-id="61170-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="61170-269">TimeSpan</span></span> |
| <span data-ttu-id="61170-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="61170-270">Interval Year</span></span> |<span data-ttu-id="61170-271">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-271">String</span></span> |
| <span data-ttu-id="61170-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="61170-272">Interval Year To Month</span></span> |<span data-ttu-id="61170-273">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-273">String</span></span> |
| <span data-ttu-id="61170-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="61170-274">Interval Month</span></span> |<span data-ttu-id="61170-275">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-275">String</span></span> |
| <span data-ttu-id="61170-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="61170-276">Period(Date)</span></span> |<span data-ttu-id="61170-277">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-277">String</span></span> |
| <span data-ttu-id="61170-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="61170-278">Period(Time)</span></span> |<span data-ttu-id="61170-279">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-279">String</span></span> |
| <span data-ttu-id="61170-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="61170-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="61170-281">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-281">String</span></span> |
| <span data-ttu-id="61170-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="61170-282">Period(Timestamp)</span></span> |<span data-ttu-id="61170-283">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-283">String</span></span> |
| <span data-ttu-id="61170-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="61170-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="61170-285">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-285">String</span></span> |
| <span data-ttu-id="61170-286">Xml</span><span class="sxs-lookup"><span data-stu-id="61170-286">Xml</span></span> |<span data-ttu-id="61170-287">Строка</span><span class="sxs-lookup"><span data-stu-id="61170-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="61170-288">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="61170-288">Map source to sink columns</span></span>
<span data-ttu-id="61170-289">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="61170-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="61170-290">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="61170-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="61170-291">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="61170-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="61170-292">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="61170-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="61170-293">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="61170-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="61170-294">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="61170-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="61170-295">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="61170-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="61170-296">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="61170-296">Performance and Tuning</span></span>
<span data-ttu-id="61170-297">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="61170-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
