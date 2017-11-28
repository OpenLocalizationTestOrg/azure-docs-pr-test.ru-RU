---
title: "aaaMove tooand данных из SQL Server | Документы Microsoft"
description: "Дополнительные сведения о как toomove данных из SQL Server базы данных, локально или на виртуальной Машине Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="c693f-103">Переместить tooand данных из SQL Server локально или в IaaS (ВМ Azure) с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="c693f-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="c693f-104">В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данные из локальной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="c693f-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="c693f-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="c693f-106">Supported scenarios</span></span>
<span data-ttu-id="c693f-107">Можно скопировать данные **из базы данных SQL Server** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="c693f-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="c693f-108">Можно скопировать данные из hello, следуя хранилищ данных **базы данных SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="c693f-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="c693f-109">Поддерживаемые версии SQL Server</span><span class="sxs-lookup"><span data-stu-id="c693f-109">Supported SQL Server versions</span></span>
<span data-ttu-id="c693f-110">Эта поддержка соединителя SQL Server, копирование данных из / toohello следующие версии экземпляра, размещенного локально, либо в Azure IaaS с помощью проверки подлинности SQL и проверка подлинности Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="c693f-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="c693f-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="c693f-111">Enabling connectivity</span></span>
<span data-ttu-id="c693f-112">Основные понятия Hello и шаги, необходимые для соединения с SQL Server, размещенный в локальной или в Azure IaaS (инфраструктура как услуга) виртуальных машин hello же.</span><span class="sxs-lookup"><span data-stu-id="c693f-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="c693f-113">В обоих случаях необходимо toouse шлюз управления данными для подключения.</span><span class="sxs-lookup"><span data-stu-id="c693f-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="c693f-114">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="c693f-115">Настройка экземпляра шлюза необходима для подключения к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="c693f-116">При установке шлюза на hello же локальной машины или облака экземпляр виртуальной Машины как hello SQL Server для повышения производительности, рекомендуется установить их на отдельных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="c693f-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="c693f-117">Наличие шлюза hello и SQL Server на отдельных компьютерах уменьшает конкуренцию за ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c693f-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c693f-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c693f-118">Getting started</span></span>
<span data-ttu-id="c693f-119">Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Server или в нее с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="c693f-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="c693f-120">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="c693f-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c693f-121">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="c693f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="c693f-122">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="c693f-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c693f-123">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="c693f-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c693f-124">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="c693f-125">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="c693f-125">Create a **data factory**.</span></span> <span data-ttu-id="c693f-126">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="c693f-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="c693f-127">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="c693f-128">Например при копировании данных из tooan базы данных SQL Server хранилище больших двоичных объектов создается две связанные службы toolink вашей базы данных SQL Server и фабрику данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c693f-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="c693f-129">Свойства связанной службы, определенные tooSQL базы данных сервера, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="c693f-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="c693f-130">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="c693f-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="c693f-131">В примере hello, упомянутые в последнем шаге hello создайте таблицу dataset hello toospecify SQL в базе данных SQL Server, содержащий hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="c693f-132">Создайте другой контейнер больших двоичных объектов dataset toospecify hello и hello папке, содержащей данные hello копируются hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="c693f-133">Свойства набора данных, определенных tooSQL базы данных сервера, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="c693f-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="c693f-134">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="c693f-135">В примере hello приведенные выше используются SqlSource в BlobSink источника и в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="c693f-136">Аналогично при копировании из хранилища больших двоичных объектов tooSQL базы данных сервера использовать BlobSource и SqlSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="c693f-137">Свойства действия копирования, определенные tooSQL базы данных сервера, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="c693f-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="c693f-138">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="c693f-139">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="c693f-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c693f-140">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c693f-141">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной базы данных SQL Server см. в разделе [JSON примеры](#json-examples-for-copying-data-from-and-to-sql-server) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c693f-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="c693f-142">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooSQL сервера:</span><span class="sxs-lookup"><span data-stu-id="c693f-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c693f-143">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="c693f-143">Linked service properties</span></span>
<span data-ttu-id="c693f-144">Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="c693f-145">Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="c693f-146">Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.</span><span class="sxs-lookup"><span data-stu-id="c693f-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="c693f-147">Свойство</span><span class="sxs-lookup"><span data-stu-id="c693f-147">Property</span></span> | <span data-ttu-id="c693f-148">Описание</span><span class="sxs-lookup"><span data-stu-id="c693f-148">Description</span></span> | <span data-ttu-id="c693f-149">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c693f-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c693f-150">type</span><span class="sxs-lookup"><span data-stu-id="c693f-150">type</span></span> |<span data-ttu-id="c693f-151">свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="c693f-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="c693f-152">Да</span><span class="sxs-lookup"><span data-stu-id="c693f-152">Yes</span></span> |
| <span data-ttu-id="c693f-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="c693f-153">connectionString</span></span> |<span data-ttu-id="c693f-154">Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="c693f-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="c693f-155">Да</span><span class="sxs-lookup"><span data-stu-id="c693f-155">Yes</span></span> |
| <span data-ttu-id="c693f-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c693f-156">gatewayName</span></span> |<span data-ttu-id="c693f-157">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="c693f-158">Да</span><span class="sxs-lookup"><span data-stu-id="c693f-158">Yes</span></span> |
| <span data-ttu-id="c693f-159">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="c693f-159">username</span></span> |<span data-ttu-id="c693f-160">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="c693f-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="c693f-161">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="c693f-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="c693f-162">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-162">No</span></span> |
| <span data-ttu-id="c693f-163">пароль</span><span class="sxs-lookup"><span data-stu-id="c693f-163">password</span></span> |<span data-ttu-id="c693f-164">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="c693f-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="c693f-165">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-165">No</span></span> |

<span data-ttu-id="c693f-166">Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):</span><span class="sxs-lookup"><span data-stu-id="c693f-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="c693f-167">Примеры</span><span class="sxs-lookup"><span data-stu-id="c693f-167">Samples</span></span>
<span data-ttu-id="c693f-168">**JSON для использования проверки подлинности SQL**</span><span class="sxs-lookup"><span data-stu-id="c693f-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="c693f-169">**JSON для использования проверки подлинности Windows**</span><span class="sxs-lookup"><span data-stu-id="c693f-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="c693f-170">Шлюз управления данными будет олицетворять указанное hello базы данных SQL Server в локальной toohello в tooconnect учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="c693f-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c693f-171">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="c693f-171">Dataset properties</span></span>
<span data-ttu-id="c693f-172">В образцах hello использовании набора данных типа **SqlServerTable** toorepresent таблицы в базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="c693f-173">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c693f-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c693f-174">Разделы JSON набора данных, такие как структура, доступность и политика, одинаковы для всех типов наборов данных (SQL Server, большой двоичный объект Azure, таблица Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c693f-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c693f-175">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c693f-176">Hello **typeProperties** раздел для набора данных hello типа **SqlServerTable** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="c693f-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="c693f-177">Свойство</span><span class="sxs-lookup"><span data-stu-id="c693f-177">Property</span></span> | <span data-ttu-id="c693f-178">Описание</span><span class="sxs-lookup"><span data-stu-id="c693f-178">Description</span></span> | <span data-ttu-id="c693f-179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c693f-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c693f-180">tableName</span><span class="sxs-lookup"><span data-stu-id="c693f-180">tableName</span></span> |<span data-ttu-id="c693f-181">Имя hello таблицы или представления в экземпляр базы данных SQL Server hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="c693f-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="c693f-182">Да</span><span class="sxs-lookup"><span data-stu-id="c693f-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c693f-183">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="c693f-183">Copy activity properties</span></span>
<span data-ttu-id="c693f-184">При перемещении данных из базы данных SQL Server, следует установить hello исходного типа в действие копирования hello слишком**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="c693f-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="c693f-185">Аналогичным образом, при перемещении базы данных SQL Server tooa данных задаются тип приемника hello в действии копирования hello слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="c693f-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="c693f-186">Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.</span><span class="sxs-lookup"><span data-stu-id="c693f-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="c693f-187">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c693f-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c693f-188">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="c693f-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="c693f-189">Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.</span><span class="sxs-lookup"><span data-stu-id="c693f-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="c693f-190">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="c693f-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="c693f-191">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="c693f-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="c693f-192">SqlSource</span></span>
<span data-ttu-id="c693f-193">Если источник в операции копирования имеет тип **SqlSource**, hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="c693f-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="c693f-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="c693f-194">Property</span></span> | <span data-ttu-id="c693f-195">Описание</span><span class="sxs-lookup"><span data-stu-id="c693f-195">Description</span></span> | <span data-ttu-id="c693f-196">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="c693f-196">Allowed values</span></span> | <span data-ttu-id="c693f-197">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c693f-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c693f-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="c693f-198">sqlReaderQuery</span></span> |<span data-ttu-id="c693f-199">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="c693f-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="c693f-200">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="c693f-200">SQL query string.</span></span> <span data-ttu-id="c693f-201">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="c693f-201">For example: select * from MyTable.</span></span> <span data-ttu-id="c693f-202">Может ссылаться на несколько таблиц из базы данных hello ссылается hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="c693f-203">Если не указан, hello выполняемой инструкции SQL: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="c693f-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="c693f-204">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-204">No</span></span> |
| <span data-ttu-id="c693f-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="c693f-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="c693f-206">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="c693f-207">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="c693f-207">Name of hello stored procedure.</span></span> <span data-ttu-id="c693f-208">Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="c693f-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="c693f-209">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-209">No</span></span> |
| <span data-ttu-id="c693f-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="c693f-210">storedProcedureParameters</span></span> |<span data-ttu-id="c693f-211">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="c693f-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="c693f-212">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="c693f-212">Name/value pairs.</span></span> <span data-ttu-id="c693f-213">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="c693f-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="c693f-214">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-214">No</span></span> |

