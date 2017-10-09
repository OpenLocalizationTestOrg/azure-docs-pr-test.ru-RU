---
title: "aaaCopy tooand данных из хранилища Озера данных Azure | Документы Microsoft"
description: "Узнайте, как toocopy tooand данных из хранилища Озера данных с помощью фабрики данных Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="47b96-103">Tooand копирования данных из хранилища Озера данных с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="47b96-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="47b96-104">В этой статье объясняется, как toouse действие копирования в tooand данных toomove фабрики данных Azure из хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="47b96-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статью Обзор перемещение данных в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="47b96-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="47b96-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="47b96-106">Supported scenarios</span></span>
<span data-ttu-id="47b96-107">Можно скопировать данные **из хранилища Озера данных Azure** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="47b96-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="47b96-108">Можно скопировать данные из hello, следуя хранилищ данных **tooAzure хранилища Озера данных**:</span><span class="sxs-lookup"><span data-stu-id="47b96-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="47b96-109">Прежде чем создавать конвейер с действием копирования, создайте учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47b96-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="47b96-110">Дополнительные сведения см. в статье [Начало работы с хранилищем озера данных Azure с помощью портала Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47b96-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="47b96-111">Поддерживаемые типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="47b96-111">Supported authentication types</span></span>
<span data-ttu-id="47b96-112">Соединитель Hello хранилища Озера данных поддерживает следующие типы проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="47b96-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="47b96-113">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="47b96-113">Service principal authentication</span></span>
* <span data-ttu-id="47b96-114">Проверка подлинности учетных данных пользователя (OAuth)</span><span class="sxs-lookup"><span data-stu-id="47b96-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="47b96-115">Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для копирования данных по расписанию.</span><span class="sxs-lookup"><span data-stu-id="47b96-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="47b96-116">При проверке подлинности учетных данных пользователя может истечь срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="47b96-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="47b96-117">Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="47b96-118">Начало работы</span><span class="sxs-lookup"><span data-stu-id="47b96-118">Get started</span></span>
<span data-ttu-id="47b96-119">Можно создать конвейер с действием копирования, которое перемещает данные из Azure Data Lake Store или обратно с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="47b96-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="47b96-120">Hello простым способом toocreate toocopy данных конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="47b96-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="47b96-121">Учебник по созданию конвейера с помощью мастера копирования hello см. в разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="47b96-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="47b96-122">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="47b96-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="47b96-123">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="47b96-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="47b96-124">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="47b96-125">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="47b96-125">Create a **data factory**.</span></span> <span data-ttu-id="47b96-126">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="47b96-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="47b96-127">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="47b96-128">Например при копировании данных из tooan хранилища BLOB-объектов Azure хранилища Озера данных Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="47b96-129">Свойства связанной службы, определенные tooAzure хранилища Озера данных, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="47b96-130">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="47b96-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="47b96-131">В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="47b96-132">И создать другой набор данных toospecify hello папки и путь к файлу в хранилище Озера данных hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="47b96-133">Свойства набора данных, определенных tooAzure хранилища Озера данных, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="47b96-134">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="47b96-135">В примере hello приведенные выше используются BlobSource в исходной и AzureDataLakeStoreSink в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="47b96-136">Аналогично при копировании из хранилища Озера данных Azure tooAzure хранилища BLOB-объектов используется AzureDataLakeStoreSource и BlobSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="47b96-137">Свойства действия копирования, определенные tooAzure хранилища Озера данных, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="47b96-138">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="47b96-139">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="47b96-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="47b96-140">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="47b96-141">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища Озера данных Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-data-lake-store) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="47b96-142">Hello в следующих разделах приведены сведения о JSON свойства, используемые toodefine хранилища Озера конкретных tooData сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="47b96-143">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="47b96-143">Linked service properties</span></span>
<span data-ttu-id="47b96-144">Связанная служба связывает фабрику данных tooa хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="47b96-145">Создание связанной службы типа **AzureDataLakeStore** toolink фабрики данных tooyour данные хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="47b96-146">Hello в следующей таблице описываются JSON элементы конкретного хранилища Озера tooData связанные службы.</span><span class="sxs-lookup"><span data-stu-id="47b96-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="47b96-147">Вы можете выбирать между проверкой подлинности субъекта-службы и учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="47b96-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="47b96-148">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-148">Property</span></span> | <span data-ttu-id="47b96-149">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-149">Description</span></span> | <span data-ttu-id="47b96-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="47b96-151">**type**</span><span class="sxs-lookup"><span data-stu-id="47b96-151">**type**</span></span> | <span data-ttu-id="47b96-152">свойство типа Hello должно быть задано слишком**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="47b96-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="47b96-153">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-153">Yes</span></span> |
| <span data-ttu-id="47b96-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="47b96-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="47b96-155">Сведения о hello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="47b96-156">Эти сведения принимает одно из следующих форматов hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="47b96-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="47b96-157">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-157">Yes</span></span> |
| <span data-ttu-id="47b96-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="47b96-158">**subscriptionId**</span></span> | <span data-ttu-id="47b96-159">Принадлежит hello toowhich идентификатор подписки Azure хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="47b96-160">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="47b96-160">Required for sink</span></span> |
| <span data-ttu-id="47b96-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="47b96-161">**resourceGroupName**</span></span> | <span data-ttu-id="47b96-162">Принадлежит ресурс Azure группы имя toowhich hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="47b96-163">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="47b96-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="47b96-164">Проверка подлинности на основе субъекта-службы (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="47b96-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="47b96-165">toouse основной проверки подлинности службы, регистрация сущности приложения в Azure Active Directory (Azure AD) и предоставьте его hello доступа к хранилищу Озера tooData.</span><span class="sxs-lookup"><span data-stu-id="47b96-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="47b96-166">Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="47b96-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="47b96-167">Запишите следующие значения, которые вы используете hello toodefine hello связанной службы:</span><span class="sxs-lookup"><span data-stu-id="47b96-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="47b96-168">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="47b96-168">Application ID</span></span>
* <span data-ttu-id="47b96-169">Ключ приложения</span><span class="sxs-lookup"><span data-stu-id="47b96-169">Application key</span></span> 
* <span data-ttu-id="47b96-170">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="47b96-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47b96-171">При использовании конвейеры данных tooauthor приветствия мастера копирования убедитесь, что предоставляются hello участника-службы по крайней мере **чтения** роль в системе контроля доступа (Управление удостоверениями и доступом) для учетной записи хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="47b96-172">Кроме того, по крайней мере предоставить субъекту-службе hello **чтения + Execute** разрешение корневого хранилища Озера данных tooyour («/») и его дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="47b96-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="47b96-173">В противном случае может появиться сообщение hello «hello, предоставленные учетные данные являются недопустимыми».</span><span class="sxs-lookup"><span data-stu-id="47b96-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="47b96-174">После создания или обновления участника службы в Azure AD, занимает несколько минут для эффекта tootake изменения hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="47b96-175">Проверьте hello субъекта-службы и конфигурации списка управления Доступом управления доступа хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="47b96-176">Если по-прежнему отображается приветственное сообщение «hello, предоставленные учетные данные являются недопустимыми», подождите и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="47b96-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="47b96-177">Используйте основной проверки подлинности службы, указав hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="47b96-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="47b96-178">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-178">Property</span></span> | <span data-ttu-id="47b96-179">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-179">Description</span></span> | <span data-ttu-id="47b96-180">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="47b96-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="47b96-181">**servicePrincipalId**</span></span> | <span data-ttu-id="47b96-182">Укажите идентификатор клиента приложения hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="47b96-183">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-183">Yes</span></span> |
| <span data-ttu-id="47b96-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="47b96-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="47b96-185">Укажите ключ приложения hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-185">Specify hello application's key.</span></span> | <span data-ttu-id="47b96-186">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-186">Yes</span></span> |
| <span data-ttu-id="47b96-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="47b96-187">**tenant**</span></span> | <span data-ttu-id="47b96-188">Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение.</span><span class="sxs-lookup"><span data-stu-id="47b96-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="47b96-189">Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="47b96-190">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-190">Yes</span></span> |

<span data-ttu-id="47b96-191">**Пример. Проверка подлинности на основе субъекта-службы**</span><span class="sxs-lookup"><span data-stu-id="47b96-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="47b96-192">Использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="47b96-192">User credential authentication</span></span>
<span data-ttu-id="47b96-193">Кроме того можно использовать toocopy проверки подлинности учетных данных пользователя из или хранилища Озера tooData, указав hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="47b96-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="47b96-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-194">Property</span></span> | <span data-ttu-id="47b96-195">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-195">Description</span></span> | <span data-ttu-id="47b96-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="47b96-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="47b96-197">**authorization**</span></span> | <span data-ttu-id="47b96-198">Нажмите кнопку hello **авторизовать** в hello редактор фабрики данных и ввести учетные данные, назначает hello автоматически авторизации URL-адрес toothis свойство.</span><span class="sxs-lookup"><span data-stu-id="47b96-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="47b96-199">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-199">Yes</span></span> |
| <span data-ttu-id="47b96-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="47b96-200">**sessionId**</span></span> | <span data-ttu-id="47b96-201">Идентификатор сеанса OAuth из сеанса авторизации OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="47b96-202">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="47b96-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="47b96-203">Этот параметр автоматически создается при использовании hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="47b96-204">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-204">Yes</span></span> |

<span data-ttu-id="47b96-205">**Пример. Использование проверки подлинности на основе учетных данных пользователя**</span><span class="sxs-lookup"><span data-stu-id="47b96-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="47b96-206">Срок действия маркера</span><span class="sxs-lookup"><span data-stu-id="47b96-206">Token expiration</span></span>
<span data-ttu-id="47b96-207">Здравствуйте, код авторизации, создать с помощью hello **авторизовать** кнопку срок действия истекает через некоторое время.</span><span class="sxs-lookup"><span data-stu-id="47b96-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="47b96-208">следующие сообщения Hello означает, что истек срок действия токена проверки подлинности, hello:</span><span class="sxs-lookup"><span data-stu-id="47b96-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="47b96-209">"Произошла ошибка при операции с учетными данными: invalid_grant — AADSTS70002. Ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="47b96-210">AADSTS70008: hello предоставляется право доступа просрочен или отозван.</span><span class="sxs-lookup"><span data-stu-id="47b96-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="47b96-211">Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Метка времени: 2015-12-15 21-09-31Z".</span><span class="sxs-lookup"><span data-stu-id="47b96-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="47b96-212">Hello следующей таблице показаны hello сроков различных типов учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="47b96-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="47b96-213">Тип пользователя</span><span class="sxs-lookup"><span data-stu-id="47b96-213">User type</span></span> | <span data-ttu-id="47b96-214">Срок действия</span><span class="sxs-lookup"><span data-stu-id="47b96-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="47b96-215">Учетные записи пользователей, которые *не* управляются с помощью Azure Active Directory (например, @hotmail.com или @live.com).</span><span class="sxs-lookup"><span data-stu-id="47b96-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="47b96-216">12 часов</span><span class="sxs-lookup"><span data-stu-id="47b96-216">12 hours</span></span> |
| <span data-ttu-id="47b96-217">Учетные записи пользователей, которые управляются с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47b96-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="47b96-218">запустить через 14 дней после последнего фрагмента hello</span><span class="sxs-lookup"><span data-stu-id="47b96-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="47b96-219">90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней.</span><span class="sxs-lookup"><span data-stu-id="47b96-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="47b96-220">Если изменить пароль, прежде чем срок действия токена hello, hello срок действия токена истекает немедленно.</span><span class="sxs-lookup"><span data-stu-id="47b96-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="47b96-221">Вы увидите сообщение hello, приведенные выше в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="47b96-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="47b96-222">Повторно авторизовать hello учетной записи с помощью hello **авторизовать** кнопки, когда tooredeploy hello истечения срока действия маркера hello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="47b96-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="47b96-223">Также можно создать значения для hello **sessionId** и **авторизации** свойств программным путем с помощью hello следующий код:</span><span class="sxs-lookup"><span data-stu-id="47b96-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="47b96-224">Дополнительные сведения о классах hello фабрики данных, используемые в коде hello см hello [класса AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [класса AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), и [ Класс AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) разделы.</span><span class="sxs-lookup"><span data-stu-id="47b96-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="47b96-225">Добавить tooversion ссылки `2.9.10826.1824` из `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` для hello `WindowsFormsWebAuthenticationDialog` класс, используемый в коде hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="47b96-226">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="47b96-226">Dataset properties</span></span>
<span data-ttu-id="47b96-227">toospecify toorepresent набора данных, входные данные в хранилище Озера данных, задайте hello **тип** свойства набора данных hello слишком**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="47b96-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="47b96-228">Набор hello **linkedServiceName** свойство toohello имя набора данных hello hello хранилища Озера данных связанной службы.</span><span class="sxs-lookup"><span data-stu-id="47b96-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="47b96-229">Полный список разделов JSON и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="47b96-230">Разделы набора данных в JSON, такие как **structure**, **availability** и **policy**, одинаковы для всех типов наборов данных (таких как базы данных SQL, Blob-объекты Azure и таблицы Azure).</span><span class="sxs-lookup"><span data-stu-id="47b96-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="47b96-231">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет сведения, такие как расположение и формат данных hello в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="47b96-232">Hello **typeProperties** раздел для набора данных типа **AzureDataLakeStore** содержит hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="47b96-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="47b96-233">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-233">Property</span></span> | <span data-ttu-id="47b96-234">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-234">Description</span></span> | <span data-ttu-id="47b96-235">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="47b96-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="47b96-236">**folderPath**</span></span> |<span data-ttu-id="47b96-237">Контейнер toohello путь к папке, в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="47b96-238">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-238">Yes</span></span> |
| <span data-ttu-id="47b96-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="47b96-239">**fileName**</span></span> |<span data-ttu-id="47b96-240">Имя файла hello в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="47b96-241">Hello **fileName** свойство является необязательным, без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="47b96-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="47b96-242">При указании **fileName**, действие hello (включая копирования) работает на конкретный файл hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="47b96-243">Когда **fileName** не указан, копия включает все файлы в **folderPath** во входном наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="47b96-244">Когда **fileName** не указано для выходной набор данных и **preserveHierarchy** не указан в приемник действие hello hello созданный файл имеет имя в формате hello данных. _Идентификатор GUID_.txt ".</span><span class="sxs-lookup"><span data-stu-id="47b96-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="47b96-245">Например: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="47b96-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="47b96-246">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-246">No</span></span> |
| <span data-ttu-id="47b96-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="47b96-247">**partitionedBy**</span></span> |<span data-ttu-id="47b96-248">Hello **partitionedBy** свойство является необязательным.</span><span class="sxs-lookup"><span data-stu-id="47b96-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="47b96-249">Можно использовать toospecify динамического путь и имя файла для временных рядов данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="47b96-250">Например, путь к папке (**folderPath**) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="47b96-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="47b96-251">Дополнительные сведения и примеры см. в разделе [hello свойство partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="47b96-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="47b96-252">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-252">No</span></span> |
| <span data-ttu-id="47b96-253">**format**</span><span class="sxs-lookup"><span data-stu-id="47b96-253">**format**</span></span> | <span data-ttu-id="47b96-254">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, и  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="47b96-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="47b96-255">Набор hello **тип** свойства в разделе **формат** tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="47b96-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="47b96-256">Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат ORC](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) подразделы hello [сжатие файлов и форматы, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="47b96-257">Файлы toocopy» как-является» между файловых хранилищ (двоичный копия), пропустите hello `format` раздела оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="47b96-258">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-258">No</span></span> |
| <span data-ttu-id="47b96-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="47b96-259">**compression**</span></span> | <span data-ttu-id="47b96-260">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="47b96-261">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="47b96-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="47b96-262">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="47b96-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="47b96-263">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="47b96-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="47b96-264">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="47b96-265">Свойство partitionedBy Hello</span><span class="sxs-lookup"><span data-stu-id="47b96-265">hello partitionedBy property</span></span>
<span data-ttu-id="47b96-266">Можно указать динамический **folderPath** и **fileName** свойства для данных временных рядов с hello **partitionedBy** свойств функции фабрики данных и система переменные.</span><span class="sxs-lookup"><span data-stu-id="47b96-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="47b96-267">Дополнительные сведения см. в разделе hello [фабрики данных Azure - функции и системные переменные](data-factory-functions-variables.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="47b96-268">В следующий пример, hello `{Slice}` заменяется hello значение системной переменной фабрики данных hello `SliceStart` в указанный формат hello (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="47b96-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="47b96-269">Имя Hello `SliceStart` ссылается toohello время начала среза hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="47b96-270">Hello `folderPath` свойство отличается для каждого среза, как `wikidatagateway/wikisampledataout/2014100103` или `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="47b96-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="47b96-271">В следующий пример, hello год, месяц, день и время hello `SliceStart` извлекаются в отдельные переменные, используемые hello `folderPath` и `fileName` свойства:</span><span class="sxs-lookup"><span data-stu-id="47b96-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="47b96-272">Дополнительные сведения о наборах данных временных рядов, планирования и срезов, в разделе hello [наборов данных в фабрике данных Azure](data-factory-create-datasets.md) и [фабрики данных планированием и выполнением](data-factory-scheduling-and-execution.md) статей.</span><span class="sxs-lookup"><span data-stu-id="47b96-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="47b96-273">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="47b96-273">Copy activity properties</span></span>
<span data-ttu-id="47b96-274">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="47b96-275">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="47b96-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="47b96-276">Здравствуйте, свойств, доступных в hello **typeProperties** раздел действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="47b96-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="47b96-277">Для операции копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="47b96-278">**AzureDataLakeStoreSource** поддерживает следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="47b96-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="47b96-279">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-279">Property</span></span> | <span data-ttu-id="47b96-280">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-280">Description</span></span> | <span data-ttu-id="47b96-281">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="47b96-281">Allowed values</span></span> | <span data-ttu-id="47b96-282">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47b96-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="47b96-283">**recursive**</span></span> |<span data-ttu-id="47b96-284">Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="47b96-285">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="47b96-285">True (default value), False</span></span> |<span data-ttu-id="47b96-286">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-286">No</span></span> |


<span data-ttu-id="47b96-287">**AzureDataLakeStoreSink** поддерживает следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="47b96-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="47b96-288">Свойство</span><span class="sxs-lookup"><span data-stu-id="47b96-288">Property</span></span> | <span data-ttu-id="47b96-289">Описание</span><span class="sxs-lookup"><span data-stu-id="47b96-289">Description</span></span> | <span data-ttu-id="47b96-290">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="47b96-290">Allowed values</span></span> | <span data-ttu-id="47b96-291">Обязательно</span><span class="sxs-lookup"><span data-stu-id="47b96-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47b96-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="47b96-292">**copyBehavior**</span></span> |<span data-ttu-id="47b96-293">Задает способ копирования hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="47b96-294"><b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="47b96-295">Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.</span><span class="sxs-lookup"><span data-stu-id="47b96-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="47b96-296"><b>FlattenHierarchy</b>: все файлы из исходной папки hello создаются в первый уровень hello hello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="47b96-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="47b96-297">автоматически созданные имена создаваемых файлов целевой Hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="47b96-298"><b>MergeFiles</b>: объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="47b96-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="47b96-299">Если hello имя файла или большого двоичного объекта указан, hello объединенный файл называется hello указанное имя.</span><span class="sxs-lookup"><span data-stu-id="47b96-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="47b96-300">В противном случае имя файла hello создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="47b96-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="47b96-301">Нет</span><span class="sxs-lookup"><span data-stu-id="47b96-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="47b96-302">Примеры recursive и copyBehavior</span><span class="sxs-lookup"><span data-stu-id="47b96-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="47b96-303">Этот раздел описывает поведение функции hello операции копирования для различных сочетаний значений рекурсивные и copyBehavior hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="47b96-304">recursive</span><span class="sxs-lookup"><span data-stu-id="47b96-304">recursive</span></span> | <span data-ttu-id="47b96-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="47b96-305">copyBehavior</span></span> | <span data-ttu-id="47b96-306">Результаты выполнения операции</span><span class="sxs-lookup"><span data-stu-id="47b96-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47b96-307">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-307">true</span></span> |<span data-ttu-id="47b96-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="47b96-308">preserveHierarchy</span></span> |<span data-ttu-id="47b96-309">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-310">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-310">Folder1</span></span><br/><span data-ttu-id="47b96-311">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-312">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-313">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-317">Hello целевую папку Folder1 создается с таким же структуру как исходной hello hello</span><span class="sxs-lookup"><span data-stu-id="47b96-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="47b96-318">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-318">Folder1</span></span><br/><span data-ttu-id="47b96-319">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-320">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-321">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="47b96-325">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-325">true</span></span> |<span data-ttu-id="47b96-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="47b96-326">flattenHierarchy</span></span> |<span data-ttu-id="47b96-327">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-328">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-328">Folder1</span></span><br/><span data-ttu-id="47b96-329">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-330">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-331">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-335">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="47b96-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-336">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-336">Folder1</span></span><br/><span data-ttu-id="47b96-337">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="47b96-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="47b96-338">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="47b96-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="47b96-339">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"</span><span class="sxs-lookup"><span data-stu-id="47b96-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="47b96-340">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"</span><span class="sxs-lookup"><span data-stu-id="47b96-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="47b96-341">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5"</span><span class="sxs-lookup"><span data-stu-id="47b96-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="47b96-342">Да</span><span class="sxs-lookup"><span data-stu-id="47b96-342">true</span></span> |<span data-ttu-id="47b96-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="47b96-343">mergeFiles</span></span> |<span data-ttu-id="47b96-344">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-345">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-345">Folder1</span></span><br/><span data-ttu-id="47b96-346">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-347">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-348">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-352">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="47b96-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-353">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-353">Folder1</span></span><br/><span data-ttu-id="47b96-354">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="47b96-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="47b96-355">нет</span><span class="sxs-lookup"><span data-stu-id="47b96-355">false</span></span> |<span data-ttu-id="47b96-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="47b96-356">preserveHierarchy</span></span> |<span data-ttu-id="47b96-357">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="47b96-358">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-358">Folder1</span></span><br/><span data-ttu-id="47b96-359">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-360">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-361">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-365">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="47b96-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="47b96-366">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-366">Folder1</span></span><br/><span data-ttu-id="47b96-367">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-368">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="47b96-369">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="47b96-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="47b96-370">нет</span><span class="sxs-lookup"><span data-stu-id="47b96-370">false</span></span> |<span data-ttu-id="47b96-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="47b96-371">flattenHierarchy</span></span> |<span data-ttu-id="47b96-372">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="47b96-373">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-373">Folder1</span></span><br/><span data-ttu-id="47b96-374">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-375">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-376">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-380">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="47b96-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="47b96-381">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-381">Folder1</span></span><br/><span data-ttu-id="47b96-382">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="47b96-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="47b96-383">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="47b96-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="47b96-384">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="47b96-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="47b96-385">нет</span><span class="sxs-lookup"><span data-stu-id="47b96-385">false</span></span> |<span data-ttu-id="47b96-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="47b96-386">mergeFiles</span></span> |<span data-ttu-id="47b96-387">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="47b96-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="47b96-388">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-388">Folder1</span></span><br/><span data-ttu-id="47b96-389">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="47b96-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="47b96-390">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="47b96-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="47b96-391">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="47b96-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="47b96-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="47b96-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="47b96-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="47b96-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="47b96-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="47b96-395">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="47b96-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="47b96-396">Папка1</span><span class="sxs-lookup"><span data-stu-id="47b96-396">Folder1</span></span><br/><span data-ttu-id="47b96-397">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="47b96-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="47b96-398">Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="47b96-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="47b96-399">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="47b96-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="47b96-400">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="47b96-400">Supported file and compression formats</span></span>
<span data-ttu-id="47b96-401">Дополнительные сведения см. в разделе hello [сжатие файлов и форматы в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="47b96-402">Примеры JSON для копирования данных tooand из хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="47b96-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="47b96-403">Следующие примеры Hello предоставьте пример JSON определения.</span><span class="sxs-lookup"><span data-stu-id="47b96-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="47b96-404">Можно использовать эти образец определения toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47b96-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="47b96-405">Здравствуйте примерах показано, как toocopy tooand данных из хранилища хранилища Озера данных и больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="47b96-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="47b96-406">Тем не менее, данные можно скопировать _непосредственно_ из любого tooany источников hello приемников hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="47b96-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="47b96-407">Дополнительные сведения см. в разделе hello раздел «поддерживаемые хранилищ данных и форматы» в hello [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="47b96-408">Пример: Копирование данных из хранилища больших двоичных объектов tooAzure хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="47b96-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="47b96-409">пример кода Hello в этом разделе показано:</span><span class="sxs-lookup"><span data-stu-id="47b96-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="47b96-410">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="47b96-411">Связанная служба типа [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="47b96-412">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="47b96-413">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="47b96-414">[Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="47b96-415">Hello примерах показано, как временных рядов данных из хранилища больших двоичных объектов будет скопирован хранилища Озера tooData каждый час.</span><span class="sxs-lookup"><span data-stu-id="47b96-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="47b96-416">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="47b96-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="47b96-417">**Связанная служба Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="47b96-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="47b96-418">Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="47b96-419">**Входной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="47b96-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="47b96-420">В следующем примере hello, данных берется из нового большого двоичного объекта каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="47b96-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="47b96-421">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="47b96-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="47b96-422">путь к папке Hello использует hello год, месяц и день часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="47b96-423">Имя файла Hello использует часть hello время начала часа hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="47b96-424">Hello `"external": true` параметр уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

<span data-ttu-id="47b96-425">**Выходной набор данных Azure Data Lake Store:**</span><span class="sxs-lookup"><span data-stu-id="47b96-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="47b96-426">следующие хранилища Озера tooData данных копии пример Hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="47b96-427">Новые данные копируются хранилища Озера tooData каждый час.</span><span class="sxs-lookup"><span data-stu-id="47b96-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="47b96-428">**Действие копирования в конвейере с BLOB-объектом в качестве источника и Data Lake Store в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="47b96-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="47b96-429">В следующем примере hello, hello конвейера содержит операции копирования, настроенный toouse hello наборы входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="47b96-430">Действие копирования Hello — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="47b96-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="47b96-431">В определении JSON конвейера hello, hello `source` тип установлен слишком`BlobSource`и hello `sink` тип установлен слишком`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="47b96-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="47b96-432">Пример: Копирование данных из хранилища Озера данных Azure tooan BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="47b96-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="47b96-433">пример кода Hello в этом разделе показано:</span><span class="sxs-lookup"><span data-stu-id="47b96-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="47b96-434">Связанная служба типа [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="47b96-435">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="47b96-436">Входной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="47b96-437">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="47b96-438">[Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [AzureDataLakeStoreSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="47b96-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="47b96-439">Каждый час кода Hello копируется из tooan хранилища Озера данных Azure BLOB-объекта данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="47b96-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="47b96-440">**Связанная служба Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="47b96-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="47b96-441">Сведения о конфигурации, в разделе hello [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="47b96-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="47b96-442">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="47b96-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="47b96-443">**Входной набор данных Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="47b96-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="47b96-444">В этом примере параметр `"external"` слишком`true` информирует hello служба фабрики данных, таблица hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="47b96-445">**Выходной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="47b96-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="47b96-446">В следующем примере hello, данные записываются новый большой двоичный объект tooa каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="47b96-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="47b96-447">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="47b96-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="47b96-448">путь к папке Hello использует hello год, месяц, день и часы часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
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

<span data-ttu-id="47b96-449">**Действие копирования в конвейере с Azure Data Lake Store в качестве источника и BLOB-объектом в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="47b96-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="47b96-450">В следующем примере hello, hello конвейера содержит операции копирования, настроенный toouse hello наборы входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="47b96-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="47b96-451">Действие копирования Hello — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="47b96-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="47b96-452">В определении JSON конвейера hello, hello `source` тип установлен слишком`AzureDataLakeStoreSource`и hello `sink` тип установлен слишком`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="47b96-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="47b96-453">В определении действия копирования hello также можно сопоставить столбцы из hello исходного набора данных toocolumns в наборе данных приемник hello.</span><span class="sxs-lookup"><span data-stu-id="47b96-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="47b96-454">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="47b96-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="47b96-455">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="47b96-455">Performance and tuning</span></span>
<span data-ttu-id="47b96-456">toolearn о hello факторы, влияющие на производительность действие копирования и как toooptimize, разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="47b96-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
