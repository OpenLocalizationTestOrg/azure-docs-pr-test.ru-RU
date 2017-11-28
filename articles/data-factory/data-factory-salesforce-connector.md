---
title: "aaaMove данные из Salesforce с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из Salesforce с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="e004a-103">Перемещение данных из Salesforce с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="e004a-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="e004a-104">В этой статье рассматриваются способы действие копирования данных toocopy фабрики данных Azure из хранилища данных tooany Salesforce, перечислены под заголовком столбца приемник hello hello [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="e004a-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e004a-105">Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования и сочетания поддерживаемых данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="e004a-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="e004a-106">Фабрика данных Azure в настоящее время поддерживает только для перемещения данных из Salesforce слишком[приемника хранилища данных поддерживается](data-factory-data-movement-activities.md#supported-data-stores-and-formats), но не поддерживает перемещение данных из других tooSalesforce хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="e004a-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="e004a-107">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="e004a-107">Supported versions</span></span>
<span data-ttu-id="e004a-108">Этот соединитель поддерживает следующие выпусков Salesforce hello: Developer Edition, Professional Edition, Enterprise Edition или выпуск неограниченное.</span><span class="sxs-lookup"><span data-stu-id="e004a-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="e004a-109">Он также поддерживает копирование из рабочей среды Salesforce, песочницы и пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="e004a-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e004a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e004a-110">Prerequisites</span></span>
* <span data-ttu-id="e004a-111">Требуется включить разрешения API.</span><span class="sxs-lookup"><span data-stu-id="e004a-111">API permission must be enabled.</span></span> <span data-ttu-id="e004a-112">Дополнительные сведения о включении доступа к API в Salesforce с помощью набора разрешений см. [здесь](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/).</span><span class="sxs-lookup"><span data-stu-id="e004a-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="e004a-113">toocopy данные из хранилищ данных Salesforce tooon организациями, необходимо иметь по крайней мере 2.0 шлюза управления данных, установленный в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="e004a-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="e004a-114">Ограничения запросов Salesforce</span><span class="sxs-lookup"><span data-stu-id="e004a-114">Salesforce request limits</span></span>
<span data-ttu-id="e004a-115">Для Salesforce установлены ограничения на общее число запросов API и одновременных запросов API.</span><span class="sxs-lookup"><span data-stu-id="e004a-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="e004a-116">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="e004a-116">Note hello following points:</span></span>

- <span data-ttu-id="e004a-117">Если hello число одновременных запросов превышает предел hello, регулирование и вы увидите случайные сбои.</span><span class="sxs-lookup"><span data-stu-id="e004a-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="e004a-118">Если hello общее число запросов превышает предел hello, hello учетной записи Salesforce будет заблокирован на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="e004a-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="e004a-119">Может также возникать ошибка «REQUEST_LIMIT_EXCEEDED» hello в обоих случаях.</span><span class="sxs-lookup"><span data-stu-id="e004a-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="e004a-120">Hello» API ограничения запросов» в разделе hello [Salesforce разработчика ограничения](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="e004a-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e004a-121">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="e004a-121">Getting started</span></span>
<span data-ttu-id="e004a-122">Вы можете создать конвейер с действием копирования, который перемещает данные из Salesforce, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="e004a-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="e004a-123">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="e004a-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e004a-124">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="e004a-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e004a-125">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="e004a-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e004a-126">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="e004a-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e004a-127">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="e004a-128">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e004a-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e004a-129">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="e004a-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e004a-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="e004a-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e004a-131">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="e004a-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e004a-132">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e004a-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e004a-133">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из Salesforce в разделе [пример JSON: копирует данные из Salesforce tooAzure большого двоичного объекта](#json-example-copy-data-from-salesforce-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e004a-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e004a-134">Hello в следующих разделах подробно JSON свойства, которые являются определенной tooSalesforce используется toodefine фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="e004a-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e004a-135">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="e004a-135">Linked service properties</span></span>
<span data-ttu-id="e004a-136">Привет, в следующей таблице приводится описание элементов JSON, которые зависят от конкретного toohello Salesforce связанные службы.</span><span class="sxs-lookup"><span data-stu-id="e004a-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="e004a-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="e004a-137">Property</span></span> | <span data-ttu-id="e004a-138">Описание</span><span class="sxs-lookup"><span data-stu-id="e004a-138">Description</span></span> | <span data-ttu-id="e004a-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e004a-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e004a-140">type</span><span class="sxs-lookup"><span data-stu-id="e004a-140">type</span></span> |<span data-ttu-id="e004a-141">свойство типа Hello должно быть присвоено: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="e004a-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="e004a-142">Да</span><span class="sxs-lookup"><span data-stu-id="e004a-142">Yes</span></span> |
| <span data-ttu-id="e004a-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="e004a-143">environmentUrl</span></span> | <span data-ttu-id="e004a-144">Укажите URL-адрес Salesforce экземпляр hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="e004a-145">— URL-адрес по умолчанию — https://login.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="e004a-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="e004a-146">-toocopy данных из "песочницы", укажите «https://test.salesforce.com».</span><span class="sxs-lookup"><span data-stu-id="e004a-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="e004a-147">-задать toocopy данные из пользовательского домена, например, «https://[domain].my.salesforce.com».</span><span class="sxs-lookup"><span data-stu-id="e004a-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="e004a-148">Нет</span><span class="sxs-lookup"><span data-stu-id="e004a-148">No</span></span> |
| <span data-ttu-id="e004a-149">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="e004a-149">username</span></span> |<span data-ttu-id="e004a-150">Укажите имя пользователя для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="e004a-151">Да</span><span class="sxs-lookup"><span data-stu-id="e004a-151">Yes</span></span> |
| <span data-ttu-id="e004a-152">пароль</span><span class="sxs-lookup"><span data-stu-id="e004a-152">password</span></span> |<span data-ttu-id="e004a-153">Укажите пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="e004a-154">Да</span><span class="sxs-lookup"><span data-stu-id="e004a-154">Yes</span></span> |
| <span data-ttu-id="e004a-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="e004a-155">securityToken</span></span> |<span data-ttu-id="e004a-156">Укажите маркер безопасности для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="e004a-157">В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции tooreset/get маркер безопасности.</span><span class="sxs-lookup"><span data-stu-id="e004a-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="e004a-158">toolearn о маркерах безопасности, см в разделе [безопасности и hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="e004a-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="e004a-159">Да</span><span class="sxs-lookup"><span data-stu-id="e004a-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e004a-160">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="e004a-160">Dataset properties</span></span>
<span data-ttu-id="e004a-161">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="e004a-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e004a-162">Разделы structure, availability и policy JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="e004a-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="e004a-163">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e004a-164">Hello typeProperties статьи для набора данных типа hello **RelationalTable** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="e004a-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="e004a-165">Свойство</span><span class="sxs-lookup"><span data-stu-id="e004a-165">Property</span></span> | <span data-ttu-id="e004a-166">Описание</span><span class="sxs-lookup"><span data-stu-id="e004a-166">Description</span></span> | <span data-ttu-id="e004a-167">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e004a-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e004a-168">tableName</span><span class="sxs-lookup"><span data-stu-id="e004a-168">tableName</span></span> |<span data-ttu-id="e004a-169">Имя таблицы hello в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e004a-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="e004a-170">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="e004a-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e004a-171">для любого пользовательского объекта требуется Hello «__c» часть hello имя API.</span><span class="sxs-lookup"><span data-stu-id="e004a-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="e004a-173">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="e004a-173">Copy activity properties</span></span>
<span data-ttu-id="e004a-174">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="e004a-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e004a-175">Такие свойства, как имя, описание, входные и выходные таблицы, различные политики, доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="e004a-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="e004a-176">Hello свойства, доступные в Здравствуйте раздел typeProperties hello активности hello другой стороны, могут различаться для каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="e004a-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="e004a-177">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e004a-178">В действии копирования, когда источник hello типа hello **RelationalSource** (включая Salesforce), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="e004a-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e004a-179">Свойство</span><span class="sxs-lookup"><span data-stu-id="e004a-179">Property</span></span> | <span data-ttu-id="e004a-180">Описание</span><span class="sxs-lookup"><span data-stu-id="e004a-180">Description</span></span> | <span data-ttu-id="e004a-181">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="e004a-181">Allowed values</span></span> | <span data-ttu-id="e004a-182">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e004a-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e004a-183">query</span><span class="sxs-lookup"><span data-stu-id="e004a-183">query</span></span> |<span data-ttu-id="e004a-184">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="e004a-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e004a-185">Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) .</span><span class="sxs-lookup"><span data-stu-id="e004a-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="e004a-186">Пример: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="e004a-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="e004a-187">Нет (если hello **tableName** из hello **dataset** указан)</span><span class="sxs-lookup"><span data-stu-id="e004a-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e004a-188">для любого пользовательского объекта требуется Hello «__c» часть hello имя API.</span><span class="sxs-lookup"><span data-stu-id="e004a-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="e004a-190">Советы по запросам</span><span class="sxs-lookup"><span data-stu-id="e004a-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="e004a-191">Получение данных с использованием предложения WHERE в столбце даты и времени</span><span class="sxs-lookup"><span data-stu-id="e004a-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="e004a-192">Если указать hello SOQL или SQL-запрос toohello внимания оплаты различие формата даты и времени.</span><span class="sxs-lookup"><span data-stu-id="e004a-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="e004a-193">Например:</span><span class="sxs-lookup"><span data-stu-id="e004a-193">For example:</span></span>

* <span data-ttu-id="e004a-194">**Пример SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e004a-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="e004a-195">**Пример SQL**:</span><span class="sxs-lookup"><span data-stu-id="e004a-195">**SQL sample**:</span></span>
    * <span data-ttu-id="e004a-196">**С помощью запроса hello toospecify мастер копирования:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e004a-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="e004a-197">**С помощью JSON редактирование запроса hello toospecify (escape-знак правильно):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="e004a-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="e004a-198">Извлечение данных из отчета Salesforce</span><span class="sxs-lookup"><span data-stu-id="e004a-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="e004a-199">Из отчетов Salesforce можно извлекать данные, указывая запросы в формате `{call "<report name>"}`, например:</span><span class="sxs-lookup"><span data-stu-id="e004a-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="e004a-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="e004a-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="e004a-201">Восстановление удаленных записей из корзины Salesforce</span><span class="sxs-lookup"><span data-stu-id="e004a-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="e004a-202">записи tooquery hello мягкий удалены из корзины Salesforce, можно указать **«IsDeleted = 1»** в запросе.</span><span class="sxs-lookup"><span data-stu-id="e004a-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="e004a-203">Например,</span><span class="sxs-lookup"><span data-stu-id="e004a-203">For example,</span></span>

* <span data-ttu-id="e004a-204">Укажите tooquery только записи удалены hello, «выберите * из MyTable__c **где IsDeleted = 1**»</span><span class="sxs-lookup"><span data-stu-id="e004a-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="e004a-205">Укажите tooquery все hello записей, включая существующие hello и удалении hello» выберите * из MyTable__c **где IsDeleted = 0 или IsDeleted = 1**»</span><span class="sxs-lookup"><span data-stu-id="e004a-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="e004a-206">Пример JSON: копирует данные из Salesforce tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="e004a-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="e004a-207">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e004a-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e004a-208">Они показывают как toocopy данные из Salesforce tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="e004a-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="e004a-209">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="e004a-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="e004a-210">Ниже приведены hello артефактов фабрики данных, вам потребуется toocreate tooimplement hello сценария.</span><span class="sxs-lookup"><span data-stu-id="e004a-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="e004a-211">последующих список hello Hello разделах содержатся подробные сведения об этих действиях.</span><span class="sxs-lookup"><span data-stu-id="e004a-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="e004a-212">Связанной службы типа hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e004a-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="e004a-213">Связанной службы типа hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="e004a-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="e004a-214">Входным [dataset](data-factory-create-datasets.md) типа hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="e004a-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="e004a-215">Вывод [dataset](data-factory-create-datasets.md) типа hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="e004a-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="e004a-216">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e004a-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="e004a-217">**Связанная служба SalesForce**</span><span class="sxs-lookup"><span data-stu-id="e004a-217">**Salesforce linked service**</span></span>

<span data-ttu-id="e004a-218">В этом примере используется hello **Salesforce** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="e004a-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="e004a-219">В разделе hello [Salesforce связанная служба](#linked-service-properties) раздел для hello свойств, поддерживаемых этой связанной службы.</span><span class="sxs-lookup"><span data-stu-id="e004a-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="e004a-220">В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции как tooreset/get hello маркера безопасности.</span><span class="sxs-lookup"><span data-stu-id="e004a-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="e004a-221">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="e004a-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="e004a-222">**Входной набор данных Salesforce**</span><span class="sxs-lookup"><span data-stu-id="e004a-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
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

<span data-ttu-id="e004a-223">Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="e004a-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e004a-224">для любого пользовательского объекта требуется Hello «__c» часть hello имя API.</span><span class="sxs-lookup"><span data-stu-id="e004a-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="e004a-226">**Выходной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="e004a-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="e004a-227">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="e004a-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="e004a-228">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="e004a-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="e004a-229">Hello конвейера содержит действие копирования, который настроен toouse hello входные и выходные наборы данных, а — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="e004a-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="e004a-230">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource**и hello **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e004a-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="e004a-231">В разделе [свойства типа RelationalSource](#copy-activity-properties) hello список свойств, которые поддерживаются hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="e004a-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="e004a-232">для любого пользовательского объекта требуется Hello «__c» часть hello имя API.</span><span class="sxs-lookup"><span data-stu-id="e004a-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="e004a-234">Сопоставление типов для Salesforce</span><span class="sxs-lookup"><span data-stu-id="e004a-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="e004a-235">Тип данных Salesforce</span><span class="sxs-lookup"><span data-stu-id="e004a-235">Salesforce type</span></span> | <span data-ttu-id="e004a-236">Тип на основе .NET</span><span class="sxs-lookup"><span data-stu-id="e004a-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="e004a-237">Автонумерация</span><span class="sxs-lookup"><span data-stu-id="e004a-237">Auto Number</span></span> |<span data-ttu-id="e004a-238">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-238">String</span></span> |
| <span data-ttu-id="e004a-239">Флажок</span><span class="sxs-lookup"><span data-stu-id="e004a-239">Checkbox</span></span> |<span data-ttu-id="e004a-240">Логический</span><span class="sxs-lookup"><span data-stu-id="e004a-240">Boolean</span></span> |
| <span data-ttu-id="e004a-241">Валюта</span><span class="sxs-lookup"><span data-stu-id="e004a-241">Currency</span></span> |<span data-ttu-id="e004a-242">Double</span><span class="sxs-lookup"><span data-stu-id="e004a-242">Double</span></span> |
| <span data-ttu-id="e004a-243">Дата</span><span class="sxs-lookup"><span data-stu-id="e004a-243">Date</span></span> |<span data-ttu-id="e004a-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="e004a-244">DateTime</span></span> |
| <span data-ttu-id="e004a-245">Дата и время</span><span class="sxs-lookup"><span data-stu-id="e004a-245">Date/Time</span></span> |<span data-ttu-id="e004a-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="e004a-246">DateTime</span></span> |
| <span data-ttu-id="e004a-247">Email</span><span class="sxs-lookup"><span data-stu-id="e004a-247">Email</span></span> |<span data-ttu-id="e004a-248">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-248">String</span></span> |
| <span data-ttu-id="e004a-249">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="e004a-249">Id</span></span> |<span data-ttu-id="e004a-250">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-250">String</span></span> |
| <span data-ttu-id="e004a-251">Связь для подстановки</span><span class="sxs-lookup"><span data-stu-id="e004a-251">Lookup Relationship</span></span> |<span data-ttu-id="e004a-252">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-252">String</span></span> |
| <span data-ttu-id="e004a-253">Список множественного выбора</span><span class="sxs-lookup"><span data-stu-id="e004a-253">Multi-Select Picklist</span></span> |<span data-ttu-id="e004a-254">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-254">String</span></span> |
| <span data-ttu-id="e004a-255">Number</span><span class="sxs-lookup"><span data-stu-id="e004a-255">Number</span></span> |<span data-ttu-id="e004a-256">Double</span><span class="sxs-lookup"><span data-stu-id="e004a-256">Double</span></span> |
| <span data-ttu-id="e004a-257">Процент</span><span class="sxs-lookup"><span data-stu-id="e004a-257">Percent</span></span> |<span data-ttu-id="e004a-258">Double</span><span class="sxs-lookup"><span data-stu-id="e004a-258">Double</span></span> |
| <span data-ttu-id="e004a-259">Номер телефона</span><span class="sxs-lookup"><span data-stu-id="e004a-259">Phone</span></span> |<span data-ttu-id="e004a-260">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-260">String</span></span> |
| <span data-ttu-id="e004a-261">Список выбора</span><span class="sxs-lookup"><span data-stu-id="e004a-261">Picklist</span></span> |<span data-ttu-id="e004a-262">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-262">String</span></span> |
| <span data-ttu-id="e004a-263">текст</span><span class="sxs-lookup"><span data-stu-id="e004a-263">Text</span></span> |<span data-ttu-id="e004a-264">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-264">String</span></span> |
| <span data-ttu-id="e004a-265">Текстовое поле</span><span class="sxs-lookup"><span data-stu-id="e004a-265">Text Area</span></span> |<span data-ttu-id="e004a-266">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-266">String</span></span> |
| <span data-ttu-id="e004a-267">Текстовое поле (длинное)</span><span class="sxs-lookup"><span data-stu-id="e004a-267">Text Area (Long)</span></span> |<span data-ttu-id="e004a-268">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-268">String</span></span> |
| <span data-ttu-id="e004a-269">Текстовое поле (расширенное)</span><span class="sxs-lookup"><span data-stu-id="e004a-269">Text Area (Rich)</span></span> |<span data-ttu-id="e004a-270">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-270">String</span></span> |
| <span data-ttu-id="e004a-271">Текст (зашифрованный)</span><span class="sxs-lookup"><span data-stu-id="e004a-271">Text (Encrypted)</span></span> |<span data-ttu-id="e004a-272">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-272">String</span></span> |
| <span data-ttu-id="e004a-273">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e004a-273">URL</span></span> |<span data-ttu-id="e004a-274">Строка</span><span class="sxs-lookup"><span data-stu-id="e004a-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="e004a-275">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e004a-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="e004a-276">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="e004a-276">Performance and tuning</span></span>
<span data-ttu-id="e004a-277">. В разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="e004a-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
