---
title: "Перемещение данных из Salesforce с помощью фабрики данных | Документация Майкрософт"
description: "Узнайте, как перемещать данные из Salesforce с использованием фабрики данных Azure."
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
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="39b5e-103">Перемещение данных из Salesforce с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="39b5e-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="39b5e-104">В этой статье описано, как переместить данные из Salesforce в любое хранилище данных, указанное в таблице [поддерживаемых хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) (столбец "Приемник"), с использованием действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="39b5e-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="39b5e-105">Эта статья основана на статье о [действиях перемещения данных](data-factory-data-movement-activities.md) , в которой приведены общие сведения о перемещении данных с помощью действия копирования и поддерживаемых сочетаниях хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="39b5e-106">Сейчас фабрика данных Azure поддерживает только перемещение данных из Salesforce в другие [поддерживаемые хранилища-приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats), но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="39b5e-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="39b5e-107">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="39b5e-107">Supported versions</span></span>
<span data-ttu-id="39b5e-108">Этот соединитель поддерживает следующие выпуски Salesforce: Developer Edition, Professional Edition, Enterprise Edition или Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="39b5e-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="39b5e-109">Он также поддерживает копирование из рабочей среды Salesforce, песочницы и пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="39b5e-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39b5e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="39b5e-110">Prerequisites</span></span>
* <span data-ttu-id="39b5e-111">Требуется включить разрешения API.</span><span class="sxs-lookup"><span data-stu-id="39b5e-111">API permission must be enabled.</span></span> <span data-ttu-id="39b5e-112">Дополнительные сведения о включении доступа к API в Salesforce с помощью набора разрешений см. [здесь](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/).</span><span class="sxs-lookup"><span data-stu-id="39b5e-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="39b5e-113">Чтобы скопировать данные из Salesforce в локальное хранилище данных, в локальной среде необходимо установить шлюз управления данными версии не ниже 2.0.</span><span class="sxs-lookup"><span data-stu-id="39b5e-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="39b5e-114">Ограничения запросов Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-114">Salesforce request limits</span></span>
<span data-ttu-id="39b5e-115">Для Salesforce установлены ограничения на общее число запросов API и одновременных запросов API.</span><span class="sxs-lookup"><span data-stu-id="39b5e-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="39b5e-116">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="39b5e-116">Note the following points:</span></span>

