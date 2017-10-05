---
title: "Перемещение данных из локальной системы HDFS | Документация Майкрософт"
description: "Узнайте, как перемещать данные из локальной системы HDFS с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="cddeb-103">Перемещение данных из локальной системы HDFS с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="cddeb-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="cddeb-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локальной системы HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="cddeb-105">Этот документ является продолжением статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="cddeb-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="cddeb-106">Данные из HDFS можно скопировать в любое поддерживаемое хранилище данных, используемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="cddeb-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="cddeb-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, см. в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="cddeb-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="cddeb-108">Сейчас фабрика данных поддерживает перемещение данных из локальной системы HDFS в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="cddeb-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="cddeb-109">Действие копирования не удаляет исходный файл после его успешного копирования в место назначения.</span><span class="sxs-lookup"><span data-stu-id="cddeb-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="cddeb-110">Если необходимо удалить исходный файл после успешного копирования, создайте настраиваемое действие для удаления файла и используйте это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="cddeb-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="cddeb-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="cddeb-111">Enabling connectivity</span></span>
<span data-ttu-id="cddeb-112">Служба фабрики данных поддерживает подключение к локальной системе HDFS с помощью шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="cddeb-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="cddeb-113">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="cddeb-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="cddeb-114">Шлюз используется для подключения к HDFS, даже если он размещен на виртуальных машинах Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="cddeb-115">Убедитесь, что шлюзу управления данными доступны **ВСЕ** адреса [сервер_узла_имен]:[порт_узла_имен] и [сервер_узла_данных]:[порт_узла_данных] кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cddeb-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="cddeb-116">По умолчанию используются [порт_узла_имен] 50070 и [порт_узла_данных] 50075.</span><span class="sxs-lookup"><span data-stu-id="cddeb-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="cddeb-117">Хотя шлюз можно установить на тот же локальный компьютер или виртуальную машину Azure, где находится HDFS, мы рекомендуем устанавливать шлюз на отдельный компьютер или отдельную виртуальную машину Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="cddeb-118">Если для шлюза будет выделен отдельный компьютер, это минимизирует вероятность конфликта ресурсов и повысит производительность.</span><span class="sxs-lookup"><span data-stu-id="cddeb-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="cddeb-119">При установке шлюза на отдельный компьютер у компьютера должен быть доступ к машине с HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cddeb-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="cddeb-120">Getting started</span></span>
<span data-ttu-id="cddeb-121">Вы можете создать конвейер с действием копирования, которое перемещает данные из HDFS, с помощью разных средств и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="cddeb-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="cddeb-122">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="cddeb-123">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="cddeb-124">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cddeb-125">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="cddeb-126">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cddeb-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="cddeb-127">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="cddeb-128">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="cddeb-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="cddeb-129">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="cddeb-130">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="cddeb-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="cddeb-131">При использовании средств и API-интерфейсов (за исключением .NET API) эти сущности фабрики данных определяются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cddeb-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="cddeb-132">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных HDFS, вы найдете в разделе [Пример определений JSON. Копирование данных из локальной системы HDFS в хранилище BLOB-объектов Azure](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cddeb-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="cddeb-133">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для системы HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cddeb-134">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="cddeb-134">Linked service properties</span></span>
<span data-ttu-id="cddeb-135">Связанная служба привязывает хранилище данных к фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="cddeb-136">Для связи локальной системы HDFS с фабрикой данных следует создать связанную службу типа **Hdfs**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="cddeb-137">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="cddeb-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="cddeb-138">Property</span></span> | <span data-ttu-id="cddeb-139">Описание</span><span class="sxs-lookup"><span data-stu-id="cddeb-139">Description</span></span> | <span data-ttu-id="cddeb-140">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cddeb-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cddeb-141">type</span><span class="sxs-lookup"><span data-stu-id="cddeb-141">type</span></span> |<span data-ttu-id="cddeb-142">Для свойства type необходимо задать значение **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="cddeb-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="cddeb-143">Да</span><span class="sxs-lookup"><span data-stu-id="cddeb-143">Yes</span></span> |
| <span data-ttu-id="cddeb-144">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="cddeb-144">Url</span></span> |<span data-ttu-id="cddeb-145">URL-адрес в HDFS</span><span class="sxs-lookup"><span data-stu-id="cddeb-145">URL to the HDFS</span></span> |<span data-ttu-id="cddeb-146">Да</span><span class="sxs-lookup"><span data-stu-id="cddeb-146">Yes</span></span> |
| <span data-ttu-id="cddeb-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cddeb-147">authenticationType</span></span> |<span data-ttu-id="cddeb-148">Anonymous или Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="cddeb-149">Чтобы использовать **аутентификацию Kerberos** для соединителя HDFS, настройте локальную среду, как описано [здесь](#use-kerberos-authentication-for-hdfs-connector).</span><span class="sxs-lookup"><span data-stu-id="cddeb-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="cddeb-150">Да</span><span class="sxs-lookup"><span data-stu-id="cddeb-150">Yes</span></span> |
| <span data-ttu-id="cddeb-151">userName</span><span class="sxs-lookup"><span data-stu-id="cddeb-151">userName</span></span> |<span data-ttu-id="cddeb-152">Имя пользователя для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-152">Username for Windows authentication.</span></span> |<span data-ttu-id="cddeb-153">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="cddeb-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="cddeb-154">пароль</span><span class="sxs-lookup"><span data-stu-id="cddeb-154">password</span></span> |<span data-ttu-id="cddeb-155">Пароль для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-155">Password for Windows authentication.</span></span> |<span data-ttu-id="cddeb-156">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="cddeb-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="cddeb-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cddeb-157">gatewayName</span></span> |<span data-ttu-id="cddeb-158">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной системе HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="cddeb-159">Да</span><span class="sxs-lookup"><span data-stu-id="cddeb-159">Yes</span></span> |
| <span data-ttu-id="cddeb-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="cddeb-160">encryptedCredential</span></span> |<span data-ttu-id="cddeb-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выводит учетные данные доступа.</span><span class="sxs-lookup"><span data-stu-id="cddeb-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="cddeb-162">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="cddeb-163">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="cddeb-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="cddeb-164">Использовать проверку подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="cddeb-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="cddeb-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="cddeb-165">Dataset properties</span></span>
<span data-ttu-id="cddeb-166">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cddeb-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cddeb-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cddeb-168">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="cddeb-169">Раздел typeProperties набора данных типа **FileShare** (который включает набор данных HDFS) содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="cddeb-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="cddeb-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="cddeb-170">Property</span></span> | <span data-ttu-id="cddeb-171">Описание</span><span class="sxs-lookup"><span data-stu-id="cddeb-171">Description</span></span> | <span data-ttu-id="cddeb-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cddeb-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cddeb-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="cddeb-173">folderPath</span></span> |<span data-ttu-id="cddeb-174">Путь к папке,</span><span class="sxs-lookup"><span data-stu-id="cddeb-174">Path to the folder.</span></span> <span data-ttu-id="cddeb-175">Пример: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="cddeb-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="cddeb-176">Чтобы указать специальные знаки в строке, используйте escape-знак "\".</span><span class="sxs-lookup"><span data-stu-id="cddeb-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="cddeb-177">Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".</span><span class="sxs-lookup"><span data-stu-id="cddeb-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="cddeb-178">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="cddeb-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="cddeb-179">Да</span><span class="sxs-lookup"><span data-stu-id="cddeb-179">Yes</span></span> |
| <span data-ttu-id="cddeb-180">fileName</span><span class="sxs-lookup"><span data-stu-id="cddeb-180">fileName</span></span> |<span data-ttu-id="cddeb-181">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="cddeb-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="cddeb-182">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="cddeb-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="cddeb-183">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="cddeb-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="cddeb-184">Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="cddeb-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="cddeb-185">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-185">No</span></span> |
| <span data-ttu-id="cddeb-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cddeb-186">partitionedBy</span></span> |<span data-ttu-id="cddeb-187">Чтобы указать для временного ряда данных динамические путь к папке и имя файла, используйте свойство partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="cddeb-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="cddeb-188">Например, путь к папке (folderPath) каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="cddeb-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="cddeb-189">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-189">No</span></span> |
| <span data-ttu-id="cddeb-190">свойства</span><span class="sxs-lookup"><span data-stu-id="cddeb-190">format</span></span> | <span data-ttu-id="cddeb-191">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cddeb-192">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="cddeb-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="cddeb-193">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="cddeb-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cddeb-194">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cddeb-195">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-195">No</span></span> |
| <span data-ttu-id="cddeb-196">compression</span><span class="sxs-lookup"><span data-stu-id="cddeb-196">compression</span></span> | <span data-ttu-id="cddeb-197">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="cddeb-198">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="cddeb-199">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cddeb-200">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="cddeb-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cddeb-201">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="cddeb-202">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="cddeb-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="cddeb-203">Использование свойства partionedBy</span><span class="sxs-lookup"><span data-stu-id="cddeb-203">Using partionedBy property</span></span>
<span data-ttu-id="cddeb-204">Как сказано выше, для данных временных рядов путь к папке (folderPath) и имя файла (fileName) можно указывать динамически. Это делается с помощью свойства **partitionedBy**, [функций фабрики данных и системных переменных](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="cddeb-205">Чтобы узнать больше о наборах данных временных рядов, планировании и срезах, ознакомьтесь со статьями [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md), [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) и [Конвейеры и действия в фабрике данных Azure: создание конвейеров, цепочки действий и расписаний для них](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="cddeb-206">Пример 1</span><span class="sxs-lookup"><span data-stu-id="cddeb-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="cddeb-207">В этом примере {Slice} заменяется значением SliceStart (системная переменная фабрики данных) в формате ГГГГММДДЧЧ.</span><span class="sxs-lookup"><span data-stu-id="cddeb-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="cddeb-208">SliceStart указывает время начала среза.</span><span class="sxs-lookup"><span data-stu-id="cddeb-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="cddeb-209">Значение folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="cddeb-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="cddeb-210">Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="cddeb-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="cddeb-211">Пример 2</span><span class="sxs-lookup"><span data-stu-id="cddeb-211">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="cddeb-212">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="cddeb-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cddeb-213">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="cddeb-213">Copy activity properties</span></span>
<span data-ttu-id="cddeb-214">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cddeb-215">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="cddeb-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="cddeb-216">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="cddeb-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="cddeb-217">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="cddeb-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="cddeb-218">Для действия копирования, когда источник относится к типу **FileSystemSource** , в разделе typeProperties доступны указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="cddeb-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="cddeb-219">**FileSystemSource** поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="cddeb-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="cddeb-220">Свойство</span><span class="sxs-lookup"><span data-stu-id="cddeb-220">Property</span></span> | <span data-ttu-id="cddeb-221">Описание</span><span class="sxs-lookup"><span data-stu-id="cddeb-221">Description</span></span> | <span data-ttu-id="cddeb-222">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="cddeb-222">Allowed values</span></span> | <span data-ttu-id="cddeb-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cddeb-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cddeb-224">recursive</span><span class="sxs-lookup"><span data-stu-id="cddeb-224">recursive</span></span> |<span data-ttu-id="cddeb-225">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="cddeb-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="cddeb-226">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cddeb-226">True, False (default)</span></span> |<span data-ttu-id="cddeb-227">Нет</span><span class="sxs-lookup"><span data-stu-id="cddeb-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="cddeb-228">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="cddeb-228">Supported file and compression formats</span></span>
<span data-ttu-id="cddeb-229">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="cddeb-230">Пример определений JSON. Копирование данных из локальной системы HDFS в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="cddeb-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="cddeb-231">Из этого примера вы узнаете, как копировать данные из локальной файловой системы HDFS в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cddeb-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="cddeb-232">Тем не менее данные можно копировать **непосредственно** в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cddeb-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="cddeb-233">Пример содержит определения JSON для следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cddeb-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="cddeb-234">Используя эти определения, вы можете создать конвейер для копирования данных из HDFS в хранилище BLOB-объектов Azure с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="cddeb-235">Связанная служба типа [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="cddeb-236">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cddeb-237">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="cddeb-238">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cddeb-239">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cddeb-240">В примере данные из локальной системы HDFS копируются в BLOB-объект Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="cddeb-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="cddeb-241">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="cddeb-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="cddeb-242">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="cddeb-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="cddeb-243">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="cddeb-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="cddeb-244">**Связанная служба HDFS.** В этом примере используется проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="cddeb-245">Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="cddeb-246">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="cddeb-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="cddeb-247">**Входной набор данных HDFS.** Этот набор данных ссылается на папку в файловой системе HDFS DataTransfer/UnitTest/.</span><span class="sxs-lookup"><span data-stu-id="cddeb-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="cddeb-248">Конвейер копирует все файлы из этой папки в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="cddeb-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="cddeb-249">Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="cddeb-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="cddeb-250">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="cddeb-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cddeb-251">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="cddeb-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cddeb-252">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="cddeb-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cddeb-253">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="cddeb-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="cddeb-254">**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="cddeb-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="cddeb-255">Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="cddeb-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cddeb-256">В определении JSON конвейера для типа **source** установлено значение **FileSystemSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="cddeb-257">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="cddeb-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="cddeb-258">Использование аутентификации Kerberos для соединителя HDFS</span><span class="sxs-lookup"><span data-stu-id="cddeb-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="cddeb-259">Есть два способа настроить локальную среду для использования аутентификации Kerberos в соединителе HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="cddeb-260">Вы можете применить тот, который соответствует вашему сценарию.</span><span class="sxs-lookup"><span data-stu-id="cddeb-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="cddeb-261">Способ 1. [Присоединение компьютера шлюза к области Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="cddeb-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="cddeb-262">Вариант 2. [Активация взаимного доверия между доменом Windows и областью Kerberos](#kerberos-mutual-trust).</span><span class="sxs-lookup"><span data-stu-id="cddeb-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="cddeb-263"><a name="kerberos-join-realm"></a>Способ 1. Присоединение компьютера шлюза к области Kerberos</span><span class="sxs-lookup"><span data-stu-id="cddeb-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="cddeb-264">Условие</span><span class="sxs-lookup"><span data-stu-id="cddeb-264">Requirement:</span></span>

* <span data-ttu-id="cddeb-265">Компьютер шлюза нужно присоединить к области Kerberos; его нельзя присоединять к домену Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="cddeb-266">Процесс настройки</span><span class="sxs-lookup"><span data-stu-id="cddeb-266">How to configure:</span></span>

<span data-ttu-id="cddeb-267">**Настройка на компьютере шлюза**</span><span class="sxs-lookup"><span data-stu-id="cddeb-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="cddeb-268">Запустите служебную программу **Ksetup** для настройки сервера центра распространения ключей и области Kerberos.</span><span class="sxs-lookup"><span data-stu-id="cddeb-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="cddeb-269">Компьютер должен быть настроен как член рабочей группы, так как области Kerberos отличаются от доменов Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="cddeb-270">Для этого нужно настроить область Kerberos и добавить сервер центра распространения ключей, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="cddeb-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="cddeb-271">Вместо *REALM.COM* укажите соответствующее имя области.</span><span class="sxs-lookup"><span data-stu-id="cddeb-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="cddeb-272">**Перезапустите** компьютер после выполнения этих двух команд.</span><span class="sxs-lookup"><span data-stu-id="cddeb-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="cddeb-273">Проверьте конфигурацию с помощью команды **Ksetup**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="cddeb-274">Результат должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="cddeb-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="cddeb-275">**Настройка фабрики данных Azure**</span><span class="sxs-lookup"><span data-stu-id="cddeb-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="cddeb-276">Настройте соединитель HDFS на использование **аутентификации Windows**, указав имя участника Kerberos и пароль для подключения к источнику данных HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="cddeb-277">Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="cddeb-278"><a name="kerberos-mutual-trust"></a>Вариант 2. Активация взаимного доверия между доменом Windows и областью Kerberos</span><span class="sxs-lookup"><span data-stu-id="cddeb-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="cddeb-279">Условие</span><span class="sxs-lookup"><span data-stu-id="cddeb-279">Requirement:</span></span>
*   <span data-ttu-id="cddeb-280">Компьютер шлюза должен быть присоединен к домену Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="cddeb-281">Вам потребуются права на изменение параметров контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="cddeb-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="cddeb-282">Процесс настройки</span><span class="sxs-lookup"><span data-stu-id="cddeb-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="cddeb-283">Вместо REALM.COM и AD.COM в приведенном ниже примере укажите соответствующие имена области и контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="cddeb-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="cddeb-284">**Настройка на сервере центра распространения ключей**</span><span class="sxs-lookup"><span data-stu-id="cddeb-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="cddeb-285">Измените конфигурацию центра распространения ключей в файле **krb5.conf**, чтобы создать отношения доверия с доменом Windows, как указано ниже в шаблоне конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cddeb-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="cddeb-286">По умолчанию эта конфигурация находится в файле **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="cddeb-287">**Перезапустите** службу KDC после настройки.</span><span class="sxs-lookup"><span data-stu-id="cddeb-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="cddeb-288">Подготовьте субъект-службу с именем **krbtgt/REALM.COM@AD.COM** на сервере центра распространения ключей, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cddeb-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="cddeb-289">В файле **hadoop.security.auth_to_local** добавьте к конфигурации HDFS правило `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="cddeb-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="cddeb-290">**Настройка на контроллере домена**</span><span class="sxs-lookup"><span data-stu-id="cddeb-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="cddeb-291">Выполните приведенные ниже команды **Ksetup**, чтобы добавить запись области:</span><span class="sxs-lookup"><span data-stu-id="cddeb-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="cddeb-292">Установите доверительные отношения между доменом Windows и областью Kerberos.</span><span class="sxs-lookup"><span data-stu-id="cddeb-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="cddeb-293">Вместо [password] укажите пароль субъекта **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="cddeb-294">Выберите алгоритм шифрования, используемый в Kerberos.</span><span class="sxs-lookup"><span data-stu-id="cddeb-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="cddeb-295">Последовательно выберите "Диспетчер серверов" > "Управление групповой политикой" > "Домен" > "Объекты групповой политики" > "Групповая политика по умолчанию или действующая групповая политика", затем нажмите "Редактировать".</span><span class="sxs-lookup"><span data-stu-id="cddeb-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="cddeb-296">Откроется всплывающее окно **редактора управления групповой политикой**. Последовательно выберите "Конфигурация компьютера" > "Политики" > "Параметры Windows" > "Параметры безопасности" > "Локальные политики" > "Параметры безопасности". Затем щелкните **Сетевая безопасность: настройка типов шифрования, разрешенных Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="cddeb-297">Выберите алгоритм шифрования, который вы хотите использовать при подключении к центру распространения ключей.</span><span class="sxs-lookup"><span data-stu-id="cddeb-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="cddeb-298">Обычно можно просто выбрать все доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="cddeb-298">Commonly, you can simply select all the options.</span></span>

        ![Типы шифрования конфигурации для Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="cddeb-300">С помощью команды **Ksetup** задайте алгоритм шифрования, который будет использоваться для этой области.</span><span class="sxs-lookup"><span data-stu-id="cddeb-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="cddeb-301">Создайте сопоставление между субъектом Kerberos и учетной записью домена, чтобы использовать субъект Kerberos в домене Windows.</span><span class="sxs-lookup"><span data-stu-id="cddeb-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="cddeb-302">Щелкните "Средства администрирования" и выберите **Пользователи и компьютеры Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="cddeb-303">Настройте расширенные функции, щелкнув **Просмотр** > **Расширенные функции**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="cddeb-304">Найдите учетную запись, для которой нужно создать сопоставление, и щелкните ее правой кнопкой мыши, чтобы открыть **Сопоставление имен** > **Имена Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="cddeb-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="cddeb-305">Добавьте субъект-службу из области.</span><span class="sxs-lookup"><span data-stu-id="cddeb-305">Add a principal from the realm.</span></span>

        ![Сопоставление удостоверения безопасности](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="cddeb-307">**Настройка на компьютере шлюза**</span><span class="sxs-lookup"><span data-stu-id="cddeb-307">**On gateway machine:**</span></span>

* <span data-ttu-id="cddeb-308">Выполните приведенные ниже команды **Ksetup**, чтобы добавить запись области.</span><span class="sxs-lookup"><span data-stu-id="cddeb-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="cddeb-309">**Настройка фабрики данных Azure**</span><span class="sxs-lookup"><span data-stu-id="cddeb-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="cddeb-310">Настройте соединитель HDFS для использования **аутентификации Windows**, указав учетную запись домена или имя субъекта-службы Kerberos для подключения к источнику данных HDFS.</span><span class="sxs-lookup"><span data-stu-id="cddeb-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="cddeb-311">Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cddeb-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="cddeb-312">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cddeb-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="cddeb-313">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="cddeb-313">Performance and Tuning</span></span>
<span data-ttu-id="cddeb-314">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="cddeb-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
