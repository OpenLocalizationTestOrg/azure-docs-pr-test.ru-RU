---
title: "Перемещение данных в базу данных SQL Server и обратно | Документация Майкрософт"
description: "Узнайте, как с помощью фабрики данных Azure перемещать данные в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure."
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
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="89b65-103">Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="89b65-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="89b65-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные в локальную базу данных SQL Server и обратно.</span><span class="sxs-lookup"><span data-stu-id="89b65-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="89b65-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="89b65-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="89b65-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="89b65-106">Supported scenarios</span></span>
<span data-ttu-id="89b65-107">Данные можно скопировать **из базы данных SQL Server** в следующие хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="89b65-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="89b65-108">Данные можно скопировать **в базу данных SQL Server** из следующих хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="89b65-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="89b65-109">Поддерживаемые версии SQL Server</span><span class="sxs-lookup"><span data-stu-id="89b65-109">Supported SQL Server versions</span></span>
<span data-ttu-id="89b65-110">Этот соединитель SQL Server поддерживает копирование данных в экземпляры следующих версий, размещенные в локальной среде или в Azure IaaS, и обратно с использованием проверки подлинности SQL и Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005.</span><span class="sxs-lookup"><span data-stu-id="89b65-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="89b65-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="89b65-111">Enabling connectivity</span></span>
<span data-ttu-id="89b65-112">Где бы ни размещалась система SQL Server — локально или на виртуальных машинах Azure IaaS (инфраструктура как услуга), — основные понятия и действия, необходимые для соединения с ней, одинаковы.</span><span class="sxs-lookup"><span data-stu-id="89b65-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="89b65-113">В обоих случаях для подключения необходимо использовать шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="89b65-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="89b65-114">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="89b65-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="89b65-115">Настройка экземпляра шлюза необходима для подключения к SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="89b65-116">Вы можете установить шлюз на тот же локальный компьютер или экземпляр облачной виртуальной машины, на котором установлена система SQL Server, однако для более эффективной работы мы рекомендуем устанавливать их на разные компьютеры.</span><span class="sxs-lookup"><span data-stu-id="89b65-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="89b65-117">Размещение шлюза и SQL Server на разных компьютерах уменьшает конкуренцию за ресурсы.</span><span class="sxs-lookup"><span data-stu-id="89b65-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89b65-118">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="89b65-118">Getting started</span></span>
<span data-ttu-id="89b65-119">Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Server или в нее с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="89b65-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="89b65-120">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="89b65-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="89b65-121">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="89b65-122">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="89b65-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="89b65-123">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="89b65-124">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="89b65-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="89b65-125">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="89b65-125">Create a **data factory**.</span></span> <span data-ttu-id="89b65-126">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="89b65-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="89b65-127">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="89b65-128">Например, при копировании данных из базы данных SQL Server в хранилище BLOB-объектов Azure создайте две связанные службы, чтобы связать базу данных SQL Server и учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="89b65-129">Сведения о свойствах связанной службы, относящихся к базе данных SQL Server, см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="89b65-130">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="89b65-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="89b65-131">В примере, упомянутом в последнем шаге, создайте набор данных, чтобы указать таблицу SQL в базе данных SQL Server, содержащую входные данные.</span><span class="sxs-lookup"><span data-stu-id="89b65-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="89b65-132">И создайте другой набор данных, чтобы указать контейнер BLOB-объектов и папку, содержащую данные, скопированные из базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="89b65-133">Сведения о свойствах набора данных, относящихся к базе данных SQL Server, см. в разделе [Свойства набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="89b65-134">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="89b65-135">В примере выше SqlSource используется как источник, а BlobSink — как приемник для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="89b65-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="89b65-136">Аналогично, при копировании из хранилища BLOB-объектов Azure в базу данных SQL Server в действии копирования используются BlobSource и SqlSink.</span><span class="sxs-lookup"><span data-stu-id="89b65-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="89b65-137">Сведения о свойствах действия копирования, относящихся к базе данных SQL Server, см. в разделе [Свойства действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="89b65-138">Для получения сведений о том, как использовать хранилище данных как источник или приемник, щелкните ссылку в предыдущем разделе об источнике данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="89b65-139">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="89b65-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="89b65-140">При использовании средств и API-интерфейсов (за исключением .NET API) эти сущности фабрики данных определяются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="89b65-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="89b65-141">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных в локальную базу данных SQL Server и обратно, см. в разделе [Примеры определений JSON](#json-examples-for-copying-data-from-and-to-sql-server) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="89b65-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="89b65-142">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="89b65-143">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="89b65-143">Linked service properties</span></span>
<span data-ttu-id="89b65-144">Создайте связанную службу типа **OnPremisesSqlServer**, чтобы связать локальную базу данных SQL Server с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="89b65-145">В следующей таблице содержится описание элементов JSON, которые относятся к локальной связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="89b65-146">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="89b65-147">Свойство</span><span class="sxs-lookup"><span data-stu-id="89b65-147">Property</span></span> | <span data-ttu-id="89b65-148">Описание</span><span class="sxs-lookup"><span data-stu-id="89b65-148">Description</span></span> | <span data-ttu-id="89b65-149">Обязательно</span><span class="sxs-lookup"><span data-stu-id="89b65-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89b65-150">type</span><span class="sxs-lookup"><span data-stu-id="89b65-150">type</span></span> |<span data-ttu-id="89b65-151">Свойству type необходимо присвоить значение **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="89b65-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="89b65-152">Да</span><span class="sxs-lookup"><span data-stu-id="89b65-152">Yes</span></span> |
| <span data-ttu-id="89b65-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="89b65-153">connectionString</span></span> |<span data-ttu-id="89b65-154">Укажите сведения о параметре connectionString, необходимые для подключения к локальной базе данных SQL Server с помощью проверки подлинности SQL или проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="89b65-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="89b65-155">Да</span><span class="sxs-lookup"><span data-stu-id="89b65-155">Yes</span></span> |
| <span data-ttu-id="89b65-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="89b65-156">gatewayName</span></span> |<span data-ttu-id="89b65-157">Имя шлюза, который службе фабрики данных следует использовать для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="89b65-158">Да</span><span class="sxs-lookup"><span data-stu-id="89b65-158">Yes</span></span> |
| <span data-ttu-id="89b65-159">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="89b65-159">username</span></span> |<span data-ttu-id="89b65-160">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="89b65-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="89b65-161">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="89b65-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="89b65-162">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-162">No</span></span> |
| <span data-ttu-id="89b65-163">пароль</span><span class="sxs-lookup"><span data-stu-id="89b65-163">password</span></span> |<span data-ttu-id="89b65-164">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="89b65-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="89b65-165">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-165">No</span></span> |