<span data-ttu-id="c693f-215">Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Server источника tooget hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="c693f-216">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="c693f-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="c693f-217">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используемые toobuild toorun запрос select для hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="c693f-218">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="c693f-219">При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c693f-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="c693f-220">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c693f-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="c693f-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="c693f-221">SqlSink</span></span>
<span data-ttu-id="c693f-222">**SqlSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="c693f-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="c693f-223">Свойство</span><span class="sxs-lookup"><span data-stu-id="c693f-223">Property</span></span> | <span data-ttu-id="c693f-224">Описание</span><span class="sxs-lookup"><span data-stu-id="c693f-224">Description</span></span> | <span data-ttu-id="c693f-225">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="c693f-225">Allowed values</span></span> | <span data-ttu-id="c693f-226">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c693f-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c693f-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="c693f-227">writeBatchTimeout</span></span> |<span data-ttu-id="c693f-228">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="c693f-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="c693f-229">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="c693f-229">timespan</span></span><br/><br/> <span data-ttu-id="c693f-230">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="c693f-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="c693f-231">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-231">No</span></span> |
| <span data-ttu-id="c693f-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="c693f-232">writeBatchSize</span></span> |<span data-ttu-id="c693f-233">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="c693f-234">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="c693f-234">Integer (number of rows)</span></span> |<span data-ttu-id="c693f-235">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="c693f-235">No (default: 10000)</span></span> |
| <span data-ttu-id="c693f-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="c693f-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="c693f-237">Укажите запрос для действия копирования tooexecute, таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="c693f-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="c693f-238">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="c693f-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="c693f-239">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="c693f-239">A query statement.</span></span> |<span data-ttu-id="c693f-240">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-240">No</span></span> |
| <span data-ttu-id="c693f-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="c693f-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="c693f-242">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="c693f-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="c693f-243">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="c693f-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="c693f-244">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="c693f-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="c693f-245">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-245">No</span></span> |
| <span data-ttu-id="c693f-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="c693f-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="c693f-247">Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="c693f-248">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="c693f-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="c693f-249">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-249">No</span></span> |
| <span data-ttu-id="c693f-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="c693f-250">storedProcedureParameters</span></span> |<span data-ttu-id="c693f-251">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="c693f-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="c693f-252">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="c693f-252">Name/value pairs.</span></span> <span data-ttu-id="c693f-253">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="c693f-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="c693f-254">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-254">No</span></span> |
| <span data-ttu-id="c693f-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="c693f-255">sqlWriterTableType</span></span> |<span data-ttu-id="c693f-256">Укажите toobe имя типа таблицы, используемых в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="c693f-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="c693f-257">Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей.</span><span class="sxs-lookup"><span data-stu-id="c693f-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="c693f-258">Кода хранимой процедуры можно объединять hello данные копируются с существующими данными.</span><span class="sxs-lookup"><span data-stu-id="c693f-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="c693f-259">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="c693f-259">A table type name.</span></span> |<span data-ttu-id="c693f-260">Нет</span><span class="sxs-lookup"><span data-stu-id="c693f-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="c693f-261">Примеры JSON для копирования данных из и tooSQL сервера</span><span class="sxs-lookup"><span data-stu-id="c693f-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="c693f-262">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c693f-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c693f-263">Здравствуйте, следующие примеры Показать как toocopy tooand данных из SQL Server и хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c693f-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="c693f-264">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c693f-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="c693f-265">Пример: Копирование данных из SQL Server tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c693f-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="c693f-266">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="c693f-266">hello following sample shows:</span></span>

