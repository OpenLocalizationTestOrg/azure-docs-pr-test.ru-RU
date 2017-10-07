---
title: "aaaMove данных из HDFS в локальной среде | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из локальной HDFS, с помощью фабрики данных Azure."
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
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="f6041-103">Перемещение данных из локальной системы HDFS с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="f6041-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="f6041-104">В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данных из HDFS в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="f6041-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="f6041-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="f6041-106">Можно скопировать данные из хранилища данных приемник tooany поддерживается HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="f6041-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="f6041-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f6041-108">Фабрики данных в настоящее время поддерживает только перемещения данных из хранилищ данных tooother HDFS в локальной среде, но не для перемещения данных из других данных tooan хранилищ локальной HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="f6041-109">Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello.</span><span class="sxs-lookup"><span data-stu-id="f6041-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="f6041-110">Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="f6041-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="f6041-111">Enabling connectivity</span></span>
<span data-ttu-id="f6041-112">Служба фабрики данных поддерживает подключения локальной tooon HDFS, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="f6041-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="f6041-113">В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="f6041-114">Используйте tooHDFS tooconnect шлюза hello, даже если она размещается на виртуальной Машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="f6041-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="f6041-115">Убедитесь, что hello шлюз управления данными можно получить доступ к слишком**все** hello [имя узла сервера]: [порт узла name] и [серверов узла данных]: [порт данных узла] hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f6041-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="f6041-116">По умолчанию используются [порт_узла_имен] 50070 и [порт_узла_данных] 50075.</span><span class="sxs-lookup"><span data-stu-id="f6041-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="f6041-117">Хотя можно установить шлюз на hello же локального компьютера или виртуальной Машине Azure hello как hello HDFS, рекомендуется устанавливать шлюз hello на отдельных машин/Azure IaaS виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f6041-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="f6041-118">Если для шлюза будет выделен отдельный компьютер, это минимизирует вероятность конфликта ресурсов и повысит производительность.</span><span class="sxs-lookup"><span data-stu-id="f6041-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="f6041-119">При установке шлюза hello на отдельном компьютере hello машина должна была машину hello может tooaccess с hello HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f6041-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="f6041-120">Getting started</span></span>
<span data-ttu-id="f6041-121">Вы можете создать конвейер с действием копирования, которое перемещает данные из HDFS, с помощью разных средств и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="f6041-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="f6041-122">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="f6041-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f6041-123">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="f6041-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f6041-124">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="f6041-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f6041-125">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="f6041-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="f6041-126">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="f6041-127">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f6041-128">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="f6041-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="f6041-129">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="f6041-130">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="f6041-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f6041-131">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f6041-132">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных HDFS см [пример JSON: копирование данных из HDFS в локальной среде tooAzure большого двоичного объекта](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) данной статьи.</span><span class="sxs-lookup"><span data-stu-id="f6041-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="f6041-133">Hello в следующих разделах подробно JSON свойства, которые являются определенной tooHDFS используется toodefine фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="f6041-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f6041-134">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="f6041-134">Linked service properties</span></span>
<span data-ttu-id="f6041-135">Связанная служба связывает фабрику данных tooa хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="f6041-136">Создание связанной службы типа **Hdfs** toolink фабрикой данных tooyour HDFS в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="f6041-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="f6041-137">Hello в следующей таблице приводится описание службы конкретных tooHDFS связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="f6041-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="f6041-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="f6041-138">Property</span></span> | <span data-ttu-id="f6041-139">Описание</span><span class="sxs-lookup"><span data-stu-id="f6041-139">Description</span></span> | <span data-ttu-id="f6041-140">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f6041-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6041-141">type</span><span class="sxs-lookup"><span data-stu-id="f6041-141">type</span></span> |<span data-ttu-id="f6041-142">свойство типа Hello должно быть присвоено: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="f6041-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="f6041-143">Да</span><span class="sxs-lookup"><span data-stu-id="f6041-143">Yes</span></span> |
| <span data-ttu-id="f6041-144">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="f6041-144">Url</span></span> |<span data-ttu-id="f6041-145">URL-адрес toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="f6041-145">URL toohello HDFS</span></span> |<span data-ttu-id="f6041-146">Да</span><span class="sxs-lookup"><span data-stu-id="f6041-146">Yes</span></span> |
| <span data-ttu-id="f6041-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f6041-147">authenticationType</span></span> |<span data-ttu-id="f6041-148">Anonymous или Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="f6041-149">toouse **проверки подлинности Kerberos** HDFS соединителя, см. в разделе слишком[в этом разделе](#use-kerberos-authentication-for-hdfs-connector) tooset вверх в локальной среде соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f6041-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="f6041-150">Да</span><span class="sxs-lookup"><span data-stu-id="f6041-150">Yes</span></span> |
| <span data-ttu-id="f6041-151">userName</span><span class="sxs-lookup"><span data-stu-id="f6041-151">userName</span></span> |<span data-ttu-id="f6041-152">Имя пользователя для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-152">Username for Windows authentication.</span></span> |<span data-ttu-id="f6041-153">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="f6041-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="f6041-154">пароль</span><span class="sxs-lookup"><span data-stu-id="f6041-154">password</span></span> |<span data-ttu-id="f6041-155">Пароль для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-155">Password for Windows authentication.</span></span> |<span data-ttu-id="f6041-156">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="f6041-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="f6041-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f6041-157">gatewayName</span></span> |<span data-ttu-id="f6041-158">Имя шлюза hello, hello служба фабрики данных следует использовать tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="f6041-159">Да</span><span class="sxs-lookup"><span data-stu-id="f6041-159">Yes</span></span> |
| <span data-ttu-id="f6041-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f6041-160">encryptedCredential</span></span> |<span data-ttu-id="f6041-161">[Новый AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выходных данных учетные данные доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="f6041-162">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="f6041-163">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="f6041-163">Using Anonymous authentication</span></span>

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

### <a name="using-windows-authentication"></a><span data-ttu-id="f6041-164">Использовать проверку подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="f6041-164">Using Windows authentication</span></span>

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
## <a name="dataset-properties"></a><span data-ttu-id="f6041-165">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="f6041-165">Dataset properties</span></span>
<span data-ttu-id="f6041-166">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f6041-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f6041-167">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="f6041-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f6041-168">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f6041-169">Hello typeProperties статьи для набора данных типа **FileShare** (включает набор данных HDFS) имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="f6041-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="f6041-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="f6041-170">Property</span></span> | <span data-ttu-id="f6041-171">Описание</span><span class="sxs-lookup"><span data-stu-id="f6041-171">Description</span></span> | <span data-ttu-id="f6041-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f6041-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6041-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="f6041-173">folderPath</span></span> |<span data-ttu-id="f6041-174">Путь к папке toohello.</span><span class="sxs-lookup"><span data-stu-id="f6041-174">Path toohello folder.</span></span> <span data-ttu-id="f6041-175">Пример: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="f6041-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="f6041-176">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="f6041-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="f6041-177">Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".</span><span class="sxs-lookup"><span data-stu-id="f6041-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="f6041-178">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="f6041-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="f6041-179">Да</span><span class="sxs-lookup"><span data-stu-id="f6041-179">Yes</span></span> |
| <span data-ttu-id="f6041-180">fileName</span><span class="sxs-lookup"><span data-stu-id="f6041-180">fileName</span></span> |<span data-ttu-id="f6041-181">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="f6041-182">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="f6041-183">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f6041-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="f6041-184">Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="f6041-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="f6041-185">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-185">No</span></span> |
| <span data-ttu-id="f6041-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="f6041-186">partitionedBy</span></span> |<span data-ttu-id="f6041-187">partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="f6041-188">Например, путь к папке (folderPath) каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="f6041-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="f6041-189">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-189">No</span></span> |
| <span data-ttu-id="f6041-190">свойства</span><span class="sxs-lookup"><span data-stu-id="f6041-190">format</span></span> | <span data-ttu-id="f6041-191">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f6041-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f6041-192">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="f6041-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="f6041-193">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="f6041-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="f6041-194">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="f6041-195">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-195">No</span></span> |
| <span data-ttu-id="f6041-196">compression</span><span class="sxs-lookup"><span data-stu-id="f6041-196">compression</span></span> | <span data-ttu-id="f6041-197">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="f6041-198">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f6041-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f6041-199">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="f6041-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f6041-200">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f6041-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f6041-201">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="f6041-202">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="f6041-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="f6041-203">Использование свойства partionedBy</span><span class="sxs-lookup"><span data-stu-id="f6041-203">Using partionedBy property</span></span>
<span data-ttu-id="f6041-204">Как упоминалось в предыдущем разделе hello, можно указать динамического folderPath и filename для временного ряда данных с hello **partitionedBy** свойства [функции фабрики данных, а системные переменные hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="f6041-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="f6041-205">toolearn Дополнительные сведения о наборах данных ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и исполнение](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md) статей.</span><span class="sxs-lookup"><span data-stu-id="f6041-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="f6041-206">Пример 1</span><span class="sxs-lookup"><span data-stu-id="f6041-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="f6041-207">В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ) указан.</span><span class="sxs-lookup"><span data-stu-id="f6041-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="f6041-208">Hello SliceStart ссылается toostart время hello среза.</span><span class="sxs-lookup"><span data-stu-id="f6041-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="f6041-209">Hello folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="f6041-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="f6041-210">Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="f6041-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="f6041-211">Пример 2</span><span class="sxs-lookup"><span data-stu-id="f6041-211">Sample 2:</span></span>

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
<span data-ttu-id="f6041-212">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="f6041-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f6041-213">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="f6041-213">Copy activity properties</span></span>
<span data-ttu-id="f6041-214">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f6041-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f6041-215">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="f6041-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f6041-216">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="f6041-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="f6041-217">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="f6041-218">Для действия копирования, когда источник типа **FileSystemSource** hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="f6041-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="f6041-219">**FileSystemSource** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="f6041-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="f6041-220">Свойство</span><span class="sxs-lookup"><span data-stu-id="f6041-220">Property</span></span> | <span data-ttu-id="f6041-221">Описание</span><span class="sxs-lookup"><span data-stu-id="f6041-221">Description</span></span> | <span data-ttu-id="f6041-222">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f6041-222">Allowed values</span></span> | <span data-ttu-id="f6041-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f6041-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f6041-224">recursive</span><span class="sxs-lookup"><span data-stu-id="f6041-224">recursive</span></span> |<span data-ttu-id="f6041-225">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="f6041-226">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="f6041-226">True, False (default)</span></span> |<span data-ttu-id="f6041-227">Нет</span><span class="sxs-lookup"><span data-stu-id="f6041-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f6041-228">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="f6041-228">Supported file and compression formats</span></span>
<span data-ttu-id="f6041-229">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="f6041-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="f6041-230">Пример JSON: копирование данных из HDFS в локальной среде tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="f6041-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="f6041-231">В этом примере показано, как данные toocopy из tooAzure HDFS локального хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f6041-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="f6041-232">Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f6041-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="f6041-233">Образец Hello предоставляет определения JSON для hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="f6041-234">Можно использовать эти определения toocreate toocopy конвейера данных из HDFS tooAzure хранилища больших двоичных объектов с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f6041-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="f6041-235">Связанная служба типа [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="f6041-236">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f6041-237">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="f6041-238">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f6041-239">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f6041-240">Образец Hello копирует данные из локальной HDFS tooan BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="f6041-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="f6041-241">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f6041-242">В качестве первого шага можно Настройте шлюз управления данными hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="f6041-243">Здравствуйте, инструкциям hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f6041-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f6041-244">**HDFS связанной службы:** в этом примере используется hello проверку подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="f6041-245">Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="f6041-246">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="f6041-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="f6041-247">**HDFS входной набор данных:** toohello HDFS папку DataTransfer/UnitTest ссылается этот набор данных или.</span><span class="sxs-lookup"><span data-stu-id="f6041-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="f6041-248">конвейер Hello копирует все файлы hello в это место назначения toohello папки.</span><span class="sxs-lookup"><span data-stu-id="f6041-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="f6041-249">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="f6041-250">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="f6041-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f6041-251">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="f6041-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f6041-252">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="f6041-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f6041-253">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="f6041-254">**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="f6041-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="f6041-255">конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="f6041-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f6041-256">В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f6041-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f6041-257">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="f6041-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="f6041-258">Использование аутентификации Kerberos для соединителя HDFS</span><span class="sxs-lookup"><span data-stu-id="f6041-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="f6041-259">Существует два tooset параметры копирования hello в локальную среду так, чтобы toouse проверки подлинности Kerberos в соединитель HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="f6041-260">Можно выбрать один hello лучше подходит в случае.</span><span class="sxs-lookup"><span data-stu-id="f6041-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="f6041-261">Способ 1. [Присоединение компьютера шлюза к области Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="f6041-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="f6041-262">Вариант 2. [Активация взаимного доверия между доменом Windows и областью Kerberos](#kerberos-mutual-trust).</span><span class="sxs-lookup"><span data-stu-id="f6041-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="f6041-263"><a name="kerberos-join-realm"></a>Способ 1. Присоединение компьютера шлюза к области Kerberos</span><span class="sxs-lookup"><span data-stu-id="f6041-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="f6041-264">Условие</span><span class="sxs-lookup"><span data-stu-id="f6041-264">Requirement:</span></span>

* <span data-ttu-id="f6041-265">компьютер шлюза Hello должен сферы Kerberos toojoin hello и не удается подключиться к любому домену Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="f6041-266">Как tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="f6041-266">How tooconfigure:</span></span>

<span data-ttu-id="f6041-267">**Настройка на компьютере шлюза**</span><span class="sxs-lookup"><span data-stu-id="f6041-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="f6041-268">Запустите hello **Ksetup** tooconfigure программа hello сервером центра распространения КЛЮЧЕЙ Kerberos и область.</span><span class="sxs-lookup"><span data-stu-id="f6041-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="f6041-269">машины Hello должен быть настроен как член рабочей группы, поскольку областью Kerberos отличается от домена Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="f6041-270">Это достигается путем установки сферы Kerberos hello и добавления сервера KDC следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f6041-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="f6041-271">Вместо *REALM.COM* укажите соответствующее имя области.</span><span class="sxs-lookup"><span data-stu-id="f6041-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="f6041-272">**Перезапустите** машину hello после выполнения этих команд 2.</span><span class="sxs-lookup"><span data-stu-id="f6041-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="f6041-273">Проверка конфигурации hello с **Ksetup** команды.</span><span class="sxs-lookup"><span data-stu-id="f6041-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="f6041-274">выходные данные Hello должен иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="f6041-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="f6041-275">**Настройка фабрики данных Azure**</span><span class="sxs-lookup"><span data-stu-id="f6041-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="f6041-276">Настройка с помощью соединителя hello HDFS **проверки подлинности Windows** вместе с Kerberos основного имени и пароля tooconnect toohello HDFS источника данных.</span><span class="sxs-lookup"><span data-stu-id="f6041-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="f6041-277">Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="f6041-278"><a name="kerberos-mutual-trust"></a>Вариант 2. Активация взаимного доверия между доменом Windows и областью Kerberos</span><span class="sxs-lookup"><span data-stu-id="f6041-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="f6041-279">Условие</span><span class="sxs-lookup"><span data-stu-id="f6041-279">Requirement:</span></span>
*   <span data-ttu-id="f6041-280">компьютер шлюза Hello необходимо присоединить к домену Windows.</span><span class="sxs-lookup"><span data-stu-id="f6041-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="f6041-281">Требуется задать параметры разрешений tooupdate hello контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="f6041-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="f6041-282">Как tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="f6041-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="f6041-283">Замените REALM.COM и AD.COM в hello, следующий учебник с собственного соответствующей области и контроллер домена, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f6041-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="f6041-284">**Настройка на сервере центра распространения ключей**</span><span class="sxs-lookup"><span data-stu-id="f6041-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="f6041-285">Изменение конфигурации KDC hello в **krb5.conf** toolet файл KDC доверия домена Windows, ссылающиеся toohello следующий шаблон конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f6041-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="f6041-286">По умолчанию hello конфигурации находится в **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="f6041-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

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

  <span data-ttu-id="f6041-287">**Перезапустите** hello после настройки службы KDC.</span><span class="sxs-lookup"><span data-stu-id="f6041-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="f6041-288">Подготовка участника с именем  **krbtgt/REALM.COM@AD.COM**  Server KDC с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6041-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="f6041-289">В файле **hadoop.security.auth_to_local** добавьте к конфигурации HDFS правило `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="f6041-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="f6041-290">**Настройка на контроллере домена**</span><span class="sxs-lookup"><span data-stu-id="f6041-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="f6041-291">Запустите следующие hello **Ksetup** tooadd запись в области команд:</span><span class="sxs-lookup"><span data-stu-id="f6041-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="f6041-292">Установление доверия из домена Windows tooKerberos области.</span><span class="sxs-lookup"><span data-stu-id="f6041-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="f6041-293">[пароль] — пароль hello участника hello  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="f6041-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="f6041-294">Выберите алгоритм шифрования, используемый в Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f6041-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="f6041-295">Go tooServer Manager > Управление групповой политикой > домена > объекты групповой политики > по умолчанию или активная политика домена и редактирования.</span><span class="sxs-lookup"><span data-stu-id="f6041-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="f6041-296">В hello **редактор управления групповыми политиками** всплывающего окна, откройте tooComputer конфигурации > политики > Параметры Windows > Параметры безопасности > Локальные политики > Параметры безопасности и настройте **сети безопасность: Настройка разрешены для протокола Kerberos типов шифрования**.</span><span class="sxs-lookup"><span data-stu-id="f6041-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="f6041-297">Алгоритм шифрования выберите hello требуется toouse при подключении tooKDC.</span><span class="sxs-lookup"><span data-stu-id="f6041-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="f6041-298">Как правило можно выбрать все параметры hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-298">Commonly, you can simply select all hello options.</span></span>

        ![Типы шифрования конфигурации для Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="f6041-300">Используйте **Ksetup** команда toospecify hello шифрования алгоритм toobe на hello СФЕРЫ.</span><span class="sxs-lookup"><span data-stu-id="f6041-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="f6041-301">Создайте участника в порядке toouse участника Kerberos в домене Windows hello сопоставление учетной записи домена hello и Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f6041-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="f6041-302">Запустите средства администрирования hello > **Active Directory — пользователи и компьютеры**.</span><span class="sxs-lookup"><span data-stu-id="f6041-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="f6041-303">Настройте расширенные функции, щелкнув **Просмотр** > **Расширенные функции**.</span><span class="sxs-lookup"><span data-stu-id="f6041-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="f6041-304">Найдите hello toowhich учетной записи необходимые toocreate сопоставления затем щелкните правой кнопкой мыши tooview **сопоставления имен** > щелкните **имена Kerberos** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f6041-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="f6041-305">Добавление участника из сферы hello.</span><span class="sxs-lookup"><span data-stu-id="f6041-305">Add a principal from hello realm.</span></span>

        ![Сопоставление удостоверения безопасности](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="f6041-307">**Настройка на компьютере шлюза**</span><span class="sxs-lookup"><span data-stu-id="f6041-307">**On gateway machine:**</span></span>

* <span data-ttu-id="f6041-308">Запустите следующие hello **Ksetup** tooadd запись в области команд.</span><span class="sxs-lookup"><span data-stu-id="f6041-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="f6041-309">**Настройка фабрики данных Azure**</span><span class="sxs-lookup"><span data-stu-id="f6041-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="f6041-310">Настройка с помощью соединителя hello HDFS **проверки подлинности Windows** вместе с вашей учетной записи домена или источник данных участника Kerberos tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="f6041-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="f6041-311">Проверьте сведения о конфигурации — [свойства связанной службы HDFS](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f6041-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="f6041-312">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f6041-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="f6041-313">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="f6041-313">Performance and Tuning</span></span>
<span data-ttu-id="f6041-314">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="f6041-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
