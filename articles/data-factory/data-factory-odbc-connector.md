---
title: "aaaMove данные из хранилищ данных ODBC | Документы Microsoft"
description: "Дополнительные сведения о хранением данных toomove из данных ODBC с помощью фабрики данных Azure."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="823ee-103">Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="823ee-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="823ee-104">В этой статье объясняется, как хранить hello toouse действие копирования в фабрике данных Azure toomove данных из локальных данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="823ee-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="823ee-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="823ee-106">Можно скопировать данные из ODBC хранилища поддерживается tooany приемник данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="823ee-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="823ee-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="823ee-108">Фабрика данных в настоящее время поддерживает только при перемещении данных из объекта данных ODBC хранения tooother хранилищ данных, но не для переноса данных из другого хранилища данных сохраняет tooan данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="823ee-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="823ee-109">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="823ee-109">Enabling connectivity</span></span>
<span data-ttu-id="823ee-110">Служба фабрики данных поддерживает подключения ODBC tooon локальные источники, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="823ee-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="823ee-111">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="823ee-112">Используйте хранилище данных ODBC tooan tooconnect hello шлюза, даже если она размещается на виртуальной Машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="823ee-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="823ee-113">Hello шлюз можно установить на hello же локального компьютера или hello виртуальную Машину Azure в качестве хранилища данных ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="823ee-114">Тем не менее, рекомендуется установить на отдельных машин/Azure IaaS виртуальной Машины шлюза hello tooavoid о конфликтах ресурсов и для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="823ee-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="823ee-115">При установке шлюза hello на отдельном компьютере hello машина должна была может tooaccess hello машины с хранилищем данных ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="823ee-116">Помимо hello шлюз управления данными необходимо также tooinstall hello ODBC driver для hello хранилища данных на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="823ee-117">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="823ee-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="823ee-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="823ee-118">Getting started</span></span>
<span data-ttu-id="823ee-119">Вы можете создать конвейер с действием копирования, который перемещает данные из хранилища данных ODBC, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="823ee-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="823ee-120">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="823ee-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="823ee-121">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="823ee-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="823ee-122">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="823ee-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="823ee-123">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="823ee-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="823ee-124">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="823ee-125">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="823ee-126">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="823ee-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="823ee-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="823ee-128">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="823ee-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="823ee-129">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="823ee-130">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных ODBC см. в разделе [пример JSON: копирование данных из данных ODBC хранения больших двоичных объектов tooAzure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="823ee-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="823ee-131">Hello в следующих разделах содержатся сведения о свойствах JSON, которые находятся в хранилище данных определенного tooODBC сущностей фабрики данных используется toodefine:</span><span class="sxs-lookup"><span data-stu-id="823ee-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="823ee-132">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="823ee-132">Linked service properties</span></span>
<span data-ttu-id="823ee-133">Hello в следующей таблице приводится описание службы конкретных tooODBC связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="823ee-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="823ee-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="823ee-134">Property</span></span> | <span data-ttu-id="823ee-135">Описание</span><span class="sxs-lookup"><span data-stu-id="823ee-135">Description</span></span> | <span data-ttu-id="823ee-136">Обязательно</span><span class="sxs-lookup"><span data-stu-id="823ee-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="823ee-137">type</span><span class="sxs-lookup"><span data-stu-id="823ee-137">type</span></span> |<span data-ttu-id="823ee-138">свойство типа Hello должно быть присвоено: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="823ee-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="823ee-139">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-139">Yes</span></span> |
| <span data-ttu-id="823ee-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="823ee-140">connectionString</span></span> |<span data-ttu-id="823ee-141">Hello учетные данные не доступа часть строки подключения hello и необязательный шифрование учетных данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="823ee-142">Примеры в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-142">See examples in hello following sections.</span></span> |<span data-ttu-id="823ee-143">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-143">Yes</span></span> |
| <span data-ttu-id="823ee-144">credential</span><span class="sxs-lookup"><span data-stu-id="823ee-144">credential</span></span> |<span data-ttu-id="823ee-145">учетные данные доступа Hello часть hello строка подключения, указанная в формате значение свойства драйвера.</span><span class="sxs-lookup"><span data-stu-id="823ee-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="823ee-146">Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="823ee-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="823ee-147">Нет</span><span class="sxs-lookup"><span data-stu-id="823ee-147">No</span></span> |
| <span data-ttu-id="823ee-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="823ee-148">authenticationType</span></span> |<span data-ttu-id="823ee-149">Тип проверки подлинности используется хранилище данных tooconnect toohello ODBC.</span><span class="sxs-lookup"><span data-stu-id="823ee-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="823ee-150">Возможными значениями являются: "Анонимная" и "Обычная".</span><span class="sxs-lookup"><span data-stu-id="823ee-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="823ee-151">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-151">Yes</span></span> |
| <span data-ttu-id="823ee-152">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="823ee-152">username</span></span> |<span data-ttu-id="823ee-153">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="823ee-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="823ee-154">Нет</span><span class="sxs-lookup"><span data-stu-id="823ee-154">No</span></span> |
| <span data-ttu-id="823ee-155">пароль</span><span class="sxs-lookup"><span data-stu-id="823ee-155">password</span></span> |<span data-ttu-id="823ee-156">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="823ee-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="823ee-157">Нет</span><span class="sxs-lookup"><span data-stu-id="823ee-157">No</span></span> |
| <span data-ttu-id="823ee-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="823ee-158">gatewayName</span></span> |<span data-ttu-id="823ee-159">Имя шлюза hello, hello служба фабрики данных должна использовать хранилище данных ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="823ee-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="823ee-160">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="823ee-161">Использовать обычную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="823ee-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="823ee-162">Использовать обычную проверку подлинности и шифрование учетных данных</span><span class="sxs-lookup"><span data-stu-id="823ee-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="823ee-163">Можно зашифровать учетные данные hello, с помощью hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (версии 1.0 Azure PowerShell) командлета или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 или более ранней версии hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="823ee-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="823ee-164">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="823ee-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="823ee-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="823ee-165">Dataset properties</span></span>
<span data-ttu-id="823ee-166">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="823ee-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="823ee-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="823ee-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="823ee-168">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="823ee-169">Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных ODBC) имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="823ee-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="823ee-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="823ee-170">Property</span></span> | <span data-ttu-id="823ee-171">Описание</span><span class="sxs-lookup"><span data-stu-id="823ee-171">Description</span></span> | <span data-ttu-id="823ee-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="823ee-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="823ee-173">tableName</span><span class="sxs-lookup"><span data-stu-id="823ee-173">tableName</span></span> |<span data-ttu-id="823ee-174">Имя таблицы hello в хранилище данных ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="823ee-175">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="823ee-176">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="823ee-176">Copy activity properties</span></span>
<span data-ttu-id="823ee-177">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="823ee-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="823ee-178">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="823ee-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="823ee-179">Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="823ee-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="823ee-180">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="823ee-181">В действии копирования, когда источник типа **RelationalSource** (включая ODBC), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="823ee-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="823ee-182">Свойство</span><span class="sxs-lookup"><span data-stu-id="823ee-182">Property</span></span> | <span data-ttu-id="823ee-183">Описание</span><span class="sxs-lookup"><span data-stu-id="823ee-183">Description</span></span> | <span data-ttu-id="823ee-184">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="823ee-184">Allowed values</span></span> | <span data-ttu-id="823ee-185">Обязательно</span><span class="sxs-lookup"><span data-stu-id="823ee-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="823ee-186">query</span><span class="sxs-lookup"><span data-stu-id="823ee-186">query</span></span> |<span data-ttu-id="823ee-187">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="823ee-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="823ee-188">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="823ee-188">SQL query string.</span></span> <span data-ttu-id="823ee-189">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="823ee-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="823ee-190">Да</span><span class="sxs-lookup"><span data-stu-id="823ee-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="823ee-191">Пример JSON: копирование данных из данных ODBC хранения tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="823ee-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="823ee-192">В этом примере предоставляет определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="823ee-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="823ee-193">В нем показано, как toocopy из ODBC источника tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="823ee-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="823ee-194">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="823ee-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="823ee-195">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="823ee-196">Связанная служба типа [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="823ee-197">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="823ee-198">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="823ee-199">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="823ee-200">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="823ee-201">Образец Hello копирует данные из результатов запроса в большой двоичный объект ODBC tooa данных хранения каждый час.</span><span class="sxs-lookup"><span data-stu-id="823ee-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="823ee-202">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="823ee-203">В качестве первого шага можно Настройте шлюз управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="823ee-204">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="823ee-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="823ee-205">**ODBC связанная служба** в этом примере используется hello обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="823ee-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="823ee-206">Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы ODBC](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="823ee-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="823ee-207">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="823ee-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="823ee-208">**Входной набор данных ODBC**</span><span class="sxs-lookup"><span data-stu-id="823ee-208">**ODBC input dataset**</span></span>

<span data-ttu-id="823ee-209">Образец Hello предполагается создания таблицы «MyTable» в базе данных ODBC, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="823ee-210">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="823ee-211">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="823ee-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="823ee-212">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="823ee-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="823ee-213">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="823ee-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="823ee-214">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="823ee-215">**Действие копирования в конвейере с хранилищем данных ODBC (RelationalSource) в качестве источника и большим двоичным объектом в качестве приемника (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="823ee-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="823ee-216">конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="823ee-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="823ee-217">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="823ee-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="823ee-218">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="823ee-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="823ee-219">Сопоставление типов для ODBC</span><span class="sxs-lookup"><span data-stu-id="823ee-219">Type mapping for ODBC</span></span>
<span data-ttu-id="823ee-220">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:</span><span class="sxs-lookup"><span data-stu-id="823ee-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="823ee-221">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="823ee-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="823ee-222">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="823ee-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="823ee-223">При перемещении данных из хранилищ данных ODBC, типы данных ODBC: too.NET сопоставленные типы, как упоминалось в hello [сопоставления типов данных ODBC](https://msdn.microsoft.com/library/cc668763.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="823ee-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="823ee-224">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="823ee-224">Map source toosink columns</span></span>
<span data-ttu-id="823ee-225">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="823ee-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="823ee-226">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="823ee-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="823ee-227">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="823ee-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="823ee-228">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="823ee-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="823ee-229">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="823ee-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="823ee-230">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="823ee-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="823ee-231">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="823ee-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="823ee-232">Хранилище GE Historian</span><span class="sxs-lookup"><span data-stu-id="823ee-232">GE Historian store</span></span>
<span data-ttu-id="823ee-233">Создать ODBC связанной службы toolink [Proficy Historian GE (теперь GE Historian)](http://www.geautomation.com/products/proficy-historian) фабрики данных Azure tooan хранилище данных, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="823ee-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="823ee-234">Установите шлюз управления данными на локальном компьютере и зарегистрируйте шлюз hello с портала hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="823ee-235">установлены на компьютере локального шлюза Hello использует драйвер ODBC для hello для toohello tooconnect GE Historian GE Historian хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="823ee-236">Установка драйвера hello таким образом, в том случае, если он еще не установлена на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="823ee-237">Подробные сведения см. в разделе [Включение соединения](#enabling-connectivity).</span><span class="sxs-lookup"><span data-stu-id="823ee-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="823ee-238">Прежде чем использовать hello GE Historian хранения в решении фабрики данных, проверьте подключения шлюза hello toohello хранилища данных, с помощью инструкций в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="823ee-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="823ee-239">Прочитать статью hello с начала hello подробный обзор использования ODBC данных хранятся в виде источника хранилищ данных в ходе операции копирования.</span><span class="sxs-lookup"><span data-stu-id="823ee-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="823ee-240">Устранение проблем подключения</span><span class="sxs-lookup"><span data-stu-id="823ee-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="823ee-241">проблемы с подключением tootroubleshoot использовать hello **диагностики** вкладке **диспетчера конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="823ee-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="823ee-242">Запустите **диспетчер конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="823ee-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="823ee-243">Можно либо запустить «C:\Program Files\Microsoft данных управления Gateway\1.0\Shared\ConfigManager.exe» непосредственно (или) поиска для **шлюза** toofind ссылку слишком**шлюз управления данными Майкрософт** приложения, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="823ee-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Поиск шлюза](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="823ee-245">Переключение toohello **диагностики** вкладки.</span><span class="sxs-lookup"><span data-stu-id="823ee-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Диагностика шлюза](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="823ee-247">Выберите hello **тип** данных хранения (связанной службы).</span><span class="sxs-lookup"><span data-stu-id="823ee-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="823ee-248">Укажите **проверки подлинности** и введите **учетные данные** (или) введите **строка подключения** , является хранилищем данных используется tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="823ee-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="823ee-249">Нажмите кнопку **Проверка соединения** hello подключения tootest toohello-хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="823ee-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="823ee-250">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="823ee-250">Performance and Tuning</span></span>
<span data-ttu-id="823ee-251">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="823ee-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
