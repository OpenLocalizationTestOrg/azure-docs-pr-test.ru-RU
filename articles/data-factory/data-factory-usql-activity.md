---
title: "aaaTransform данных с помощью скрипт U-SQL - Azure | Документы Microsoft"
description: "Узнайте, как службы вычислений tooprocess или преобразования данных, выполняя сценарии U-SQL на аналитики Озера данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="3acba-103">Преобразование данных с помощью сценариев U-SQL в Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3acba-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="3acba-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="3acba-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="3acba-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="3acba-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="3acba-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="3acba-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="3acba-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="3acba-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="3acba-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="3acba-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="3acba-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="3acba-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="3acba-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="3acba-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="3acba-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="3acba-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="3acba-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3acba-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="3acba-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="3acba-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="3acba-114">Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб.</span><span class="sxs-lookup"><span data-stu-id="3acba-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="3acba-115">В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки.</span><span class="sxs-lookup"><span data-stu-id="3acba-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="3acba-116">В этой статье описывается hello **действия U-SQL аналитики Озера данных** , на котором запущена **U-SQL** скрипта на **аналитики Озера данных Azure** вычислений связанной службы.</span><span class="sxs-lookup"><span data-stu-id="3acba-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="3acba-117">Перед созданием конвейера с действием U-SQL в Data Lake Analytics следует создать учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3acba-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="3acba-118">toolearn о аналитики Озера данных Azure, в разделе [Приступая к работе с аналитики Озера данных Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3acba-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="3acba-119">Просмотрите hello [сборки в первом учебнике конвейера](data-factory-build-your-first-pipeline.md) для фабрики данных toocreate подробное описание действий, связанных служб, наборы данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="3acba-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="3acba-120">Редактор фабрики данных или toocreate сущностей фабрики данных в Visual Studio или Azure PowerShell с помощью фрагментов JSON.</span><span class="sxs-lookup"><span data-stu-id="3acba-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="3acba-121">Поддерживаемые типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="3acba-121">Supported authentication types</span></span>
<span data-ttu-id="3acba-122">Действие U-SQL поддерживает указанные ниже типы проверки подлинности Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3acba-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="3acba-123">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="3acba-123">Service principal authentication</span></span>
* <span data-ttu-id="3acba-124">Проверка подлинности учетных данных пользователя (OAuth)</span><span class="sxs-lookup"><span data-stu-id="3acba-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="3acba-125">Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для выполнения U-SQL по расписанию.</span><span class="sxs-lookup"><span data-stu-id="3acba-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="3acba-126">При проверке подлинности учетных данных пользователя может истечь срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="3acba-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="3acba-127">Сведения о конфигурации, в разделе hello [связанные свойства службы](#azure-data-lake-analytics-linked-service) раздела.</span><span class="sxs-lookup"><span data-stu-id="3acba-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="3acba-128">Связанная служба аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="3acba-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="3acba-129">Вы создаете **аналитики Озера данных Azure** связанные toolink служба фабрики данных Azure tooan службы вычислений аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3acba-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="3acba-130">действия U-SQL аналитики Озера данных в конвейере hello Hello ссылается toothis связанной службы.</span><span class="sxs-lookup"><span data-stu-id="3acba-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="3acba-131">Hello следующей таблице приводится описание hello универсальных свойств, используемых в определении JSON hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="3acba-132">Вы можете выбирать между проверкой подлинности на основе субъекта-службы и учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="3acba-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="3acba-133">Свойство</span><span class="sxs-lookup"><span data-stu-id="3acba-133">Property</span></span> | <span data-ttu-id="3acba-134">Описание</span><span class="sxs-lookup"><span data-stu-id="3acba-134">Description</span></span> | <span data-ttu-id="3acba-135">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3acba-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3acba-136">**type**</span><span class="sxs-lookup"><span data-stu-id="3acba-136">**type**</span></span> |<span data-ttu-id="3acba-137">свойство типа Hello должно быть присвоено: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="3acba-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="3acba-138">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-138">Yes</span></span> |
| <span data-ttu-id="3acba-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="3acba-139">**accountName**</span></span> |<span data-ttu-id="3acba-140">Имя учетной записи аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3acba-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="3acba-141">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-141">Yes</span></span> |
| <span data-ttu-id="3acba-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="3acba-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="3acba-143">Универсальный код ресурса (URI) аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3acba-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="3acba-144">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-144">No</span></span> |
| <span data-ttu-id="3acba-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="3acba-145">**subscriptionId**</span></span> |<span data-ttu-id="3acba-146">Идентификатор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="3acba-146">Azure subscription id</span></span> |<span data-ttu-id="3acba-147">Нет (если не указан, подписка hello используется фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="3acba-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="3acba-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="3acba-148">**resourceGroupName**</span></span> |<span data-ttu-id="3acba-149">Имя группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="3acba-149">Azure resource group name</span></span> |<span data-ttu-id="3acba-150">Нет (если не указан, группа ресурсов для hello используется фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="3acba-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="3acba-151">Проверка подлинности на основе субъекта-службы (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="3acba-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="3acba-152">toouse основной проверки подлинности службы, регистрация сущности приложения в Azure Active Directory (Azure AD) и предоставьте его hello доступа к хранилищу Озера tooData.</span><span class="sxs-lookup"><span data-stu-id="3acba-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="3acba-153">Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="3acba-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="3acba-154">Запишите следующие значения, которые вы используете hello toodefine hello связанной службы:</span><span class="sxs-lookup"><span data-stu-id="3acba-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="3acba-155">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="3acba-155">Application ID</span></span>
* <span data-ttu-id="3acba-156">Ключ приложения</span><span class="sxs-lookup"><span data-stu-id="3acba-156">Application key</span></span> 
* <span data-ttu-id="3acba-157">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="3acba-157">Tenant ID</span></span>

<span data-ttu-id="3acba-158">Используйте основной проверки подлинности службы, указав hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3acba-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="3acba-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="3acba-159">Property</span></span> | <span data-ttu-id="3acba-160">Описание</span><span class="sxs-lookup"><span data-stu-id="3acba-160">Description</span></span> | <span data-ttu-id="3acba-161">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3acba-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3acba-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="3acba-162">**servicePrincipalId**</span></span> | <span data-ttu-id="3acba-163">Укажите идентификатор клиента приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="3acba-164">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-164">Yes</span></span> |
| <span data-ttu-id="3acba-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="3acba-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="3acba-166">Укажите ключ приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-166">Specify hello application's key.</span></span> | <span data-ttu-id="3acba-167">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-167">Yes</span></span> |
| <span data-ttu-id="3acba-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="3acba-168">**tenant**</span></span> | <span data-ttu-id="3acba-169">Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение.</span><span class="sxs-lookup"><span data-stu-id="3acba-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="3acba-170">Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3acba-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="3acba-171">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-171">Yes</span></span> |

<span data-ttu-id="3acba-172">**Пример. Проверка подлинности на основе субъекта-службы**</span><span class="sxs-lookup"><span data-stu-id="3acba-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="3acba-173">Использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="3acba-173">User credential authentication</span></span>
<span data-ttu-id="3acba-174">Кроме того можно использовать проверку подлинности учетных данных пользователя для аналитики Озера данных, указав hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3acba-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="3acba-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="3acba-175">Property</span></span> | <span data-ttu-id="3acba-176">Описание</span><span class="sxs-lookup"><span data-stu-id="3acba-176">Description</span></span> | <span data-ttu-id="3acba-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3acba-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3acba-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="3acba-178">**authorization**</span></span> | <span data-ttu-id="3acba-179">Нажмите кнопку hello **авторизовать** в hello редактор фабрики данных и ввести учетные данные, назначает hello автоматически авторизации URL-адрес toothis свойство.</span><span class="sxs-lookup"><span data-stu-id="3acba-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="3acba-180">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-180">Yes</span></span> |
| <span data-ttu-id="3acba-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="3acba-181">**sessionId**</span></span> | <span data-ttu-id="3acba-182">Идентификатор сеанса OAuth из сеанса авторизации OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="3acba-183">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="3acba-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="3acba-184">Этот параметр автоматически создается при использовании hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3acba-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="3acba-185">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-185">Yes</span></span> |

<span data-ttu-id="3acba-186">**Пример. Использование проверки подлинности на основе учетных данных пользователя**</span><span class="sxs-lookup"><span data-stu-id="3acba-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="3acba-187">Срок действия маркера</span><span class="sxs-lookup"><span data-stu-id="3acba-187">Token expiration</span></span>
<span data-ttu-id="3acba-188">Здравствуйте, код авторизации, созданный с помощью hello **авторизовать** кнопку срок действия истекает спустя некоторое время.</span><span class="sxs-lookup"><span data-stu-id="3acba-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="3acba-189">См. в следующей таблице для hello сроков действия для различных типов учетных записей пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="3acba-190">Может появиться сообщение об ошибке после hello hello проверки подлинности при **истечения срока действия маркера**: Ошибка действия учетных данных: invalid_grant - AADSTS70002: ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="3acba-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="3acba-191">AADSTS70008: hello предоставляется право доступа просрочен или отозван.</span><span class="sxs-lookup"><span data-stu-id="3acba-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="3acba-192">Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Временная отметка: 2015-12-15 21:09:31Z".</span><span class="sxs-lookup"><span data-stu-id="3acba-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="3acba-193">Тип пользователя</span><span class="sxs-lookup"><span data-stu-id="3acba-193">User type</span></span> | <span data-ttu-id="3acba-194">Срок действия</span><span class="sxs-lookup"><span data-stu-id="3acba-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="3acba-195">Учетные записи пользователей, которые не управляются с помощью Azure Active Directory (@hotmail.com, @live.com и т. д.)</span><span class="sxs-lookup"><span data-stu-id="3acba-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="3acba-196">12 часов</span><span class="sxs-lookup"><span data-stu-id="3acba-196">12 hours</span></span> |
| <span data-ttu-id="3acba-197">Учетные записи пользователей, которые управляются Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="3acba-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="3acba-198">Запустите через 14 дней после последнего фрагмента hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="3acba-199">90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней.</span><span class="sxs-lookup"><span data-stu-id="3acba-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="3acba-200">tooavoid и разрешения этой ошибки, повторно авторизовать с помощью hello **авторизовать** когда hello **истечения срока действия маркера** и повторного развертывания hello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="3acba-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="3acba-201">Значения свойств **sessionId** и **authorization** также можно задавать программно с помощью кода:</span><span class="sxs-lookup"><span data-stu-id="3acba-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="3acba-202">В разделе [класс AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [класс AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), и [AuthorizationSessionGetResponse класса](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) подробные сведения о hello фабрики данных классы, используемые в коде hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="3acba-203">Добавьте ссылку на: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll для hello WindowsFormsWebAuthenticationDialog класса.</span><span class="sxs-lookup"><span data-stu-id="3acba-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="3acba-204">Действие U-SQL в аналитике озера данных</span><span class="sxs-lookup"><span data-stu-id="3acba-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="3acba-205">Привет, следующий фрагмент JSON определяет конвейера действием U-SQL аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3acba-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="3acba-206">Определение действия Hello имеет ссылку toohello службы связаны аналитики Озера данных Azure, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="3acba-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="3acba-207">Hello следующей таблице описаны имена и описания свойства, которые являются определенной toothis действия.</span><span class="sxs-lookup"><span data-stu-id="3acba-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="3acba-208">Свойство</span><span class="sxs-lookup"><span data-stu-id="3acba-208">Property</span></span> | <span data-ttu-id="3acba-209">Описание</span><span class="sxs-lookup"><span data-stu-id="3acba-209">Description</span></span> | <span data-ttu-id="3acba-210">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3acba-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3acba-211">type</span><span class="sxs-lookup"><span data-stu-id="3acba-211">type</span></span> |<span data-ttu-id="3acba-212">свойство типа Hello должно быть задано слишком**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="3acba-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="3acba-213">Да</span><span class="sxs-lookup"><span data-stu-id="3acba-213">Yes</span></span> |
| <span data-ttu-id="3acba-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="3acba-214">scriptPath</span></span> |<span data-ttu-id="3acba-215">Toofolder путь, содержащий скрипт hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3acba-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="3acba-216">Имя файла hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="3acba-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="3acba-217">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="3acba-217">No (if you use script)</span></span> |
| <span data-ttu-id="3acba-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="3acba-218">scriptLinkedService</span></span> |<span data-ttu-id="3acba-219">Связанной службы, которая связывает hello хранилища, содержащий фабрики данных toohello сценария hello</span><span class="sxs-lookup"><span data-stu-id="3acba-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="3acba-220">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="3acba-220">No (if you use script)</span></span> |
| <span data-ttu-id="3acba-221">script</span><span class="sxs-lookup"><span data-stu-id="3acba-221">script</span></span> |<span data-ttu-id="3acba-222">Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="3acba-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="3acba-223">Например, `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="3acba-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="3acba-224">Нет (при использовании scriptPath и scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="3acba-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="3acba-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="3acba-225">degreeOfParallelism</span></span> |<span data-ttu-id="3acba-226">Максимальное количество узлов Hello одновременно использовать toorun hello задания.</span><span class="sxs-lookup"><span data-stu-id="3acba-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="3acba-227">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-227">No</span></span> |
| <span data-ttu-id="3acba-228">priority</span><span class="sxs-lookup"><span data-stu-id="3acba-228">priority</span></span> |<span data-ttu-id="3acba-229">Определяет, какие задания из всех, поставленных в очередь должна быть выбранного toorun сначала.</span><span class="sxs-lookup"><span data-stu-id="3acba-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="3acba-230">Hello hello снижать hello более высокий приоритет hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="3acba-231">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-231">No</span></span> |
| <span data-ttu-id="3acba-232">parameters</span><span class="sxs-lookup"><span data-stu-id="3acba-232">parameters</span></span> |<span data-ttu-id="3acba-233">Параметры для скрипта hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="3acba-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="3acba-234">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-234">No</span></span> |
| <span data-ttu-id="3acba-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="3acba-235">runtimeVersion</span></span> | <span data-ttu-id="3acba-236">Версия среды выполнения toouse engine hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="3acba-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="3acba-237">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-237">No</span></span> | 
| <span data-ttu-id="3acba-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="3acba-238">compilationMode</span></span> | <p><span data-ttu-id="3acba-239">Режим компиляции U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3acba-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="3acba-240">Может иметь одно из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="3acba-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="3acba-241">**Semantic**: выполнение только семантических проверок и необходимых проверок работоспособности.</span><span class="sxs-lookup"><span data-stu-id="3acba-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="3acba-242">**Full:** выполнение полной компиляции hello, включая проверку синтаксиса оптимизации, создание кода, и т. д.</span><span class="sxs-lookup"><span data-stu-id="3acba-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="3acba-243">**SingleBox:** выполнения полной компиляции hello с tooSingleBox параметр TargetType.</span><span class="sxs-lookup"><span data-stu-id="3acba-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="3acba-244">Если не указать значение для этого свойства, hello сервер определяет режим оптимальной компиляции hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="3acba-245">Нет</span><span class="sxs-lookup"><span data-stu-id="3acba-245">No</span></span> | 

<span data-ttu-id="3acba-246">В разделе [SearchLogProcessing.txt сценарий определения](#sample-u-sql-script) hello скрипт определения.</span><span class="sxs-lookup"><span data-stu-id="3acba-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="3acba-247">Примеры входных и выходных наборов данных</span><span class="sxs-lookup"><span data-stu-id="3acba-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="3acba-248">Входной набор данных</span><span class="sxs-lookup"><span data-stu-id="3acba-248">Input dataset</span></span>
<span data-ttu-id="3acba-249">В этом примере hello входные данные хранятся в хранилище Озера данных Azure (SearchLog.tsv файл в папке datalake или ввода hello).</span><span class="sxs-lookup"><span data-stu-id="3acba-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="3acba-250">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="3acba-250">Output dataset</span></span>
<span data-ttu-id="3acba-251">В этом примере hello выходных данных, полученных при hello скрипт U-SQL хранится в хранилище Озера данных Azure (datalake/выходная папка).</span><span class="sxs-lookup"><span data-stu-id="3acba-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="3acba-252">Пример связанной службы Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3acba-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="3acba-253">Вот определение hello образца hello хранилища Озера данных Azure связанной службы, используемые наборы данных hello ввода вывода.</span><span class="sxs-lookup"><span data-stu-id="3acba-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="3acba-254">В разделе [перемещения tooand данных из хранилища Озера данных Azure](data-factory-azure-datalake-connector.md) статьи для описания свойств JSON.</span><span class="sxs-lookup"><span data-stu-id="3acba-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="3acba-255">Пример сценария U-SQL</span><span class="sxs-lookup"><span data-stu-id="3acba-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="3acba-256">Здравствуйте, значения для  **@in**  и  **@out**  параметры в сценарий hello U-SQL, передаются динамически по ADF с помощью раздела «параметры» hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="3acba-257">См. раздел «Параметры» hello в определении конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="3acba-258">Другие свойства, такие как degreeOfParallelism и приоритет также можно указать в определении конвейера для hello заданий, запускаемых на hello Служба аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3acba-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="3acba-259">Динамические параметры</span><span class="sxs-lookup"><span data-stu-id="3acba-259">Dynamic parameters</span></span>
<span data-ttu-id="3acba-260">Увеличение и уменьшение hello пример конвейера определения параметров назначаются с фиксированными значениями.</span><span class="sxs-lookup"><span data-stu-id="3acba-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="3acba-261">Вместо этого — toouse возможных динамических параметров.</span><span class="sxs-lookup"><span data-stu-id="3acba-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="3acba-262">Например:</span><span class="sxs-lookup"><span data-stu-id="3acba-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="3acba-263">В этом случае входные файлы по-прежнему извлекаются из папки /datalake/input hello и выходные файлы создаются в папке /datalake/output hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="3acba-264">имена файлов Hello являются динамическими по времени начала фрагмента hello.</span><span class="sxs-lookup"><span data-stu-id="3acba-264">hello file names are dynamic based on hello slice start time.</span></span>  

