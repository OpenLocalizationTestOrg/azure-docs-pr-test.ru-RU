---
title: "Перемещение данных из хранилищ данных ODBC | Документация Майкрософт"
description: "Узнайте, как перемещать данные из хранилищ данных ODBC с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="194b3-103">Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="194b3-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="194b3-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локального хранилища данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="194b3-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="194b3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="194b3-106">Данные из хранилища данных ODBC можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="194b3-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="194b3-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="194b3-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="194b3-108">Сейчас фабрика данных поддерживает только перемещение данных из хранилища данных ODBC в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="194b3-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="194b3-109">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="194b3-109">Enabling connectivity</span></span>
<span data-ttu-id="194b3-110">Служба фабрики данных поддерживает подключение к локальным источникам ODBC с помощью шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="194b3-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="194b3-111">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="194b3-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="194b3-112">Используйте шлюз для подключения к локальному хранилищу данных ODBC, даже если он размещен на виртуальной машине IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="194b3-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="194b3-113">Шлюз можно установить на тот же локальный компьютер или виртуальную машину Azure, что и хранилище данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="194b3-114">Тем не менее рекомендуется установить шлюз на отдельный компьютер или виртуальную машину IaaS SQL Azure, чтобы избежать конфликта ресурсов, а также для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="194b3-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="194b3-115">При установке шлюза на отдельный компьютер у компьютера должен быть доступ к машине с хранилищем данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="194b3-116">Помимо шлюза управления данными на компьютере с шлюзом необходимо также установить драйвер ODBC для хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="194b3-117">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="194b3-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="194b3-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="194b3-118">Getting started</span></span>
<span data-ttu-id="194b3-119">Вы можете создать конвейер с действием копирования, который перемещает данные из хранилища данных ODBC, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="194b3-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="194b3-120">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="194b3-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="194b3-121">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="194b3-122">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="194b3-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="194b3-123">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="194b3-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="194b3-124">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="194b3-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="194b3-125">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="194b3-126">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="194b3-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="194b3-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="194b3-128">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="194b3-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="194b3-129">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="194b3-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="194b3-130">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных ODBC, приведены в разделе [Пример JSON. Копирование данных из хранилища данных ODBC в большой двоичный объект Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="194b3-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="194b3-131">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к хранилищу данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="194b3-132">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="194b3-132">Linked service properties</span></span>
<span data-ttu-id="194b3-133">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="194b3-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="194b3-134">Property</span></span> | <span data-ttu-id="194b3-135">Описание</span><span class="sxs-lookup"><span data-stu-id="194b3-135">Description</span></span> | <span data-ttu-id="194b3-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="194b3-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="194b3-137">type</span><span class="sxs-lookup"><span data-stu-id="194b3-137">type</span></span> |<span data-ttu-id="194b3-138">Для свойства type необходимо задать значение **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="194b3-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="194b3-139">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-139">Yes</span></span> |
| <span data-ttu-id="194b3-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="194b3-140">connectionString</span></span> |<span data-ttu-id="194b3-141">Учетные данные в строке подключения, не используемые для получения доступа, а также дополнительные зашифрованные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="194b3-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="194b3-142">Примеры приведены в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="194b3-142">See examples in the following sections.</span></span> |<span data-ttu-id="194b3-143">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-143">Yes</span></span> |
| <span data-ttu-id="194b3-144">credential</span><span class="sxs-lookup"><span data-stu-id="194b3-144">credential</span></span> |<span data-ttu-id="194b3-145">Учетные данные в строке подключения, используемые для получения доступа и указанные в формате "драйвер-определенное свойство-значение".</span><span class="sxs-lookup"><span data-stu-id="194b3-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="194b3-146">Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="194b3-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="194b3-147">Нет</span><span class="sxs-lookup"><span data-stu-id="194b3-147">No</span></span> |
| <span data-ttu-id="194b3-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="194b3-148">authenticationType</span></span> |<span data-ttu-id="194b3-149">Тип проверки подлинности, используемый для подключения к хранилищу данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="194b3-150">Возможными значениями являются: "Анонимная" и "Обычная".</span><span class="sxs-lookup"><span data-stu-id="194b3-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="194b3-151">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-151">Yes</span></span> |
| <span data-ttu-id="194b3-152">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="194b3-152">username</span></span> |<span data-ttu-id="194b3-153">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="194b3-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="194b3-154">Нет</span><span class="sxs-lookup"><span data-stu-id="194b3-154">No</span></span> |
| <span data-ttu-id="194b3-155">пароль</span><span class="sxs-lookup"><span data-stu-id="194b3-155">password</span></span> |<span data-ttu-id="194b3-156">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="194b3-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="194b3-157">Нет</span><span class="sxs-lookup"><span data-stu-id="194b3-157">No</span></span> |
| <span data-ttu-id="194b3-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="194b3-158">gatewayName</span></span> |<span data-ttu-id="194b3-159">Имя шлюза, который следует использовать службе фабрики данных для подключения к хранилищу данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="194b3-160">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="194b3-161">Использовать обычную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="194b3-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="194b3-162">Использовать обычную проверку подлинности и шифрование учетных данных</span><span class="sxs-lookup"><span data-stu-id="194b3-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="194b3-163">Учетные данные можно зашифровать с помощью командлета [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0) или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (Azure PowerShell 0.9 или более ранней версии).</span><span class="sxs-lookup"><span data-stu-id="194b3-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="194b3-164">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="194b3-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="194b3-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="194b3-165">Dataset properties</span></span>
<span data-ttu-id="194b3-166">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="194b3-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="194b3-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="194b3-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="194b3-168">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="194b3-169">Раздел typeProperties набора данных типа **RelationalTable** (который включает в себя набор данных ODBC) содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="194b3-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="194b3-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="194b3-170">Property</span></span> | <span data-ttu-id="194b3-171">Описание</span><span class="sxs-lookup"><span data-stu-id="194b3-171">Description</span></span> | <span data-ttu-id="194b3-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="194b3-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="194b3-173">tableName</span><span class="sxs-lookup"><span data-stu-id="194b3-173">tableName</span></span> |<span data-ttu-id="194b3-174">Имя таблицы в хранилище данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="194b3-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="194b3-175">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="194b3-176">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="194b3-176">Copy activity properties</span></span>
<span data-ttu-id="194b3-177">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="194b3-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="194b3-178">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="194b3-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="194b3-179">С другой стороны, свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="194b3-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="194b3-180">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="194b3-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="194b3-181">В случае действия копирования, когда источник относится к типу **RelationalSource** (который содержит ODBC), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="194b3-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="194b3-182">Свойство</span><span class="sxs-lookup"><span data-stu-id="194b3-182">Property</span></span> | <span data-ttu-id="194b3-183">Описание</span><span class="sxs-lookup"><span data-stu-id="194b3-183">Description</span></span> | <span data-ttu-id="194b3-184">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="194b3-184">Allowed values</span></span> | <span data-ttu-id="194b3-185">Обязательно</span><span class="sxs-lookup"><span data-stu-id="194b3-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="194b3-186">query</span><span class="sxs-lookup"><span data-stu-id="194b3-186">query</span></span> |<span data-ttu-id="194b3-187">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-187">Use the custom query to read data.</span></span> |<span data-ttu-id="194b3-188">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="194b3-188">SQL query string.</span></span> <span data-ttu-id="194b3-189">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="194b3-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="194b3-190">Да</span><span class="sxs-lookup"><span data-stu-id="194b3-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="194b3-191">Пример JSON. Копирование данных из хранилища данных ODBC в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="194b3-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="194b3-192">Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="194b3-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="194b3-193">Он демонстрирует, как скопировать данные из источника ODBC в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="194b3-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="194b3-194">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="194b3-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="194b3-195">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="194b3-196">Связанная служба типа [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="194b3-197">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="194b3-198">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="194b3-199">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="194b3-200">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="194b3-201">В примере данные из результата выполнения запроса к хранилищу данных ODBC каждый час копируются в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="194b3-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="194b3-202">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="194b3-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="194b3-203">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="194b3-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="194b3-204">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="194b3-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="194b3-205">**Связанная служба ODBC**. В этом примере используется обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="194b3-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="194b3-206">Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы ODBC](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="194b3-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="194b3-207">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="194b3-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="194b3-208">**Входной набор данных ODBC**</span><span class="sxs-lookup"><span data-stu-id="194b3-208">**ODBC input dataset**</span></span>

<span data-ttu-id="194b3-209">В примере предполагается, что таблица MyTable уже создана в базе данных ODBC и содержит столбец с именем timestampcolumn для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="194b3-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="194b3-210">Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="194b3-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="194b3-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="194b3-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="194b3-212">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="194b3-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="194b3-213">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="194b3-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="194b3-214">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="194b3-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="194b3-215">**Действие копирования в конвейере с хранилищем данных ODBC (RelationalSource) в качестве источника и большим двоичным объектом в качестве приемника (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="194b3-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="194b3-216">Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="194b3-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="194b3-217">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="194b3-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="194b3-218">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="194b3-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="194b3-219">Сопоставление типов для ODBC</span><span class="sxs-lookup"><span data-stu-id="194b3-219">Type mapping for ODBC</span></span>
<span data-ttu-id="194b3-220">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="194b3-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="194b3-221">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="194b3-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="194b3-222">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="194b3-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="194b3-223">При перемещении данных из хранилищ данных ODBC типы данных ODBC сопоставляются с типами .NET. Ознакомьтесь со статьей [Сопоставления типов данных ODBC](https://msdn.microsoft.com/library/cc668763.aspx).</span><span class="sxs-lookup"><span data-stu-id="194b3-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="194b3-224">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="194b3-224">Map source to sink columns</span></span>
<span data-ttu-id="194b3-225">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="194b3-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="194b3-226">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="194b3-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="194b3-227">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="194b3-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="194b3-228">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="194b3-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="194b3-229">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="194b3-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="194b3-230">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="194b3-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="194b3-231">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="194b3-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="194b3-232">Хранилище GE Historian</span><span class="sxs-lookup"><span data-stu-id="194b3-232">GE Historian store</span></span>
<span data-ttu-id="194b3-233">Создание связанной службы ODBC для связи хранилища данных [Proficy Historian GE (теперь GE Historian)](http://www.geautomation.com/products/proficy-historian) с фабрикой данных Azure выполняется, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="194b3-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="194b3-234">Установите шлюз управления данными на локальном компьютере и зарегистрируйте этот шлюз на портале.</span><span class="sxs-lookup"><span data-stu-id="194b3-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="194b3-235">Шлюз, установленный на локальном компьютере, использует драйвер ODBC для GE Historian для подключения к хранилищу данных GE Historian.</span><span class="sxs-lookup"><span data-stu-id="194b3-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="194b3-236">Поэтому необходимо установить драйвер на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="194b3-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="194b3-237">Подробные сведения см. в разделе [Включение соединения](#enabling-connectivity).</span><span class="sxs-lookup"><span data-stu-id="194b3-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="194b3-238">Прежде чем использовать хранилище GE Historian в решении фабрики данных, убедитесь, что шлюз может подключаться к хранилищу данных с помощью инструкций в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="194b3-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="194b3-239">В начале статьи приводится подробный обзор использования хранилищ данных ODBC в качестве исходных хранилищ данных в ходе операции копирования.</span><span class="sxs-lookup"><span data-stu-id="194b3-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="194b3-240">Устранение проблем подключения</span><span class="sxs-lookup"><span data-stu-id="194b3-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="194b3-241">Для устранения проблем подключения используйте вкладку **Диагностика** **диспетчера конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="194b3-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="194b3-242">Запустите **диспетчер конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="194b3-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="194b3-243">Можно запустить файл "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" напрямую или выполнить поиск по слову **шлюз**, чтобы найти ссылку на приложение **Шлюз управления данными Майкрософт**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="194b3-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Поиск шлюза](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="194b3-245">Перейдите на вкладку **Диагностика** .</span><span class="sxs-lookup"><span data-stu-id="194b3-245">Switch to the **Diagnostics** tab.</span></span>

    ![Диагностика шлюза](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="194b3-247">Выберите **тип** хранилища данных (связанная служба).</span><span class="sxs-lookup"><span data-stu-id="194b3-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="194b3-248">Укажите тип **аутентификации** и введите **учетные данные** или **строку подключения** для подключения к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="194b3-249">Щелкните **Проверить подключение** , чтобы проверить подключение к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="194b3-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="194b3-250">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="194b3-250">Performance and Tuning</span></span>
<span data-ttu-id="194b3-251">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="194b3-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
