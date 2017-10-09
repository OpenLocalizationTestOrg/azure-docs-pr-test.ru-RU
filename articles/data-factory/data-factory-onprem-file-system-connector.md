---
title: "aaaCopy данных из файловой системы, с помощью фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как toocopy tooand данных из локальной файловой системы с помощью фабрики данных Azure."
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
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="efa11-103">Копирование данных tooand из локальной файловой системы с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="efa11-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="efa11-104">В этой статье объясняется, как toouse hello действие копирования в данных toocopy фабрики данных Azure из локальной файловой системы.</span><span class="sxs-lookup"><span data-stu-id="efa11-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="efa11-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="efa11-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="efa11-106">Supported scenarios</span></span>
<span data-ttu-id="efa11-107">Можно скопировать данные **из локальной файловой системы** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="efa11-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="efa11-108">Можно скопировать данные из hello, следуя хранилищ данных **tooan в локальной файловой системе**:</span><span class="sxs-lookup"><span data-stu-id="efa11-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="efa11-109">Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello.</span><span class="sxs-lookup"><span data-stu-id="efa11-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="efa11-110">Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="efa11-111">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="efa11-111">Enabling connectivity</span></span>
<span data-ttu-id="efa11-112">Фабрика данных поддерживает подключения tooand из локальной файловой системы через **шлюз управления данными**.</span><span class="sxs-lookup"><span data-stu-id="efa11-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="efa11-113">Необходимо установить hello шлюз управления данными в локальной среде hello фабрики данных службы tooconnect tooany поддерживаемые локальные данные хранилища в том числе файловой системы.</span><span class="sxs-lookup"><span data-stu-id="efa11-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="efa11-114">toolearn о шлюз управления данными и получить пошаговые инструкции по настройке шлюза hello. в разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="efa11-115">Помимо шлюз управления данными другие двоичные файлы должны установить toobe toocommunicate tooand из локальной файловой системы.</span><span class="sxs-lookup"><span data-stu-id="efa11-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="efa11-116">Необходимо установить и использовать hello шлюз управления данными, даже когда hello файловой системы на виртуальной Машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="efa11-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="efa11-117">Подробные сведения о шлюзе hello. в разделе [шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="efa11-118">Установка toouse общую папку Linux [Samba](https://www.samba.org/) на сервер Linux и установить шлюз управления данными на сервере Windows.</span><span class="sxs-lookup"><span data-stu-id="efa11-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="efa11-119">Установка шлюза управления данными на сервер Linux не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="efa11-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="efa11-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="efa11-120">Getting started</span></span>
<span data-ttu-id="efa11-121">Можно создать конвейер с действием копирования, которое перемещает данные из файловой системы и обратно с помощью различных средств и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="efa11-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="efa11-122">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="efa11-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="efa11-123">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="efa11-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="efa11-124">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="efa11-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="efa11-125">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="efa11-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="efa11-126">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="efa11-127">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="efa11-127">Create a **data factory**.</span></span> <span data-ttu-id="efa11-128">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="efa11-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="efa11-129">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="efa11-130">Например при копировании данных из больших двоичных объектов Azure хранилища tooan в локальной файловой системы создается две связанные службы toolink в локальной файловой системы и фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="efa11-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="efa11-131">Свойства связанной службы, определенные tooan в локальной файловой системе, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="efa11-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="efa11-132">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="efa11-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="efa11-133">В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="efa11-134">И создать другой набор данных toospecify hello папку и имя файла (необязательно) в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="efa11-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="efa11-135">Свойства набора данных, определенных tooon в локальной файловой системе, см. в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="efa11-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="efa11-136">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="efa11-137">В примере hello приведенные выше используются BlobSource в исходной и FileSystemSink в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="efa11-138">Аналогично при копировании из локального файла системы tooAzure хранилища BLOB-объектов используется FileSystemSource и BlobSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="efa11-139">Свойства действия копирования, определенные tooon в локальной файловой системе, см. в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="efa11-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="efa11-140">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="efa11-141">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="efa11-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="efa11-142">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="efa11-143">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из файловой системы см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-file-system) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="efa11-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="efa11-144">Hello в следующих разделах содержатся сведения о свойствах JSON, которые являются системными toofile определенных сущностей фабрики данных используется toodefine:</span><span class="sxs-lookup"><span data-stu-id="efa11-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="efa11-145">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="efa11-145">Linked service properties</span></span>
<span data-ttu-id="efa11-146">Можно связать локального файла tooan данных Azure заводе hello **файловый сервер в локальной** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="efa11-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="efa11-147">Привет, в следующей таблице приводится описание JSON элементы, которые являются определенной toohello файловый сервер в локальной связанной службы.</span><span class="sxs-lookup"><span data-stu-id="efa11-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="efa11-148">Свойство</span><span class="sxs-lookup"><span data-stu-id="efa11-148">Property</span></span> | <span data-ttu-id="efa11-149">Описание</span><span class="sxs-lookup"><span data-stu-id="efa11-149">Description</span></span> | <span data-ttu-id="efa11-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efa11-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa11-151">type</span><span class="sxs-lookup"><span data-stu-id="efa11-151">type</span></span> |<span data-ttu-id="efa11-152">Убедитесь, что свойство типа hello слишком**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="efa11-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="efa11-153">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-153">Yes</span></span> |
| <span data-ttu-id="efa11-154">host</span><span class="sxs-lookup"><span data-stu-id="efa11-154">host</span></span> |<span data-ttu-id="efa11-155">Указывает путь к корневому каталогу hello hello папке, что toocopy.</span><span class="sxs-lookup"><span data-stu-id="efa11-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="efa11-156">Использовать hello escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="efa11-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="efa11-157">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="efa11-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="efa11-158">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-158">Yes</span></span> |
| <span data-ttu-id="efa11-159">userid</span><span class="sxs-lookup"><span data-stu-id="efa11-159">userid</span></span> |<span data-ttu-id="efa11-160">Укажите идентификатор hello hello пользователя, имеющего доступ toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="efa11-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="efa11-161">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="efa11-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="efa11-162">пароль</span><span class="sxs-lookup"><span data-stu-id="efa11-162">password</span></span> |<span data-ttu-id="efa11-163">Задать пароль hello hello пользователя (userid).</span><span class="sxs-lookup"><span data-stu-id="efa11-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="efa11-164">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="efa11-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="efa11-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="efa11-165">encryptedCredential</span></span> |<span data-ttu-id="efa11-166">Укажите hello зашифрованные учетные данные, которые можно получить, выполнив командлет New-AzureRmDataFactoryEncryptValue hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="efa11-167">Нет (Если вы выберете toospecify идентификатор пользователя и пароль в виде обычного текста)</span><span class="sxs-lookup"><span data-stu-id="efa11-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="efa11-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="efa11-168">gatewayName</span></span> |<span data-ttu-id="efa11-169">Указывает имя фабрики данных для использования локального файла tooconnect toohello сервера шлюза hello hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="efa11-170">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="efa11-171">Примеры определений связанной службы и набора данных</span><span class="sxs-lookup"><span data-stu-id="efa11-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="efa11-172">Сценарий</span><span class="sxs-lookup"><span data-stu-id="efa11-172">Scenario</span></span> | <span data-ttu-id="efa11-173">Размещение в определении связанной службы</span><span class="sxs-lookup"><span data-stu-id="efa11-173">Host in linked service definition</span></span> | <span data-ttu-id="efa11-174">Путь к файлу в определении набора данных</span><span class="sxs-lookup"><span data-stu-id="efa11-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa11-175">Локальная папка на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="efa11-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="efa11-176">Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*"</span><span class="sxs-lookup"><span data-stu-id="efa11-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="efa11-177">"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="efa11-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="efa11-178">localhost (для версий, предшествующих версии 2.0 шлюза управления данными)</span><span class="sxs-lookup"><span data-stu-id="efa11-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="efa11-179">.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="efa11-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="efa11-180">"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0)</span><span class="sxs-lookup"><span data-stu-id="efa11-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="efa11-181">Удаленная общая папка:</span><span class="sxs-lookup"><span data-stu-id="efa11-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="efa11-182">Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*"</span><span class="sxs-lookup"><span data-stu-id="efa11-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="efa11-183">\\\\\\\\сервер\\\\общая_папка</span><span class="sxs-lookup"><span data-stu-id="efa11-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="efa11-184">.\\\\ или "папка\\\\вложенная_папка"</span><span class="sxs-lookup"><span data-stu-id="efa11-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="efa11-185">Пример указания имени пользователя и пароля в виде обычного текста</span><span class="sxs-lookup"><span data-stu-id="efa11-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="efa11-186">Пример использования encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="efa11-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="efa11-187">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="efa11-187">Dataset properties</span></span>
<span data-ttu-id="efa11-188">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="efa11-189">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="efa11-190">раздел typeProperties Hello отличается для каждого типа набора данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="efa11-191">Он предоставляет сведения, такие как расположение hello и формат данных hello в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="efa11-192">Hello typeProperties статьи для набора данных hello типа **FileShare** имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="efa11-193">Свойство</span><span class="sxs-lookup"><span data-stu-id="efa11-193">Property</span></span> | <span data-ttu-id="efa11-194">Описание</span><span class="sxs-lookup"><span data-stu-id="efa11-194">Description</span></span> | <span data-ttu-id="efa11-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efa11-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa11-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="efa11-196">folderPath</span></span> |<span data-ttu-id="efa11-197">Указывает папку toohello вложенным hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="efa11-198">Использовать hello escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="efa11-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="efa11-199">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="efa11-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="efa11-200">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="efa11-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="efa11-201">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-201">Yes</span></span> |
| <span data-ttu-id="efa11-202">fileName</span><span class="sxs-lookup"><span data-stu-id="efa11-202">fileName</span></span> |<span data-ttu-id="efa11-203">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="efa11-204">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="efa11-205">При **fileName** не указано для выходной набор данных и **preserveHierarchy** не указан в приемник действия hello hello созданный файл имеет имя в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="efa11-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="efa11-206">`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="efa11-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="efa11-207">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-207">No</span></span> |
| <span data-ttu-id="efa11-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="efa11-208">fileFilter</span></span> |<span data-ttu-id="efa11-209">Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.</span><span class="sxs-lookup"><span data-stu-id="efa11-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="efa11-210">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="efa11-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="efa11-211">Пример 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="efa11-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="efa11-212">Пример 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="efa11-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="efa11-213">Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="efa11-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="efa11-214">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-214">No</span></span> |
| <span data-ttu-id="efa11-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="efa11-215">partitionedBy</span></span> |<span data-ttu-id="efa11-216">PartitionedBy toospecify динамический folderPath и fileName можно использовать для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="efa11-217">Например, можно параметризовать значение folderPath для каждого часа получения данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="efa11-218">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-218">No</span></span> |
| <span data-ttu-id="efa11-219">свойства</span><span class="sxs-lookup"><span data-stu-id="efa11-219">format</span></span> | <span data-ttu-id="efa11-220">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="efa11-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="efa11-221">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="efa11-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="efa11-222">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="efa11-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="efa11-223">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="efa11-224">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-224">No</span></span> |
| <span data-ttu-id="efa11-225">compression</span><span class="sxs-lookup"><span data-stu-id="efa11-225">compression</span></span> | <span data-ttu-id="efa11-226">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="efa11-227">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="efa11-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="efa11-228">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="efa11-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="efa11-229">См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="efa11-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="efa11-230">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="efa11-231">Свойства filename и fileFilter невозможно использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="efa11-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="efa11-232">Использование свойства partitionedBy</span><span class="sxs-lookup"><span data-stu-id="efa11-232">Using partitionedBy property</span></span>
<span data-ttu-id="efa11-233">Как упоминалось в предыдущем разделе hello, можно указать динамического folderPath и filename для временного ряда данных с hello **partitionedBy** свойства [функции фабрики данных, а системные переменные hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="efa11-234">см. Дополнительные сведения о наборах данных временных рядов, планирования и срезов, toounderstand [Создание наборов данных](data-factory-create-datasets.md), [планирования и выполнения](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="efa11-235">Пример 1</span><span class="sxs-lookup"><span data-stu-id="efa11-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="efa11-236">В этом примере {Slice} заменяется значение hello hello системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ).</span><span class="sxs-lookup"><span data-stu-id="efa11-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="efa11-237">SliceStart ссылается toostart время hello среза.</span><span class="sxs-lookup"><span data-stu-id="efa11-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="efa11-238">Hello folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="efa11-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="efa11-239">Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="efa11-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="efa11-240">Пример 2</span><span class="sxs-lookup"><span data-stu-id="efa11-240">Sample 2:</span></span>

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

<span data-ttu-id="efa11-241">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые свойства hello folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="efa11-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="efa11-242">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="efa11-242">Copy activity properties</span></span>
<span data-ttu-id="efa11-243">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="efa11-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="efa11-244">Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="efa11-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="efa11-245">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="efa11-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="efa11-246">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="efa11-247">При перемещении данных из файловой системы в локальной установке hello исходного типа в действие копирования hello слишком**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="efa11-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="efa11-248">Аналогичным образом, при перемещении данных tooan в локальной файловой системы, установите тип приемника hello в действии копирования hello слишком**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="efa11-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="efa11-249">Этот раздел содержит список свойств, поддерживаемых типами FileSystemSource и FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="efa11-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="efa11-250">**FileSystemSource** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="efa11-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="efa11-251">Свойство</span><span class="sxs-lookup"><span data-stu-id="efa11-251">Property</span></span> | <span data-ttu-id="efa11-252">Описание</span><span class="sxs-lookup"><span data-stu-id="efa11-252">Description</span></span> | <span data-ttu-id="efa11-253">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="efa11-253">Allowed values</span></span> | <span data-ttu-id="efa11-254">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efa11-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="efa11-255">recursive</span><span class="sxs-lookup"><span data-stu-id="efa11-255">recursive</span></span> |<span data-ttu-id="efa11-256">Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="efa11-257">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="efa11-257">True, False (default)</span></span> |<span data-ttu-id="efa11-258">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-258">No</span></span> |

<span data-ttu-id="efa11-259">**FileSystemSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="efa11-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="efa11-260">Свойство</span><span class="sxs-lookup"><span data-stu-id="efa11-260">Property</span></span> | <span data-ttu-id="efa11-261">Описание</span><span class="sxs-lookup"><span data-stu-id="efa11-261">Description</span></span> | <span data-ttu-id="efa11-262">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="efa11-262">Allowed values</span></span> | <span data-ttu-id="efa11-263">Обязательно</span><span class="sxs-lookup"><span data-stu-id="efa11-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="efa11-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="efa11-264">copyBehavior</span></span> |<span data-ttu-id="efa11-265">Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы.</span><span class="sxs-lookup"><span data-stu-id="efa11-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="efa11-266">**PreserveHierarchy:** сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="efa11-267">То есть относительный путь hello hello исходный файл toohello исходную папку hello такой же, как относительный путь hello hello целевой файл toohello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="efa11-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="efa11-268">**FlattenHierarchy:** все файлы из исходной папки hello создаются в первый уровень hello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="efa11-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="efa11-269">Hello целевые файлы создаются с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="efa11-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="efa11-270">**MergeFiles:** объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="efa11-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="efa11-271">Если указано имя BLOB-объекта или имени файла hello hello объединенный файл называется hello указанным именем.</span><span class="sxs-lookup"><span data-stu-id="efa11-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="efa11-272">В противном случае присваивается автоматически созданное имя файла.</span><span class="sxs-lookup"><span data-stu-id="efa11-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="efa11-273">Нет</span><span class="sxs-lookup"><span data-stu-id="efa11-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="efa11-274">Примеры recursive и copyBehavior</span><span class="sxs-lookup"><span data-stu-id="efa11-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="efa11-275">Этот раздел описывает поведение функции hello операции копирования для различных сочетаний значений для свойств рекурсивные и copyBehavior hello hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="efa11-276">Значение recursive</span><span class="sxs-lookup"><span data-stu-id="efa11-276">recursive value</span></span> | <span data-ttu-id="efa11-277">Значение copyBehavior</span><span class="sxs-lookup"><span data-stu-id="efa11-277">copyBehavior value</span></span> | <span data-ttu-id="efa11-278">Результаты выполнения операции</span><span class="sxs-lookup"><span data-stu-id="efa11-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa11-279">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-279">true</span></span> |<span data-ttu-id="efa11-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="efa11-280">preserveHierarchy</span></span> |<span data-ttu-id="efa11-281">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-282">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-282">Folder1</span></span><br/><span data-ttu-id="efa11-283">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-284">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-285">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-289">Hello целевую папку Folder1 создается с таким же структуру как исходной hello hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="efa11-290">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-290">Folder1</span></span><br/><span data-ttu-id="efa11-291">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-292">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-293">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="efa11-297">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-297">true</span></span> |<span data-ttu-id="efa11-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="efa11-298">flattenHierarchy</span></span> |<span data-ttu-id="efa11-299">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-300">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-300">Folder1</span></span><br/><span data-ttu-id="efa11-301">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-302">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-303">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-307">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="efa11-308">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-308">Folder1</span></span><br/><span data-ttu-id="efa11-309">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="efa11-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="efa11-310">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="efa11-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="efa11-311">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"</span><span class="sxs-lookup"><span data-stu-id="efa11-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="efa11-312">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"</span><span class="sxs-lookup"><span data-stu-id="efa11-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="efa11-313">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5"</span><span class="sxs-lookup"><span data-stu-id="efa11-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="efa11-314">Да</span><span class="sxs-lookup"><span data-stu-id="efa11-314">true</span></span> |<span data-ttu-id="efa11-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="efa11-315">mergeFiles</span></span> |<span data-ttu-id="efa11-316">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-317">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-317">Folder1</span></span><br/><span data-ttu-id="efa11-318">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-319">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-320">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-324">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="efa11-325">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-325">Folder1</span></span><br/><span data-ttu-id="efa11-326">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="efa11-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="efa11-327">нет</span><span class="sxs-lookup"><span data-stu-id="efa11-327">false</span></span> |<span data-ttu-id="efa11-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="efa11-328">preserveHierarchy</span></span> |<span data-ttu-id="efa11-329">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-330">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-330">Folder1</span></span><br/><span data-ttu-id="efa11-331">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-332">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-333">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-337">Hello целевую папку Folder1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="efa11-338">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-338">Folder1</span></span><br/><span data-ttu-id="efa11-339">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-340">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="efa11-341">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="efa11-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="efa11-342">нет</span><span class="sxs-lookup"><span data-stu-id="efa11-342">false</span></span> |<span data-ttu-id="efa11-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="efa11-343">flattenHierarchy</span></span> |<span data-ttu-id="efa11-344">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-345">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-345">Folder1</span></span><br/><span data-ttu-id="efa11-346">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-347">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-348">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-352">Hello целевую папку Folder1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="efa11-353">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-353">Folder1</span></span><br/><span data-ttu-id="efa11-354">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="efa11-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="efa11-355">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="efa11-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="efa11-356">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="efa11-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="efa11-357">нет</span><span class="sxs-lookup"><span data-stu-id="efa11-357">false</span></span> |<span data-ttu-id="efa11-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="efa11-358">mergeFiles</span></span> |<span data-ttu-id="efa11-359">Источник папку Folder1 hello следующая структура,</span><span class="sxs-lookup"><span data-stu-id="efa11-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="efa11-360">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-360">Folder1</span></span><br/><span data-ttu-id="efa11-361">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="efa11-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="efa11-362">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="efa11-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="efa11-363">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="efa11-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="efa11-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="efa11-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="efa11-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="efa11-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="efa11-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="efa11-367">Hello целевую папку Folder1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="efa11-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="efa11-368">Папка1</span><span class="sxs-lookup"><span data-stu-id="efa11-368">Folder1</span></span><br/><span data-ttu-id="efa11-369">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="efa11-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="efa11-370">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="efa11-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="efa11-371">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="efa11-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="efa11-372">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="efa11-372">Supported file and compression formats</span></span>
<span data-ttu-id="efa11-373">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="efa11-374">Примеры JSON для копирования данных tooand из файловой системы</span><span class="sxs-lookup"><span data-stu-id="efa11-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="efa11-375">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="efa11-376">Они показывают как toocopy tooand данных из хранилища больших двоичных объектов Azure и локальной файловой системе.</span><span class="sxs-lookup"><span data-stu-id="efa11-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="efa11-377">Тем не менее, можно скопировать данные *непосредственно* из любого tooany источников hello hello приемников, перечисленных в [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью копирования действия в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="efa11-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="efa11-378">Пример: Копирование данных из tooAzure системы файл локального хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="efa11-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="efa11-379">В этом примере показано, как данные toocopy из tooAzure системы файл локального хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="efa11-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="efa11-380">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="efa11-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="efa11-381">Связанная служба типа [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="efa11-382">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="efa11-383">Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="efa11-384">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="efa11-385">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="efa11-386">Следующий образец Hello копирует данные временных рядов с tooAzure системы файл локального хранилища больших двоичных объектов каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="efa11-387">свойства Hello JSON, используемые в этих примерах описаны в разделах hello после образцы hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="efa11-388">В качестве первого шага, настроить шлюз управления данными согласно инструкциям hello [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="efa11-389">**Связанная служба локального файлового сервера**</span><span class="sxs-lookup"><span data-stu-id="efa11-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="efa11-390">Мы рекомендуем использовать hello **encryptedCredential** свойство вместо hello **userid** и **пароль** свойства.</span><span class="sxs-lookup"><span data-stu-id="efa11-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="efa11-391">Подробные сведения о связанной службе файлового сервера см. в [соответствующем разделе](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="efa11-392">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="efa11-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="efa11-393">**Входной набор данных локальной файловой системы**</span><span class="sxs-lookup"><span data-stu-id="efa11-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="efa11-394">Данные берутся из нового файла каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="efa11-395">Здравствуйте, folderPath и fileName свойства определяются на основе времени начала hello hello среза.</span><span class="sxs-lookup"><span data-stu-id="efa11-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="efa11-396">Параметр `"external": "true"` информирует фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="efa11-397">**Выходной набор данных хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="efa11-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="efa11-398">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="efa11-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="efa11-399">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="efa11-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="efa11-400">путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="efa11-401">**Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="efa11-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="efa11-402">Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="efa11-403">В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**, и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="efa11-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="efa11-404">Пример: Копирование данных из базы данных SQL Azure tooan в локальной файловой системы</span><span class="sxs-lookup"><span data-stu-id="efa11-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="efa11-405">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="efa11-405">hello following sample shows:</span></span>

* <span data-ttu-id="efa11-406">Связанная служба типа [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="efa11-407">Связанная служба типа [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="efa11-408">Входной набор данных типа [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="efa11-409">Выходной набор данных типа [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="efa11-410">Конвейер с действием копирования, в котором используются [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) и [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="efa11-411">Образец Hello копирует данные временных рядов с Azure SQL таблицы tooan в локальной файловой системе каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="efa11-412">После образцы hello Hello JSON свойства, которые используются в образцах описаны в разделах.</span><span class="sxs-lookup"><span data-stu-id="efa11-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="efa11-413">**Связанная служба базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="efa11-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="efa11-414">**Связанная служба локального файлового сервера**</span><span class="sxs-lookup"><span data-stu-id="efa11-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="efa11-415">Мы рекомендуем использовать hello **encryptedCredential** свойство вместо использования hello **userid** и **пароль** свойства.</span><span class="sxs-lookup"><span data-stu-id="efa11-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="efa11-416">Подробные сведения о связанной службе файловой системы см. в [соответствующем разделе](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="efa11-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="efa11-417">**Входной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="efa11-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="efa11-418">Образец Hello предполагается, что вы создали таблицу «MyTable» в Azure SQL и она содержит столбец с именем «timestampcolumn» для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="efa11-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="efa11-419">Параметр ``“external”: ”true”`` информирует фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="efa11-420">**Выходной набор данных локальной файловой системы**</span><span class="sxs-lookup"><span data-stu-id="efa11-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="efa11-421">Данные — новый файл скопированный tooa каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="efa11-422">Hello folderPath и fileName для большого двоичного объекта hello определяются на основе времени начала hello hello среза.</span><span class="sxs-lookup"><span data-stu-id="efa11-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

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

<span data-ttu-id="efa11-423">**Действие копирования в конвейере с базой данных SQL в качестве источника и файловой системой в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="efa11-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="efa11-424">Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="efa11-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="efa11-425">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource**и hello **приемник** тип установлен слишком**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="efa11-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="efa11-426">Hello SQL-запрос, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="efa11-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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


<span data-ttu-id="efa11-427">Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="efa11-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="efa11-428">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="efa11-429">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="efa11-429">Performance and tuning</span></span>
 <span data-ttu-id="efa11-430">toolearn о ключе факторы, производительность hello влияние перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize, разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="efa11-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
