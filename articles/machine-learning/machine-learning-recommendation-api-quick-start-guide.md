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
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="3d310-104">Краткое руководство по hello машины обучения рекомендации API (версия 1)</span><span class="sxs-lookup"><span data-stu-id="3d310-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="3d310-105">Необходимо запустить с помощью hello [Когнитивных служба API рекомендации](https://www.microsoft.com/cognitive-services/recommendations-api) вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="3d310-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="3d310-106">Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует.</span><span class="sxs-lookup"><span data-stu-id="3d310-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="3d310-107">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="3d310-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="3d310-108">Дополнительные сведения о [toohello перенос новую службу Когнитивных](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="3d310-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="3d310-109">В этом документе описывается способ tooonboard вашей машины обучения Microsoft Azure рекомендации toouse службу или приложение.</span><span class="sxs-lookup"><span data-stu-id="3d310-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="3d310-110">Дополнительные сведения можно найти на hello API рекомендации в hello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="3d310-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="3d310-111">Общая информация</span><span class="sxs-lookup"><span data-stu-id="3d310-111">General overview</span></span>
<span data-ttu-id="3d310-112">toouse Azure Machine Learning рекомендации, необходимые hello tootake следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="3d310-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="3d310-113">Создание модели - модели — это контейнер, данные об использовании, данные каталога и hello модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="3d310-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="3d310-114">Импорт данных каталога - каталог содержит сведения о метаданных для элементов hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="3d310-115">Импортировать данные об использовании. Данные об использовании можно передать одним из двух способов (или обоими):</span><span class="sxs-lookup"><span data-stu-id="3d310-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="3d310-116">Отправляя этот файл, содержащий данные об использовании hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="3d310-117">путем отправки событий сбора данных.</span><span class="sxs-lookup"><span data-stu-id="3d310-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="3d310-118">Обычно вы загружаете файл использования в порядке toobe может toocreate модель начальной рекомендации (начальной загрузки) и использовать его, пока система hello собирает достаточное количество данных, используя формат приобретения данных hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="3d310-119">Построение модели рекомендаций - это асинхронной операции, в которых hello системы рекомендаций принимает все данные об использовании hello и создает модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="3d310-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="3d310-120">Эта операция может занять несколько минут или несколько часов в зависимости от hello параметры конфигурации построения размера данных hello и hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="3d310-121">При активации hello сборки, вы получите идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="3d310-122">Используйте toocheck после окончания процесса построения hello перед запуском tooconsume рекомендации.</span><span class="sxs-lookup"><span data-stu-id="3d310-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="3d310-123">Получить рекомендации. Получите рекомендации для определенного элемента или списка элементов.</span><span class="sxs-lookup"><span data-stu-id="3d310-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="3d310-124">Все шаги hello выполняются с помощью hello API рекомендации обучения машины Azure.</span><span class="sxs-lookup"><span data-stu-id="3d310-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="3d310-125">Вы можете загрузить пример приложения, которое реализует каждое из этих действий из hello [также коллекции.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="3d310-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="3d310-126">Ограничения</span><span class="sxs-lookup"><span data-stu-id="3d310-126">Limitations</span></span>
* <span data-ttu-id="3d310-127">Hello моделей для каждой подписки не более 10.</span><span class="sxs-lookup"><span data-stu-id="3d310-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="3d310-128">Максимальное количество элементов, содержащихся в каталоге для Hello составляет 100 000.</span><span class="sxs-lookup"><span data-stu-id="3d310-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="3d310-129">Hello использования точек, которые хранятся не более 5 000 000 ~.</span><span class="sxs-lookup"><span data-stu-id="3d310-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="3d310-130">Если новые будут отправлены или отмечены Hello старые будут удалены.</span><span class="sxs-lookup"><span data-stu-id="3d310-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="3d310-131">Hello максимальный объем данных, который может быть отправлен в POST (например, импорт каталога данных, импорт данных об использовании) — 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="3d310-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="3d310-132">Hello число транзакций в секунду для построения модели рекомендаций, не активен — ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="3d310-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="3d310-133">Построение модели рекомендация активной может быть установлено too20TPS.</span><span class="sxs-lookup"><span data-stu-id="3d310-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="3d310-134">Интеграция</span><span class="sxs-lookup"><span data-stu-id="3d310-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="3d310-135">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="3d310-135">Authentication</span></span>
<span data-ttu-id="3d310-136">Microsoft Azure Marketplace поддерживает либо hello метод проверки подлинности Basic или OAuth.</span><span class="sxs-lookup"><span data-stu-id="3d310-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="3d310-137">Можно легко находить hello ключи учетной записи, перейдя по toohello ключей в marketplace hello в разделе [параметры учетной записи](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="3d310-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="3d310-138">Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="3d310-138">Basic Authentication</span></span>
<span data-ttu-id="3d310-139">Добавьте заголовок Authorization hello:</span><span class="sxs-lookup"><span data-stu-id="3d310-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="3d310-140">Преобразовать tooBase64 (C#)</span><span class="sxs-lookup"><span data-stu-id="3d310-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="3d310-141">Преобразовать tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3d310-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="3d310-142">URI службы</span><span class="sxs-lookup"><span data-stu-id="3d310-142">Service URI</span></span>
<span data-ttu-id="3d310-143">Корень службы Hello URI для hello API-интерфейсов Azure машины обучения рекомендации [здесь.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="3d310-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="3d310-144">Hello полный URI службы представляется с помощью элементов hello спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="3d310-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="3d310-145">Версия API</span><span class="sxs-lookup"><span data-stu-id="3d310-145">API version</span></span>
<span data-ttu-id="3d310-146">Каждый вызов API будет, в конце hello вызывается apiVersion, который следует задать параметр запроса слишком «1.0».</span><span class="sxs-lookup"><span data-stu-id="3d310-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="3d310-147">Учет регистра в идентификаторах</span><span class="sxs-lookup"><span data-stu-id="3d310-147">IDs are case-sensitive</span></span>
<span data-ttu-id="3d310-148">Идентификаторы, возвращенные любой hello API-интерфейсы, зависят от регистра и должен использоваться таким образом, при передаче в качестве параметров при последующих вызовах API.</span><span class="sxs-lookup"><span data-stu-id="3d310-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="3d310-149">Например, регистр учитывается в идентификаторах моделей и каталогов.</span><span class="sxs-lookup"><span data-stu-id="3d310-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="3d310-150">Создание модели</span><span class="sxs-lookup"><span data-stu-id="3d310-150">Create a model</span></span>
<span data-ttu-id="3d310-151">Создание запроса create model.</span><span class="sxs-lookup"><span data-stu-id="3d310-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="3d310-152">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-152">HTTP Method</span></span> | <span data-ttu-id="3d310-153">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-154">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="3d310-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-156">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-156">Parameter Name</span></span> | <span data-ttu-id="3d310-157">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-158">modelName</span><span class="sxs-lookup"><span data-stu-id="3d310-158">modelName</span></span> |<span data-ttu-id="3d310-159">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="3d310-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3d310-160">Максимальная длина: 20</span><span class="sxs-lookup"><span data-stu-id="3d310-160">Max length: 20</span></span> |
| <span data-ttu-id="3d310-161">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-161">apiVersion</span></span> |<span data-ttu-id="3d310-162">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-162">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-163">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-163">Request Body</span></span> |<span data-ttu-id="3d310-164">НЕТ</span><span class="sxs-lookup"><span data-stu-id="3d310-164">NONE</span></span> |

<span data-ttu-id="3d310-165">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-165">**Response**:</span></span>

<span data-ttu-id="3d310-166">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="3d310-167">`feed/entry/content/properties/id`— Содержит идентификатор hello модели.</span><span class="sxs-lookup"><span data-stu-id="3d310-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="3d310-168">Обратите внимание, что идентификатор hello модели с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="3d310-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="3d310-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="3d310-170">Импорт данных каталога</span><span class="sxs-lookup"><span data-stu-id="3d310-170">Import catalog data</span></span>
<span data-ttu-id="3d310-171">При передаче нескольких каталогов файлы toohello же модель с несколькими вызовами, будет вставлен только hello новые элементы каталога.</span><span class="sxs-lookup"><span data-stu-id="3d310-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="3d310-172">Существующие элементы останутся на основе исходных значений hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="3d310-173">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-173">HTTP Method</span></span> | <span data-ttu-id="3d310-174">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-175">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="3d310-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-177">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-177">Parameter Name</span></span> | <span data-ttu-id="3d310-178">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-179">modelId</span><span class="sxs-lookup"><span data-stu-id="3d310-179">modelId</span></span> |<span data-ttu-id="3d310-180">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-181">filename</span><span class="sxs-lookup"><span data-stu-id="3d310-181">filename</span></span> |<span data-ttu-id="3d310-182">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="3d310-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3d310-183">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="3d310-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3d310-184">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="3d310-184">Max length: 50</span></span> |
| <span data-ttu-id="3d310-185">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-185">apiVersion</span></span> |<span data-ttu-id="3d310-186">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-186">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-187">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-187">Request Body</span></span> |<span data-ttu-id="3d310-188">Данные каталога.</span><span class="sxs-lookup"><span data-stu-id="3d310-188">Catalog data.</span></span> <span data-ttu-id="3d310-189">Формат:</span><span class="sxs-lookup"><span data-stu-id="3d310-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="3d310-190">Имя</span><span class="sxs-lookup"><span data-stu-id="3d310-190">Name</span></span></th><th><span data-ttu-id="3d310-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3d310-191">Mandatory</span></span></th><th><span data-ttu-id="3d310-192">Тип</span><span class="sxs-lookup"><span data-stu-id="3d310-192">Type</span></span></th><th><span data-ttu-id="3d310-193">Описание</span><span class="sxs-lookup"><span data-stu-id="3d310-193">Description</span></span></th></tr><tr><td><span data-ttu-id="3d310-194">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="3d310-194">Item Id</span></span></td><td><span data-ttu-id="3d310-195">Да</span><span class="sxs-lookup"><span data-stu-id="3d310-195">Yes</span></span></td><td><span data-ttu-id="3d310-196">Буквенно-цифровой, максимальная длина — 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="3d310-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="3d310-197">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="3d310-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="3d310-198">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="3d310-198">Item Name</span></span></td><td><span data-ttu-id="3d310-199">Да</span><span class="sxs-lookup"><span data-stu-id="3d310-199">Yes</span></span></td><td><span data-ttu-id="3d310-200">Буквенно-цифровой, максимальная длина — 255 знаков.</span><span class="sxs-lookup"><span data-stu-id="3d310-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="3d310-201">Имя элемента.</span><span class="sxs-lookup"><span data-stu-id="3d310-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="3d310-202">Категория элемента</span><span class="sxs-lookup"><span data-stu-id="3d310-202">Item Category</span></span></td><td><span data-ttu-id="3d310-203">Да</span><span class="sxs-lookup"><span data-stu-id="3d310-203">Yes</span></span></td><td><span data-ttu-id="3d310-204">Буквенно-цифровой, максимальная длина — 255 знаков.</span><span class="sxs-lookup"><span data-stu-id="3d310-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="3d310-205">Категория toowhich, это элемент принадлежит (например, кулинарии книг, Драма...)</span><span class="sxs-lookup"><span data-stu-id="3d310-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="3d310-206">Описание</span><span class="sxs-lookup"><span data-stu-id="3d310-206">Description</span></span></td><td><span data-ttu-id="3d310-207">Нет</span><span class="sxs-lookup"><span data-stu-id="3d310-207">No</span></span></td><td><span data-ttu-id="3d310-208">Буквенно-цифровой, максимальная длина — 4000 знаков.</span><span class="sxs-lookup"><span data-stu-id="3d310-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="3d310-209">Описание элемента.</span><span class="sxs-lookup"><span data-stu-id="3d310-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="3d310-210">Максимальный размер файла равен 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="3d310-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="3d310-211">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="3d310-212">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-212">**Response**:</span></span>

<span data-ttu-id="3d310-213">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="3d310-214">`Feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="3d310-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3d310-215">`Feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.</span><span class="sxs-lookup"><span data-stu-id="3d310-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="3d310-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="3d310-217">Импорт данных об использовании</span><span class="sxs-lookup"><span data-stu-id="3d310-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="3d310-218">Отправка файла</span><span class="sxs-lookup"><span data-stu-id="3d310-218">Uploading a file</span></span>
<span data-ttu-id="3d310-219">В этом разделе показано, как данные об использовании tooupload с помощью файла.</span><span class="sxs-lookup"><span data-stu-id="3d310-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="3d310-220">Можно вызывать этот API несколько раз с данными об использовании.</span><span class="sxs-lookup"><span data-stu-id="3d310-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="3d310-221">Для всех вызовов сохранятся все данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="3d310-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="3d310-222">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-222">HTTP Method</span></span> | <span data-ttu-id="3d310-223">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-224">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="3d310-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-225">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-226">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-226">Parameter Name</span></span> | <span data-ttu-id="3d310-227">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-228">modelId</span><span class="sxs-lookup"><span data-stu-id="3d310-228">modelId</span></span> |<span data-ttu-id="3d310-229">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-230">filename</span><span class="sxs-lookup"><span data-stu-id="3d310-230">filename</span></span> |<span data-ttu-id="3d310-231">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="3d310-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3d310-232">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="3d310-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3d310-233">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="3d310-233">Max length: 50</span></span> |
| <span data-ttu-id="3d310-234">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-234">apiVersion</span></span> |<span data-ttu-id="3d310-235">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-235">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-236">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-236">Request Body</span></span> |<span data-ttu-id="3d310-237">Данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="3d310-237">Usage data.</span></span> <span data-ttu-id="3d310-238">Формат:</span><span class="sxs-lookup"><span data-stu-id="3d310-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="3d310-239">Имя</span><span class="sxs-lookup"><span data-stu-id="3d310-239">Name</span></span></th><th><span data-ttu-id="3d310-240">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3d310-240">Mandatory</span></span></th><th><span data-ttu-id="3d310-241">Тип</span><span class="sxs-lookup"><span data-stu-id="3d310-241">Type</span></span></th><th><span data-ttu-id="3d310-242">Описание</span><span class="sxs-lookup"><span data-stu-id="3d310-242">Description</span></span></th></tr><tr><td><span data-ttu-id="3d310-243">Идентификатор пользователя</span><span class="sxs-lookup"><span data-stu-id="3d310-243">User Id</span></span></td><td><span data-ttu-id="3d310-244">Да</span><span class="sxs-lookup"><span data-stu-id="3d310-244">Yes</span></span></td><td><span data-ttu-id="3d310-245">Буквенно-цифровой</span><span class="sxs-lookup"><span data-stu-id="3d310-245">Alphanumeric</span></span></td><td><span data-ttu-id="3d310-246">Уникальный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d310-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="3d310-247">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="3d310-247">Item Id</span></span></td><td><span data-ttu-id="3d310-248">Да</span><span class="sxs-lookup"><span data-stu-id="3d310-248">Yes</span></span></td><td><span data-ttu-id="3d310-249">Буквенно-цифровой, максимальная длина — 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="3d310-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="3d310-250">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="3d310-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="3d310-251">Время</span><span class="sxs-lookup"><span data-stu-id="3d310-251">Time</span></span></td><td><span data-ttu-id="3d310-252">Нет</span><span class="sxs-lookup"><span data-stu-id="3d310-252">No</span></span></td><td><span data-ttu-id="3d310-253">Дата в формате: ГГГГ/ММ/ДДТЧЧ:ММ:СС (например, 2013/06/20Т10:00:00).</span><span class="sxs-lookup"><span data-stu-id="3d310-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="3d310-254">Время данных</span><span class="sxs-lookup"><span data-stu-id="3d310-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="3d310-255">Событие</span><span class="sxs-lookup"><span data-stu-id="3d310-255">Event</span></span></td><td><span data-ttu-id="3d310-256">Нет. Если указано, необходимо также указать дату</span><span class="sxs-lookup"><span data-stu-id="3d310-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="3d310-257">Одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="3d310-257">One of hello following:</span></span><br><span data-ttu-id="3d310-258">• Click</span><span class="sxs-lookup"><span data-stu-id="3d310-258">• Click</span></span><br><span data-ttu-id="3d310-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="3d310-259">• RecommendationClick</span></span><br><span data-ttu-id="3d310-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="3d310-260">•    AddShopCart</span></span><br><span data-ttu-id="3d310-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="3d310-261">• RemoveShopCart</span></span><br><span data-ttu-id="3d310-262">• Покупка</span><span class="sxs-lookup"><span data-stu-id="3d310-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="3d310-263">Максимальный размер файла равен 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="3d310-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="3d310-264">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="3d310-265">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-265">**Response**:</span></span>

<span data-ttu-id="3d310-266">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="3d310-267">`Feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="3d310-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3d310-268">`Feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.</span><span class="sxs-lookup"><span data-stu-id="3d310-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="3d310-269">`Feed\entry\content\properties\FileId` — идентификатор файла.</span><span class="sxs-lookup"><span data-stu-id="3d310-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="3d310-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="3d310-271">Использование функции сбора данных</span><span class="sxs-lookup"><span data-stu-id="3d310-271">Using data acquisition</span></span>
<span data-ttu-id="3d310-272">В этом разделе показано, как toosend событий в реальном времени tooAzure машины обучения рекомендации, обычно с веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="3d310-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="3d310-273">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-273">HTTP Method</span></span> | <span data-ttu-id="3d310-274">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-275">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="3d310-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-276">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-276">Parameter Name</span></span> | <span data-ttu-id="3d310-277">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-278">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-278">apiVersion</span></span> |<span data-ttu-id="3d310-279">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-279">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-280">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-280">Request body</span></span> |<span data-ttu-id="3d310-281">Записи данных событий для каждого события необходимо toosend.</span><span class="sxs-lookup"><span data-stu-id="3d310-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="3d310-282">Для hello одного сеанса пользователя или браузера hello таким же Идентификатором hello SessionId поля, необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="3d310-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="3d310-283">(Пример текста события см. ниже.)</span><span class="sxs-lookup"><span data-stu-id="3d310-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="3d310-284">Пример события Click:</span><span class="sxs-lookup"><span data-stu-id="3d310-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="3d310-285">Пример события RecommendationClick:</span><span class="sxs-lookup"><span data-stu-id="3d310-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="3d310-286">Пример события AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="3d310-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="3d310-287">Пример события RemoveShopCart:</span><span class="sxs-lookup"><span data-stu-id="3d310-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="3d310-288">Пример события Purchase:</span><span class="sxs-lookup"><span data-stu-id="3d310-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="3d310-289">Пример отправки событий двух типов, Click и AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="3d310-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="3d310-290">**Ответ**. Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="3d310-291">Построение модели рекомендаций</span><span class="sxs-lookup"><span data-stu-id="3d310-291">Build a recommendation model</span></span>
| <span data-ttu-id="3d310-292">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-292">HTTP Method</span></span> | <span data-ttu-id="3d310-293">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-294">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="3d310-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-295">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-296">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-296">Parameter Name</span></span> | <span data-ttu-id="3d310-297">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-298">modelId</span><span class="sxs-lookup"><span data-stu-id="3d310-298">modelId</span></span> |<span data-ttu-id="3d310-299">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="3d310-300">userDescription</span></span> |<span data-ttu-id="3d310-301">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="3d310-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="3d310-302">Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См.</span><span class="sxs-lookup"><span data-stu-id="3d310-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="3d310-303">пример выше.</span><span class="sxs-lookup"><span data-stu-id="3d310-303">See example above.</span></span><br><span data-ttu-id="3d310-304">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="3d310-304">Max length: 50</span></span> |
| <span data-ttu-id="3d310-305">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-305">apiVersion</span></span> |<span data-ttu-id="3d310-306">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-306">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-307">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-307">Request Body</span></span> |<span data-ttu-id="3d310-308">НЕТ</span><span class="sxs-lookup"><span data-stu-id="3d310-308">NONE</span></span> |

<span data-ttu-id="3d310-309">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-309">**Response**:</span></span>

<span data-ttu-id="3d310-310">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-310">HTTP Status code: 200</span></span>

<span data-ttu-id="3d310-311">Это асинхронный интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="3d310-311">This is an asynchronous API.</span></span> <span data-ttu-id="3d310-312">В качестве ответа вы получите идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-312">You will get a build ID as a response.</span></span> <span data-ttu-id="3d310-313">tooknow после окончания сборки hello, следует вызвать API hello «Получить строит состояние из модели» и найдите этот идентификатор построения в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="3d310-314">Обратите внимание, что сборка может занять от toohours минут в зависимости от размера данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="3d310-315">Пока hello сборки завершается, не должны занимать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="3d310-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="3d310-316">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="3d310-316">Valid build status:</span></span>

* <span data-ttu-id="3d310-317">Create — модель создана;</span><span class="sxs-lookup"><span data-stu-id="3d310-317">Create – Model was created.</span></span>
* <span data-ttu-id="3d310-318">Queued — сборка модели запущена и поставлена в очередь;</span><span class="sxs-lookup"><span data-stu-id="3d310-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="3d310-319">Building — сборка модели выполняется;</span><span class="sxs-lookup"><span data-stu-id="3d310-319">Building – Model is being built.</span></span>
* <span data-ttu-id="3d310-320">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="3d310-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="3d310-321">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="3d310-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="3d310-322">Canceled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="3d310-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="3d310-323">Canceling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="3d310-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="3d310-324">Обратите внимание, hello пути не удается найти идентификатор сборки hello.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="3d310-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="3d310-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="3d310-326">Получение состояния сборки модели</span><span class="sxs-lookup"><span data-stu-id="3d310-326">Get build status of a model</span></span>
| <span data-ttu-id="3d310-327">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-327">HTTP Method</span></span> | <span data-ttu-id="3d310-328">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-329">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="3d310-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-330">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-331">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-331">Parameter Name</span></span> | <span data-ttu-id="3d310-332">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-333">modelId</span><span class="sxs-lookup"><span data-stu-id="3d310-333">modelId</span></span> |<span data-ttu-id="3d310-334">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="3d310-335">onlyLastBuild</span></span> |<span data-ttu-id="3d310-336">Указывает ли все hello tooreturn строить журнал hello модели или только состояние hello hello последнюю сборку.</span><span class="sxs-lookup"><span data-stu-id="3d310-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="3d310-337">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-337">apiVersion</span></span> |<span data-ttu-id="3d310-338">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-338">1.0</span></span> |

<span data-ttu-id="3d310-339">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-339">**Response**:</span></span>

<span data-ttu-id="3d310-340">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-340">HTTP Status code: 200</span></span>

<span data-ttu-id="3d310-341">Hello ответ включает одной записи для каждого построения.</span><span class="sxs-lookup"><span data-stu-id="3d310-341">hello response includes one entry per build.</span></span> <span data-ttu-id="3d310-342">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="3d310-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="3d310-343">`feed/entry/content/properties/UserName`— Имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="3d310-344">`feed/entry/content/properties/ModelName`— Имя модели hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="3d310-345">`feed/entry/content/properties/ModelId` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="3d310-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="3d310-346">`feed/entry/content/properties/IsDeployed`— Сборки hello развернут ли (так)</span><span class="sxs-lookup"><span data-stu-id="3d310-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="3d310-347">активная сборка).</span><span class="sxs-lookup"><span data-stu-id="3d310-347">active build).</span></span>
* <span data-ttu-id="3d310-348">`feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="3d310-349">`feed/entry/content/properties/BuildType`-Тип сборки hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="3d310-350">`feed/entry/content/properties/Status` — состояние сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="3d310-351">Может принимать одно из следующих hello: ошибка, построение, в очереди, Отмена, отменено, успех</span><span class="sxs-lookup"><span data-stu-id="3d310-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="3d310-352">`feed/entry/content/properties/StatusMessage`— Сведения о состоянии сообщения (применяется только toospecific состояния).</span><span class="sxs-lookup"><span data-stu-id="3d310-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="3d310-353">`feed/entry/content/properties/Progress` — ход выполнения сборки (%).</span><span class="sxs-lookup"><span data-stu-id="3d310-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="3d310-354">`feed/entry/content/properties/StartTime` — время начала сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="3d310-355">`feed/entry/content/properties/EndTime` — время окончания сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="3d310-356">`feed/entry/content/properties/ExecutionTime` — длительность сборки.</span><span class="sxs-lookup"><span data-stu-id="3d310-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="3d310-357">`feed/entry/content/properties/ProgressStep`— Сведения о текущей стадии hello, построение выполняется.</span><span class="sxs-lookup"><span data-stu-id="3d310-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="3d310-358">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="3d310-358">Valid build status:</span></span>

* <span data-ttu-id="3d310-359">Created — запись запроса сборки создана;</span><span class="sxs-lookup"><span data-stu-id="3d310-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="3d310-360">Queued — запрос сборки инициирован и помещен в очередь;</span><span class="sxs-lookup"><span data-stu-id="3d310-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="3d310-361">Building — сборка выполняется;</span><span class="sxs-lookup"><span data-stu-id="3d310-361">Building – Build is in process.</span></span>
* <span data-ttu-id="3d310-362">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="3d310-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="3d310-363">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="3d310-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="3d310-364">Canceled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="3d310-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="3d310-365">Canceling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="3d310-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="3d310-366">Допустимые значения типа сборки:</span><span class="sxs-lookup"><span data-stu-id="3d310-366">Valid values for build type:</span></span>

* <span data-ttu-id="3d310-367">Rank — сборка рейтинга;</span><span class="sxs-lookup"><span data-stu-id="3d310-367">Rank - Rank build.</span></span> <span data-ttu-id="3d310-368">(Сведения о построении ранг, см. toohello документа «Рекомендации обучения машины API documentation»).</span><span class="sxs-lookup"><span data-stu-id="3d310-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="3d310-369">Recommendation — сборка рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="3d310-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="3d310-370">Fbt — сборка часто покупаемых вместе элементов.</span><span class="sxs-lookup"><span data-stu-id="3d310-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="3d310-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="3d310-372">Получение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="3d310-372">Get recommendations</span></span>
| <span data-ttu-id="3d310-373">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-373">HTTP Method</span></span> | <span data-ttu-id="3d310-374">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-375">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="3d310-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-376">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-377">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-377">Parameter Name</span></span> | <span data-ttu-id="3d310-378">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-379">modelId</span><span class="sxs-lookup"><span data-stu-id="3d310-379">modelId</span></span> |<span data-ttu-id="3d310-380">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="3d310-381">itemIds</span></span> |<span data-ttu-id="3d310-382">Список разделенных запятыми hello toorecommend элементы для.</span><span class="sxs-lookup"><span data-stu-id="3d310-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="3d310-383">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="3d310-383">Max length: 1024</span></span> |
| <span data-ttu-id="3d310-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3d310-384">numberOfResults</span></span> |<span data-ttu-id="3d310-385">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="3d310-385">Number of required results</span></span> |
| <span data-ttu-id="3d310-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3d310-386">includeMetatadata</span></span> |<span data-ttu-id="3d310-387">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="3d310-387">Future use, always false</span></span> |
| <span data-ttu-id="3d310-388">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-388">apiVersion</span></span> |<span data-ttu-id="3d310-389">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-389">1.0</span></span> |

<span data-ttu-id="3d310-390">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="3d310-390">**Response:**</span></span>

<span data-ttu-id="3d310-391">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-391">HTTP Status code: 200</span></span>

<span data-ttu-id="3d310-392">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="3d310-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3d310-393">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="3d310-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="3d310-394">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="3d310-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3d310-395">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3d310-396">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="3d310-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3d310-397">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="3d310-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="3d310-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-398">OData XML</span></span>

<span data-ttu-id="3d310-399">Пример ответа Hello ниже включает 10 рекомендуемые элементы:</span><span class="sxs-lookup"><span data-stu-id="3d310-399">hello example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="3d310-400">Обновление модели</span><span class="sxs-lookup"><span data-stu-id="3d310-400">Update model</span></span>
<span data-ttu-id="3d310-401">Вы можете обновить описание модели hello или hello идентификатором активного построения.</span><span class="sxs-lookup"><span data-stu-id="3d310-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="3d310-402">*Активный идентификатор сборки* — каждая сборка каждой модели имеет собственный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="3d310-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="3d310-403">Идентификатор построения active Hello является первой успешной сборки hello всех новых моделей.</span><span class="sxs-lookup"><span data-stu-id="3d310-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="3d310-404">После иметь идентификатор активного построения и выполнить дополнительные сборки для hello одной модели необходимо tooexplicitly задать его значение как hello по умолчанию идентификатор сборки, если требуется.</span><span class="sxs-lookup"><span data-stu-id="3d310-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="3d310-405">После получения рекомендаций, если не указан идентификатор сборки hello нужного toouse, по умолчанию hello один будет использоваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="3d310-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="3d310-406">Этот механизм позволяет - после модели рекомендаций в производственной среде - toobuild новых моделей и проверить их, прежде чем продвинуть их tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3d310-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="3d310-407">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="3d310-407">HTTP Method</span></span> | <span data-ttu-id="3d310-408">URI</span><span class="sxs-lookup"><span data-stu-id="3d310-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-409">ОТПРАВКА</span><span class="sxs-lookup"><span data-stu-id="3d310-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3d310-410">Пример:</span><span class="sxs-lookup"><span data-stu-id="3d310-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3d310-411">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="3d310-411">Parameter Name</span></span> | <span data-ttu-id="3d310-412">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3d310-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d310-413">id</span><span class="sxs-lookup"><span data-stu-id="3d310-413">id</span></span> |<span data-ttu-id="3d310-414">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="3d310-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="3d310-415">версия_API</span><span class="sxs-lookup"><span data-stu-id="3d310-415">apiVersion</span></span> |<span data-ttu-id="3d310-416">1.0</span><span class="sxs-lookup"><span data-stu-id="3d310-416">1.0</span></span> |
|  | |
| <span data-ttu-id="3d310-417">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="3d310-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="3d310-418">Обратите внимание, что hello XML теги описание ActiveBuildId являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="3d310-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="3d310-419">Если вы не хотите tooset описание или ActiveBuildId, удалите весь тег hello.</span><span class="sxs-lookup"><span data-stu-id="3d310-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="3d310-420">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="3d310-420">**Response**:</span></span>

<span data-ttu-id="3d310-421">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="3d310-421">HTTP Status code: 200</span></span>

<span data-ttu-id="3d310-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="3d310-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="3d310-423">Юридическая информация</span><span class="sxs-lookup"><span data-stu-id="3d310-423">Legal</span></span>
<span data-ttu-id="3d310-424">Данный документ предоставляется «как есть».</span><span class="sxs-lookup"><span data-stu-id="3d310-424">This document is provided "as-is".</span></span> <span data-ttu-id="3d310-425">Сведения и мнения, представленные в данном документе, включая URL-адреса и ссылки на другие веб-сайты, могут быть изменены без предварительного уведомления.</span><span class="sxs-lookup"><span data-stu-id="3d310-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="3d310-426">Некоторые примеры, содержащиеся в данном документе, являются вымышленными и приводятся исключительно в демонстрационных целях.</span><span class="sxs-lookup"><span data-stu-id="3d310-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="3d310-427">Любое сходство с реальными ситуациями случайно.</span><span class="sxs-lookup"><span data-stu-id="3d310-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="3d310-428">Этот документ не предоставляет никаких законных прав интеллектуальной собственности tooany в продуктах корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3d310-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="3d310-429">Вы можете скопировать и использовать данный документ для внутренних справочных целей.</span><span class="sxs-lookup"><span data-stu-id="3d310-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="3d310-430">© Корпорация Майкрософт, 2014.</span><span class="sxs-lookup"><span data-stu-id="3d310-430">© 2014 Microsoft.</span></span> <span data-ttu-id="3d310-431">Все права защищены.</span><span class="sxs-lookup"><span data-stu-id="3d310-431">All rights reserved.</span></span> 