1. <span data-ttu-id="c693f-267">Связанная служба типа [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="c693f-268">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c693f-269">Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c693f-270">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c693f-271">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c693f-272">Образец Hello копирует данные временных рядов с tooan таблицы SQL Server BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="c693f-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="c693f-273">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="c693f-274">В качестве первого шага настройки шлюза управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="c693f-275">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c693f-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c693f-276">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c693f-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="c693f-277">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="c693f-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="c693f-278">**Входной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c693f-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="c693f-279">Образец Hello предполагается создания таблицы «MyTable» в SQL Server, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="c693f-280">Вы можете запрашивать через несколько таблиц в одной базе данных с помощью одного набора данных, но одна таблица должна использоваться для набора данных hello tableName typeProperty приветствия.</span><span class="sxs-lookup"><span data-stu-id="c693f-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="c693f-281">Параметр «external»: «true» уведомляет службу фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
<span data-ttu-id="c693f-282">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="c693f-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="c693f-283">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="c693f-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c693f-284">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="c693f-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c693f-285">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c693f-286">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="c693f-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="c693f-287">конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="c693f-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c693f-288">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c693f-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="c693f-289">запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="c693f-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="c693f-290">В этом примере **sqlReaderQuery** указан для hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="c693f-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="c693f-291">Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Server исходных данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="c693f-292">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="c693f-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="c693f-293">Hello sqlReaderQuery ссылаться на несколько таблиц в базе данных hello ссылается hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="c693f-294">Это не таблица hello ограниченный tooonly, задайте как hello typeProperty tableName набора данных.</span><span class="sxs-lookup"><span data-stu-id="c693f-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="c693f-295">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используется toobuild toorun запрос select для hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="c693f-296">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="c693f-297">В разделе hello [источника Sql](#sqlsource) раздел и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) список свойств, поддерживаемых SqlSource и BlobSink hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="c693f-298">Пример: Копирование данных из больших двоичных объектов Azure tooSQL сервера</span><span class="sxs-lookup"><span data-stu-id="c693f-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="c693f-299">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="c693f-299">hello following sample shows:</span></span>

1. <span data-ttu-id="c693f-300">Hello связанной службы типа [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="c693f-301">Hello связанной службы типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c693f-302">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c693f-303">Выходной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c693f-304">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="c693f-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="c693f-305">Образец Hello копирует временных рядов данных из таблицы SQL Server tooa BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="c693f-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="c693f-306">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="c693f-307">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c693f-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="c693f-308">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="c693f-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="c693f-309">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="c693f-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="c693f-310">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c693f-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c693f-311">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="c693f-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c693f-312">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="c693f-313">«external»: параметр «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
<span data-ttu-id="c693f-314">**Выходной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="c693f-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="c693f-315">Образец Hello копирует tooa таблицу данных, с именем «MyTable» в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="c693f-316">Создать таблицу hello в SQL Server с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c693f-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="c693f-317">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="c693f-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c693f-318">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="c693f-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="c693f-319">конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="c693f-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c693f-320">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="c693f-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="c693f-321">Устранение неполадок с подключением</span><span class="sxs-lookup"><span data-stu-id="c693f-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="c693f-322">Настройка удаленных соединений tooaccept SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c693f-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="c693f-323">Запустите **SQL Server Management Studio**, щелкните правой кнопкой мыши свой **сервер** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="c693f-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="c693f-324">Выберите **подключений** из списка hello и проверка **toohello сервера разрешить удаленные соединения**.</span><span class="sxs-lookup"><span data-stu-id="c693f-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Включение удаленных подключений](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="c693f-326">В разделе [Настройка параметра конфигурации сервера remote access hello](https://msdn.microsoft.com/library/ms191464.aspx) подробное описание шагов.</span><span class="sxs-lookup"><span data-stu-id="c693f-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="c693f-327">Запустите **диспетчер конфигурации SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c693f-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="c693f-328">Разверните **сетевая конфигурация SQL Server** для hello экземпляра, который хотите, а затем выберите **протоколы для MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="c693f-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="c693f-329">Вы увидите протоколов в правой области hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="c693f-330">Включите TCP/TP, щелкнув правой кнопкой мыши имя протокола **TCP/IP** и выбрав пункт **Включить**.</span><span class="sxs-lookup"><span data-stu-id="c693f-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Включение TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="c693f-332">Подробные сведения и альтернативные способы включения протокола TCP/IP см. в статье [Включение или отключение сетевого протокола сервера](https://msdn.microsoft.com/library/ms191294.aspx).</span><span class="sxs-lookup"><span data-stu-id="c693f-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="c693f-333">В том же окне hello, дважды щелкните **TCP/IP** toolaunch **свойства TCP/IP** окна.</span><span class="sxs-lookup"><span data-stu-id="c693f-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="c693f-334">Переключение toohello **IP-адреса** вкладки. Прокрутите вниз toosee **IPAll** раздела.</span><span class="sxs-lookup"><span data-stu-id="c693f-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="c693f-335">Запишите hello ** TCP-порт ** (по умолчанию — **1433**).</span><span class="sxs-lookup"><span data-stu-id="c693f-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="c693f-336">Создание **правило для брандмауэра Windows hello** на hello машины tooallow входящий трафик через этот порт.</span><span class="sxs-lookup"><span data-stu-id="c693f-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="c693f-337">**Проверка подключения**: tooconnect toohello SQL Server с помощью полного имени, используйте SQL Server Management Studio с другого компьютера.</span><span class="sxs-lookup"><span data-stu-id="c693f-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="c693f-338">Например, <machine><domain>.corp<company>.com,1433.</span><span class="sxs-lookup"><span data-stu-id="c693f-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="c693f-339">В разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="c693f-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="c693f-340">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="c693f-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="c693f-341">Столбцы идентификаторов в целевой базе данных hello</span><span class="sxs-lookup"><span data-stu-id="c693f-341">Identity columns in hello target database</span></span>
<span data-ttu-id="c693f-342">Этот раздел содержит пример, в котором данные копируются из исходной таблицы с без идентификатора столбца tooa целевую таблицу со столбцом идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="c693f-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="c693f-343">**Исходная таблица:**</span><span class="sxs-lookup"><span data-stu-id="c693f-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="c693f-344">**Целевая таблица:**</span><span class="sxs-lookup"><span data-stu-id="c693f-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="c693f-345">Обратите внимание, что этот hello целевая таблица имеет столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="c693f-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="c693f-346">**Определение JSON исходного набора данных**</span><span class="sxs-lookup"><span data-stu-id="c693f-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="c693f-347">**Определение JSON целевого набора данных**</span><span class="sxs-lookup"><span data-stu-id="c693f-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="c693f-348">Обратите внимание, что у исходной и целевой таблиц разные схемы (в целевой есть дополнительный столбец с идентификаторами).</span><span class="sxs-lookup"><span data-stu-id="c693f-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="c693f-349">В этом случае необходимо toospecify **структуры** свойство в определении набора данных целевого hello, который не содержит столбца идентификаторов hello.</span><span class="sxs-lookup"><span data-stu-id="c693f-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="c693f-350">Вызов хранимой процедуры из приемника SQL</span><span class="sxs-lookup"><span data-stu-id="c693f-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="c693f-351">Пример вызова хранимой процедуры из приемника SQL в действии копирования в конвейере приведен в статье [Invoke stored procedure from copy activity in Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md) (Вызов хранимой процедуры из действия копирования в фабрике данных Azure).</span><span class="sxs-lookup"><span data-stu-id="c693f-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="c693f-352">Сопоставление типов SQL Server</span><span class="sxs-lookup"><span data-stu-id="c693f-352">Type mapping for SQL server</span></span>
<span data-ttu-id="c693f-353">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статья hello действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="c693f-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="c693f-354">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="c693f-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="c693f-355">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="c693f-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="c693f-356">После перемещения данных слишком & из SQL server, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот.</span><span class="sxs-lookup"><span data-stu-id="c693f-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="c693f-357">сопоставление Hello выполняется аналогично hello сопоставление типов данных SQL Server для ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="c693f-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="c693f-358">Тип ядра СУБД SQL Server</span><span class="sxs-lookup"><span data-stu-id="c693f-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="c693f-359">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c693f-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c693f-360">bigint</span><span class="sxs-lookup"><span data-stu-id="c693f-360">bigint</span></span> |<span data-ttu-id="c693f-361">Int64</span><span class="sxs-lookup"><span data-stu-id="c693f-361">Int64</span></span> |
| <span data-ttu-id="c693f-362">binary;</span><span class="sxs-lookup"><span data-stu-id="c693f-362">binary</span></span> |<span data-ttu-id="c693f-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-363">Byte[]</span></span> |
| <span data-ttu-id="c693f-364">bit</span><span class="sxs-lookup"><span data-stu-id="c693f-364">bit</span></span> |<span data-ttu-id="c693f-365">Логический</span><span class="sxs-lookup"><span data-stu-id="c693f-365">Boolean</span></span> |
| <span data-ttu-id="c693f-366">char;</span><span class="sxs-lookup"><span data-stu-id="c693f-366">char</span></span> |<span data-ttu-id="c693f-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-367">String, Char[]</span></span> |
| <span data-ttu-id="c693f-368">дата</span><span class="sxs-lookup"><span data-stu-id="c693f-368">date</span></span> |<span data-ttu-id="c693f-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="c693f-369">DateTime</span></span> |
| <span data-ttu-id="c693f-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="c693f-370">Datetime</span></span> |<span data-ttu-id="c693f-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="c693f-371">DateTime</span></span> |
| <span data-ttu-id="c693f-372">datetime2;</span><span class="sxs-lookup"><span data-stu-id="c693f-372">datetime2</span></span> |<span data-ttu-id="c693f-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="c693f-373">DateTime</span></span> |
| <span data-ttu-id="c693f-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="c693f-374">Datetimeoffset</span></span> |<span data-ttu-id="c693f-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="c693f-375">DateTimeOffset</span></span> |
| <span data-ttu-id="c693f-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="c693f-376">Decimal</span></span> |<span data-ttu-id="c693f-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="c693f-377">Decimal</span></span> |
| <span data-ttu-id="c693f-378">Атрибут FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="c693f-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="c693f-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-379">Byte[]</span></span> |
| <span data-ttu-id="c693f-380">Float</span><span class="sxs-lookup"><span data-stu-id="c693f-380">Float</span></span> |<span data-ttu-id="c693f-381">Double</span><span class="sxs-lookup"><span data-stu-id="c693f-381">Double</span></span> |
| <span data-ttu-id="c693f-382">изображение</span><span class="sxs-lookup"><span data-stu-id="c693f-382">image</span></span> |<span data-ttu-id="c693f-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-383">Byte[]</span></span> |
| <span data-ttu-id="c693f-384">int</span><span class="sxs-lookup"><span data-stu-id="c693f-384">int</span></span> |<span data-ttu-id="c693f-385">Int32</span><span class="sxs-lookup"><span data-stu-id="c693f-385">Int32</span></span> |
| <span data-ttu-id="c693f-386">money;</span><span class="sxs-lookup"><span data-stu-id="c693f-386">money</span></span> |<span data-ttu-id="c693f-387">Decimal</span><span class="sxs-lookup"><span data-stu-id="c693f-387">Decimal</span></span> |
| <span data-ttu-id="c693f-388">nchar;</span><span class="sxs-lookup"><span data-stu-id="c693f-388">nchar</span></span> |<span data-ttu-id="c693f-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-389">String, Char[]</span></span> |
| <span data-ttu-id="c693f-390">ntext</span><span class="sxs-lookup"><span data-stu-id="c693f-390">ntext</span></span> |<span data-ttu-id="c693f-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-391">String, Char[]</span></span> |
| <span data-ttu-id="c693f-392">numeric</span><span class="sxs-lookup"><span data-stu-id="c693f-392">numeric</span></span> |<span data-ttu-id="c693f-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="c693f-393">Decimal</span></span> |
| <span data-ttu-id="c693f-394">nvarchar;</span><span class="sxs-lookup"><span data-stu-id="c693f-394">nvarchar</span></span> |<span data-ttu-id="c693f-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-395">String, Char[]</span></span> |
| <span data-ttu-id="c693f-396">real;</span><span class="sxs-lookup"><span data-stu-id="c693f-396">real</span></span> |<span data-ttu-id="c693f-397">Single</span><span class="sxs-lookup"><span data-stu-id="c693f-397">Single</span></span> |
| <span data-ttu-id="c693f-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="c693f-398">rowversion</span></span> |<span data-ttu-id="c693f-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-399">Byte[]</span></span> |
| <span data-ttu-id="c693f-400">smalldatetime;</span><span class="sxs-lookup"><span data-stu-id="c693f-400">smalldatetime</span></span> |<span data-ttu-id="c693f-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="c693f-401">DateTime</span></span> |
| <span data-ttu-id="c693f-402">smallint;</span><span class="sxs-lookup"><span data-stu-id="c693f-402">smallint</span></span> |<span data-ttu-id="c693f-403">Int16</span><span class="sxs-lookup"><span data-stu-id="c693f-403">Int16</span></span> |
| <span data-ttu-id="c693f-404">smallmoney;</span><span class="sxs-lookup"><span data-stu-id="c693f-404">smallmoney</span></span> |<span data-ttu-id="c693f-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="c693f-405">Decimal</span></span> |
| <span data-ttu-id="c693f-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="c693f-406">sql_variant</span></span> |<span data-ttu-id="c693f-407">Object *</span><span class="sxs-lookup"><span data-stu-id="c693f-407">Object *</span></span> |
| <span data-ttu-id="c693f-408">text</span><span class="sxs-lookup"><span data-stu-id="c693f-408">text</span></span> |<span data-ttu-id="c693f-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-409">String, Char[]</span></span> |
| <span data-ttu-id="c693f-410">time</span><span class="sxs-lookup"><span data-stu-id="c693f-410">time</span></span> |<span data-ttu-id="c693f-411">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="c693f-411">TimeSpan</span></span> |
| <span data-ttu-id="c693f-412">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c693f-412">timestamp</span></span> |<span data-ttu-id="c693f-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-413">Byte[]</span></span> |
| <span data-ttu-id="c693f-414">tinyint;</span><span class="sxs-lookup"><span data-stu-id="c693f-414">tinyint</span></span> |<span data-ttu-id="c693f-415">Byte</span><span class="sxs-lookup"><span data-stu-id="c693f-415">Byte</span></span> |
| <span data-ttu-id="c693f-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="c693f-416">uniqueidentifier</span></span> |<span data-ttu-id="c693f-417">Guid</span><span class="sxs-lookup"><span data-stu-id="c693f-417">Guid</span></span> |
| <span data-ttu-id="c693f-418">varbinary;</span><span class="sxs-lookup"><span data-stu-id="c693f-418">varbinary</span></span> |<span data-ttu-id="c693f-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c693f-419">Byte[]</span></span> |
| <span data-ttu-id="c693f-420">varchar.</span><span class="sxs-lookup"><span data-stu-id="c693f-420">varchar</span></span> |<span data-ttu-id="c693f-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="c693f-421">String, Char[]</span></span> |
| <span data-ttu-id="c693f-422">xml</span><span class="sxs-lookup"><span data-stu-id="c693f-422">xml</span></span> |<span data-ttu-id="c693f-423">xml</span><span class="sxs-lookup"><span data-stu-id="c693f-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="c693f-424">Сопоставление столбцов toosink источника</span><span class="sxs-lookup"><span data-stu-id="c693f-424">Mapping source toosink columns</span></span>
<span data-ttu-id="c693f-425">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c693f-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="c693f-426">Повторяющаяся операция копирования</span><span class="sxs-lookup"><span data-stu-id="c693f-426">Repeatable copy</span></span>
<span data-ttu-id="c693f-427">При копировании данных tooSQL базы данных сервера, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c693f-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="c693f-428">tooperform UPSERT. Вместо этого в разделе [tooSqlSink Repeatable записи](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) статьи.</span><span class="sxs-lookup"><span data-stu-id="c693f-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="c693f-429">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="c693f-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="c693f-430">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="c693f-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c693f-431">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="c693f-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c693f-432">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="c693f-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c693f-433">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c693f-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c693f-434">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="c693f-434">Performance and Tuning</span></span>
<span data-ttu-id="c693f-435">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="c693f-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
