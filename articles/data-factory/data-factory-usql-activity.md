---
title: "Преобразование данных с помощью сценария U-SQL в Azure | Документация Майкрософт"
description: "Узнайте, как обрабатывать и преобразовывать данные с помощью сценариев U-SQL в службе вычислений Azure Data Lake Analytics."
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
ms.openlocfilehash: 49a809af92ed1bc6664fbdd3bf1aabf36afb8180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="2caa5-103">Преобразование данных с помощью сценариев U-SQL в Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2caa5-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2caa5-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="2caa5-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="2caa5-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="2caa5-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2caa5-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="2caa5-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2caa5-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="2caa5-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2caa5-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="2caa5-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2caa5-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2caa5-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2caa5-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2caa5-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2caa5-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="2caa5-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2caa5-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2caa5-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2caa5-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="2caa5-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="2caa5-114">Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб.</span><span class="sxs-lookup"><span data-stu-id="2caa5-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="2caa5-115">В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки.</span><span class="sxs-lookup"><span data-stu-id="2caa5-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="2caa5-116">В этой статье описывается **действие U-SQL в Data Lake Analytics**, которое запускает сценарий **U-SQL** в связанной службе вычислений **Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2caa5-116">This article describes the **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="2caa5-117">Перед созданием конвейера с действием U-SQL в Data Lake Analytics следует создать учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2caa5-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="2caa5-118">Дополнительные сведения об Azure Data Lake Analytics см. в статье [Начало работы с аналитикой озера данных Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2caa5-118">To learn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="2caa5-119">В руководстве по [созданию первого конвейера](data-factory-build-your-first-pipeline.md) подробно описаны процедуры создания фабрики данных, связанных служб, наборов данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="2caa5-119">Review the [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps to create a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="2caa5-120">Для создания сущностей фабрики данных запустите предложенные фрагменты кода JSON в редакторе фабрики данных, Visual Studio или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2caa5-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell to create Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="2caa5-121">Поддерживаемые типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="2caa5-121">Supported authentication types</span></span>
<span data-ttu-id="2caa5-122">Действие U-SQL поддерживает указанные ниже типы проверки подлинности Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2caa5-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="2caa5-123">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="2caa5-123">Service principal authentication</span></span>
* <span data-ttu-id="2caa5-124">Проверка подлинности учетных данных пользователя (OAuth)</span><span class="sxs-lookup"><span data-stu-id="2caa5-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="2caa5-125">Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для выполнения U-SQL по расписанию.</span><span class="sxs-lookup"><span data-stu-id="2caa5-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="2caa5-126">При проверке подлинности учетных данных пользователя может истечь срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="2caa5-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="2caa5-127">Сведения о настройке см. в разделе [Свойства связанной службы](#azure-data-lake-analytics-linked-service).</span><span class="sxs-lookup"><span data-stu-id="2caa5-127">For configuration details, see the [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="2caa5-128">Связанная служба аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="2caa5-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="2caa5-129">Можно создать связанную службу **Azure Data Lake Analytics** , чтобы связать службу вычислений Azure Data Lake Analytics с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2caa5-129">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="2caa5-130">Действие U-SQL Data Lake Analytics в конвейере ссылается на эту связанную службу.</span><span class="sxs-lookup"><span data-stu-id="2caa5-130">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="2caa5-131">В следующей таблице приведены описания универсальных свойств из определения JSON.</span><span class="sxs-lookup"><span data-stu-id="2caa5-131">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="2caa5-132">Вы можете выбирать между проверкой подлинности на основе субъекта-службы и учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="2caa5-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="2caa5-133">Свойство</span><span class="sxs-lookup"><span data-stu-id="2caa5-133">Property</span></span> | <span data-ttu-id="2caa5-134">Описание</span><span class="sxs-lookup"><span data-stu-id="2caa5-134">Description</span></span> | <span data-ttu-id="2caa5-135">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2caa5-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2caa5-136">**type**</span><span class="sxs-lookup"><span data-stu-id="2caa5-136">**type**</span></span> |<span data-ttu-id="2caa5-137">Свойству type необходимо присвоить значение **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="2caa5-137">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="2caa5-138">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-138">Yes</span></span> |
| <span data-ttu-id="2caa5-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="2caa5-139">**accountName**</span></span> |<span data-ttu-id="2caa5-140">Имя учетной записи аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2caa5-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="2caa5-141">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-141">Yes</span></span> |
| <span data-ttu-id="2caa5-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="2caa5-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="2caa5-143">Универсальный код ресурса (URI) аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2caa5-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="2caa5-144">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-144">No</span></span> |
| <span data-ttu-id="2caa5-145">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="2caa5-145">**subscriptionId**</span></span> |<span data-ttu-id="2caa5-146">Идентификатор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="2caa5-146">Azure subscription id</span></span> |<span data-ttu-id="2caa5-147">Нет (если не указан, используется подписка фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="2caa5-147">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="2caa5-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="2caa5-148">**resourceGroupName**</span></span> |<span data-ttu-id="2caa5-149">Имя группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="2caa5-149">Azure resource group name</span></span> |<span data-ttu-id="2caa5-150">Нет (если не указано, используется группа ресурсов фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="2caa5-150">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="2caa5-151">Проверка подлинности на основе субъекта-службы (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="2caa5-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="2caa5-152">При использовании проверки подлинности на основе субъекта-службы необходимо зарегистрировать сущность приложения в Azure Active Directory (Azure AD) и предоставить ей доступ к Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2caa5-152">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="2caa5-153">Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="2caa5-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="2caa5-154">Запишите следующие значения, которые используются для определения связанной службы:</span><span class="sxs-lookup"><span data-stu-id="2caa5-154">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="2caa5-155">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="2caa5-155">Application ID</span></span>
* <span data-ttu-id="2caa5-156">Ключ приложения</span><span class="sxs-lookup"><span data-stu-id="2caa5-156">Application key</span></span> 
* <span data-ttu-id="2caa5-157">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="2caa5-157">Tenant ID</span></span>

<span data-ttu-id="2caa5-158">Используйте проверку подлинности на основе субъекта-службы, указав следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="2caa5-158">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="2caa5-159">Свойство</span><span class="sxs-lookup"><span data-stu-id="2caa5-159">Property</span></span> | <span data-ttu-id="2caa5-160">Описание</span><span class="sxs-lookup"><span data-stu-id="2caa5-160">Description</span></span> | <span data-ttu-id="2caa5-161">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2caa5-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2caa5-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="2caa5-162">**servicePrincipalId**</span></span> | <span data-ttu-id="2caa5-163">Укажите идентификатора клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="2caa5-163">Specify the application's client ID.</span></span> | <span data-ttu-id="2caa5-164">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-164">Yes</span></span> |
| <span data-ttu-id="2caa5-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="2caa5-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="2caa5-166">Укажите ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="2caa5-166">Specify the application's key.</span></span> | <span data-ttu-id="2caa5-167">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-167">Yes</span></span> |
| <span data-ttu-id="2caa5-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="2caa5-168">**tenant**</span></span> | <span data-ttu-id="2caa5-169">Укажите сведения о клиенте (доменное имя или идентификатор клиента), в котором находится приложение.</span><span class="sxs-lookup"><span data-stu-id="2caa5-169">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="2caa5-170">Эти сведения можно получить, наведя указатель мыши на правый верхний угол страницы портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2caa5-170">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="2caa5-171">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-171">Yes</span></span> |

<span data-ttu-id="2caa5-172">**Пример. Проверка подлинности на основе субъекта-службы**</span><span class="sxs-lookup"><span data-stu-id="2caa5-172">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="2caa5-173">Использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="2caa5-173">User credential authentication</span></span>
<span data-ttu-id="2caa5-174">Кроме того, для Data Lake Analytics можно использовать проверку подлинности на основе учетных данных пользователя, указав приведенные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="2caa5-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="2caa5-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="2caa5-175">Property</span></span> | <span data-ttu-id="2caa5-176">Описание</span><span class="sxs-lookup"><span data-stu-id="2caa5-176">Description</span></span> | <span data-ttu-id="2caa5-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2caa5-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2caa5-178">**authorization**</span><span class="sxs-lookup"><span data-stu-id="2caa5-178">**authorization**</span></span> | <span data-ttu-id="2caa5-179">Нажмите кнопку **Авторизовать** в редакторе фабрики данных и введите учетные данные. URL-адрес авторизации будет создан автоматически и присвоен этому свойству.</span><span class="sxs-lookup"><span data-stu-id="2caa5-179">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="2caa5-180">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-180">Yes</span></span> |
| <span data-ttu-id="2caa5-181">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="2caa5-181">**sessionId**</span></span> | <span data-ttu-id="2caa5-182">Идентификатор сеанса OAuth из сеанса авторизации OAuth.</span><span class="sxs-lookup"><span data-stu-id="2caa5-182">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="2caa5-183">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="2caa5-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="2caa5-184">Этот параметр создается автоматически при использовании редактора фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2caa5-184">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="2caa5-185">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-185">Yes</span></span> |

<span data-ttu-id="2caa5-186">**Пример. Использование проверки подлинности на основе учетных данных пользователя**</span><span class="sxs-lookup"><span data-stu-id="2caa5-186">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="2caa5-187">Срок действия маркера</span><span class="sxs-lookup"><span data-stu-id="2caa5-187">Token expiration</span></span>
<span data-ttu-id="2caa5-188">Срок действия кода авторизации, созданного с помощью кнопки **Авторизовать**, через некоторое время истекает.</span><span class="sxs-lookup"><span data-stu-id="2caa5-188">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="2caa5-189">Сроки действия для различных типов учетных записей пользователей см. в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="2caa5-189">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="2caa5-190">По истечении **срока действия маркера** проверки подлинности может появиться следующее сообщение об ошибке: "Произошла ошибка при операции с учетными данными: invalid_grant — AADSTS70002: ошибка при проверке учетных данных".</span><span class="sxs-lookup"><span data-stu-id="2caa5-190">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="2caa5-191">AADSTS70008: срок действия предоставленных прав доступа истек или они были отозваны.</span><span class="sxs-lookup"><span data-stu-id="2caa5-191">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="2caa5-192">Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Временная отметка: 2015-12-15 21:09:31Z".</span><span class="sxs-lookup"><span data-stu-id="2caa5-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="2caa5-193">Тип пользователя</span><span class="sxs-lookup"><span data-stu-id="2caa5-193">User type</span></span> | <span data-ttu-id="2caa5-194">Срок действия</span><span class="sxs-lookup"><span data-stu-id="2caa5-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="2caa5-195">Учетные записи пользователей, которые не управляются с помощью Azure Active Directory (@hotmail.com, @live.com и т. д.)</span><span class="sxs-lookup"><span data-stu-id="2caa5-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="2caa5-196">12 часов</span><span class="sxs-lookup"><span data-stu-id="2caa5-196">12 hours</span></span> |
| <span data-ttu-id="2caa5-197">Учетные записи пользователей, которые управляются Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="2caa5-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="2caa5-198">14 дней после последнего запуска среза.</span><span class="sxs-lookup"><span data-stu-id="2caa5-198">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="2caa5-199">90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней.</span><span class="sxs-lookup"><span data-stu-id="2caa5-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="2caa5-200">Чтобы избежать этой ошибки или исправить ее, вам потребуется повторно авторизоваться с помощью кнопки **Авторизовать** и повторно развернуть связанную службу, когда **срок действия маркера истечет**.</span><span class="sxs-lookup"><span data-stu-id="2caa5-200">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="2caa5-201">Значения свойств **sessionId** и **authorization** также можно задавать программно с помощью кода:</span><span class="sxs-lookup"><span data-stu-id="2caa5-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="2caa5-202">Подробные сведения о классах фабрики данных, используемых в коде, см. в статьях [AzureDataLakeStoreLinkedService — класс](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService — класс](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) и [AuthorizationSessionGetResponse — класс](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="2caa5-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="2caa5-203">Для использования класса WindowsFormsWebAuthenticationDialog следует добавить ссылку на Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll.</span><span class="sxs-lookup"><span data-stu-id="2caa5-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="2caa5-204">Действие U-SQL в аналитике озера данных</span><span class="sxs-lookup"><span data-stu-id="2caa5-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="2caa5-205">В следующем фрагменте кода JSON определяется конвейер с действием U-SQL в аналитике озера данных.</span><span class="sxs-lookup"><span data-stu-id="2caa5-205">The following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="2caa5-206">Определение действия содержит ссылку на созданную ранее связанную службу аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2caa5-206">The activity definition has a reference to the Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline to compute events for en-gb locale and date less than 2012/02/19.",
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

<span data-ttu-id="2caa5-207">В следующей таблице описаны имена и описания свойств, относящихся к этому действию.</span><span class="sxs-lookup"><span data-stu-id="2caa5-207">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="2caa5-208">Свойство</span><span class="sxs-lookup"><span data-stu-id="2caa5-208">Property</span></span> | <span data-ttu-id="2caa5-209">Описание</span><span class="sxs-lookup"><span data-stu-id="2caa5-209">Description</span></span> | <span data-ttu-id="2caa5-210">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2caa5-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2caa5-211">Тип</span><span class="sxs-lookup"><span data-stu-id="2caa5-211">type</span></span> |<span data-ttu-id="2caa5-212">Для свойства type нужно задать значение **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="2caa5-212">The type property must be set to **DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="2caa5-213">Да</span><span class="sxs-lookup"><span data-stu-id="2caa5-213">Yes</span></span> |
| <span data-ttu-id="2caa5-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="2caa5-214">scriptPath</span></span> |<span data-ttu-id="2caa5-215">Путь к папке, содержащей скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="2caa5-215">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="2caa5-216">В имени файла учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="2caa5-216">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="2caa5-217">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="2caa5-217">No (if you use script)</span></span> |
| <span data-ttu-id="2caa5-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="2caa5-218">scriptLinkedService</span></span> |<span data-ttu-id="2caa5-219">Связанная служба, которая связывает хранилище, содержащее скрипт, с фабрикой данных</span><span class="sxs-lookup"><span data-stu-id="2caa5-219">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="2caa5-220">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="2caa5-220">No (if you use script)</span></span> |
| <span data-ttu-id="2caa5-221">script</span><span class="sxs-lookup"><span data-stu-id="2caa5-221">script</span></span> |<span data-ttu-id="2caa5-222">Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2caa5-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="2caa5-223">Например, `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="2caa5-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="2caa5-224">Нет (при использовании scriptPath и scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="2caa5-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="2caa5-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="2caa5-225">degreeOfParallelism</span></span> |<span data-ttu-id="2caa5-226">Максимальное количество узлов, используемых одновременно для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="2caa5-226">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="2caa5-227">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-227">No</span></span> |
| <span data-ttu-id="2caa5-228">priority</span><span class="sxs-lookup"><span data-stu-id="2caa5-228">priority</span></span> |<span data-ttu-id="2caa5-229">Определяет, какие задания из всех в очереди должны запускаться в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="2caa5-229">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="2caa5-230">Чем меньше число, тем выше приоритет.</span><span class="sxs-lookup"><span data-stu-id="2caa5-230">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="2caa5-231">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-231">No</span></span> |
| <span data-ttu-id="2caa5-232">parameters</span><span class="sxs-lookup"><span data-stu-id="2caa5-232">parameters</span></span> |<span data-ttu-id="2caa5-233">Параметры скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="2caa5-233">Parameters for the U-SQL script</span></span> |<span data-ttu-id="2caa5-234">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-234">No</span></span> |
| <span data-ttu-id="2caa5-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="2caa5-235">runtimeVersion</span></span> | <span data-ttu-id="2caa5-236">Версия среды выполнения обработчика U-SQL, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="2caa5-236">Runtime version of the U-SQL engine to use</span></span> | <span data-ttu-id="2caa5-237">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-237">No</span></span> | 
| <span data-ttu-id="2caa5-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="2caa5-238">compilationMode</span></span> | <p><span data-ttu-id="2caa5-239">Режим компиляции U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2caa5-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="2caa5-240">Может иметь одно из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="2caa5-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="2caa5-241">**Semantic**: выполнение только семантических проверок и необходимых проверок работоспособности.</span><span class="sxs-lookup"><span data-stu-id="2caa5-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="2caa5-242">**Full:** выполнение полной компиляции, включая проверку синтаксиса, оптимизацию, создание кода и т. д.</span><span class="sxs-lookup"><span data-stu-id="2caa5-242">**Full:** Perform the full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="2caa5-243">**SingleBox:** выполнение полной компиляции с параметром TargetType, заданным для SingleBox.</span><span class="sxs-lookup"><span data-stu-id="2caa5-243">**SingleBox:** Perform the full compilation, with TargetType setting to SingleBox.</span></span></li></ul><p><span data-ttu-id="2caa5-244">Если не указать значение для этого свойства, сервер определит оптимальный режим компиляции.</span><span class="sxs-lookup"><span data-stu-id="2caa5-244">If you don't specify a value for this property, the server determines the optimal compilation mode.</span></span> </p>| <span data-ttu-id="2caa5-245">Нет</span><span class="sxs-lookup"><span data-stu-id="2caa5-245">No</span></span> | 

<span data-ttu-id="2caa5-246">Определение сценария см. в разделе [Определение сценария SearchLogProcessing.txt](#sample-u-sql-script).</span><span class="sxs-lookup"><span data-stu-id="2caa5-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for the script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="2caa5-247">Примеры входных и выходных наборов данных</span><span class="sxs-lookup"><span data-stu-id="2caa5-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="2caa5-248">Входной набор данных</span><span class="sxs-lookup"><span data-stu-id="2caa5-248">Input dataset</span></span>
<span data-ttu-id="2caa5-249">В этом примере входной набор данных находится в хранилище озера данных Azure (файл SearchLog.tsv в папке datalake/input).</span><span class="sxs-lookup"><span data-stu-id="2caa5-249">In this example, the input data resides in an Azure Data Lake Store (SearchLog.tsv file in the datalake/input folder).</span></span> 

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

### <a name="output-dataset"></a><span data-ttu-id="2caa5-250">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="2caa5-250">Output dataset</span></span>
<span data-ttu-id="2caa5-251">В этом примере выходные данные, порождаемые скриптом U-SQL, сохраняются в хранилище озера данных Azure (папка datalake/output).</span><span class="sxs-lookup"><span data-stu-id="2caa5-251">In this example, the output data produced by the U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

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

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="2caa5-252">Пример связанной службы Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2caa5-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="2caa5-253">Вот определение примера связанной службы Azure Data Lake Store, используемой наборами входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="2caa5-253">Here is the definition of the sample Azure Data Lake Store linked service used by the input/output datasets.</span></span> 

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

<span data-ttu-id="2caa5-254">Описания свойств JSON см. в статье [Перемещение данных в озеро данных Azure и обратно с помощью фабрики данных Azure](data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="2caa5-254">See [Move data to and from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="2caa5-255">Пример сценария U-SQL</span><span class="sxs-lookup"><span data-stu-id="2caa5-255">Sample U-SQL Script</span></span>

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
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="2caa5-256">Значения параметров **@in** и **@out** в сценарии U-SQL передаются динамически с помощью ADF, используя раздел parameters.</span><span class="sxs-lookup"><span data-stu-id="2caa5-256">The values for **@in** and **@out** parameters in the U-SQL script are passed dynamically by ADF using the ‘parameters’ section.</span></span> <span data-ttu-id="2caa5-257">См. раздел parameters в определении конвейера.</span><span class="sxs-lookup"><span data-stu-id="2caa5-257">See the ‘parameters’ section in the pipeline definition.</span></span>

<span data-ttu-id="2caa5-258">В определении конвейера для заданий, которые выполняются в службе Azure Data Lake Analytics, можно определить другие свойства, например degreeOfParallelism и priority.</span><span class="sxs-lookup"><span data-stu-id="2caa5-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for the jobs that run on the Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="2caa5-259">Динамические параметры</span><span class="sxs-lookup"><span data-stu-id="2caa5-259">Dynamic parameters</span></span>
<span data-ttu-id="2caa5-260">В примере определения конвейера параметрам in и out присвоено жестко заданные значения.</span><span class="sxs-lookup"><span data-stu-id="2caa5-260">In the sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="2caa5-261">Вместо этого можно использовать динамические параметры.</span><span class="sxs-lookup"><span data-stu-id="2caa5-261">It is possible to use dynamic parameters instead.</span></span> <span data-ttu-id="2caa5-262">Например:</span><span class="sxs-lookup"><span data-stu-id="2caa5-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="2caa5-263">В этом случае входные файлы по-прежнему берутся из папки /datalake/input, а выходные файлы создаются в папке /datalake/output.</span><span class="sxs-lookup"><span data-stu-id="2caa5-263">In this case, input files are still picked up from the /datalake/input folder and output files are generated in the /datalake/output folder.</span></span> <span data-ttu-id="2caa5-264">Имена файлов присваиваются динамически, на основе времени начала среза.</span><span class="sxs-lookup"><span data-stu-id="2caa5-264">The file names are dynamic based on the slice start time.</span></span>  