<span data-ttu-id="89b65-166">Вы можете зашифровать учетные данные с помощью командлета **New-AzureRmDataFactoryEncryptValue** и использовать их в строке подключения, как показано в следующем примере (свойство **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="89b65-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="89b65-167">Примеры</span><span class="sxs-lookup"><span data-stu-id="89b65-167">Samples</span></span>
<span data-ttu-id="89b65-168">**JSON для использования проверки подлинности SQL**</span><span class="sxs-lookup"><span data-stu-id="89b65-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="89b65-169">**JSON для использования проверки подлинности Windows**</span><span class="sxs-lookup"><span data-stu-id="89b65-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="89b65-170">Шлюз управления данными будет действовать от имени соответствующей учетной записи пользователя для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="89b65-171">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="89b65-171">Dataset properties</span></span>
<span data-ttu-id="89b65-172">В примерах использовался набор данных типа **SqlServerTable** для представления таблицы в базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="89b65-173">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="89b65-174">Разделы JSON набора данных, такие как структура, доступность и политика, одинаковы для всех типов наборов данных (SQL Server, большой двоичный объект Azure, таблица Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="89b65-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="89b65-175">Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="89b65-176">Раздел **typeProperties** для набора данных с типом **SqlServerTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="89b65-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="89b65-177">Свойство</span><span class="sxs-lookup"><span data-stu-id="89b65-177">Property</span></span> | <span data-ttu-id="89b65-178">Описание</span><span class="sxs-lookup"><span data-stu-id="89b65-178">Description</span></span> | <span data-ttu-id="89b65-179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="89b65-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89b65-180">tableName</span><span class="sxs-lookup"><span data-stu-id="89b65-180">tableName</span></span> |<span data-ttu-id="89b65-181">Имя таблицы или представления в экземпляре базы данных SQL Server, на который ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="89b65-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="89b65-182">Да</span><span class="sxs-lookup"><span data-stu-id="89b65-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="89b65-183">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="89b65-183">Copy activity properties</span></span>
<span data-ttu-id="89b65-184">При перемещении данных из базы данных SQL Server в действии копирования задается тип источника **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="89b65-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="89b65-185">Аналогично, при перемещении данных в базу данных SQL Server в действии копирования задается тип источника **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="89b65-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="89b65-186">Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.</span><span class="sxs-lookup"><span data-stu-id="89b65-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="89b65-187">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="89b65-188">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="89b65-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="89b65-189">Действие копирования принимает только один набор входных данных и возвращает только один набор выходных.</span><span class="sxs-lookup"><span data-stu-id="89b65-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="89b65-190">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="89b65-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="89b65-191">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="89b65-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="89b65-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="89b65-192">SqlSource</span></span>
<span data-ttu-id="89b65-193">Когда источник в действии копирования относится к типу **SqlSource**, в разделе **typeProperties** доступны указанные ниже свойства:</span><span class="sxs-lookup"><span data-stu-id="89b65-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="89b65-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="89b65-194">Property</span></span> | <span data-ttu-id="89b65-195">Описание</span><span class="sxs-lookup"><span data-stu-id="89b65-195">Description</span></span> | <span data-ttu-id="89b65-196">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="89b65-196">Allowed values</span></span> | <span data-ttu-id="89b65-197">Обязательно</span><span class="sxs-lookup"><span data-stu-id="89b65-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89b65-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="89b65-198">sqlReaderQuery</span></span> |<span data-ttu-id="89b65-199">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-199">Use the custom query to read data.</span></span> |<span data-ttu-id="89b65-200">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="89b65-200">SQL query string.</span></span> <span data-ttu-id="89b65-201">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="89b65-201">For example: select * from MyTable.</span></span> <span data-ttu-id="89b65-202">Может ссылаться на несколько таблиц из базы данных, на которую ссылается входной набор данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="89b65-203">Если не указано другое, выполняется инструкция SQL select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="89b65-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="89b65-204">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-204">No</span></span> |
| <span data-ttu-id="89b65-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="89b65-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="89b65-206">Имя хранимой процедуры, которая считывает данные из исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="89b65-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="89b65-207">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-207">Name of the stored procedure.</span></span> <span data-ttu-id="89b65-208">Последней инструкцией SQL должна быть инструкция SELECT в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="89b65-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="89b65-209">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-209">No</span></span> |
| <span data-ttu-id="89b65-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="89b65-210">storedProcedureParameters</span></span> |<span data-ttu-id="89b65-211">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="89b65-212">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="89b65-212">Name/value pairs.</span></span> <span data-ttu-id="89b65-213">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="89b65-214">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-214">No</span></span> |

<span data-ttu-id="89b65-215">Если для SqlSource указано **sqlReaderQuery** , то действие копирования выполняет этот запрос для источника базы данных SQL Server с целью получения данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="89b65-216">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="89b65-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="89b65-217">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса select к базе данных SQL Server будут использованы столбцы, определенные в разделе структуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="89b65-218">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="89b65-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="89b65-219">При использовании **sqlReaderStoredProcedureName** по-прежнему необходимо указать значение свойства **tableName** в наборе данных JSON.</span><span class="sxs-lookup"><span data-stu-id="89b65-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="89b65-220">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="89b65-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="89b65-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="89b65-221">SqlSink</span></span>
<span data-ttu-id="89b65-222">**SqlSink** поддерживает указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="89b65-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="89b65-223">Свойство</span><span class="sxs-lookup"><span data-stu-id="89b65-223">Property</span></span> | <span data-ttu-id="89b65-224">Описание</span><span class="sxs-lookup"><span data-stu-id="89b65-224">Description</span></span> | <span data-ttu-id="89b65-225">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="89b65-225">Allowed values</span></span> | <span data-ttu-id="89b65-226">Обязательно</span><span class="sxs-lookup"><span data-stu-id="89b65-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89b65-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="89b65-227">writeBatchTimeout</span></span> |<span data-ttu-id="89b65-228">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="89b65-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="89b65-229">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="89b65-229">timespan</span></span><br/><br/> <span data-ttu-id="89b65-230">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="89b65-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="89b65-231">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-231">No</span></span> |
| <span data-ttu-id="89b65-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="89b65-232">writeBatchSize</span></span> |<span data-ttu-id="89b65-233">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="89b65-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="89b65-234">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="89b65-234">Integer (number of rows)</span></span> |<span data-ttu-id="89b65-235">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="89b65-235">No (default: 10000)</span></span> |
| <span data-ttu-id="89b65-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="89b65-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="89b65-237">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="89b65-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="89b65-238">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="89b65-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="89b65-239">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="89b65-239">A query statement.</span></span> |<span data-ttu-id="89b65-240">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-240">No</span></span> |
| <span data-ttu-id="89b65-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="89b65-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="89b65-242">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="89b65-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="89b65-243">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="89b65-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="89b65-244">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="89b65-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="89b65-245">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-245">No</span></span> |
| <span data-ttu-id="89b65-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="89b65-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="89b65-247">Имя хранимой процедуры, обновляющей данные или вставляющей их в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="89b65-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="89b65-248">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-248">Name of the stored procedure.</span></span> |<span data-ttu-id="89b65-249">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-249">No</span></span> |
| <span data-ttu-id="89b65-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="89b65-250">storedProcedureParameters</span></span> |<span data-ttu-id="89b65-251">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="89b65-252">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="89b65-252">Name/value pairs.</span></span> <span data-ttu-id="89b65-253">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="89b65-254">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-254">No</span></span> |
| <span data-ttu-id="89b65-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="89b65-255">sqlWriterTableType</span></span> |<span data-ttu-id="89b65-256">Укажите имя типа таблицы для использования в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="89b65-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="89b65-257">Действие копирования делает перемещаемые данные доступными во временной таблице этого типа.</span><span class="sxs-lookup"><span data-stu-id="89b65-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="89b65-258">Код хранимой процедуры затем можно использовать для объединения копируемых и существующих данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="89b65-259">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="89b65-259">A table type name.</span></span> |<span data-ttu-id="89b65-260">Нет</span><span class="sxs-lookup"><span data-stu-id="89b65-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="89b65-261">Примеры JSON для копирования данных в SQL Server и обратно</span><span class="sxs-lookup"><span data-stu-id="89b65-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="89b65-262">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="89b65-263">В следующих примерах показано, как копировать данные в базу данных SQL Server и хранилище BLOB-объектов Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="89b65-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="89b65-264">Тем не менее данные можно копировать **непосредственно** из любых источников в любой указанный [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемник. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="89b65-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="89b65-265">Пример. Копирование данных из базы данных SQL Server в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="89b65-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="89b65-266">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="89b65-266">The following sample shows:</span></span>

1. <span data-ttu-id="89b65-267">Связанная служба типа [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="89b65-268">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="89b65-269">Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="89b65-270">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="89b65-271">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="89b65-272">В этом примере данные временного ряда каждый час копируются из таблицы SQL Server в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="89b65-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="89b65-273">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="89b65-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="89b65-274">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="89b65-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="89b65-275">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="89b65-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="89b65-276">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="89b65-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="89b65-277">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="89b65-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="89b65-278">**Входной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="89b65-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="89b65-279">В примере предполагается, что вы уже создали таблицу MyTable в SQL Server и она содержит столбец с именем timestampcolumn для данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="89b65-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="89b65-280">Можно выполнить запрос к нескольким таблицам в одной базе данных, используя один набор данных, но для typeProperty tableName набора данных нужно указать одну таблицу.</span><span class="sxs-lookup"><span data-stu-id="89b65-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="89b65-281">Если для параметра external задать значение true, то фабрика данных воспримет этот набор данных как внешний, который создан не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="89b65-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="89b65-282">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="89b65-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="89b65-283">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="89b65-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="89b65-284">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="89b65-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="89b65-285">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="89b65-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="89b65-286">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="89b65-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="89b65-287">Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="89b65-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="89b65-288">В определении JSON конвейера для типа **source** установлено значение **SqlSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="89b65-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="89b65-289">SQL-запрос, указанный для свойства **SqlReaderQuery** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="89b65-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="89b65-290">В этом примере для свойства SqlSource указано **sqlReaderQuery** .</span><span class="sxs-lookup"><span data-stu-id="89b65-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="89b65-291">Действие копирования выполняет этот запрос к источнику базы данных SQL Server с целью получения данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="89b65-292">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="89b65-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="89b65-293">Свойство sqlReaderQuery может ссылаться на несколько таблиц из базы данных, на которую ссылается входной набор данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="89b65-294">Он не ограничивается таблицей, заданной свойством typeProperty в качестве параметра tableName набора данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="89b65-295">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса select к базе данных SQL Server будут использованы столбцы, определенные в разделе структуры.</span><span class="sxs-lookup"><span data-stu-id="89b65-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="89b65-296">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="89b65-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="89b65-297">Список свойств, поддерживаемых SqlSource и BlobSink, см. в разделах [SqlSource](#sqlsource) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="89b65-298">Пример. Копирование данных из BLOB-объекта Azure в базу данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="89b65-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="89b65-299">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="89b65-299">The following sample shows:</span></span>

1. <span data-ttu-id="89b65-300">Связанная служба типа [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="89b65-301">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="89b65-302">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="89b65-303">Выходной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="89b65-304">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="89b65-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="89b65-305">В этом примере данные временного ряда каждый час копируются из большого двоичного объекта Azure в таблицу SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="89b65-306">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="89b65-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="89b65-307">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="89b65-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="89b65-308">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="89b65-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="89b65-309">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="89b65-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="89b65-310">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="89b65-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="89b65-311">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="89b65-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="89b65-312">В пути к папке используется год, месяц и день начала, а в имени файла — час начала.</span><span class="sxs-lookup"><span data-stu-id="89b65-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="89b65-313">Когда для параметра external задано значение true, служба фабрики данных считает этот набор данных внешним по отношению к себе и не созданным в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="89b65-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="89b65-314">**Выходной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="89b65-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="89b65-315">В этом примере данные копируются в таблицу MyTable, которая создана в базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="89b65-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="89b65-316">Создайте в базе данных SQL Server таблицу с тем же количеством столбцов, которое должно быть в CSV-файле большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="89b65-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="89b65-317">Новые строки добавляются в таблицу каждый час.</span><span class="sxs-lookup"><span data-stu-id="89b65-317">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="89b65-318">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="89b65-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="89b65-319">Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="89b65-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="89b65-320">В определении JSON конвейера для типа **source** установлено значение **BlobSource**, а для типа **sink** — значение **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="89b65-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="89b65-321">Устранение неполадок с подключением</span><span class="sxs-lookup"><span data-stu-id="89b65-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="89b65-322">Настройте SQL Server для приема удаленных подключений.</span><span class="sxs-lookup"><span data-stu-id="89b65-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="89b65-323">Запустите **SQL Server Management Studio**, щелкните правой кнопкой мыши свой **сервер** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="89b65-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="89b65-324">Выберите в списке пункт **Подключения** и установите флажок **Allow remote connections to the server** (Разрешить удаленные подключения к этому серверу).</span><span class="sxs-lookup"><span data-stu-id="89b65-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Включение удаленных подключений](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="89b65-326">Подробные инструкции см. в статье [Настройка параметра конфигурации сервера remote access](https://msdn.microsoft.com/library/ms191464.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b65-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="89b65-327">Запустите **диспетчер конфигурации SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="89b65-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="89b65-328">Разверните узел **Сетевая конфигурация SQL Server** для нужного экземпляра и выберите пункт **Protocols for MSSQLSERVER** (Протоколы для MSSQLSERVER).</span><span class="sxs-lookup"><span data-stu-id="89b65-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="89b65-329">Вы должны увидеть протоколы на панели справа.</span><span class="sxs-lookup"><span data-stu-id="89b65-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="89b65-330">Включите TCP/TP, щелкнув правой кнопкой мыши имя протокола **TCP/IP** и выбрав пункт **Включить**.</span><span class="sxs-lookup"><span data-stu-id="89b65-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Включение TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="89b65-332">Подробные сведения и альтернативные способы включения протокола TCP/IP см. в статье [Включение или отключение сетевого протокола сервера](https://msdn.microsoft.com/library/ms191294.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b65-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="89b65-333">В этом же окне дважды щелкните **TCP/IP**, чтобы открыть окно **TCP/IP Properties** (Свойства TCP/IP).</span><span class="sxs-lookup"><span data-stu-id="89b65-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="89b65-334">Перейдите на вкладку **IP-адреса** .</span><span class="sxs-lookup"><span data-stu-id="89b65-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="89b65-335">Прокрутите вниз до раздела **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="89b65-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="89b65-336">Запишите значение параметра **TCP-порт** (по умолчанию — **1433**).</span><span class="sxs-lookup"><span data-stu-id="89b65-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="89b65-337">Создайте на компьютере **правило брандмауэра Windows** , чтобы разрешить входящий трафик через этот порт.</span><span class="sxs-lookup"><span data-stu-id="89b65-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="89b65-338">**Проверьте подключение**.</span><span class="sxs-lookup"><span data-stu-id="89b65-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="89b65-339">Например, <machine><domain>.corp<company>.com,1433.</span><span class="sxs-lookup"><span data-stu-id="89b65-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="89b65-340">Дополнительные сведения см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="89b65-341">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="89b65-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="89b65-342">Столбцы идентификаторов в целевой базе данных</span><span class="sxs-lookup"><span data-stu-id="89b65-342">Identity columns in the target database</span></span>
<span data-ttu-id="89b65-343">В этом разделе приведен пример копирования данных из исходной таблицы без столбца идентификаторов в целевую таблицу со столбцом идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="89b65-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="89b65-344">**Исходная таблица:**</span><span class="sxs-lookup"><span data-stu-id="89b65-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="89b65-345">**Целевая таблица:**</span><span class="sxs-lookup"><span data-stu-id="89b65-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="89b65-346">Обратите внимание, что в целевой таблице есть столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="89b65-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="89b65-347">**Определение JSON исходного набора данных**</span><span class="sxs-lookup"><span data-stu-id="89b65-347">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="89b65-348">**Определение JSON целевого набора данных**</span><span class="sxs-lookup"><span data-stu-id="89b65-348">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="89b65-349">Обратите внимание, что у исходной и целевой таблиц разные схемы (в целевой есть дополнительный столбец с идентификаторами).</span><span class="sxs-lookup"><span data-stu-id="89b65-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="89b65-350">В этом случае необходимо указать свойство **structure** в определении целевого набора данных, которое не включает в себя столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="89b65-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="89b65-351">Вызов хранимой процедуры из приемника SQL</span><span class="sxs-lookup"><span data-stu-id="89b65-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="89b65-352">Пример вызова хранимой процедуры из приемника SQL в действии копирования в конвейере приведен в статье [Invoke stored procedure from copy activity in Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md) (Вызов хранимой процедуры из действия копирования в фабрике данных Azure).</span><span class="sxs-lookup"><span data-stu-id="89b65-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="89b65-353">Сопоставление типов SQL Server</span><span class="sxs-lookup"><span data-stu-id="89b65-353">Type mapping for SQL server</span></span>
<span data-ttu-id="89b65-354">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в 2 этапа:</span><span class="sxs-lookup"><span data-stu-id="89b65-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="89b65-355">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="89b65-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="89b65-356">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="89b65-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="89b65-357">Когда данные перемещаются в базу данных SQL Server и обратно, для преобразования типа SQL в тип .NET и наоборот используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="89b65-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="89b65-358">Сопоставление аналогично сопоставлению типов данных SQL Server для ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="89b65-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="89b65-359">Тип ядра СУБД SQL Server</span><span class="sxs-lookup"><span data-stu-id="89b65-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="89b65-360">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="89b65-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="89b65-361">bigint</span><span class="sxs-lookup"><span data-stu-id="89b65-361">bigint</span></span> |<span data-ttu-id="89b65-362">Int64</span><span class="sxs-lookup"><span data-stu-id="89b65-362">Int64</span></span> |
| <span data-ttu-id="89b65-363">binary;</span><span class="sxs-lookup"><span data-stu-id="89b65-363">binary</span></span> |<span data-ttu-id="89b65-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-364">Byte[]</span></span> |
| <span data-ttu-id="89b65-365">bit</span><span class="sxs-lookup"><span data-stu-id="89b65-365">bit</span></span> |<span data-ttu-id="89b65-366">Логический</span><span class="sxs-lookup"><span data-stu-id="89b65-366">Boolean</span></span> |
| <span data-ttu-id="89b65-367">char;</span><span class="sxs-lookup"><span data-stu-id="89b65-367">char</span></span> |<span data-ttu-id="89b65-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-368">String, Char[]</span></span> |
| <span data-ttu-id="89b65-369">дата</span><span class="sxs-lookup"><span data-stu-id="89b65-369">date</span></span> |<span data-ttu-id="89b65-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="89b65-370">DateTime</span></span> |
| <span data-ttu-id="89b65-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="89b65-371">Datetime</span></span> |<span data-ttu-id="89b65-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="89b65-372">DateTime</span></span> |
| <span data-ttu-id="89b65-373">datetime2;</span><span class="sxs-lookup"><span data-stu-id="89b65-373">datetime2</span></span> |<span data-ttu-id="89b65-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="89b65-374">DateTime</span></span> |
| <span data-ttu-id="89b65-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="89b65-375">Datetimeoffset</span></span> |<span data-ttu-id="89b65-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="89b65-376">DateTimeOffset</span></span> |
| <span data-ttu-id="89b65-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="89b65-377">Decimal</span></span> |<span data-ttu-id="89b65-378">Decimal</span><span class="sxs-lookup"><span data-stu-id="89b65-378">Decimal</span></span> |
| <span data-ttu-id="89b65-379">Атрибут FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="89b65-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="89b65-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-380">Byte[]</span></span> |
| <span data-ttu-id="89b65-381">Float</span><span class="sxs-lookup"><span data-stu-id="89b65-381">Float</span></span> |<span data-ttu-id="89b65-382">Double</span><span class="sxs-lookup"><span data-stu-id="89b65-382">Double</span></span> |
| <span data-ttu-id="89b65-383">изображение</span><span class="sxs-lookup"><span data-stu-id="89b65-383">image</span></span> |<span data-ttu-id="89b65-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-384">Byte[]</span></span> |
| <span data-ttu-id="89b65-385">int</span><span class="sxs-lookup"><span data-stu-id="89b65-385">int</span></span> |<span data-ttu-id="89b65-386">Int32</span><span class="sxs-lookup"><span data-stu-id="89b65-386">Int32</span></span> |
| <span data-ttu-id="89b65-387">money;</span><span class="sxs-lookup"><span data-stu-id="89b65-387">money</span></span> |<span data-ttu-id="89b65-388">Decimal</span><span class="sxs-lookup"><span data-stu-id="89b65-388">Decimal</span></span> |
| <span data-ttu-id="89b65-389">nchar;</span><span class="sxs-lookup"><span data-stu-id="89b65-389">nchar</span></span> |<span data-ttu-id="89b65-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-390">String, Char[]</span></span> |
| <span data-ttu-id="89b65-391">ntext</span><span class="sxs-lookup"><span data-stu-id="89b65-391">ntext</span></span> |<span data-ttu-id="89b65-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-392">String, Char[]</span></span> |
| <span data-ttu-id="89b65-393">numeric</span><span class="sxs-lookup"><span data-stu-id="89b65-393">numeric</span></span> |<span data-ttu-id="89b65-394">Decimal</span><span class="sxs-lookup"><span data-stu-id="89b65-394">Decimal</span></span> |
| <span data-ttu-id="89b65-395">nvarchar;</span><span class="sxs-lookup"><span data-stu-id="89b65-395">nvarchar</span></span> |<span data-ttu-id="89b65-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-396">String, Char[]</span></span> |
| <span data-ttu-id="89b65-397">real;</span><span class="sxs-lookup"><span data-stu-id="89b65-397">real</span></span> |<span data-ttu-id="89b65-398">Single</span><span class="sxs-lookup"><span data-stu-id="89b65-398">Single</span></span> |
| <span data-ttu-id="89b65-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="89b65-399">rowversion</span></span> |<span data-ttu-id="89b65-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-400">Byte[]</span></span> |
| <span data-ttu-id="89b65-401">smalldatetime;</span><span class="sxs-lookup"><span data-stu-id="89b65-401">smalldatetime</span></span> |<span data-ttu-id="89b65-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="89b65-402">DateTime</span></span> |
| <span data-ttu-id="89b65-403">smallint;</span><span class="sxs-lookup"><span data-stu-id="89b65-403">smallint</span></span> |<span data-ttu-id="89b65-404">Int16</span><span class="sxs-lookup"><span data-stu-id="89b65-404">Int16</span></span> |
| <span data-ttu-id="89b65-405">smallmoney;</span><span class="sxs-lookup"><span data-stu-id="89b65-405">smallmoney</span></span> |<span data-ttu-id="89b65-406">Decimal</span><span class="sxs-lookup"><span data-stu-id="89b65-406">Decimal</span></span> |
| <span data-ttu-id="89b65-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="89b65-407">sql_variant</span></span> |<span data-ttu-id="89b65-408">Object *</span><span class="sxs-lookup"><span data-stu-id="89b65-408">Object *</span></span> |
| <span data-ttu-id="89b65-409">text</span><span class="sxs-lookup"><span data-stu-id="89b65-409">text</span></span> |<span data-ttu-id="89b65-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-410">String, Char[]</span></span> |
| <span data-ttu-id="89b65-411">time</span><span class="sxs-lookup"><span data-stu-id="89b65-411">time</span></span> |<span data-ttu-id="89b65-412">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="89b65-412">TimeSpan</span></span> |
| <span data-ttu-id="89b65-413">Timestamp</span><span class="sxs-lookup"><span data-stu-id="89b65-413">timestamp</span></span> |<span data-ttu-id="89b65-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-414">Byte[]</span></span> |
| <span data-ttu-id="89b65-415">tinyint;</span><span class="sxs-lookup"><span data-stu-id="89b65-415">tinyint</span></span> |<span data-ttu-id="89b65-416">Byte</span><span class="sxs-lookup"><span data-stu-id="89b65-416">Byte</span></span> |
| <span data-ttu-id="89b65-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="89b65-417">uniqueidentifier</span></span> |<span data-ttu-id="89b65-418">Guid</span><span class="sxs-lookup"><span data-stu-id="89b65-418">Guid</span></span> |
| <span data-ttu-id="89b65-419">varbinary;</span><span class="sxs-lookup"><span data-stu-id="89b65-419">varbinary</span></span> |<span data-ttu-id="89b65-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="89b65-420">Byte[]</span></span> |
| <span data-ttu-id="89b65-421">varchar.</span><span class="sxs-lookup"><span data-stu-id="89b65-421">varchar</span></span> |<span data-ttu-id="89b65-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="89b65-422">String, Char[]</span></span> |
| <span data-ttu-id="89b65-423">xml</span><span class="sxs-lookup"><span data-stu-id="89b65-423">xml</span></span> |<span data-ttu-id="89b65-424">xml</span><span class="sxs-lookup"><span data-stu-id="89b65-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="89b65-425">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="89b65-425">Mapping source to sink columns</span></span>
<span data-ttu-id="89b65-426">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в разделе [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="89b65-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="89b65-427">Повторяющаяся операция копирования</span><span class="sxs-lookup"><span data-stu-id="89b65-427">Repeatable copy</span></span>
<span data-ttu-id="89b65-428">При копировании данных в базу данных SQL Server действие копирования по умолчанию добавляет данные в таблицу приемника.</span><span class="sxs-lookup"><span data-stu-id="89b65-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="89b65-429">Чтобы вместо этого выполнить операцию UPSERT, изучите раздел [Повторяемая запись в SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="89b65-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="89b65-430">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="89b65-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="89b65-431">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="89b65-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="89b65-432">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="89b65-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="89b65-433">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="89b65-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="89b65-434">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="89b65-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="89b65-435">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="89b65-435">Performance and Tuning</span></span>
<span data-ttu-id="89b65-436">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="89b65-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
