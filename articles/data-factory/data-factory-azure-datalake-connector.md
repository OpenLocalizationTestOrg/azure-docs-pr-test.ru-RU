---
title: "Копирование данных в Azure Data Lake Store и обратно | Документация Майкрософт"
description: "Узнайте, как с помощью фабрики данных Azure копировать данные в Data Lake Store и обратно"
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
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="06876-103">Копирование данных в Data Lake Store и обратно с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="06876-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="06876-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные в Azure Data Lake Store и обратно.</span><span class="sxs-lookup"><span data-stu-id="06876-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="06876-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="06876-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="06876-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="06876-106">Supported scenarios</span></span>
<span data-ttu-id="06876-107">Данные можно скопировать **из Azure Data Lake Store** в следующие хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="06876-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="06876-108">Данные можно скопировать **в Azure Data Lake Store** из следующих хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="06876-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="06876-109">Прежде чем создавать конвейер с действием копирования, создайте учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="06876-110">Дополнительные сведения см. в статье [Начало работы с хранилищем озера данных Azure с помощью портала Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="06876-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="06876-111">Поддерживаемые типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="06876-111">Supported authentication types</span></span>
<span data-ttu-id="06876-112">Соединитель Data Lake Store поддерживает следующие типы проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="06876-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="06876-113">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="06876-113">Service principal authentication</span></span>
* <span data-ttu-id="06876-114">Проверка подлинности учетных данных пользователя (OAuth)</span><span class="sxs-lookup"><span data-stu-id="06876-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="06876-115">Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для копирования данных по расписанию.</span><span class="sxs-lookup"><span data-stu-id="06876-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="06876-116">При проверке подлинности учетных данных пользователя может истечь срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="06876-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="06876-117">Сведения о настройке см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="06876-118">Начало работы</span><span class="sxs-lookup"><span data-stu-id="06876-118">Get started</span></span>
<span data-ttu-id="06876-119">Можно создать конвейер с действием копирования, которое перемещает данные из Azure Data Lake Store или обратно с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="06876-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="06876-120">Проще всего создать конвейер для копирования данных с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="06876-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="06876-121">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="06876-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="06876-122">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="06876-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="06876-123">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="06876-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="06876-124">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="06876-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="06876-125">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="06876-125">Create a **data factory**.</span></span> <span data-ttu-id="06876-126">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="06876-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="06876-127">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="06876-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="06876-128">Например, при копировании данных из хранилища BLOB-объектов Azure в Azure Data Lake Store создайте две связанные службы, чтобы связать учетную запись хранения Azure и Azure Data Lake Store с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="06876-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="06876-129">Сведения о свойствах связанной службы, относящихся к Azure Data Lake Store, см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="06876-130">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="06876-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="06876-131">В примере, упомянутом на последнем этапе, создайте набор данных, чтобы указать контейнер BLOB-объектов и папку, содержащую входные данные.</span><span class="sxs-lookup"><span data-stu-id="06876-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="06876-132">Также создайте другой набор данных, чтобы указать папку, содержащую данные, скопированные из хранилища BLOB-объектов, и путь к ней в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="06876-133">Сведения о свойствах набора данных, относящихся к Azure Data Lake Store, см. в разделе [Свойства набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="06876-134">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="06876-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="06876-135">В примере выше BlobSource используется как источник, а AzureDataLakeStoreSink — как приемник для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="06876-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="06876-136">Аналогично, при копировании из Azure Data Lake Store в хранилище BLOB-объектов Azure в действии копирования используются AzureDataLakeStoreSource и BlobSink.</span><span class="sxs-lookup"><span data-stu-id="06876-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="06876-137">Сведения о свойствах действия копирования, относящихся к Azure Data Lake Store, см. в разделе [Свойства действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="06876-138">Для получения сведений о том, как использовать хранилище данных как источник или приемник, щелкните ссылку в предыдущем разделе об источнике данных.</span><span class="sxs-lookup"><span data-stu-id="06876-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="06876-139">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="06876-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="06876-140">При использовании средств и API-интерфейсов (за исключением .NET API) эти сущности фабрики данных определяются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="06876-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="06876-141">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных из Azure Data Lake Store, см. в разделе [Примеры определений JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="06876-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="06876-142">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="06876-143">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="06876-143">Linked service properties</span></span>
<span data-ttu-id="06876-144">Связанная служба привязывает хранилище данных к фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="06876-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="06876-145">Для связи Data Lake Store с фабрикой данных следует создать связанную службу типа **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="06876-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="06876-146">В приведенной ниже таблице описываются элементы JSON, которые относятся к связанным службам Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="06876-147">Вы можете выбирать между проверкой подлинности субъекта-службы и учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="06876-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="06876-148">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-148">Property</span></span> | <span data-ttu-id="06876-149">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-149">Description</span></span> | <span data-ttu-id="06876-150">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="06876-151">**type**</span><span class="sxs-lookup"><span data-stu-id="06876-151">**type**</span></span> | <span data-ttu-id="06876-152">Для свойства type следует задать значение **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="06876-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="06876-153">Да</span><span class="sxs-lookup"><span data-stu-id="06876-153">Yes</span></span> |
| <span data-ttu-id="06876-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="06876-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="06876-155">Сведения об учетной записи Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="06876-156">Эти данные принимают один из следующих форматов: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="06876-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="06876-157">Да</span><span class="sxs-lookup"><span data-stu-id="06876-157">Yes</span></span> |
| <span data-ttu-id="06876-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="06876-158">**subscriptionId**</span></span> | <span data-ttu-id="06876-159">Идентификатор подписки Azure, к которой принадлежит учетная запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="06876-160">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="06876-160">Required for sink</span></span> |
| <span data-ttu-id="06876-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="06876-161">**resourceGroupName**</span></span> | <span data-ttu-id="06876-162">Имя группы ресурсов Azure, к которой принадлежит учетная запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="06876-163">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="06876-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="06876-164">Проверка подлинности на основе субъекта-службы (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="06876-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="06876-165">При использовании проверки подлинности на основе субъекта-службы необходимо зарегистрировать сущность приложения в Azure Active Directory (Azure AD) и предоставить ей доступ к Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="06876-166">Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="06876-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="06876-167">Запишите следующие значения, которые используются для определения связанной службы:</span><span class="sxs-lookup"><span data-stu-id="06876-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="06876-168">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="06876-168">Application ID</span></span>
* <span data-ttu-id="06876-169">Ключ приложения</span><span class="sxs-lookup"><span data-stu-id="06876-169">Application key</span></span> 
* <span data-ttu-id="06876-170">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="06876-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06876-171">Если вы используете мастер копирования для создания конвейеров данных, обязательно назначьте субъекту-службе как минимум роль **читателя** в службе управления доступом (управления идентификацией и доступом) для учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="06876-172">Кроме того, предоставьте субъекту-службе разрешения на **чтение и выполнение** в корневом каталоге Data Lake Store ("/") и его дочерних элементах.</span><span class="sxs-lookup"><span data-stu-id="06876-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="06876-173">Иначе может появиться сообщение "Указаны недопустимые учетные данные".</span><span class="sxs-lookup"><span data-stu-id="06876-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="06876-174">Для применения изменений после создания или обновления субъекта-службы в Azure AD может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="06876-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="06876-175">Внимательно проверьте конфигурацию списка управления доступом (ACL) субъекта-службы и Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="06876-176">Если по-прежнему отображается сообщение "Указаны недопустимые учетные данные", подождите некоторое время и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="06876-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="06876-177">Используйте проверку подлинности на основе субъекта-службы, указав следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="06876-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="06876-178">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-178">Property</span></span> | <span data-ttu-id="06876-179">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-179">Description</span></span> | <span data-ttu-id="06876-180">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="06876-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="06876-181">**servicePrincipalId**</span></span> | <span data-ttu-id="06876-182">Укажите идентификатора клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="06876-182">Specify the application's client ID.</span></span> | <span data-ttu-id="06876-183">Да</span><span class="sxs-lookup"><span data-stu-id="06876-183">Yes</span></span> |
| <span data-ttu-id="06876-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="06876-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="06876-185">Укажите ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="06876-185">Specify the application's key.</span></span> | <span data-ttu-id="06876-186">Да</span><span class="sxs-lookup"><span data-stu-id="06876-186">Yes</span></span> |
| <span data-ttu-id="06876-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="06876-187">**tenant**</span></span> | <span data-ttu-id="06876-188">Укажите сведения о клиенте (доменное имя или идентификатор клиента), в котором находится приложение.</span><span class="sxs-lookup"><span data-stu-id="06876-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="06876-189">Эти сведения можно получить, наведя указатель мыши на правый верхний угол страницы портала Azure.</span><span class="sxs-lookup"><span data-stu-id="06876-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="06876-190">Да</span><span class="sxs-lookup"><span data-stu-id="06876-190">Yes</span></span> |

<span data-ttu-id="06876-191">**Пример. Проверка подлинности на основе субъекта-службы**</span><span class="sxs-lookup"><span data-stu-id="06876-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="06876-192">Использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="06876-192">User credential authentication</span></span>
<span data-ttu-id="06876-193">Также для копирования данных в Data Lake Store и обратно можно использовать проверку подлинности на основе учетных данных пользователя, указав приведенные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="06876-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="06876-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-194">Property</span></span> | <span data-ttu-id="06876-195">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-195">Description</span></span> | <span data-ttu-id="06876-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="06876-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="06876-197">**authorization**</span></span> | <span data-ttu-id="06876-198">Нажмите кнопку **Авторизовать** в редакторе фабрики данных и введите учетные данные. URL-адрес авторизации будет создан автоматически и присвоен этому свойству.</span><span class="sxs-lookup"><span data-stu-id="06876-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="06876-199">Да</span><span class="sxs-lookup"><span data-stu-id="06876-199">Yes</span></span> |
| <span data-ttu-id="06876-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="06876-200">**sessionId**</span></span> | <span data-ttu-id="06876-201">Идентификатор сеанса OAuth из сеанса авторизации OAuth.</span><span class="sxs-lookup"><span data-stu-id="06876-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="06876-202">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="06876-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="06876-203">Этот параметр создается автоматически при использовании редактора фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="06876-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="06876-204">Да</span><span class="sxs-lookup"><span data-stu-id="06876-204">Yes</span></span> |

<span data-ttu-id="06876-205">**Пример. Использование проверки подлинности на основе учетных данных пользователя**</span><span class="sxs-lookup"><span data-stu-id="06876-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="06876-206">Срок действия маркера</span><span class="sxs-lookup"><span data-stu-id="06876-206">Token expiration</span></span>
<span data-ttu-id="06876-207">Срок действия кода авторизации, созданного с помощью кнопки **Авторизовать**, через некоторое время истекает.</span><span class="sxs-lookup"><span data-stu-id="06876-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="06876-208">Следующее сообщение означает, что срок действия маркера проверки подлинности истек.</span><span class="sxs-lookup"><span data-stu-id="06876-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="06876-209">"Произошла ошибка при операции с учетными данными: invalid_grant — AADSTS70002. Ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="06876-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="06876-210">AADSTS70008: срок действия предоставленных прав доступа истек или они были отозваны.</span><span class="sxs-lookup"><span data-stu-id="06876-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="06876-211">Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Метка времени: 2015-12-15 21-09-31Z".</span><span class="sxs-lookup"><span data-stu-id="06876-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="06876-212">Сроки действия для различных типов учетных записей пользователей см. в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="06876-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="06876-213">Тип пользователя</span><span class="sxs-lookup"><span data-stu-id="06876-213">User type</span></span> | <span data-ttu-id="06876-214">Срок действия</span><span class="sxs-lookup"><span data-stu-id="06876-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="06876-215">Учетные записи пользователей, которые *не* управляются с помощью Azure Active Directory (например, @hotmail.com или @live.com).</span><span class="sxs-lookup"><span data-stu-id="06876-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="06876-216">12 часов</span><span class="sxs-lookup"><span data-stu-id="06876-216">12 hours</span></span> |
| <span data-ttu-id="06876-217">Учетные записи пользователей, которые управляются с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06876-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="06876-218">14 дней после последнего выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="06876-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="06876-219">90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней.</span><span class="sxs-lookup"><span data-stu-id="06876-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="06876-220">Если пароль изменяется прежде, чем срок действия маркера истечет, маркер мгновенно устаревает.</span><span class="sxs-lookup"><span data-stu-id="06876-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="06876-221">Появится сообщение, упомянутое ранее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="06876-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="06876-222">Когда срок действия маркера истечет, вы можете повторно авторизовать учетную запись с помощью кнопки **Авторизовать** и повторно развернуть связанную службу.</span><span class="sxs-lookup"><span data-stu-id="06876-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="06876-223">Значения свойств **sessionId** и **authorization** также можно задавать программно с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="06876-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


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
<span data-ttu-id="06876-224">Подробные сведения о классах фабрики данных, используемых в коде, см. в статьях, посвященных классам [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) и [AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="06876-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="06876-225">Добавьте ссылку на версию `2.9.10826.1824` `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` для класса `WindowsFormsWebAuthenticationDialog`, используемого в коде.</span><span class="sxs-lookup"><span data-stu-id="06876-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="06876-226">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="06876-226">Dataset properties</span></span>
<span data-ttu-id="06876-227">Чтобы указать набор данных, представляющий входные данные в Data Lake Store, присвойте свойству **типа** набора данных значение **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="06876-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="06876-228">Для свойства **linkedServiceName** набора данных задайте имя связанной службы Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="06876-229">Полный список разделов и свойств JSON, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="06876-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="06876-230">Разделы набора данных в JSON, такие как **structure**, **availability** и **policy**, одинаковы для всех типов наборов данных (таких как базы данных SQL, Blob-объекты Azure и таблицы Azure).</span><span class="sxs-lookup"><span data-stu-id="06876-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="06876-231">Раздел **typeProperties** отличается для разных типов наборов данных. Он содержит такие сведения, как расположение данных в хранилище данных и формат данных.</span><span class="sxs-lookup"><span data-stu-id="06876-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="06876-232">Раздел **typeProperties** набора данных типа **AzureDataLakeStore** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="06876-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="06876-233">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-233">Property</span></span> | <span data-ttu-id="06876-234">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-234">Description</span></span> | <span data-ttu-id="06876-235">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="06876-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="06876-236">**folderPath**</span></span> |<span data-ttu-id="06876-237">Путь к контейнеру и папке в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="06876-238">Да</span><span class="sxs-lookup"><span data-stu-id="06876-238">Yes</span></span> |
| <span data-ttu-id="06876-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="06876-239">**fileName**</span></span> |<span data-ttu-id="06876-240">Имя файла в Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="06876-241">Свойство **fileName** является необязательным и в нем учитывается регистр символов.</span><span class="sxs-lookup"><span data-stu-id="06876-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="06876-242">Если указать значение **fileName**, то действие (включая копирование) работает с определенным файлом.</span><span class="sxs-lookup"><span data-stu-id="06876-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="06876-243">Если значение **fileName** не указано, то копируются все файлы в **folderPath** для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="06876-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="06876-244">Если значение **fileName** не указано для выходного набора данных, а значение **preserveHierarchy** не указано в приемнике действия, имя созданного файла будет иметь формат Data._GUID_.txt.</span><span class="sxs-lookup"><span data-stu-id="06876-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="06876-245">Например: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="06876-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="06876-246">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-246">No</span></span> |
| <span data-ttu-id="06876-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="06876-247">**partitionedBy**</span></span> |<span data-ttu-id="06876-248">Свойство **partitionedBy** является необязательным.</span><span class="sxs-lookup"><span data-stu-id="06876-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="06876-249">Его можно использовать, чтобы указать динамический путь к папке и имя файла для данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="06876-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="06876-250">Например, путь к папке (**folderPath**) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="06876-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="06876-251">Дополнительные сведения и примеры см. в разделе [Свойство partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="06876-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="06876-252">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-252">No</span></span> |
| <span data-ttu-id="06876-253">**format**</span><span class="sxs-lookup"><span data-stu-id="06876-253">**format**</span></span> | <span data-ttu-id="06876-254">Поддерживаются следующие типы форматов: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** и **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="06876-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="06876-255">Свойству **type** в разделе **format** необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="06876-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="06876-256">Дополнительные сведения см. в разделах [Текстовый формат](data-factory-supported-file-and-compression-formats.md#text-format), [Формат JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Формат ORC](data-factory-supported-file-and-compression-formats.md#orc-format) и [Формат Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format) статьи [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="06876-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="06876-257">Если требуется скопировать файлы между файловыми хранилищами как есть (двоичное копирование), можно пропустить раздел `format` в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="06876-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="06876-258">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-258">No</span></span> |
| <span data-ttu-id="06876-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="06876-259">**compression**</span></span> | <span data-ttu-id="06876-260">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="06876-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="06876-261">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="06876-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="06876-262">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="06876-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="06876-263">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="06876-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="06876-264">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="06876-265">Свойство partitionedBy</span><span class="sxs-lookup"><span data-stu-id="06876-265">The partitionedBy property</span></span>
<span data-ttu-id="06876-266">Для данных временных рядов путь к папке (**folderPath**) и имя файла (**fileName**) можно указывать динамически. Это делается с помощью свойства **partitionedBy**, функций фабрики данных и системных переменных.</span><span class="sxs-lookup"><span data-stu-id="06876-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="06876-267">Подробные сведения см. в статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="06876-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="06876-268">В следующем примере `{Slice}` заменяется значением `SliceStart` (системная переменная фабрики данных) в указанном формате (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="06876-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="06876-269">`SliceStart` в имени указывает время начала среза.</span><span class="sxs-lookup"><span data-stu-id="06876-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="06876-270">Свойство `folderPath` отличается для каждого среза, как и в `wikidatagateway/wikisampledataout/2014100103` или `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="06876-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="06876-271">В следующем примере год, месяц, день и время `SliceStart` извлекаются в отдельные переменные, используемые в свойствах `folderPath` и `fileName`.</span><span class="sxs-lookup"><span data-stu-id="06876-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="06876-272">Дополнительные сведения о наборах данных временных рядов, планировании и срезах см. в статьях [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md) и [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="06876-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="06876-273">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="06876-273">Copy activity properties</span></span>
<span data-ttu-id="06876-274">Полный список разделов и свойств, используемых для определения действий, см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="06876-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="06876-275">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="06876-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="06876-276">Свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="06876-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="06876-277">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="06876-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="06876-278">**AzureDataLakeStoreSource** поддерживает следующее свойство в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="06876-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="06876-279">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-279">Property</span></span> | <span data-ttu-id="06876-280">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-280">Description</span></span> | <span data-ttu-id="06876-281">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="06876-281">Allowed values</span></span> | <span data-ttu-id="06876-282">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06876-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="06876-283">**recursive**</span></span> |<span data-ttu-id="06876-284">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="06876-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="06876-285">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="06876-285">True (default value), False</span></span> |<span data-ttu-id="06876-286">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-286">No</span></span> |


<span data-ttu-id="06876-287">**AzureDataLakeStoreSink** поддерживает следующие свойства в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="06876-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="06876-288">Свойство</span><span class="sxs-lookup"><span data-stu-id="06876-288">Property</span></span> | <span data-ttu-id="06876-289">Описание</span><span class="sxs-lookup"><span data-stu-id="06876-289">Description</span></span> | <span data-ttu-id="06876-290">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="06876-290">Allowed values</span></span> | <span data-ttu-id="06876-291">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06876-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06876-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="06876-292">**copyBehavior**</span></span> |<span data-ttu-id="06876-293">Определяет поведение копирования.</span><span class="sxs-lookup"><span data-stu-id="06876-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="06876-294"><b>PreserveHierarchy:</b> сохраняет иерархию файлов в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="06876-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="06876-295">Относительный путь исходного файла в исходной папке идентичен относительному пути целевого файла в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="06876-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="06876-296"><b>FlattenHierarchy</b>: все файлы из исходной папки создаются на первом уровне в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="06876-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="06876-297">Целевые файлы создаются с автоматически сформированными именами.</span><span class="sxs-lookup"><span data-stu-id="06876-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="06876-298"><b>MergeFiles</b>: объединяет все файлы из исходной папки в один файл.</span><span class="sxs-lookup"><span data-stu-id="06876-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="06876-299">Если указано имя Blob-объекта или имя файла, то оно присваивается объединенному файлу.</span><span class="sxs-lookup"><span data-stu-id="06876-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="06876-300">В противном случае имя файла создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="06876-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="06876-301">Нет</span><span class="sxs-lookup"><span data-stu-id="06876-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="06876-302">Примеры recursive и copyBehavior</span><span class="sxs-lookup"><span data-stu-id="06876-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="06876-303">В данном разделе описываются результаты выполнения операции копирования при использовании различных сочетаний значений recursive и copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="06876-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="06876-304">recursive</span><span class="sxs-lookup"><span data-stu-id="06876-304">recursive</span></span> | <span data-ttu-id="06876-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="06876-305">copyBehavior</span></span> | <span data-ttu-id="06876-306">Результаты выполнения операции</span><span class="sxs-lookup"><span data-stu-id="06876-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06876-307">Да</span><span class="sxs-lookup"><span data-stu-id="06876-307">true</span></span> |<span data-ttu-id="06876-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="06876-308">preserveHierarchy</span></span> |<span data-ttu-id="06876-309">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-310">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-310">Folder1</span></span><br/><span data-ttu-id="06876-311">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-312">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-313">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-317">Целевая папка "Папка1" создается с такой же структурой, как и исходная папка.</span><span class="sxs-lookup"><span data-stu-id="06876-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="06876-318">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-318">Folder1</span></span><br/><span data-ttu-id="06876-319">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-320">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-321">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="06876-325">Да</span><span class="sxs-lookup"><span data-stu-id="06876-325">true</span></span> |<span data-ttu-id="06876-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="06876-326">flattenHierarchy</span></span> |<span data-ttu-id="06876-327">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-328">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-328">Folder1</span></span><br/><span data-ttu-id="06876-329">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-330">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-331">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-335">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="06876-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-336">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-336">Folder1</span></span><br/><span data-ttu-id="06876-337">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="06876-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="06876-338">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="06876-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="06876-339">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"</span><span class="sxs-lookup"><span data-stu-id="06876-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="06876-340">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"</span><span class="sxs-lookup"><span data-stu-id="06876-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="06876-341">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5"</span><span class="sxs-lookup"><span data-stu-id="06876-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="06876-342">Да</span><span class="sxs-lookup"><span data-stu-id="06876-342">true</span></span> |<span data-ttu-id="06876-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="06876-343">mergeFiles</span></span> |<span data-ttu-id="06876-344">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-345">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-345">Folder1</span></span><br/><span data-ttu-id="06876-346">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-347">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-348">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-352">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="06876-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-353">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-353">Folder1</span></span><br/><span data-ttu-id="06876-354">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="06876-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="06876-355">нет</span><span class="sxs-lookup"><span data-stu-id="06876-355">false</span></span> |<span data-ttu-id="06876-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="06876-356">preserveHierarchy</span></span> |<span data-ttu-id="06876-357">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="06876-358">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-358">Folder1</span></span><br/><span data-ttu-id="06876-359">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-360">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-361">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-365">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="06876-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="06876-366">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-366">Folder1</span></span><br/><span data-ttu-id="06876-367">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-368">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="06876-369">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="06876-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="06876-370">нет</span><span class="sxs-lookup"><span data-stu-id="06876-370">false</span></span> |<span data-ttu-id="06876-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="06876-371">flattenHierarchy</span></span> |<span data-ttu-id="06876-372">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="06876-373">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-373">Folder1</span></span><br/><span data-ttu-id="06876-374">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-375">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-376">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-380">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="06876-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="06876-381">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-381">Folder1</span></span><br/><span data-ttu-id="06876-382">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="06876-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="06876-383">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="06876-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="06876-384">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="06876-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="06876-385">нет</span><span class="sxs-lookup"><span data-stu-id="06876-385">false</span></span> |<span data-ttu-id="06876-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="06876-386">mergeFiles</span></span> |<span data-ttu-id="06876-387">Если у исходной папки "Папка1" такая структура: </span><span class="sxs-lookup"><span data-stu-id="06876-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="06876-388">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-388">Folder1</span></span><br/><span data-ttu-id="06876-389">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="06876-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="06876-390">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="06876-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="06876-391">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="06876-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="06876-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="06876-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="06876-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="06876-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="06876-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="06876-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="06876-395">Целевая папка "Папка1" создается со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="06876-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="06876-396">Папка1</span><span class="sxs-lookup"><span data-stu-id="06876-396">Folder1</span></span><br/><span data-ttu-id="06876-397">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="06876-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="06876-398">Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="06876-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="06876-399">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="06876-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="06876-400">Поддерживаемые форматы файлов и сжатия</span><span class="sxs-lookup"><span data-stu-id="06876-400">Supported file and compression formats</span></span>
<span data-ttu-id="06876-401">Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="06876-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="06876-402">Примеры JSON для копирования данных в Data Lake Store и обратно</span><span class="sxs-lookup"><span data-stu-id="06876-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="06876-403">Ниже приведены примеры определений JSON.</span><span class="sxs-lookup"><span data-stu-id="06876-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="06876-404">Эти примеры определений можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06876-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="06876-405">В них показано, как копировать данные в Data Lake Store и хранилище BLOB-объектов Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="06876-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="06876-406">Однако данные можно скопировать данные _непосредственно_ из любых источников на любой из поддерживаемых приемников.</span><span class="sxs-lookup"><span data-stu-id="06876-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="06876-407">Дополнительные сведения см. в разделе "Поддерживаемые хранилища данных и форматы" статьи [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="06876-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="06876-408">Пример. Копирование данных из хранилища BLOB-объектов Azure в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="06876-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="06876-409">В примере кода в этом разделе показано следующее:</span><span class="sxs-lookup"><span data-stu-id="06876-409">The example code in this section shows:</span></span>

* <span data-ttu-id="06876-410">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="06876-411">Связанная служба типа [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="06876-412">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="06876-413">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="06876-414">[Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="06876-415">В этом примере показано копирование данных временного ряда из хранилища BLOB-объектов Azure в Data Lake Store каждый час.</span><span class="sxs-lookup"><span data-stu-id="06876-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="06876-416">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="06876-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="06876-417">**Связанная служба Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="06876-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="06876-418">Сведения о настройке см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="06876-419">**Входной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="06876-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="06876-420">В следующем примере данные берутся из нового BLOB-объекта каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="06876-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="06876-421">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="06876-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="06876-422">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="06876-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="06876-423">В имени файла используется часть времени начала, обозначающая час.</span><span class="sxs-lookup"><span data-stu-id="06876-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="06876-424">Параметр `"external": true` указывает фабрике данных, что эта таблица является внешней по отношению к фабрике данных, а не созданной в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="06876-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="06876-425">**Выходной набор данных Azure Data Lake Store:**</span><span class="sxs-lookup"><span data-stu-id="06876-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="06876-426">Следующий пример кода копирует данные в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="06876-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="06876-427">Новые данные копируются в Data Lake Store каждый час.</span><span class="sxs-lookup"><span data-stu-id="06876-427">New data is copied to Data Lake Store every hour.</span></span>

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


<span data-ttu-id="06876-428">**Действие копирования в конвейере с BLOB-объектом в качестве источника и Data Lake Store в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="06876-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="06876-429">В следующем примере конвейер содержит действие копирования, которое использует входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="06876-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="06876-430">Действие копирования выполняется по расписанию каждый час.</span><span class="sxs-lookup"><span data-stu-id="06876-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="06876-431">В определении JSON конвейера для типа `source` задано значение `BlobSource`, а для типа `sink` — значение `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="06876-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="06876-432">Пример. Копирование данных из Azure Data Lake Store в BLOB-объект Azure</span><span class="sxs-lookup"><span data-stu-id="06876-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="06876-433">В примере кода в этом разделе показано следующее:</span><span class="sxs-lookup"><span data-stu-id="06876-433">The example code in this section shows:</span></span>

* <span data-ttu-id="06876-434">Связанная служба типа [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="06876-435">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="06876-436">Входной [набор данных](data-factory-create-datasets.md) типа [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="06876-437">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="06876-438">[Конвейер](data-factory-create-pipelines.md) с действием копирования, который использует [AzureDataLakeStoreSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="06876-439">В этом коде данные временного ряда каждый час копируются из Data Lake Store в Blob-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="06876-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="06876-440">**Связанная служба Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="06876-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="06876-441">Сведения о настройке см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06876-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="06876-442">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="06876-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="06876-443">**Входной набор данных Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="06876-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="06876-444">В этом примере значение `true` для параметра `"external"` указывает фабрике данных, что эта таблица является внешней по отношению к фабрике данных, а не созданной в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="06876-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="06876-445">**Выходной набор данных большого двоичного объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="06876-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="06876-446">В следующем примере данные записываются в новый BLOB-объект каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="06876-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="06876-447">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="06876-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="06876-448">В пути к папке используются год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="06876-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

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

<span data-ttu-id="06876-449">**Действие копирования в конвейере с Azure Data Lake Store в качестве источника и BLOB-объектом в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="06876-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="06876-450">В следующем примере конвейер содержит действие копирования, которое использует входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="06876-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="06876-451">Действие копирования выполняется по расписанию каждый час.</span><span class="sxs-lookup"><span data-stu-id="06876-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="06876-452">В определении JSON конвейера для типа `source` задано значение `AzureDataLakeStoreSource`, а для типа `sink` — значение `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="06876-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

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

<span data-ttu-id="06876-453">В определении действия копирования также можно сопоставить столбцы из набора данных, используемого в качестве источника, со столбцами из приемника.</span><span class="sxs-lookup"><span data-stu-id="06876-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="06876-454">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="06876-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="06876-455">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="06876-455">Performance and tuning</span></span>
<span data-ttu-id="06876-456">Сведения о факторах, влияющих на производительность действия копирования, и способах оптимизации этого процесса см. в статье [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="06876-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
