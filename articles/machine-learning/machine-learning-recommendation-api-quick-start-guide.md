---
title: "Краткое руководство по API рекомендаций для машинного обучения (версии 1) | Документация Майкрософт"
description: "Рекомендации по Машинному обучению Azure. Краткое руководство по началу работы"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="2172d-104">Краткое руководство по API рекомендаций для машинного обучения (версии 1)</span><span class="sxs-lookup"><span data-stu-id="2172d-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="2172d-105">Начните использовать [API рекомендаций Cognitive Services](https://www.microsoft.com/cognitive-services/recommendations-api) вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="2172d-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="2172d-106">Когнитивная служба рекомендаций заменит эту службу, и все новые функции будут разрабатываться в ней.</span><span class="sxs-lookup"><span data-stu-id="2172d-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="2172d-107">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="2172d-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="2172d-108">Узнайте больше о [переходе на новую службу Cognitive Services](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="2172d-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="2172d-109">В этом документе описывается, как настроить вашу службу или приложение для использования службы рекомендаций машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2172d-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="2172d-110">Дополнительную информацию об API рекомендаций можно найти в [коллекции Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="2172d-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="2172d-111">Общая информация</span><span class="sxs-lookup"><span data-stu-id="2172d-111">General overview</span></span>
<span data-ttu-id="2172d-112">Для использования службы рекомендаций машинного обучения Azure необходимо сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="2172d-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="2172d-113">Создать модель. Модель — это контейнер с данными об использовании, данными каталога и моделью рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="2172d-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="2172d-114">Импортировать данные каталога. Каталог содержит метаданные элементов.</span><span class="sxs-lookup"><span data-stu-id="2172d-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="2172d-115">Импортировать данные об использовании. Данные об использовании можно передать одним из двух способов (или обоими):</span><span class="sxs-lookup"><span data-stu-id="2172d-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="2172d-116">путем загрузки файла, содержащего данные об использовании;</span><span class="sxs-lookup"><span data-stu-id="2172d-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="2172d-117">путем отправки событий сбора данных.</span><span class="sxs-lookup"><span data-stu-id="2172d-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="2172d-118">Обычно загружают файл с данными об использовании, чтобы создать исходную модель рекомендаций (программу начальной загрузки) и использовать ее, пока система не соберет достаточно данных с помощью формата сбора данных.</span><span class="sxs-lookup"><span data-stu-id="2172d-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="2172d-119">Построить модель рекомендаций. Это асинхронная операция, при которой система рекомендаций принимает все данные об использовании и создает модель рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="2172d-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="2172d-120">Эта операция может занять несколько минут или часов в зависимости от размера данных и параметров конфигурации построения.</span><span class="sxs-lookup"><span data-stu-id="2172d-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="2172d-121">При запуске сборки вы получите ее идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2172d-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="2172d-122">Используйте его для проверки завершения процесса сборки, прежде чем начать использовать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2172d-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="2172d-123">Получить рекомендации. Получите рекомендации для определенного элемента или списка элементов.</span><span class="sxs-lookup"><span data-stu-id="2172d-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="2172d-124">Все описанные выше действия выполняются с помощью API рекомендаций машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2172d-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="2172d-125">Кроме того, пример приложения, который реализует каждое из этих действий, можно скачать из [коллекции](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="2172d-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="2172d-126">Ограничения</span><span class="sxs-lookup"><span data-stu-id="2172d-126">Limitations</span></span>
* <span data-ttu-id="2172d-127">Максимальное число моделей на одну подписку — 10.</span><span class="sxs-lookup"><span data-stu-id="2172d-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="2172d-128">Максимальное количество элементов в каталоге равно 100 000.</span><span class="sxs-lookup"><span data-stu-id="2172d-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="2172d-129">Максимальное количество поддерживаемых точек использования — около 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="2172d-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="2172d-130">По мере поступления новых точек будут удаляться самые старые.</span><span class="sxs-lookup"><span data-stu-id="2172d-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="2172d-131">Максимальный размер данных, которые можно отправить в POST (например, импорт данных каталога, импорт данных об использовании), составляет 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="2172d-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="2172d-132">Число транзакций в секунду для неактивной сборки модели рекомендаций — около 2.</span><span class="sxs-lookup"><span data-stu-id="2172d-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="2172d-133">Для активной сборки модели рекомендаций это значение может достигать 20 транзакций в секунду.</span><span class="sxs-lookup"><span data-stu-id="2172d-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="2172d-134">Интеграция</span><span class="sxs-lookup"><span data-stu-id="2172d-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="2172d-135">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="2172d-135">Authentication</span></span>
<span data-ttu-id="2172d-136">Micosoft Azure Marketplace поддерживает обычную проверку подлинности и аутентификацию OAuth.</span><span class="sxs-lookup"><span data-stu-id="2172d-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="2172d-137">Ключи учетной записи можно легко найти, перейдя к ключам на сайте Marketplace в разделе [параметров учетной записи](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="2172d-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="2172d-138">Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="2172d-138">Basic Authentication</span></span>
<span data-ttu-id="2172d-139">Добавьте заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="2172d-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="2172d-140">Преобразование в Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="2172d-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="2172d-141">Преобразование в Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="2172d-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="2172d-142">URI службы</span><span class="sxs-lookup"><span data-stu-id="2172d-142">Service URI</span></span>
<span data-ttu-id="2172d-143">Корневой код URI служб для интерфейсов API рекомендаций по Машинному обучению Azure находится [здесь](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="2172d-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="2172d-144">Полный URI-код службы выражается с помощью элементов спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="2172d-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="2172d-145">Версия API</span><span class="sxs-lookup"><span data-stu-id="2172d-145">API version</span></span>
<span data-ttu-id="2172d-146">У каждого вызова API будет в конце параметр запроса, называемый apiVersion, который должен иметь значение 1.0.</span><span class="sxs-lookup"><span data-stu-id="2172d-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="2172d-147">Учет регистра в идентификаторах</span><span class="sxs-lookup"><span data-stu-id="2172d-147">IDs are case-sensitive</span></span>
<span data-ttu-id="2172d-148">Идентификаторы, возвращаемые любым API, учитывают регистр и должны использоваться в исходном виде при передаче в качестве параметров в последующих вызовах API.</span><span class="sxs-lookup"><span data-stu-id="2172d-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="2172d-149">Например, регистр учитывается в идентификаторах моделей и каталогов.</span><span class="sxs-lookup"><span data-stu-id="2172d-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="2172d-150">Создание модели</span><span class="sxs-lookup"><span data-stu-id="2172d-150">Create a model</span></span>
<span data-ttu-id="2172d-151">Создание запроса create model.</span><span class="sxs-lookup"><span data-stu-id="2172d-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="2172d-152">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-152">HTTP Method</span></span> | <span data-ttu-id="2172d-153">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-154">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="2172d-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-156">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-156">Parameter Name</span></span> | <span data-ttu-id="2172d-157">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-158">modelName</span><span class="sxs-lookup"><span data-stu-id="2172d-158">modelName</span></span> |<span data-ttu-id="2172d-159">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="2172d-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2172d-160">Максимальная длина: 20</span><span class="sxs-lookup"><span data-stu-id="2172d-160">Max length: 20</span></span> |
| <span data-ttu-id="2172d-161">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-161">apiVersion</span></span> |<span data-ttu-id="2172d-162">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-162">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-163">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-163">Request Body</span></span> |<span data-ttu-id="2172d-164">НЕТ</span><span class="sxs-lookup"><span data-stu-id="2172d-164">NONE</span></span> |

<span data-ttu-id="2172d-165">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-165">**Response**:</span></span>

<span data-ttu-id="2172d-166">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="2172d-167">`feed/entry/content/properties/id` — содержит идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="2172d-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="2172d-168">Обратите внимание, что в идентификаторе модели учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="2172d-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="2172d-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="2172d-170">Импорт данных каталога</span><span class="sxs-lookup"><span data-stu-id="2172d-170">Import catalog data</span></span>
<span data-ttu-id="2172d-171">В случае передачи нескольких файлов каталога в одну модель несколькими вызовами мы вставим только новые элементы каталога.</span><span class="sxs-lookup"><span data-stu-id="2172d-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="2172d-172">Существующие элементы останутся с исходными значениями.</span><span class="sxs-lookup"><span data-stu-id="2172d-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="2172d-173">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-173">HTTP Method</span></span> | <span data-ttu-id="2172d-174">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-175">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="2172d-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-177">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-177">Parameter Name</span></span> | <span data-ttu-id="2172d-178">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-179">modelId</span><span class="sxs-lookup"><span data-stu-id="2172d-179">modelId</span></span> |<span data-ttu-id="2172d-180">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-181">filename</span><span class="sxs-lookup"><span data-stu-id="2172d-181">filename</span></span> |<span data-ttu-id="2172d-182">Текстовый идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="2172d-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="2172d-183">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="2172d-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2172d-184">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="2172d-184">Max length: 50</span></span> |
| <span data-ttu-id="2172d-185">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-185">apiVersion</span></span> |<span data-ttu-id="2172d-186">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-186">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-187">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-187">Request Body</span></span> |<span data-ttu-id="2172d-188">Данные каталога.</span><span class="sxs-lookup"><span data-stu-id="2172d-188">Catalog data.</span></span> <span data-ttu-id="2172d-189">Формат:</span><span class="sxs-lookup"><span data-stu-id="2172d-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="2172d-190">Имя</span><span class="sxs-lookup"><span data-stu-id="2172d-190">Name</span></span></th><th><span data-ttu-id="2172d-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2172d-191">Mandatory</span></span></th><th><span data-ttu-id="2172d-192">Тип</span><span class="sxs-lookup"><span data-stu-id="2172d-192">Type</span></span></th><th><span data-ttu-id="2172d-193">Описание</span><span class="sxs-lookup"><span data-stu-id="2172d-193">Description</span></span></th></tr><tr><td><span data-ttu-id="2172d-194">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="2172d-194">Item Id</span></span></td><td><span data-ttu-id="2172d-195">Да</span><span class="sxs-lookup"><span data-stu-id="2172d-195">Yes</span></span></td><td><span data-ttu-id="2172d-196">Буквенно-цифровой, максимальная длина — 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="2172d-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="2172d-197">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="2172d-198">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="2172d-198">Item Name</span></span></td><td><span data-ttu-id="2172d-199">Да</span><span class="sxs-lookup"><span data-stu-id="2172d-199">Yes</span></span></td><td><span data-ttu-id="2172d-200">Буквенно-цифровой, максимальная длина — 255 знаков.</span><span class="sxs-lookup"><span data-stu-id="2172d-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="2172d-201">Имя элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="2172d-202">Категория элемента</span><span class="sxs-lookup"><span data-stu-id="2172d-202">Item Category</span></span></td><td><span data-ttu-id="2172d-203">Да</span><span class="sxs-lookup"><span data-stu-id="2172d-203">Yes</span></span></td><td><span data-ttu-id="2172d-204">Буквенно-цифровой, максимальная длина — 255 знаков.</span><span class="sxs-lookup"><span data-stu-id="2172d-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="2172d-205">Категория, к которой относится этот элемент (например, кулинарные книги, драма и т. д.); не может быть пустой.</span><span class="sxs-lookup"><span data-stu-id="2172d-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="2172d-206">Описание</span><span class="sxs-lookup"><span data-stu-id="2172d-206">Description</span></span></td><td><span data-ttu-id="2172d-207">Нет</span><span class="sxs-lookup"><span data-stu-id="2172d-207">No</span></span></td><td><span data-ttu-id="2172d-208">Буквенно-цифровой, максимальная длина — 4000 знаков.</span><span class="sxs-lookup"><span data-stu-id="2172d-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="2172d-209">Описание элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="2172d-210">Максимальный размер файла равен 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="2172d-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="2172d-211">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="2172d-212">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-212">**Response**:</span></span>

<span data-ttu-id="2172d-213">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="2172d-214">`Feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="2172d-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2172d-215">`Feed\entry\content\properties\ErrorCount` — количество строк, которые не были вставлены из-за ошибки.</span><span class="sxs-lookup"><span data-stu-id="2172d-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="2172d-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="2172d-217">Импорт данных об использовании</span><span class="sxs-lookup"><span data-stu-id="2172d-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="2172d-218">Отправка файла</span><span class="sxs-lookup"><span data-stu-id="2172d-218">Uploading a file</span></span>
<span data-ttu-id="2172d-219">В этом разделе показано, как передать данные по использованию с помощью файла.</span><span class="sxs-lookup"><span data-stu-id="2172d-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="2172d-220">Можно вызывать этот API несколько раз с данными об использовании.</span><span class="sxs-lookup"><span data-stu-id="2172d-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="2172d-221">Для всех вызовов сохранятся все данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="2172d-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="2172d-222">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-222">HTTP Method</span></span> | <span data-ttu-id="2172d-223">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-224">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="2172d-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-225">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-226">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-226">Parameter Name</span></span> | <span data-ttu-id="2172d-227">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-228">modelId</span><span class="sxs-lookup"><span data-stu-id="2172d-228">modelId</span></span> |<span data-ttu-id="2172d-229">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-230">filename</span><span class="sxs-lookup"><span data-stu-id="2172d-230">filename</span></span> |<span data-ttu-id="2172d-231">Текстовый идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="2172d-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="2172d-232">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="2172d-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2172d-233">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="2172d-233">Max length: 50</span></span> |
| <span data-ttu-id="2172d-234">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-234">apiVersion</span></span> |<span data-ttu-id="2172d-235">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-235">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-236">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-236">Request Body</span></span> |<span data-ttu-id="2172d-237">Данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="2172d-237">Usage data.</span></span> <span data-ttu-id="2172d-238">Формат:</span><span class="sxs-lookup"><span data-stu-id="2172d-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="2172d-239">Имя</span><span class="sxs-lookup"><span data-stu-id="2172d-239">Name</span></span></th><th><span data-ttu-id="2172d-240">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2172d-240">Mandatory</span></span></th><th><span data-ttu-id="2172d-241">Тип</span><span class="sxs-lookup"><span data-stu-id="2172d-241">Type</span></span></th><th><span data-ttu-id="2172d-242">Описание</span><span class="sxs-lookup"><span data-stu-id="2172d-242">Description</span></span></th></tr><tr><td><span data-ttu-id="2172d-243">Идентификатор пользователя</span><span class="sxs-lookup"><span data-stu-id="2172d-243">User Id</span></span></td><td><span data-ttu-id="2172d-244">Да</span><span class="sxs-lookup"><span data-stu-id="2172d-244">Yes</span></span></td><td><span data-ttu-id="2172d-245">Буквенно-цифровой</span><span class="sxs-lookup"><span data-stu-id="2172d-245">Alphanumeric</span></span></td><td><span data-ttu-id="2172d-246">Уникальный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="2172d-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="2172d-247">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="2172d-247">Item Id</span></span></td><td><span data-ttu-id="2172d-248">Да</span><span class="sxs-lookup"><span data-stu-id="2172d-248">Yes</span></span></td><td><span data-ttu-id="2172d-249">Буквенно-цифровой, максимальная длина — 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="2172d-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="2172d-250">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="2172d-251">Время</span><span class="sxs-lookup"><span data-stu-id="2172d-251">Time</span></span></td><td><span data-ttu-id="2172d-252">Нет</span><span class="sxs-lookup"><span data-stu-id="2172d-252">No</span></span></td><td><span data-ttu-id="2172d-253">Дата в формате: ГГГГ/ММ/ДДТЧЧ:ММ:СС (например, 2013/06/20Т10:00:00).</span><span class="sxs-lookup"><span data-stu-id="2172d-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="2172d-254">Время данных</span><span class="sxs-lookup"><span data-stu-id="2172d-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="2172d-255">Событие</span><span class="sxs-lookup"><span data-stu-id="2172d-255">Event</span></span></td><td><span data-ttu-id="2172d-256">Нет. Если указано, необходимо также указать дату</span><span class="sxs-lookup"><span data-stu-id="2172d-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="2172d-257">Один из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="2172d-257">One of the following:</span></span><br><span data-ttu-id="2172d-258">• Click</span><span class="sxs-lookup"><span data-stu-id="2172d-258">• Click</span></span><br><span data-ttu-id="2172d-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="2172d-259">• RecommendationClick</span></span><br><span data-ttu-id="2172d-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="2172d-260">•    AddShopCart</span></span><br><span data-ttu-id="2172d-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="2172d-261">• RemoveShopCart</span></span><br><span data-ttu-id="2172d-262">• Покупка</span><span class="sxs-lookup"><span data-stu-id="2172d-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="2172d-263">Максимальный размер файла равен 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="2172d-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="2172d-264">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="2172d-265">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-265">**Response**:</span></span>

<span data-ttu-id="2172d-266">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="2172d-267">`Feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="2172d-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2172d-268">`Feed\entry\content\properties\ErrorCount` — количество строк, которые не были вставлены из-за ошибки.</span><span class="sxs-lookup"><span data-stu-id="2172d-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="2172d-269">`Feed\entry\content\properties\FileId` — идентификатор файла.</span><span class="sxs-lookup"><span data-stu-id="2172d-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="2172d-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="2172d-271">Использование функции сбора данных</span><span class="sxs-lookup"><span data-stu-id="2172d-271">Using data acquisition</span></span>
<span data-ttu-id="2172d-272">В этом разделе показано, как отправлять события в режиме реального времени в службу рекомендаций Машинного обучения Azure с веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="2172d-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="2172d-273">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-273">HTTP Method</span></span> | <span data-ttu-id="2172d-274">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-275">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="2172d-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-276">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-276">Parameter Name</span></span> | <span data-ttu-id="2172d-277">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-278">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-278">apiVersion</span></span> |<span data-ttu-id="2172d-279">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-279">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-280">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-280">Request body</span></span> |<span data-ttu-id="2172d-281">Ввод данных события для каждого события, которое нужно отправить.</span><span class="sxs-lookup"><span data-stu-id="2172d-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="2172d-282">Одному и тому же пользователю или сеансу браузера следует отправлять один и тот же идентификатор в поле SessionId.</span><span class="sxs-lookup"><span data-stu-id="2172d-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="2172d-283">(Пример текста события см. ниже.)</span><span class="sxs-lookup"><span data-stu-id="2172d-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="2172d-284">Пример события Click:</span><span class="sxs-lookup"><span data-stu-id="2172d-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="2172d-285">Пример события RecommendationClick:</span><span class="sxs-lookup"><span data-stu-id="2172d-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2172d-286">Пример события AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="2172d-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2172d-287">Пример события RemoveShopCart:</span><span class="sxs-lookup"><span data-stu-id="2172d-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2172d-288">Пример события Purchase:</span><span class="sxs-lookup"><span data-stu-id="2172d-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="2172d-289">Пример отправки событий двух типов, Click и AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="2172d-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="2172d-290">**Ответ**. Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="2172d-291">Построение модели рекомендаций</span><span class="sxs-lookup"><span data-stu-id="2172d-291">Build a recommendation model</span></span>
| <span data-ttu-id="2172d-292">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-292">HTTP Method</span></span> | <span data-ttu-id="2172d-293">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-294">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="2172d-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-295">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-296">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-296">Parameter Name</span></span> | <span data-ttu-id="2172d-297">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-298">modelId</span><span class="sxs-lookup"><span data-stu-id="2172d-298">modelId</span></span> |<span data-ttu-id="2172d-299">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="2172d-300">userDescription</span></span> |<span data-ttu-id="2172d-301">Текстовый идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="2172d-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="2172d-302">Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См.</span><span class="sxs-lookup"><span data-stu-id="2172d-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="2172d-303">пример выше.</span><span class="sxs-lookup"><span data-stu-id="2172d-303">See example above.</span></span><br><span data-ttu-id="2172d-304">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="2172d-304">Max length: 50</span></span> |
| <span data-ttu-id="2172d-305">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-305">apiVersion</span></span> |<span data-ttu-id="2172d-306">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-306">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-307">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-307">Request Body</span></span> |<span data-ttu-id="2172d-308">НЕТ</span><span class="sxs-lookup"><span data-stu-id="2172d-308">NONE</span></span> |

<span data-ttu-id="2172d-309">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-309">**Response**:</span></span>

<span data-ttu-id="2172d-310">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-310">HTTP Status code: 200</span></span>

<span data-ttu-id="2172d-311">Это асинхронный интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="2172d-311">This is an asynchronous API.</span></span> <span data-ttu-id="2172d-312">В качестве ответа вы получите идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-312">You will get a build ID as a response.</span></span> <span data-ttu-id="2172d-313">Чтобы узнать, завершилась ли сборка, вызовите API «Get Builds Status of a Model» и найдите этот идентификатор сборки в ответе.</span><span class="sxs-lookup"><span data-stu-id="2172d-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="2172d-314">Имейте в виду, что сборка может длиться от нескольких минут до нескольких часов в зависимости от размера данных.</span><span class="sxs-lookup"><span data-stu-id="2172d-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="2172d-315">Пока сборка не завершится, использовать рекомендации нельзя.</span><span class="sxs-lookup"><span data-stu-id="2172d-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="2172d-316">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="2172d-316">Valid build status:</span></span>

* <span data-ttu-id="2172d-317">Create — модель создана;</span><span class="sxs-lookup"><span data-stu-id="2172d-317">Create – Model was created.</span></span>
* <span data-ttu-id="2172d-318">Queued — сборка модели запущена и поставлена в очередь;</span><span class="sxs-lookup"><span data-stu-id="2172d-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="2172d-319">Building — сборка модели выполняется;</span><span class="sxs-lookup"><span data-stu-id="2172d-319">Building – Model is being built.</span></span>
* <span data-ttu-id="2172d-320">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="2172d-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="2172d-321">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="2172d-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="2172d-322">Canceled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="2172d-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="2172d-323">Canceling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="2172d-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="2172d-324">Обратите внимание на то, что идентификатор сборки можно найти по следующему пути: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="2172d-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="2172d-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="2172d-326">Получение состояния сборки модели</span><span class="sxs-lookup"><span data-stu-id="2172d-326">Get build status of a model</span></span>
| <span data-ttu-id="2172d-327">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-327">HTTP Method</span></span> | <span data-ttu-id="2172d-328">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-329">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="2172d-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-330">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-331">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-331">Parameter Name</span></span> | <span data-ttu-id="2172d-332">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-333">modelId</span><span class="sxs-lookup"><span data-stu-id="2172d-333">modelId</span></span> |<span data-ttu-id="2172d-334">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="2172d-335">onlyLastBuild</span></span> |<span data-ttu-id="2172d-336">Указывает, следует вернуть весь журнал сборок модели или только состояние последней сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="2172d-337">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-337">apiVersion</span></span> |<span data-ttu-id="2172d-338">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-338">1.0</span></span> |

<span data-ttu-id="2172d-339">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-339">**Response**:</span></span>

<span data-ttu-id="2172d-340">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-340">HTTP Status code: 200</span></span>

<span data-ttu-id="2172d-341">Ответ включает одну запись для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-341">The response includes one entry per build.</span></span> <span data-ttu-id="2172d-342">Каждая запись содержит следующие данные:</span><span class="sxs-lookup"><span data-stu-id="2172d-342">Each entry has the following data:</span></span>

* <span data-ttu-id="2172d-343">`feed/entry/content/properties/UserName` — имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="2172d-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="2172d-344">`feed/entry/content/properties/ModelName` — имя модели.</span><span class="sxs-lookup"><span data-stu-id="2172d-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="2172d-345">`feed/entry/content/properties/ModelId` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="2172d-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="2172d-346">`feed/entry/content/properties/IsDeployed` — развернута ли сборка (т. е.</span><span class="sxs-lookup"><span data-stu-id="2172d-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="2172d-347">активная сборка).</span><span class="sxs-lookup"><span data-stu-id="2172d-347">active build).</span></span>
* <span data-ttu-id="2172d-348">`feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="2172d-349">`feed/entry/content/properties/BuildType` — тип сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="2172d-350">`feed/entry/content/properties/Status` — состояние сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="2172d-351">Может иметь одно из следующих значений: Error, Building, Queued, Canceling, Canceled, Success.</span><span class="sxs-lookup"><span data-stu-id="2172d-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="2172d-352">`feed/entry/content/properties/StatusMessage` — подробное сообщение о состоянии (относится только к некоторым состояниям).</span><span class="sxs-lookup"><span data-stu-id="2172d-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="2172d-353">`feed/entry/content/properties/Progress` — ход выполнения сборки (%).</span><span class="sxs-lookup"><span data-stu-id="2172d-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="2172d-354">`feed/entry/content/properties/StartTime` — время начала сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="2172d-355">`feed/entry/content/properties/EndTime` — время окончания сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="2172d-356">`feed/entry/content/properties/ExecutionTime` — длительность сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="2172d-357">`feed/entry/content/properties/ProgressStep` — сведения о текущем этапе выполняемой сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="2172d-358">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="2172d-358">Valid build status:</span></span>

* <span data-ttu-id="2172d-359">Created — запись запроса сборки создана;</span><span class="sxs-lookup"><span data-stu-id="2172d-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="2172d-360">Queued — запрос сборки инициирован и помещен в очередь;</span><span class="sxs-lookup"><span data-stu-id="2172d-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="2172d-361">Building — сборка выполняется;</span><span class="sxs-lookup"><span data-stu-id="2172d-361">Building – Build is in process.</span></span>
* <span data-ttu-id="2172d-362">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="2172d-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="2172d-363">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="2172d-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="2172d-364">Canceled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="2172d-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="2172d-365">Canceling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="2172d-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="2172d-366">Допустимые значения типа сборки:</span><span class="sxs-lookup"><span data-stu-id="2172d-366">Valid values for build type:</span></span>

* <span data-ttu-id="2172d-367">Rank — сборка рейтинга; (сведения о сборках рейтинга см.</span><span class="sxs-lookup"><span data-stu-id="2172d-367">Rank - Rank build.</span></span> <span data-ttu-id="2172d-368">в документе "Документация по интерфейсу API рекомендаций для машинного обучения".)</span><span class="sxs-lookup"><span data-stu-id="2172d-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="2172d-369">Recommendation — сборка рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="2172d-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="2172d-370">Fbt — сборка часто покупаемых вместе элементов.</span><span class="sxs-lookup"><span data-stu-id="2172d-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="2172d-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="2172d-372">Получение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="2172d-372">Get recommendations</span></span>
| <span data-ttu-id="2172d-373">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-373">HTTP Method</span></span> | <span data-ttu-id="2172d-374">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-375">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="2172d-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-376">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-377">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-377">Parameter Name</span></span> | <span data-ttu-id="2172d-378">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-379">modelId</span><span class="sxs-lookup"><span data-stu-id="2172d-379">modelId</span></span> |<span data-ttu-id="2172d-380">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="2172d-381">itemIds</span></span> |<span data-ttu-id="2172d-382">Разделенный запятыми список элементов, для которых предоставляются рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2172d-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="2172d-383">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="2172d-383">Max length: 1024</span></span> |
| <span data-ttu-id="2172d-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2172d-384">numberOfResults</span></span> |<span data-ttu-id="2172d-385">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="2172d-385">Number of required results</span></span> |
| <span data-ttu-id="2172d-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2172d-386">includeMetatadata</span></span> |<span data-ttu-id="2172d-387">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="2172d-387">Future use, always false</span></span> |
| <span data-ttu-id="2172d-388">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-388">apiVersion</span></span> |<span data-ttu-id="2172d-389">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-389">1.0</span></span> |

<span data-ttu-id="2172d-390">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="2172d-390">**Response:**</span></span>

<span data-ttu-id="2172d-391">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-391">HTTP Status code: 200</span></span>

<span data-ttu-id="2172d-392">Ответ включает одну запись для каждого рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="2172d-393">Каждая запись содержит следующие данные:</span><span class="sxs-lookup"><span data-stu-id="2172d-393">Each entry has the following data:</span></span>

* <span data-ttu-id="2172d-394">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2172d-395">`Feed\entry\content\properties\Name` — имя элемента.</span><span class="sxs-lookup"><span data-stu-id="2172d-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="2172d-396">`Feed\entry\content\properties\Rating` — оценка рекомендации. Чем выше оценка, тем выше уровень доверия.</span><span class="sxs-lookup"><span data-stu-id="2172d-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2172d-397">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="2172d-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="2172d-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-398">OData XML</span></span>

<span data-ttu-id="2172d-399">Приведенный ниже пример ответа содержит 10 рекомендованных элементов.</span><span class="sxs-lookup"><span data-stu-id="2172d-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="2172d-400">Обновление модели</span><span class="sxs-lookup"><span data-stu-id="2172d-400">Update model</span></span>
<span data-ttu-id="2172d-401">Вы можете обновить описание модели или активный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="2172d-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="2172d-402">*Активный идентификатор сборки* — каждая сборка каждой модели имеет собственный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2172d-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="2172d-403">Активный идентификатор сборки — это первая успешная сборка каждой новой модели.</span><span class="sxs-lookup"><span data-stu-id="2172d-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="2172d-404">Как только у вас будет активный идентификатор сборки и вы выполните дополнительные сборки для той же модели, следует явно задать его в качестве идентификатора сборки по умолчанию, если необходимо.</span><span class="sxs-lookup"><span data-stu-id="2172d-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="2172d-405">Если при получении рекомендаций не указать, какой идентификатор сборки нужно использовать, автоматически будет использоваться идентификатор по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2172d-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="2172d-406">Этот механизм позволяет при наличии действующей модели рекомендаций в рабочей среде выполнять сборку новых моделей и тестировать их перед выпуском.</span><span class="sxs-lookup"><span data-stu-id="2172d-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="2172d-407">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2172d-407">HTTP Method</span></span> | <span data-ttu-id="2172d-408">URI</span><span class="sxs-lookup"><span data-stu-id="2172d-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-409">ОТПРАВКА</span><span class="sxs-lookup"><span data-stu-id="2172d-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2172d-410">Пример:</span><span class="sxs-lookup"><span data-stu-id="2172d-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2172d-411">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="2172d-411">Parameter Name</span></span> | <span data-ttu-id="2172d-412">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="2172d-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2172d-413">id</span><span class="sxs-lookup"><span data-stu-id="2172d-413">id</span></span> |<span data-ttu-id="2172d-414">Уникальный идентификатор модели (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="2172d-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="2172d-415">версия_API</span><span class="sxs-lookup"><span data-stu-id="2172d-415">apiVersion</span></span> |<span data-ttu-id="2172d-416">1.0</span><span class="sxs-lookup"><span data-stu-id="2172d-416">1.0</span></span> |
|  | |
| <span data-ttu-id="2172d-417">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2172d-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="2172d-418">Обратите внимание, что теги XML Description и ActiveBuildId необязательны.</span><span class="sxs-lookup"><span data-stu-id="2172d-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="2172d-419">Если вы не хотите задавать Description или ActiveBuildId, удалите весь тег.</span><span class="sxs-lookup"><span data-stu-id="2172d-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="2172d-420">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="2172d-420">**Response**:</span></span>

<span data-ttu-id="2172d-421">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="2172d-421">HTTP Status code: 200</span></span>

<span data-ttu-id="2172d-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="2172d-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="2172d-423">Юридическая информация</span><span class="sxs-lookup"><span data-stu-id="2172d-423">Legal</span></span>
<span data-ttu-id="2172d-424">Данный документ предоставляется «как есть».</span><span class="sxs-lookup"><span data-stu-id="2172d-424">This document is provided "as-is".</span></span> <span data-ttu-id="2172d-425">Сведения и мнения, представленные в данном документе, включая URL-адреса и ссылки на другие веб-сайты, могут быть изменены без предварительного уведомления.</span><span class="sxs-lookup"><span data-stu-id="2172d-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="2172d-426">Некоторые примеры, содержащиеся в данном документе, являются вымышленными и приводятся исключительно в демонстрационных целях.</span><span class="sxs-lookup"><span data-stu-id="2172d-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="2172d-427">Любое сходство с реальными ситуациями случайно.</span><span class="sxs-lookup"><span data-stu-id="2172d-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="2172d-428">Настоящий документ не предоставляет юридических прав на интеллектуальную собственность в отношении продуктов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2172d-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="2172d-429">Вы можете скопировать и использовать данный документ для внутренних справочных целей.</span><span class="sxs-lookup"><span data-stu-id="2172d-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="2172d-430">© Корпорация Майкрософт, 2014.</span><span class="sxs-lookup"><span data-stu-id="2172d-430">© 2014 Microsoft.</span></span> <span data-ttu-id="2172d-431">Все права защищены.</span><span class="sxs-lookup"><span data-stu-id="2172d-431">All rights reserved.</span></span> 

