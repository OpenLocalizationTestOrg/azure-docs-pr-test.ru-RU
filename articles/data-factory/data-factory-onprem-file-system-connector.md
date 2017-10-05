---
title: "Копирование данных из файловой системы и обратно с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как копировать данные в локальную файловую систему и из нее с помощью фабрики данных Azure.Узнайте, как перемещать данные в локальную файловую систему и из нее с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="1882d-103">Копирование данных в локальную файловую систему или из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="1882d-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="1882d-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure копировать данные в локальную файловую систему и обратно.</span><span class="sxs-lookup"><span data-stu-id="1882d-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="1882d-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="1882d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="1882d-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="1882d-106">Supported scenarios</span></span>
<span data-ttu-id="1882d-107">Данные можно скопировать **из локальной файловой системы** в следующие хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="1882d-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="1882d-108">Данные можно скопировать **в локальную файловую систему** из следующих хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="1882d-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="1882d-109">Действие копирования не удаляет исходный файл после его успешного копирования в место назначения.</span><span class="sxs-lookup"><span data-stu-id="1882d-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="1882d-110">Если необходимо удалить исходный файл после успешного копирования, создайте настраиваемое действие для удаления файла и используйте это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="1882d-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="1882d-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="1882d-111">Enabling connectivity</span></span>
<span data-ttu-id="1882d-112">Фабрика данных поддерживает обмен данными с локальной файловой системой через **шлюз управления данными**.</span><span class="sxs-lookup"><span data-stu-id="1882d-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="1882d-113">Необходимо установить шлюз управления данными в локальной среде, чтобы фабрика данных могла подключаться к любому поддерживаемому локальному хранилищу данных, в том числе к файловой системе.</span><span class="sxs-lookup"><span data-stu-id="1882d-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="1882d-114">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="1882d-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="1882d-115">Для обмена данными с файловой системой устанавливать какие-либо двоичные файлы, кроме шлюза управления данными, не требуется.</span><span class="sxs-lookup"><span data-stu-id="1882d-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="1882d-116">Необходимо установить и использовать шлюз управления данными, даже если файловая система находится на виртуальной машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="1882d-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="1882d-117">Дополнительные сведения о шлюзе см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="1882d-118">Чтобы использовать общую папку Linux, установите [Samba](https://www.samba.org/) на сервере Linux, а шлюз управления данными — на сервере Windows.</span><span class="sxs-lookup"><span data-stu-id="1882d-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="1882d-119">Установка шлюза управления данными на сервер Linux не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1882d-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1882d-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="1882d-120">Getting started</span></span>
<span data-ttu-id="1882d-121">Можно создать конвейер с действием копирования, которое перемещает данные из файловой системы и обратно с помощью различных средств и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="1882d-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="1882d-122">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="1882d-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1882d-123">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1882d-124">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1882d-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1882d-125">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="1882d-126">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1882d-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="1882d-127">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="1882d-127">Create a **data factory**.</span></span> <span data-ttu-id="1882d-128">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="1882d-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="1882d-129">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="1882d-130">Например, при копировании данных из хранилища BLOB-объектов Azure в локальную файловую систему создайте две связанные службы, чтобы связать локальную файловую систему и учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="1882d-131">Сведения о свойствах связанной службы, относящихся к локальной файловой системе, см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="1882d-132">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="1882d-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="1882d-133">В примере, упомянутом на последнем этапе, создайте набор данных, чтобы указать контейнер BLOB-объектов и папку, содержащую входные данные.</span><span class="sxs-lookup"><span data-stu-id="1882d-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="1882d-134">Создайте другой набор данных, укажите имя папки и файла (необязательно) в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="1882d-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="1882d-135">Сведения о свойствах набора данных, относящихся к локальной файловой системе, см. в разделе [Свойства набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="1882d-136">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="1882d-137">В примере выше BlobSource используется как источник, а FileSystemSink — как приемник для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="1882d-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="1882d-138">Точно так же при копировании из локальной файловой системы в хранилище BLOB-объектов Azure в действии копирования используются FileSystemSource и BlobSink.</span><span class="sxs-lookup"><span data-stu-id="1882d-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="1882d-139">Сведения о свойствах действия копирования, относящихся к локальной файловой системе, см. в разделе [Свойства действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="1882d-140">Для получения сведений о том, как использовать хранилище данных как источник или приемник, щелкните ссылку в предыдущем разделе об источнике данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="1882d-141">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="1882d-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1882d-142">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="1882d-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1882d-143">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных из файловой системы и обратно, см. в разделе [Примеры JSON для копирования данных в файловую систему и обратно](#json-examples-for-copying-data-to-and-from-file-system) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="1882d-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="1882d-144">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для файловой системы.</span><span class="sxs-lookup"><span data-stu-id="1882d-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1882d-145">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="1882d-145">Linked service properties</span></span>
<span data-ttu-id="1882d-146">Вы можете связать локальную файловую систему с фабрикой данных Azure при помощи связанной службы **локального файлового сервера**.</span><span class="sxs-lookup"><span data-stu-id="1882d-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="1882d-147">В таблице ниже приведены описания элементов JSON, которые относятся к связанной службе локального файлового сервера.</span><span class="sxs-lookup"><span data-stu-id="1882d-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="1882d-148">Свойство</span><span class="sxs-lookup"><span data-stu-id="1882d-148">Property</span></span> | <span data-ttu-id="1882d-149">Описание</span><span class="sxs-lookup"><span data-stu-id="1882d-149">Description</span></span> | <span data-ttu-id="1882d-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1882d-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1882d-151">type</span><span class="sxs-lookup"><span data-stu-id="1882d-151">type</span></span> |<span data-ttu-id="1882d-152">Убедитесь, что свойству type присвоено значение **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="1882d-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="1882d-153">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-153">Yes</span></span> |
| <span data-ttu-id="1882d-154">host</span><span class="sxs-lookup"><span data-stu-id="1882d-154">host</span></span> |<span data-ttu-id="1882d-155">Задает корневой путь к папке, которую необходимо скопировать.</span><span class="sxs-lookup"><span data-stu-id="1882d-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="1882d-156">Чтобы указать специальные знаки в строке, используйте escape-символ "\".</span><span class="sxs-lookup"><span data-stu-id="1882d-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="1882d-157">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="1882d-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="1882d-158">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-158">Yes</span></span> |
| <span data-ttu-id="1882d-159">userid</span><span class="sxs-lookup"><span data-stu-id="1882d-159">userid</span></span> |<span data-ttu-id="1882d-160">Укажите идентификатор пользователя, имеющего доступ к серверу.</span><span class="sxs-lookup"><span data-stu-id="1882d-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="1882d-161">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="1882d-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="1882d-162">пароль</span><span class="sxs-lookup"><span data-stu-id="1882d-162">password</span></span> |<span data-ttu-id="1882d-163">Укажите пароль для пользователя (userid).</span><span class="sxs-lookup"><span data-stu-id="1882d-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="1882d-164">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="1882d-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="1882d-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1882d-165">encryptedCredential</span></span> |<span data-ttu-id="1882d-166">Укажите зашифрованные учетные данные. Чтобы их получить, выполните командлет New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="1882d-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="1882d-167">Нет (если имя пользователя и пароль указываются в виде обычного текста)</span><span class="sxs-lookup"><span data-stu-id="1882d-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="1882d-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1882d-168">gatewayName</span></span> |<span data-ttu-id="1882d-169">Задает имя шлюза, который следует использовать фабрике данных для подключения к локальному файловому серверу.</span><span class="sxs-lookup"><span data-stu-id="1882d-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="1882d-170">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="1882d-171">Примеры определений связанной службы и набора данных</span><span class="sxs-lookup"><span data-stu-id="1882d-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="1882d-172">Сценарий</span><span class="sxs-lookup"><span data-stu-id="1882d-172">Scenario</span></span> | <span data-ttu-id="1882d-173">Размещение в определении связанной службы</span><span class="sxs-lookup"><span data-stu-id="1882d-173">Host in linked service definition</span></span> | <span data-ttu-id="1882d-174">Путь к файлу в определении набора данных</span><span class="sxs-lookup"><span data-stu-id="1882d-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1882d-175">Локальная папка на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="1882d-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="1882d-176">Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*"</span><span class="sxs-lookup"><span data-stu-id="1882d-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="1882d-177">"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="1882d-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="1882d-178">localhost (для версий, предшествующих версии 2.0 шлюза управления данными)</span><span class="sxs-lookup"><span data-stu-id="1882d-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="1882d-179">.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="1882d-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="1882d-180">"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0)</span><span class="sxs-lookup"><span data-stu-id="1882d-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="1882d-181">Удаленная общая папка:</span><span class="sxs-lookup"><span data-stu-id="1882d-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="1882d-182">Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*"</span><span class="sxs-lookup"><span data-stu-id="1882d-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="1882d-183">\\\\\\\\сервер\\\\общая_папка</span><span class="sxs-lookup"><span data-stu-id="1882d-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="1882d-184">.\\\\ или "папка\\\\вложенная_папка"</span><span class="sxs-lookup"><span data-stu-id="1882d-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="1882d-185">Пример указания имени пользователя и пароля в виде обычного текста</span><span class="sxs-lookup"><span data-stu-id="1882d-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="1882d-186">Пример использования encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="1882d-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="1882d-187">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="1882d-187">Dataset properties</span></span>
<span data-ttu-id="1882d-188">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="1882d-189">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="1882d-190">Разделы typeProperties для каждого типа набора данных отличаются.</span><span class="sxs-lookup"><span data-stu-id="1882d-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="1882d-191">В этом разделе указываются такие сведения, как расположение и формат данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="1882d-192">Раздел typeProperties набора данных типа **FileShare** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="1882d-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="1882d-193">Свойство</span><span class="sxs-lookup"><span data-stu-id="1882d-193">Property</span></span> | <span data-ttu-id="1882d-194">Описание</span><span class="sxs-lookup"><span data-stu-id="1882d-194">Description</span></span> | <span data-ttu-id="1882d-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1882d-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1882d-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="1882d-196">folderPath</span></span> |<span data-ttu-id="1882d-197">Указывает вложенный путь к папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="1882d-198">Чтобы указать специальные знаки в строке, используйте escape-символ "\".</span><span class="sxs-lookup"><span data-stu-id="1882d-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="1882d-199">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="1882d-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="1882d-200">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1882d-201">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-201">Yes</span></span> |
| <span data-ttu-id="1882d-202">fileName</span><span class="sxs-lookup"><span data-stu-id="1882d-202">fileName</span></span> |<span data-ttu-id="1882d-203">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="1882d-204">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="1882d-205">Если значение **fileName** не указано для выходного набора данных, а значение **preserveHierarchy** не указано в приемнике действия, имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1882d-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="1882d-206">`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="1882d-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="1882d-207">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-207">No</span></span> |
| <span data-ttu-id="1882d-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="1882d-208">fileFilter</span></span> |<span data-ttu-id="1882d-209">Укажите фильтр для выбора подмножества файлов из folderPath. Фильтр дает возможность выбирать только некоторые файлы, а не все.</span><span class="sxs-lookup"><span data-stu-id="1882d-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="1882d-210">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="1882d-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="1882d-211">Пример 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="1882d-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="1882d-212">Пример 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="1882d-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="1882d-213">Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="1882d-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="1882d-214">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-214">No</span></span> |
| <span data-ttu-id="1882d-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1882d-215">partitionedBy</span></span> |<span data-ttu-id="1882d-216">С помощью свойства partitionedBy можно указать динамические значения folderPath и fileName для данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="1882d-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="1882d-217">Например, можно параметризовать значение folderPath для каждого часа получения данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1882d-218">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-218">No</span></span> |
| <span data-ttu-id="1882d-219">свойства</span><span class="sxs-lookup"><span data-stu-id="1882d-219">format</span></span> | <span data-ttu-id="1882d-220">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1882d-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1882d-221">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="1882d-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="1882d-222">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="1882d-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1882d-223">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1882d-224">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-224">No</span></span> |
| <span data-ttu-id="1882d-225">compression</span><span class="sxs-lookup"><span data-stu-id="1882d-225">compression</span></span> | <span data-ttu-id="1882d-226">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="1882d-227">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1882d-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1882d-228">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="1882d-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1882d-229">См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1882d-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1882d-230">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1882d-231">Свойства filename и fileFilter невозможно использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="1882d-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="1882d-232">Использование свойства partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1882d-232">Using partitionedBy property</span></span>
<span data-ttu-id="1882d-233">Как сказано выше, для данных временных рядов путь к папке (folderPath) и имя файла (fileName) можно указывать динамически. Это делается с помощью свойства **partitionedBy**, [функций фабрики данных и системных переменных](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="1882d-234">Дополнительные сведения о наборах данных временных рядов, планировании и срезах см. в статьях [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md), [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) и [Конвейеры и действия в фабрике данных Azure: создание конвейеров, цепочки действий и расписаний для них](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="1882d-235">Пример 1</span><span class="sxs-lookup"><span data-stu-id="1882d-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="1882d-236">В этом примере {Slice} заменяется значением SliceStart (системная переменная фабрики данных) в формате ГГГГММДДЧЧ.</span><span class="sxs-lookup"><span data-stu-id="1882d-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="1882d-237">SliceStart указывает время начала среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="1882d-238">Значение folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="1882d-239">Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="1882d-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="1882d-240">Пример 2</span><span class="sxs-lookup"><span data-stu-id="1882d-240">Sample 2:</span></span>

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

<span data-ttu-id="1882d-241">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="1882d-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="1882d-242">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="1882d-242">Copy activity properties</span></span>
<span data-ttu-id="1882d-243">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1882d-244">Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="1882d-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="1882d-245">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="1882d-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="1882d-246">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="1882d-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="1882d-247">При перемещении данных из локальной файловой системы в действии копирования задается тип источника **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="1882d-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="1882d-248">Точно так же при перемещении данных из локальной файловой системы в действии копирования задается тип приемника **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="1882d-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="1882d-249">Этот раздел содержит список свойств, поддерживаемых типами FileSystemSource и FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="1882d-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="1882d-250">**FileSystemSource** поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="1882d-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="1882d-251">Свойство</span><span class="sxs-lookup"><span data-stu-id="1882d-251">Property</span></span> | <span data-ttu-id="1882d-252">Описание</span><span class="sxs-lookup"><span data-stu-id="1882d-252">Description</span></span> | <span data-ttu-id="1882d-253">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="1882d-253">Allowed values</span></span> | <span data-ttu-id="1882d-254">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1882d-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1882d-255">recursive</span><span class="sxs-lookup"><span data-stu-id="1882d-255">recursive</span></span> |<span data-ttu-id="1882d-256">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="1882d-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="1882d-257">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="1882d-257">True, False (default)</span></span> |<span data-ttu-id="1882d-258">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-258">No</span></span> |

<span data-ttu-id="1882d-259">**FileSystemSink** поддерживает следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="1882d-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="1882d-260">Свойство</span><span class="sxs-lookup"><span data-stu-id="1882d-260">Property</span></span> | <span data-ttu-id="1882d-261">Описание</span><span class="sxs-lookup"><span data-stu-id="1882d-261">Description</span></span> | <span data-ttu-id="1882d-262">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="1882d-262">Allowed values</span></span> | <span data-ttu-id="1882d-263">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1882d-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1882d-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1882d-264">copyBehavior</span></span> |<span data-ttu-id="1882d-265">Это свойство определяет поведение функции копирования, когда в качестве источника используется BlobSource или FileSystem.</span><span class="sxs-lookup"><span data-stu-id="1882d-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="1882d-266">/ **PreserveHierarchy:** сохраняет иерархию файлов в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="1882d-267">То есть относительный путь исходного файла в исходной папке идентичен относительному пути целевого файла в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="1882d-268">**FlattenHierarchy**: все файлы из исходной папки создаются на первом уровне в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="1882d-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="1882d-269">Целевые файлы создаются с автоматически сформированными именами.</span><span class="sxs-lookup"><span data-stu-id="1882d-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="1882d-270">**MergeFiles**: объединяет все файлы из исходной папки в один файл.</span><span class="sxs-lookup"><span data-stu-id="1882d-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="1882d-271">Если указано имя большого двоичного объекта или имя файла, то оно присваивается объединенному файлу.</span><span class="sxs-lookup"><span data-stu-id="1882d-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="1882d-272">В противном случае присваивается автоматически созданное имя файла.</span><span class="sxs-lookup"><span data-stu-id="1882d-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="1882d-273">Нет</span><span class="sxs-lookup"><span data-stu-id="1882d-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="1882d-274">Примеры recursive и copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1882d-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="1882d-275">В данном разделе описываются результаты выполнения операции копирования при использовании различных сочетаний значений свойств recursive и copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="1882d-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="1882d-276">Значение recursive</span><span class="sxs-lookup"><span data-stu-id="1882d-276">recursive value</span></span> | <span data-ttu-id="1882d-277">Значение copyBehavior</span><span class="sxs-lookup"><span data-stu-id="1882d-277">copyBehavior value</span></span> | <span data-ttu-id="1882d-278">Результаты выполнения операции</span><span class="sxs-lookup"><span data-stu-id="1882d-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1882d-279">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-279">true</span></span> |<span data-ttu-id="1882d-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="1882d-280">preserveHierarchy</span></span> |<span data-ttu-id="1882d-281">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-282">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-282">Folder1</span></span><br/><span data-ttu-id="1882d-283">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-284">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-285">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-289">Целевая папка "Папка1" создается с такой же структурой, как и исходная папка.</span><span class="sxs-lookup"><span data-stu-id="1882d-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="1882d-290">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-290">Folder1</span></span><br/><span data-ttu-id="1882d-291">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-292">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-293">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="1882d-297">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-297">true</span></span> |<span data-ttu-id="1882d-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="1882d-298">flattenHierarchy</span></span> |<span data-ttu-id="1882d-299">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-300">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-300">Folder1</span></span><br/><span data-ttu-id="1882d-301">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-302">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-303">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-307">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1882d-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="1882d-308">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-308">Folder1</span></span><br/><span data-ttu-id="1882d-309">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="1882d-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="1882d-310">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="1882d-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="1882d-311">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"</span><span class="sxs-lookup"><span data-stu-id="1882d-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="1882d-312">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"</span><span class="sxs-lookup"><span data-stu-id="1882d-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="1882d-313">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5"</span><span class="sxs-lookup"><span data-stu-id="1882d-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="1882d-314">Да</span><span class="sxs-lookup"><span data-stu-id="1882d-314">true</span></span> |<span data-ttu-id="1882d-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="1882d-315">mergeFiles</span></span> |<span data-ttu-id="1882d-316">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-317">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-317">Folder1</span></span><br/><span data-ttu-id="1882d-318">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-319">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-320">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-324">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1882d-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="1882d-325">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-325">Folder1</span></span><br/><span data-ttu-id="1882d-326">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="1882d-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="1882d-327">нет</span><span class="sxs-lookup"><span data-stu-id="1882d-327">false</span></span> |<span data-ttu-id="1882d-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="1882d-328">preserveHierarchy</span></span> |<span data-ttu-id="1882d-329">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-330">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-330">Folder1</span></span><br/><span data-ttu-id="1882d-331">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-332">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-333">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-337">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1882d-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="1882d-338">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-338">Folder1</span></span><br/><span data-ttu-id="1882d-339">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-340">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="1882d-341">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="1882d-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="1882d-342">нет</span><span class="sxs-lookup"><span data-stu-id="1882d-342">false</span></span> |<span data-ttu-id="1882d-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="1882d-343">flattenHierarchy</span></span> |<span data-ttu-id="1882d-344">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-345">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-345">Folder1</span></span><br/><span data-ttu-id="1882d-346">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-347">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-348">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-352">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1882d-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="1882d-353">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-353">Folder1</span></span><br/><span data-ttu-id="1882d-354">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="1882d-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="1882d-355">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="1882d-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="1882d-356">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="1882d-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="1882d-357">нет</span><span class="sxs-lookup"><span data-stu-id="1882d-357">false</span></span> |<span data-ttu-id="1882d-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="1882d-358">mergeFiles</span></span> |<span data-ttu-id="1882d-359">Если у исходной папки "Папка1" следующая структура:</span><span class="sxs-lookup"><span data-stu-id="1882d-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="1882d-360">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-360">Folder1</span></span><br/><span data-ttu-id="1882d-361">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="1882d-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="1882d-362">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="1882d-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="1882d-363">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="1882d-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="1882d-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="1882d-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="1882d-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="1882d-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="1882d-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="1882d-367">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1882d-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="1882d-368">Папка1</span><span class="sxs-lookup"><span data-stu-id="1882d-368">Folder1</span></span><br/><span data-ttu-id="1882d-369">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="1882d-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="1882d-370">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="1882d-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="1882d-371">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="1882d-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="1882d-372">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="1882d-372">Supported file and compression formats</span></span>
<span data-ttu-id="1882d-373">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="1882d-374">Примеры JSON для копирования данных в файловую систему и обратно</span><span class="sxs-lookup"><span data-stu-id="1882d-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="1882d-375">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1882d-376">В них показано, как копировать данные в локальную файловую систему и хранилище BLOB-объектов Azure и из них.</span><span class="sxs-lookup"><span data-stu-id="1882d-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="1882d-377">Тем не менее вы можете скопировать данные *непосредственно* из любых источников в любые из приемников, перечисленных в разделе [Поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats), с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1882d-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="1882d-378">Пример. Копирование данных из локальной файловой системы в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1882d-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="1882d-379">В этом примере показано, как скопировать данные из локальной файловой системы в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1882d-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="1882d-380">Пример содержит следующие сущности фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="1882d-381">Связанная служба типа [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="1882d-382">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="1882d-383">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="1882d-384">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="1882d-385">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1882d-386">В следующем примере данные временных рядов каждый час копируются из локальной файловой системы в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1882d-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="1882d-387">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="1882d-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="1882d-388">В первую очередь настройте шлюз управления данными, как указано в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="1882d-389">**Связанная служба локального файлового сервера**</span><span class="sxs-lookup"><span data-stu-id="1882d-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="1882d-390">Мы рекомендуем использовать свойство **encryptedCredential** вместо свойств **userid** и **password**.</span><span class="sxs-lookup"><span data-stu-id="1882d-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="1882d-391">Подробные сведения о связанной службе файлового сервера см. в [соответствующем разделе](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="1882d-392">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="1882d-392">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="1882d-393">**Входной набор данных локальной файловой системы**</span><span class="sxs-lookup"><span data-stu-id="1882d-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="1882d-394">Данные берутся из нового файла каждый час.</span><span class="sxs-lookup"><span data-stu-id="1882d-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="1882d-395">Свойства folderPath и fileName определяются с учетом времени начала среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="1882d-396">Если задано `"external": "true"`, то фабрика данных считает эту таблицу внешней, то есть не созданной в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="1882d-397">**Выходной набор данных хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="1882d-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="1882d-398">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1882d-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1882d-399">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1882d-400">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="1882d-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="1882d-401">**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="1882d-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="1882d-402">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="1882d-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="1882d-403">В определении JSON конвейера для типа **source** установлено значение **FileSystemSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1882d-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="1882d-404">Пример. Копирование данных из базы данных SQL Azure в локальную файловую систему</span><span class="sxs-lookup"><span data-stu-id="1882d-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="1882d-405">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="1882d-405">The following sample shows:</span></span>

* <span data-ttu-id="1882d-406">Связанная служба типа [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="1882d-407">Связанная служба типа [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="1882d-408">Входной набор данных типа [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="1882d-409">Выходной набор данных типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="1882d-410">Конвейер с действием копирования, в котором используются [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) и [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="1882d-411">В этом примере данные временного ряда каждый час копируются из таблицы SQL Azure в локальную файловую систему.</span><span class="sxs-lookup"><span data-stu-id="1882d-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="1882d-412">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="1882d-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="1882d-413">**Связанная служба базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="1882d-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="1882d-414">**Связанная служба локального файлового сервера**</span><span class="sxs-lookup"><span data-stu-id="1882d-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="1882d-415">Мы рекомендуем использовать свойство **encryptedCredentia** вместо свойств **userid** и **password**.</span><span class="sxs-lookup"><span data-stu-id="1882d-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="1882d-416">Подробные сведения о связанной службе файловой системы см. в [соответствующем разделе](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1882d-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="1882d-417">**Входной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="1882d-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="1882d-418">В примере предполагается, что таблица MyTable уже создана в базе данных SQL Azure и содержит столбец timestampcolumn для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="1882d-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="1882d-419">Если задано ``“external”: ”true”``, то фабрика данных считает эту таблицу внешней, то есть не созданной в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="1882d-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="1882d-420">**Выходной набор данных локальной файловой системы**</span><span class="sxs-lookup"><span data-stu-id="1882d-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="1882d-421">Данные копируются в новый файл каждый час.</span><span class="sxs-lookup"><span data-stu-id="1882d-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="1882d-422">Свойства folderPath и fileName для большого двоичного объекта определяются с учетом времени начала среза.</span><span class="sxs-lookup"><span data-stu-id="1882d-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="1882d-423">**Действие копирования в конвейере с базой данных SQL в качестве источника и файловой системой в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="1882d-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="1882d-424">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="1882d-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="1882d-425">В определении JSON конвейера для типа **source** установлено значение **SqlSource**, а для типа **sink** — значение **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="1882d-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="1882d-426">SQL-запрос, указанный для свойства **SqlReaderQuery**, выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="1882d-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="1882d-427">Также можно сопоставить столбцы из набора данных, используемого в качестве источника, со столбцами из приемника в определении действия копирования.</span><span class="sxs-lookup"><span data-stu-id="1882d-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="1882d-428">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1882d-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1882d-429">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="1882d-429">Performance and tuning</span></span>
 <span data-ttu-id="1882d-430">Ознакомьтесь с [руководством по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в котором описываются ключевые факторы, влияющие на производительность перемещения данных (действия копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="1882d-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