- <span data-ttu-id="39b5e-117">Если количество одновременных запросов превышает ограничение, выполняется регулирование и возникают случайные ошибки.</span><span class="sxs-lookup"><span data-stu-id="39b5e-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="39b5e-118">В случае превышения ограничения на общее число запросов учетная запись Salesforce блокируется на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="39b5e-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="39b5e-119">Кроме того, в обоих случаях вы можете получить ошибку REQUEST_LIMIT_EXCEEDED.</span><span class="sxs-lookup"><span data-stu-id="39b5e-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="39b5e-120">Дополнительные сведения см. в разделе "API Request Limits" (Ограничения запросов API) статьи об [ограничениях для разработчика Salesforce](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf).</span><span class="sxs-lookup"><span data-stu-id="39b5e-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="39b5e-121">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="39b5e-121">Getting started</span></span>
<span data-ttu-id="39b5e-122">Вы можете создать конвейер с действием копирования, который перемещает данные из Salesforce, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="39b5e-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="39b5e-123">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="39b5e-124">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="39b5e-125">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="39b5e-126">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="39b5e-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="39b5e-127">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="39b5e-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="39b5e-128">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="39b5e-129">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="39b5e-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="39b5e-130">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="39b5e-131">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="39b5e-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="39b5e-132">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="39b5e-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="39b5e-133">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из Salesforce, доступен в разделе [Пример JSON. Копирование данных из Salesforce в большой двоичный объект Azure](#json-example-copy-data-from-salesforce-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="39b5e-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="39b5e-134">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39b5e-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="39b5e-135">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="39b5e-135">Linked service properties</span></span>
<span data-ttu-id="39b5e-136">В таблице ниже приведены описания элементов JSON, которые относятся к связанной службе Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39b5e-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="39b5e-137">Свойство</span><span class="sxs-lookup"><span data-stu-id="39b5e-137">Property</span></span> | <span data-ttu-id="39b5e-138">Описание</span><span class="sxs-lookup"><span data-stu-id="39b5e-138">Description</span></span> | <span data-ttu-id="39b5e-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="39b5e-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39b5e-140">type</span><span class="sxs-lookup"><span data-stu-id="39b5e-140">type</span></span> |<span data-ttu-id="39b5e-141">Для свойства type нужно задать значение **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="39b5e-142">Да</span><span class="sxs-lookup"><span data-stu-id="39b5e-142">Yes</span></span> |
| <span data-ttu-id="39b5e-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="39b5e-143">environmentUrl</span></span> | <span data-ttu-id="39b5e-144">Укажите URL-адрес экземпляра Salesforce.</span><span class="sxs-lookup"><span data-stu-id="39b5e-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="39b5e-145">— URL-адрес по умолчанию — https://login.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="39b5e-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="39b5e-146">— Чтобы скопировать данные из песочницы, укажите URL-адрес https://test.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="39b5e-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="39b5e-147">— Чтобы скопировать данные из пользовательского домена, укажите URL-адрес, например https://[домен].my.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="39b5e-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="39b5e-148">Нет</span><span class="sxs-lookup"><span data-stu-id="39b5e-148">No</span></span> |
| <span data-ttu-id="39b5e-149">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="39b5e-149">username</span></span> |<span data-ttu-id="39b5e-150">Укажите имя пользователя для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="39b5e-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="39b5e-151">Да</span><span class="sxs-lookup"><span data-stu-id="39b5e-151">Yes</span></span> |
| <span data-ttu-id="39b5e-152">password</span><span class="sxs-lookup"><span data-stu-id="39b5e-152">password</span></span> |<span data-ttu-id="39b5e-153">Укажите пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="39b5e-153">Specify a password for the user account.</span></span> |<span data-ttu-id="39b5e-154">Да</span><span class="sxs-lookup"><span data-stu-id="39b5e-154">Yes</span></span> |
| <span data-ttu-id="39b5e-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="39b5e-155">securityToken</span></span> |<span data-ttu-id="39b5e-156">Укажите маркер безопасности для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="39b5e-156">Specify a security token for the user account.</span></span> <span data-ttu-id="39b5e-157">Инструкции по получению и сбросу маркера безопасности см. в статье [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Получение маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="39b5e-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="39b5e-158">Общие сведения о маркере безопасности см. в статье [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm) (Безопасность и API).</span><span class="sxs-lookup"><span data-stu-id="39b5e-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="39b5e-159">Да</span><span class="sxs-lookup"><span data-stu-id="39b5e-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="39b5e-160">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="39b5e-160">Dataset properties</span></span>
<span data-ttu-id="39b5e-161">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="39b5e-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="39b5e-162">Разделы structure, availability и policy JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="39b5e-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="39b5e-163">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="39b5e-164">Раздел typeProperties для набора данных типа **RelationalTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="39b5e-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="39b5e-165">Свойство</span><span class="sxs-lookup"><span data-stu-id="39b5e-165">Property</span></span> | <span data-ttu-id="39b5e-166">Описание</span><span class="sxs-lookup"><span data-stu-id="39b5e-166">Description</span></span> | <span data-ttu-id="39b5e-167">Обязательно</span><span class="sxs-lookup"><span data-stu-id="39b5e-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39b5e-168">tableName</span><span class="sxs-lookup"><span data-stu-id="39b5e-168">tableName</span></span> |<span data-ttu-id="39b5e-169">Имя таблицы в Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="39b5e-170">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="39b5e-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="39b5e-171">Имя API для любых настраиваемых объектов должно содержать приставку __c.</span><span class="sxs-lookup"><span data-stu-id="39b5e-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="39b5e-173">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="39b5e-173">Copy activity properties</span></span>
<span data-ttu-id="39b5e-174">Полный список разделов и свойств, используемых для определения действий, см. в статье [Конвейеры и действия в фабрике данных Azure: создание конвейеров, цепочки действий и расписаний для них](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="39b5e-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="39b5e-175">Такие свойства, как имя, описание, входные и выходные таблицы, различные политики, доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="39b5e-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="39b5e-176">С другой стороны, свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="39b5e-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="39b5e-177">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="39b5e-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="39b5e-178">В случае действия копирования, если источник относится к типу **RelationalSource** (который содержит Salesforce), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="39b5e-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="39b5e-179">Свойство</span><span class="sxs-lookup"><span data-stu-id="39b5e-179">Property</span></span> | <span data-ttu-id="39b5e-180">Описание</span><span class="sxs-lookup"><span data-stu-id="39b5e-180">Description</span></span> | <span data-ttu-id="39b5e-181">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="39b5e-181">Allowed values</span></span> | <span data-ttu-id="39b5e-182">Обязательно</span><span class="sxs-lookup"><span data-stu-id="39b5e-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39b5e-183">query</span><span class="sxs-lookup"><span data-stu-id="39b5e-183">query</span></span> |<span data-ttu-id="39b5e-184">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-184">Use the custom query to read data.</span></span> |<span data-ttu-id="39b5e-185">Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) .</span><span class="sxs-lookup"><span data-stu-id="39b5e-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="39b5e-186">Пример: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="39b5e-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="39b5e-187">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="39b5e-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="39b5e-188">Имя API для любых настраиваемых объектов должно содержать приставку __c.</span><span class="sxs-lookup"><span data-stu-id="39b5e-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="39b5e-190">Советы по запросам</span><span class="sxs-lookup"><span data-stu-id="39b5e-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="39b5e-191">Получение данных с использованием предложения WHERE в столбце даты и времени</span><span class="sxs-lookup"><span data-stu-id="39b5e-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="39b5e-192">При указании запроса SOQL или SQL обратите внимание на различие в формате даты и времени.</span><span class="sxs-lookup"><span data-stu-id="39b5e-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="39b5e-193">Например:</span><span class="sxs-lookup"><span data-stu-id="39b5e-193">For example:</span></span>

* <span data-ttu-id="39b5e-194">**Пример SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="39b5e-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="39b5e-195">**Пример SQL**:</span><span class="sxs-lookup"><span data-stu-id="39b5e-195">**SQL sample**:</span></span>
    * <span data-ttu-id="39b5e-196">**Использование мастера копирования для указания запроса:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="39b5e-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="39b5e-197">**Использование редактирования JSON для указания запроса (соответствующие escape-символы):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="39b5e-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="39b5e-198">Извлечение данных из отчета Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="39b5e-199">Из отчетов Salesforce можно извлекать данные, указывая запросы в формате `{call "<report name>"}`, например:</span><span class="sxs-lookup"><span data-stu-id="39b5e-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="39b5e-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="39b5e-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="39b5e-201">Восстановление удаленных записей из корзины Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="39b5e-202">Чтобы запросить из корзины Salesforce обратимо удаленные записи, укажите в своем запросе **"IsDeleted = 1"**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="39b5e-203">Например,</span><span class="sxs-lookup"><span data-stu-id="39b5e-203">For example,</span></span>

* <span data-ttu-id="39b5e-204">чтобы запросить только удаленные записи, укажите select * from MyTable__c **where IsDeleted= 1**</span><span class="sxs-lookup"><span data-stu-id="39b5e-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="39b5e-205">Чтобы запросить все записи, включая существующие и удаленные, укажите select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**</span><span class="sxs-lookup"><span data-stu-id="39b5e-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="39b5e-206">Пример JSON. Копирование данных из Salesforce в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="39b5e-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="39b5e-207">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39b5e-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="39b5e-208">Вы узнаете, как копировать данные из Salesforce в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="39b5e-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="39b5e-209">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="39b5e-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="39b5e-210">Ниже приведены артефакты фабрики данных, которые необходимо создать для реализации сценария.</span><span class="sxs-lookup"><span data-stu-id="39b5e-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="39b5e-211">В разделах после списка приведены подробные сведения об этих действиях.</span><span class="sxs-lookup"><span data-stu-id="39b5e-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="39b5e-212">Связанная служба типа [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="39b5e-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="39b5e-213">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="39b5e-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="39b5e-214">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39b5e-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="39b5e-215">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39b5e-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="39b5e-216">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39b5e-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="39b5e-217">**Связанная служба SalesForce**</span><span class="sxs-lookup"><span data-stu-id="39b5e-217">**Salesforce linked service**</span></span>

<span data-ttu-id="39b5e-218">В этом примере используется связанная служба **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="39b5e-219">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Свойства связанной службы Salesforce](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39b5e-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="39b5e-220">Инструкции по получению и сбросу маркера безопасности см. в статье [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Получение маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="39b5e-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

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
<span data-ttu-id="39b5e-221">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="39b5e-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="39b5e-222">**Входной набор данных Salesforce**</span><span class="sxs-lookup"><span data-stu-id="39b5e-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="39b5e-223">Если для параметра **external** задать значение **true**, то фабрика данных воспримет этот набор данных как внешний, который создан не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="39b5e-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39b5e-224">Имя API для любых настраиваемых объектов должно содержать приставку __c.</span><span class="sxs-lookup"><span data-stu-id="39b5e-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="39b5e-226">**Выходной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="39b5e-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="39b5e-227">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="39b5e-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="39b5e-228">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="39b5e-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="39b5e-229">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="39b5e-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="39b5e-230">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="39b5e-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="39b5e-231">Список свойств, поддерживаемых RelationalSource, см. в разделе [Свойства типа RelationalSource](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39b5e-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

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
            "description": "Copy from Salesforce to an Azure blob",
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
> <span data-ttu-id="39b5e-232">Имя API для любых настраиваемых объектов должно содержать приставку __c.</span><span class="sxs-lookup"><span data-stu-id="39b5e-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="39b5e-234">Сопоставление типов для Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="39b5e-235">Тип данных Salesforce</span><span class="sxs-lookup"><span data-stu-id="39b5e-235">Salesforce type</span></span> | <span data-ttu-id="39b5e-236">Тип на основе .NET</span><span class="sxs-lookup"><span data-stu-id="39b5e-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="39b5e-237">Автонумерация</span><span class="sxs-lookup"><span data-stu-id="39b5e-237">Auto Number</span></span> |<span data-ttu-id="39b5e-238">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-238">String</span></span> |
| <span data-ttu-id="39b5e-239">Флажок</span><span class="sxs-lookup"><span data-stu-id="39b5e-239">Checkbox</span></span> |<span data-ttu-id="39b5e-240">Логический</span><span class="sxs-lookup"><span data-stu-id="39b5e-240">Boolean</span></span> |
| <span data-ttu-id="39b5e-241">Валюта</span><span class="sxs-lookup"><span data-stu-id="39b5e-241">Currency</span></span> |<span data-ttu-id="39b5e-242">Double</span><span class="sxs-lookup"><span data-stu-id="39b5e-242">Double</span></span> |
| <span data-ttu-id="39b5e-243">Дата</span><span class="sxs-lookup"><span data-stu-id="39b5e-243">Date</span></span> |<span data-ttu-id="39b5e-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="39b5e-244">DateTime</span></span> |
| <span data-ttu-id="39b5e-245">Дата и время</span><span class="sxs-lookup"><span data-stu-id="39b5e-245">Date/Time</span></span> |<span data-ttu-id="39b5e-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="39b5e-246">DateTime</span></span> |
| <span data-ttu-id="39b5e-247">Email</span><span class="sxs-lookup"><span data-stu-id="39b5e-247">Email</span></span> |<span data-ttu-id="39b5e-248">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-248">String</span></span> |
| <span data-ttu-id="39b5e-249">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="39b5e-249">Id</span></span> |<span data-ttu-id="39b5e-250">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-250">String</span></span> |
| <span data-ttu-id="39b5e-251">Связь для подстановки</span><span class="sxs-lookup"><span data-stu-id="39b5e-251">Lookup Relationship</span></span> |<span data-ttu-id="39b5e-252">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-252">String</span></span> |
| <span data-ttu-id="39b5e-253">Список множественного выбора</span><span class="sxs-lookup"><span data-stu-id="39b5e-253">Multi-Select Picklist</span></span> |<span data-ttu-id="39b5e-254">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-254">String</span></span> |
| <span data-ttu-id="39b5e-255">Number</span><span class="sxs-lookup"><span data-stu-id="39b5e-255">Number</span></span> |<span data-ttu-id="39b5e-256">Double</span><span class="sxs-lookup"><span data-stu-id="39b5e-256">Double</span></span> |
| <span data-ttu-id="39b5e-257">Процент</span><span class="sxs-lookup"><span data-stu-id="39b5e-257">Percent</span></span> |<span data-ttu-id="39b5e-258">Double</span><span class="sxs-lookup"><span data-stu-id="39b5e-258">Double</span></span> |
| <span data-ttu-id="39b5e-259">Номер телефона</span><span class="sxs-lookup"><span data-stu-id="39b5e-259">Phone</span></span> |<span data-ttu-id="39b5e-260">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-260">String</span></span> |
| <span data-ttu-id="39b5e-261">Список выбора</span><span class="sxs-lookup"><span data-stu-id="39b5e-261">Picklist</span></span> |<span data-ttu-id="39b5e-262">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-262">String</span></span> |
| <span data-ttu-id="39b5e-263">текст</span><span class="sxs-lookup"><span data-stu-id="39b5e-263">Text</span></span> |<span data-ttu-id="39b5e-264">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-264">String</span></span> |
| <span data-ttu-id="39b5e-265">Текстовое поле</span><span class="sxs-lookup"><span data-stu-id="39b5e-265">Text Area</span></span> |<span data-ttu-id="39b5e-266">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-266">String</span></span> |
| <span data-ttu-id="39b5e-267">Текстовое поле (длинное)</span><span class="sxs-lookup"><span data-stu-id="39b5e-267">Text Area (Long)</span></span> |<span data-ttu-id="39b5e-268">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-268">String</span></span> |
| <span data-ttu-id="39b5e-269">Текстовое поле (расширенное)</span><span class="sxs-lookup"><span data-stu-id="39b5e-269">Text Area (Rich)</span></span> |<span data-ttu-id="39b5e-270">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-270">String</span></span> |
| <span data-ttu-id="39b5e-271">Текст (зашифрованный)</span><span class="sxs-lookup"><span data-stu-id="39b5e-271">Text (Encrypted)</span></span> |<span data-ttu-id="39b5e-272">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-272">String</span></span> |
| <span data-ttu-id="39b5e-273">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="39b5e-273">URL</span></span> |<span data-ttu-id="39b5e-274">Строка</span><span class="sxs-lookup"><span data-stu-id="39b5e-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="39b5e-275">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в разделе [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="39b5e-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="39b5e-276">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="39b5e-276">Performance and tuning</span></span>
<span data-ttu-id="39b5e-277">Ознакомьтесь с [руководством по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в котором описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="39b5e-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
