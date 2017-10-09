---
title: "aaaMachine обучения рекомендации документации по API | Документы Microsoft"
description: "API рекомендации обучения машины документации по Azure для рекомендаций подсистемы, доступные в Microsoft Azure Marketplace hello."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="f2215-103">Машинное обучение Azure: документация по интерфейсу API рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="f2215-104">Необходимо запустить с помощью службы Когнитивных рекомендации API hello вместо этой версии.</span><span class="sxs-lookup"><span data-stu-id="f2215-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="f2215-105">Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует.</span><span class="sxs-lookup"><span data-stu-id="f2215-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="f2215-106">Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="f2215-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="f2215-107">Дополнительные сведения о [toohello перенос новой Когнитивных службы](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="f2215-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="f2215-108">В этом документе описываются интерфейсы API рекомендаций по Машинному обучению Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2215-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="f2215-109">1. Общая информация</span><span class="sxs-lookup"><span data-stu-id="f2215-109">1. General overview</span></span>
<span data-ttu-id="f2215-110">Данный документ содержит справочные материалы по интерфейсам API.</span><span class="sxs-lookup"><span data-stu-id="f2215-110">This document is an API reference.</span></span> <span data-ttu-id="f2215-111">Рекомендуется начать с документом «Azure рекомендация — быстрый запуск машинного обучения» hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="f2215-112">Hello Azure машины обучения рекомендации API можно разделить на следующие логические группы hello:</span><span class="sxs-lookup"><span data-stu-id="f2215-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="f2215-113"><ins>ограничения</ins> — ограничения API рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="f2215-114"><ins>общая информация</ins> — сведения об аутентификации, универсальном коде ресурса (URI) службы и управлении версиями.</span><span class="sxs-lookup"><span data-stu-id="f2215-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="f2215-115"><ins>Модели Basic</ins> -API, которые позволяют toodo hello основных операций модели (например создание, обновление и удаление модели).</span><span class="sxs-lookup"><span data-stu-id="f2215-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="f2215-116"><ins>Модели Дополнительно</ins> -API, которые позволяют tooget advanced анализу данных на модель hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="f2215-117"><ins>Модели бизнес-правила</ins> -API, которые позволяют бизнес-правила toomanage hello модели рекомендаций результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="f2215-118"><ins>Каталог</ins> -API, которые позволяют toodo основных операций для каталога модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="f2215-119">Каталог содержит метаданные для элементов данных об использовании hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="f2215-120"><ins>Функция</ins> -интерфейсы API, позволяющие tooget аналитики на элемент в каталог hello и как toouse этой информации toobuild рекомендации более полезными.</span><span class="sxs-lookup"><span data-stu-id="f2215-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="f2215-121"><ins>Данные об использовании</ins> -API, которые позволяют toodo основные операции с данными об использовании модели hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="f2215-122">Данные об использовании в базовой форме hello состоит из строки, содержащие пары &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="f2215-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="f2215-123"><ins>Построение</ins> - API-интерфейсы, позволяющие tootrigger модели построение и выполнение основных операций, связанных toothis сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="f2215-124">Инициировать сборку модели можно, получив значимые данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="f2215-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="f2215-125"><ins>Рекомендация</ins> -интерфейсы API, позволяющие tooconsume рекомендации после завершения построения hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="f2215-126"><ins>Данные пользователя</ins> -API, которые позволяют toofetch сведения о данных об использовании hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="f2215-127"><ins>Уведомления о</ins> -tooyour API-операции, связанные с API-интерфейсы, обеспечивающие tooreceive уведомления о проблемах.</span><span class="sxs-lookup"><span data-stu-id="f2215-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="f2215-128">(Например, вы сообщаете использование данных с помощью получения данных и большинство hello событий ошибки обработки при выполнении.</span><span class="sxs-lookup"><span data-stu-id="f2215-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="f2215-129">то вызывается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f2215-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="f2215-130">2) Ограничения</span><span class="sxs-lookup"><span data-stu-id="f2215-130">2. Limitations</span></span>
* <span data-ttu-id="f2215-131">Hello моделей для каждой подписки не более 10.</span><span class="sxs-lookup"><span data-stu-id="f2215-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="f2215-132">Hello максимальное количество сборок на модели — 20.</span><span class="sxs-lookup"><span data-stu-id="f2215-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="f2215-133">Максимальное количество элементов, содержащихся в каталоге для Hello составляет 100 000.</span><span class="sxs-lookup"><span data-stu-id="f2215-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="f2215-134">Hello использования точек, которые хранятся не более 5 000 000 ~.</span><span class="sxs-lookup"><span data-stu-id="f2215-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="f2215-135">Если новые будут отправлены или отмечены Hello старые будут удалены.</span><span class="sxs-lookup"><span data-stu-id="f2215-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="f2215-136">Hello максимальный объем данных, которые могут отправляться в POST (например импорта каталога данных, импорт данных об использовании) — 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="f2215-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="f2215-137">Максимальное количество элементов, которые можно указать при получении рекомендации Hello — 150.</span><span class="sxs-lookup"><span data-stu-id="f2215-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="f2215-138">3. Интерфейсы API: общие сведения</span><span class="sxs-lookup"><span data-stu-id="f2215-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="f2215-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-139">3.1.</span></span> <span data-ttu-id="f2215-140">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="f2215-140">Authentication</span></span>
<span data-ttu-id="f2215-141">Следуйте правилам hello Microsoft Azure Marketplace, связанные с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="f2215-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="f2215-142">Hello marketplace поддерживает метод проверки подлинности Basic или OAuth либо hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="f2215-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-143">3.2.</span></span> <span data-ttu-id="f2215-144">URI службы</span><span class="sxs-lookup"><span data-stu-id="f2215-144">Service URI</span></span>
<span data-ttu-id="f2215-145">Корень службы Hello URI для hello API-интерфейсов Azure машины обучения рекомендации [здесь.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="f2215-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="f2215-146">Hello полный URI службы представляется с помощью элементов hello спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="f2215-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="f2215-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-147">3.3.</span></span> <span data-ttu-id="f2215-148">Версия API</span><span class="sxs-lookup"><span data-stu-id="f2215-148">API version</span></span>
<span data-ttu-id="f2215-149">Каждый вызов API будет, в конце hello параметр запроса с именем apiVersion, который следует задать too1.0.</span><span class="sxs-lookup"><span data-stu-id="f2215-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="f2215-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-150">3.4.</span></span> <span data-ttu-id="f2215-151">Идентификаторы с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="f2215-151">IDs are case sensitive</span></span>
<span data-ttu-id="f2215-152">Идентификаторы, возвращенные любой hello API-интерфейсы, чувствительны к регистру и должны использоваться таким образом, при передаче в качестве параметров при последующих вызовах API.</span><span class="sxs-lookup"><span data-stu-id="f2215-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="f2215-153">Например, регистр учитывается в идентификаторах моделей и каталогов.</span><span class="sxs-lookup"><span data-stu-id="f2215-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="f2215-154">4. Качество рекомендаций и неактивные элементы</span><span class="sxs-lookup"><span data-stu-id="f2215-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="f2215-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-155">4.1.</span></span> <span data-ttu-id="f2215-156">Качество рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-156">Recommendation quality</span></span>
<span data-ttu-id="f2215-157">Создание модели рекомендаций обычно является достаточно tooallow hello системные tooprovide рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="f2215-158">Тем не менее качество рекомендаций варьируется в зависимости от использования hello обработки и hello покрытия hello каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="f2215-159">Например, если у вас есть много новых элементов (элементов без значительных использования), система hello будет иметь трудностей предоставление рекомендаций для такого элемента или с помощью такого элемента как рекомендуемые.</span><span class="sxs-lookup"><span data-stu-id="f2215-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="f2215-160">В порядке tooovercome hello холодного элемента проблему hello системы позволяет использовать hello метаданных hello элементы tooenhance hello рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="f2215-161">Эти метаданные являются tooas соответствующей функции.</span><span class="sxs-lookup"><span data-stu-id="f2215-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="f2215-162">Примерами характеристик могут служить имена автора книги или актера фильма.</span><span class="sxs-lookup"><span data-stu-id="f2215-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="f2215-163">Функции предоставляются через каталог hello в виде hello ключ значение.</span><span class="sxs-lookup"><span data-stu-id="f2215-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="f2215-164">Hello полный формат файла каталога hello, можно найти toohello [импорта раздел каталога](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="f2215-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="f2215-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-165">4.2.</span></span> <span data-ttu-id="f2215-166">Сборка рейтинга</span><span class="sxs-lookup"><span data-stu-id="f2215-166">Rank build</span></span>
<span data-ttu-id="f2215-167">Возможности могут улучшить модель рекомендаций hello, однако toodo требуются hello использование значимых функций.</span><span class="sxs-lookup"><span data-stu-id="f2215-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="f2215-168">В этих целях была введена новая сборка — сборка рейтинга.</span><span class="sxs-lookup"><span data-stu-id="f2215-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="f2215-169">Эта сборка будет ранжирования полезность функции hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="f2215-170">Значимая характеристика имеет рейтинг не ниже 2.</span><span class="sxs-lookup"><span data-stu-id="f2215-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="f2215-171">Поняв, какие из функций hello важны, запустите сборку рекомендация список hello (или подсписок) значимых функций.</span><span class="sxs-lookup"><span data-stu-id="f2215-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="f2215-172">Это возможно toouse, эти функции для расширения hello горячего элементов и новых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="f2215-173">В порядке toouse их для горячего элементов hello `UseFeatureInModel` параметр сборки должны быть настроены.</span><span class="sxs-lookup"><span data-stu-id="f2215-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="f2215-174">В функции toouse заказа для новых элементов, hello `AllowColdItemPlacement` параметр сборки должен быть включен.</span><span class="sxs-lookup"><span data-stu-id="f2215-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="f2215-175">Примечание: Это не возможные tooenable `AllowColdItemPlacement` без включения `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="f2215-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="f2215-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-176">4.3.</span></span> <span data-ttu-id="f2215-177">Обоснование рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-177">Recommendation reasoning</span></span>
<span data-ttu-id="f2215-178">Обоснование рекомендаций — еще один аспект использования характеристик.</span><span class="sxs-lookup"><span data-stu-id="f2215-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="f2215-179">На самом деле engine hello Azure Machine Learning рекомендации можно использовать функции tooprovide рекомендация объяснения (так называемый</span><span class="sxs-lookup"><span data-stu-id="f2215-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="f2215-180">рассуждения) начальные toomore достоверности в hello рекомендуется элемента от потребителя рекомендация hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="f2215-181">tooenable рассуждения, hello `AllowFeatureCorrelation` и `ReasoningFeatureList` параметры должны быть toorequesting предыдущей установки сборки рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="f2215-182">5. Базовая обработка модели</span><span class="sxs-lookup"><span data-stu-id="f2215-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="f2215-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-183">5.1.</span></span> <span data-ttu-id="f2215-184">Создание модели</span><span class="sxs-lookup"><span data-stu-id="f2215-184">Create Model</span></span>
<span data-ttu-id="f2215-185">Создает запрос на создание модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="f2215-186">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-186">HTTP Method</span></span> | <span data-ttu-id="f2215-187">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-188">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-189">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-190">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-190">Parameter Name</span></span> | <span data-ttu-id="f2215-191">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-192">modelName</span><span class="sxs-lookup"><span data-stu-id="f2215-192">modelName</span></span> |<span data-ttu-id="f2215-193">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="f2215-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f2215-194">Максимальная длина: 20</span><span class="sxs-lookup"><span data-stu-id="f2215-194">Max length: 20</span></span> |
| <span data-ttu-id="f2215-195">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-195">apiVersion</span></span> |<span data-ttu-id="f2215-196">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-196">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-197">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-197">Request Body</span></span> |<span data-ttu-id="f2215-198">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-198">NONE</span></span> |

<span data-ttu-id="f2215-199">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-199">**Response**:</span></span>

<span data-ttu-id="f2215-200">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="f2215-201">`feed/entry/content/properties/id`— Содержит идентификатор hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="f2215-202">**Примечание**. В идентификаторе модели учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="f2215-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="f2215-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="f2215-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-204">5.2.</span></span> <span data-ttu-id="f2215-205">Получение модели</span><span class="sxs-lookup"><span data-stu-id="f2215-205">Get Model</span></span>
<span data-ttu-id="f2215-206">Создает запрос на получение модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="f2215-207">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-207">HTTP Method</span></span> | <span data-ttu-id="f2215-208">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-209">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-210">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-211">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-211">Parameter Name</span></span> | <span data-ttu-id="f2215-212">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-213">id</span><span class="sxs-lookup"><span data-stu-id="f2215-213">id</span></span> |<span data-ttu-id="f2215-214">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="f2215-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="f2215-215">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-215">apiVersion</span></span> |<span data-ttu-id="f2215-216">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-216">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-217">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-217">Request Body</span></span> |<span data-ttu-id="f2215-218">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-218">NONE</span></span> |

<span data-ttu-id="f2215-219">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-219">**Response**:</span></span>

<span data-ttu-id="f2215-220">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-220">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-221">Hello модели данных можно найти в hello следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="f2215-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="f2215-222">`feed/entry/content/properties/Id` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="f2215-223">`feed/entry/content/properties/Name` — имя модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="f2215-224">`feed/entry/content/properties/Date` — дата создания модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="f2215-225">`feed/entry/content/properties/Status` — состояние модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="f2215-226">Одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="f2215-226">One of hello following:</span></span>
  * <span data-ttu-id="f2215-227">Created — модель создана и не содержит каталога и данных по использованию;</span><span class="sxs-lookup"><span data-stu-id="f2215-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="f2215-228">ReadyForBuild — модель создана и содержит каталог и данные по использованию.</span><span class="sxs-lookup"><span data-stu-id="f2215-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="f2215-229">`feed/entry/content/properties/HasActiveBuild`— Указывает, если модель hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="f2215-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="f2215-230">`feed/entry/content/properties/BuildId` — идентификатор активной сборки модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="f2215-231">`feed/entry/content/properties/Mpr` — средний процентильный рейтинг модели (MPR, подробнее см. в разделе, посвященном параметру ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="f2215-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="f2215-232">`feed/entry/content/properties/UserName` — имя внутреннего пользователя модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="f2215-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="f2215-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-234">5.3.</span></span>    <span data-ttu-id="f2215-235">Получение всех моделей</span><span class="sxs-lookup"><span data-stu-id="f2215-235">Get All Models</span></span>
<span data-ttu-id="f2215-236">Извлекает все модели hello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="f2215-237">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-237">HTTP Method</span></span> | <span data-ttu-id="f2215-238">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-239">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="f2215-240">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-241">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-241">Parameter Name</span></span> | <span data-ttu-id="f2215-242">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-243">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-243">apiVersion</span></span> |<span data-ttu-id="f2215-244">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-244">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-245">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-245">Request Body</span></span> |<span data-ttu-id="f2215-246">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-246">NONE</span></span> |

<span data-ttu-id="f2215-247">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-247">**Response**:</span></span>

<span data-ttu-id="f2215-248">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="f2215-249">`feed/entry/content/properties/Id` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="f2215-250">`feed/entry/content/properties/Name` — имя модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="f2215-251">`feed/entry/content/properties/Date` — дата создания модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="f2215-252">`feed/entry/content/properties/Status` — состояние модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="f2215-253">Одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="f2215-253">One of hello following:</span></span>
  * <span data-ttu-id="f2215-254">Created — модель создана и не содержит каталога и данных по использованию;</span><span class="sxs-lookup"><span data-stu-id="f2215-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="f2215-255">ReadyForBuild — модель создана и содержит каталог и данные по использованию.</span><span class="sxs-lookup"><span data-stu-id="f2215-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="f2215-256">`feed/entry/content/properties/HasActiveBuild`— Указывает, если модель hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="f2215-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="f2215-257">`feed/entry/content/properties/BuildId` — идентификатор активной сборки модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="f2215-258">`feed/entry/content/properties/Mpr` — средний процентильный рейтинг модели (подробнее см. в разделе, посвященном параметру ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="f2215-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="f2215-259">`feed/entry/content/properties/UserName` — имя внутреннего пользователя модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="f2215-260">`feed/entry/content/properties/UsageFileNames` — список файлов использования модели через запятую.</span><span class="sxs-lookup"><span data-stu-id="f2215-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="f2215-261">`feed/entry/content/properties/CatalogId` — идентификатор каталога модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="f2215-262">`feed/entry/content/properties/Description` — описание модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="f2215-263">`feed/entry/content/properties/CatalogFileName` — имя файла каталога модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="f2215-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="f2215-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-265">5.4.</span></span>    <span data-ttu-id="f2215-266">Обновление модели</span><span class="sxs-lookup"><span data-stu-id="f2215-266">Update Model</span></span>
<span data-ttu-id="f2215-267">Вы можете обновить описание модели hello или hello идентификатором активного построения.</span><span class="sxs-lookup"><span data-stu-id="f2215-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="f2215-268">
<ins>Активный идентификатор сборки</ins> — каждая сборка каждой модели имеет собственный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f2215-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="f2215-269">Идентификатор построения active Hello является первой успешной сборки hello всех новых моделей.</span><span class="sxs-lookup"><span data-stu-id="f2215-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="f2215-270">После иметь идентификатор активного построения и выполнить дополнительные сборки для hello одной модели необходимо tooexplicitly задать его значение как hello по умолчанию идентификатор сборки, если требуется.</span><span class="sxs-lookup"><span data-stu-id="f2215-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="f2215-271">После получения рекомендаций, если не указан идентификатор сборки hello нужного toouse, по умолчанию hello один будет использоваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="f2215-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="f2215-272">Этот механизм позволяет - после модели рекомендаций в производственной среде - toobuild новых моделей и проверить их, прежде чем продвинуть их tooproduction.</span><span class="sxs-lookup"><span data-stu-id="f2215-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="f2215-273">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-273">HTTP Method</span></span> | <span data-ttu-id="f2215-274">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-275">ОТПРАВКА</span><span class="sxs-lookup"><span data-stu-id="f2215-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-276">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-277">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-277">Parameter Name</span></span> | <span data-ttu-id="f2215-278">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-279">id</span><span class="sxs-lookup"><span data-stu-id="f2215-279">id</span></span> |<span data-ttu-id="f2215-280">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="f2215-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="f2215-281">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-281">apiVersion</span></span> |<span data-ttu-id="f2215-282">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-282">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-283">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="f2215-284">Обратите внимание, что hello XML теги описание ActiveBuildId являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="f2215-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="f2215-285">Если вы не хотите tooset описание или ActiveBuildId, удалите весь тег hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="f2215-286">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-286">**Response**:</span></span>

<span data-ttu-id="f2215-287">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="f2215-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="f2215-288">5.5.</span></span>    <span data-ttu-id="f2215-289">Удаление модели</span><span class="sxs-lookup"><span data-stu-id="f2215-289">Delete Model</span></span>
<span data-ttu-id="f2215-290">Удаляет существующую модель по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="f2215-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="f2215-291">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-291">HTTP Method</span></span> | <span data-ttu-id="f2215-292">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-293">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-294">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-295">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-295">Parameter Name</span></span> | <span data-ttu-id="f2215-296">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-297">id</span><span class="sxs-lookup"><span data-stu-id="f2215-297">id</span></span> |<span data-ttu-id="f2215-298">Уникальный идентификатор hello модели (с учетом регистра)</span><span class="sxs-lookup"><span data-stu-id="f2215-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="f2215-299">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-299">apiVersion</span></span> |<span data-ttu-id="f2215-300">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-300">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-301">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-301">Request Body</span></span> |<span data-ttu-id="f2215-302">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-302">NONE</span></span> |

<span data-ttu-id="f2215-303">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-303">**Response**:</span></span>

<span data-ttu-id="f2215-304">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-304">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="f2215-306">6. Расширенная обработка модели</span><span class="sxs-lookup"><span data-stu-id="f2215-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="f2215-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-307">6.1.</span></span>    <span data-ttu-id="f2215-308">Подробные сведения о данных модели</span><span class="sxs-lookup"><span data-stu-id="f2215-308">Model Data Insight</span></span>
<span data-ttu-id="f2215-309">Возвращает статистические данные о данных об использовании hello, эта модель создавалась с.</span><span class="sxs-lookup"><span data-stu-id="f2215-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="f2215-310">Доступно только для сборки рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="f2215-311">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-311">HTTP Method</span></span> | <span data-ttu-id="f2215-312">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-313">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-314">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-315">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-315">Parameter Name</span></span> | <span data-ttu-id="f2215-316">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-317">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-317">modelId</span></span> |<span data-ttu-id="f2215-318">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-319">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-319">apiVersion</span></span> |<span data-ttu-id="f2215-320">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-320">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-321">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-321">Request Body</span></span> |<span data-ttu-id="f2215-322">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-322">NONE</span></span> |

<span data-ttu-id="f2215-323">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-323">**Response**:</span></span>

<span data-ttu-id="f2215-324">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-324">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-325">Hello данные возвращаются в виде коллекции свойств.</span><span class="sxs-lookup"><span data-stu-id="f2215-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="f2215-326">`feed/entry/id/content/properties/key`-Содержит имя свойства hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="f2215-327">`feed/entry/id/content/properties/value`-Содержит значение свойства hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="f2215-328">в следующей таблице Hello описывается hello значение, представляющее каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="f2215-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="f2215-329">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-329">Key</span></span> | <span data-ttu-id="f2215-330">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="f2215-331">AvgItemLength</span></span> |<span data-ttu-id="f2215-332">Среднее число отдельных пользователей на элемент.</span><span class="sxs-lookup"><span data-stu-id="f2215-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="f2215-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="f2215-333">AvgUserLength</span></span> |<span data-ttu-id="f2215-334">Среднее число отдельных элементов на пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="f2215-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="f2215-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="f2215-336">Количество элементов после удаления элементов, которые нельзя смоделировать.</span><span class="sxs-lookup"><span data-stu-id="f2215-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="f2215-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="f2215-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="f2215-338">Количество точек использования после удаления пользователей и элементов, которые нельзя смоделировать.</span><span class="sxs-lookup"><span data-stu-id="f2215-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="f2215-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="f2215-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="f2215-340">Количество точек использования после удаления пользователей и элементов, которые нельзя смоделировать.</span><span class="sxs-lookup"><span data-stu-id="f2215-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="f2215-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="f2215-341">MaxItemLength</span></span> |<span data-ttu-id="f2215-342">Количество уникальных пользователей для наиболее популярных элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="f2215-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="f2215-343">MaxUserLength</span></span> |<span data-ttu-id="f2215-344">Максимальное число отдельных элементов для пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="f2215-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="f2215-345">MinItemLength</span></span> |<span data-ttu-id="f2215-346">Максимальное число отдельных пользователей для элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="f2215-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="f2215-347">MinUserLength</span></span> |<span data-ttu-id="f2215-348">Минимальное число отдельных элементов для пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="f2215-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="f2215-349">RawNumberOfItems</span></span> |<span data-ttu-id="f2215-350">Число элементов в файлах использования hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="f2215-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="f2215-351">RawNumberOfUsers</span></span> |<span data-ttu-id="f2215-352">Количество точек использования перед любыми операциями удаления.</span><span class="sxs-lookup"><span data-stu-id="f2215-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="f2215-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="f2215-353">RawNumberOfRecords</span></span> |<span data-ttu-id="f2215-354">Количество точек использования перед любыми операциями удаления.</span><span class="sxs-lookup"><span data-stu-id="f2215-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="f2215-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="f2215-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="f2215-356">Недоступно</span><span class="sxs-lookup"><span data-stu-id="f2215-356">N/A</span></span> |
| <span data-ttu-id="f2215-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="f2215-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="f2215-358">Недоступно</span><span class="sxs-lookup"><span data-stu-id="f2215-358">N/A</span></span> |
| <span data-ttu-id="f2215-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="f2215-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="f2215-360">Недоступно</span><span class="sxs-lookup"><span data-stu-id="f2215-360">N/A</span></span> |

<span data-ttu-id="f2215-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="f2215-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-362">6.2.</span></span>    <span data-ttu-id="f2215-363">Подробные сведения о модели</span><span class="sxs-lookup"><span data-stu-id="f2215-363">Model Insight</span></span>
<span data-ttu-id="f2215-364">Возвращает модель, представление в hello active сборки или (если есть) на конкретную сборку.</span><span class="sxs-lookup"><span data-stu-id="f2215-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="f2215-365">Доступно только для сборки рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="f2215-366">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-366">HTTP Method</span></span> | <span data-ttu-id="f2215-367">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-368">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-368">GET</span></span> |<span data-ttu-id="f2215-369">С активным идентификатором сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-370">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-371">С конкретным идентификатором сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-372">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-372">Parameter Name</span></span> | <span data-ttu-id="f2215-373">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-374">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-374">modelId</span></span> |<span data-ttu-id="f2215-375">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-376">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-376">buildId</span></span> |<span data-ttu-id="f2215-377">Необязательно — число, которое обозначает успешную сборку.</span><span class="sxs-lookup"><span data-stu-id="f2215-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="f2215-378">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-378">apiVersion</span></span> |<span data-ttu-id="f2215-379">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-379">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-380">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-380">Request Body</span></span> |<span data-ttu-id="f2215-381">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-381">NONE</span></span> |

<span data-ttu-id="f2215-382">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-382">**Response**:</span></span>

<span data-ttu-id="f2215-383">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-383">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-384">Hello данные возвращаются в виде коллекции свойств.</span><span class="sxs-lookup"><span data-stu-id="f2215-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="f2215-385">в следующей таблице Hello описывается hello значение, представляющее каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="f2215-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="f2215-386">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-386">Key</span></span> | <span data-ttu-id="f2215-387">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="f2215-388">CatalogCoverage</span></span> |<span data-ttu-id="f2215-389">Какая часть hello каталога можно конфигураторе с шаблонами использования.</span><span class="sxs-lookup"><span data-stu-id="f2215-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="f2215-390">остальные элементы hello Hello потребуется функции на основе содержимого.</span><span class="sxs-lookup"><span data-stu-id="f2215-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="f2215-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="f2215-391">Mpr</span></span> |<span data-ttu-id="f2215-392">Ранжирование среднее процентиля hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="f2215-393">Чем меньше это значение, тем лучше.</span><span class="sxs-lookup"><span data-stu-id="f2215-393">Lower is better.</span></span> |
| <span data-ttu-id="f2215-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="f2215-394">NumberOfDimensions</span></span> |<span data-ttu-id="f2215-395">Число измерений, используемых алгоритмом разложение hello матрицы.</span><span class="sxs-lookup"><span data-stu-id="f2215-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="f2215-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="f2215-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-397">6.3.</span></span>    <span data-ttu-id="f2215-398">Получение образца модели</span><span class="sxs-lookup"><span data-stu-id="f2215-398">Get Model Sample</span></span>
<span data-ttu-id="f2215-399">Получает образец hello модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="f2215-400">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-400">HTTP Method</span></span> | <span data-ttu-id="f2215-401">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-402">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-403">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-404">С конкретным идентификатором сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-405">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-406">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-406">Parameter Name</span></span> | <span data-ttu-id="f2215-407">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-408">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-408">modelId</span></span> |<span data-ttu-id="f2215-409">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-410">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-410">apiVersion</span></span> |<span data-ttu-id="f2215-411">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-411">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-412">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-412">Request Body</span></span> |<span data-ttu-id="f2215-413">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-413">NONE</span></span> |

<span data-ttu-id="f2215-414">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-414">**Response**:</span></span>

<span data-ttu-id="f2215-415">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-415">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-416">OData XML</span></span>

<span data-ttu-id="f2215-417">Ответ возвращается в формате необработанного текста.</span><span class="sxs-lookup"><span data-stu-id="f2215-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="f2215-418">7. Бизнес-правила модели</span><span class="sxs-lookup"><span data-stu-id="f2215-418">7. Model Business Rules</span></span>
<span data-ttu-id="f2215-419">Эти типы hello поддерживается правил являются:</span><span class="sxs-lookup"><span data-stu-id="f2215-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="f2215-420"><strong>Блокировки</strong> -блокировки позволяет tooprovide список элементы, которые не должны tooreturn в результатах рекомендация hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="f2215-421"><strong>FeatureBlockList</strong> -функция блокировки позволяет вам tooblock элементов на основе значения hello его компонентов.</span><span class="sxs-lookup"><span data-stu-id="f2215-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="f2215-422">*Не добавляйте в один список блокировок больше 1000 позиций, иначе время ожидания вызова будет превышено. Если вам требуется tooblock более 1000 элементов, можно сделать несколько вызовов блокировки.*</span><span class="sxs-lookup"><span data-stu-id="f2215-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="f2215-423"><strong>Upsale</strong> -Upsale позволяет tooenforce tooreturn элементы в результатах рекомендация hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="f2215-424"><strong>Белый список</strong> -белый список включает tooonly можно предложить рекомендаций из списка элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="f2215-425"><strong>FeatureWhiteList</strong> -белый список функций включает tooonly рекомендуется элементы, имеющие значения определенного компонента.</span><span class="sxs-lookup"><span data-stu-id="f2215-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="f2215-426"><strong>PerSeedBlockList</strong> — в список блокировок начальное значение включает tooprovide каждого элемента в список элементов, которые не возвращены в качестве рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="f2215-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-427">7.1.</span></span>    <span data-ttu-id="f2215-428">Получение правил для модели</span><span class="sxs-lookup"><span data-stu-id="f2215-428">Get Model Rules</span></span>
| <span data-ttu-id="f2215-429">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-429">HTTP Method</span></span> | <span data-ttu-id="f2215-430">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-431">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="f2215-432">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-433">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-433">Parameter Name</span></span> | <span data-ttu-id="f2215-434">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-435">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-435">modelId</span></span> |<span data-ttu-id="f2215-436">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-437">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-437">apiVersion</span></span> |<span data-ttu-id="f2215-438">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-438">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-439">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-439">Request Body</span></span> |<span data-ttu-id="f2215-440">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-440">NONE</span></span> |

<span data-ttu-id="f2215-441">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-441">**Response**:</span></span>

<span data-ttu-id="f2215-442">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="f2215-443">`feed/entry/content/properties/Id` — уникальный идентификатор правила.</span><span class="sxs-lookup"><span data-stu-id="f2215-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="f2215-444">`feed/entry/content/properties/Type`-Тип правила hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="f2215-445">`feed/entry/content/properties/Parameter` — параметр правила.</span><span class="sxs-lookup"><span data-stu-id="f2215-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="f2215-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="f2215-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-447">7.2.</span></span>    <span data-ttu-id="f2215-448">Добавление правила</span><span class="sxs-lookup"><span data-stu-id="f2215-448">Add Rule</span></span>
| <span data-ttu-id="f2215-449">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-449">HTTP Method</span></span> | <span data-ttu-id="f2215-450">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-451">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="f2215-452">ЗАГОЛОВОК</span><span class="sxs-lookup"><span data-stu-id="f2215-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="f2215-453">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-453">Parameter Name</span></span> | <span data-ttu-id="f2215-454">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-455">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-455">apiVersion</span></span> |<span data-ttu-id="f2215-456">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-456">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-457">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-457">Request Body</span></span> | |

<span data-ttu-id="f2215-458"><ins>Всякий раз предоставления идентификаторы элементов для бизнес-правил, убедитесь, что toouse hello внешний идентификатор элемента hello (hello таким же идентификатором, который использовался в файл каталога hello)</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="f2215-459">
<ins>tooadd правило блокировки:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="f2215-460"><ins>
<ins>tooadd FeatureBlockList правила:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="f2215-461"><ins>tooadd правило Upsale:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="f2215-462">
<ins>tooadd правила белого списка:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="f2215-463"><ins>
<ins>tooadd FeatureWhiteList правила:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="f2215-464"><ins>tooadd PerSeedBlockList правила:</ins></span><span class="sxs-lookup"><span data-stu-id="f2215-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="f2215-465">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-465">**Response**:</span></span>

<span data-ttu-id="f2215-466">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-466">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-467">Hello API возвращает hello вновь созданные правила с сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="f2215-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="f2215-468">Свойство правила Hello можно получить из hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="f2215-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="f2215-469">`feed/entry/content/properties/Id` — уникальный идентификатор правила.</span><span class="sxs-lookup"><span data-stu-id="f2215-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="f2215-470">`feed/entry/content/properties/Type`-Тип правила hello: блокировки или Upsale.</span><span class="sxs-lookup"><span data-stu-id="f2215-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="f2215-471">`feed/entry/content/properties/Parameter` — параметр правила.</span><span class="sxs-lookup"><span data-stu-id="f2215-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="f2215-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="f2215-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-473">7.3.</span></span>    <span data-ttu-id="f2215-474">Удаление правила</span><span class="sxs-lookup"><span data-stu-id="f2215-474">Delete Rule</span></span>
| <span data-ttu-id="f2215-475">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-475">HTTP Method</span></span> | <span data-ttu-id="f2215-476">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-477">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-478">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-479">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-479">Parameter Name</span></span> | <span data-ttu-id="f2215-480">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-481">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-481">modelId</span></span> |<span data-ttu-id="f2215-482">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-483">filterId</span><span class="sxs-lookup"><span data-stu-id="f2215-483">filterId</span></span> |<span data-ttu-id="f2215-484">Уникальный идентификатор фильтра hello</span><span class="sxs-lookup"><span data-stu-id="f2215-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="f2215-485">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-485">apiVersion</span></span> |<span data-ttu-id="f2215-486">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-486">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-487">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-487">Request Body</span></span> |<span data-ttu-id="f2215-488">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-488">NONE</span></span> |

<span data-ttu-id="f2215-489">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-489">**Response**:</span></span>

<span data-ttu-id="f2215-490">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="f2215-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-491">7.4.</span></span>    <span data-ttu-id="f2215-492">Удаление всех правил</span><span class="sxs-lookup"><span data-stu-id="f2215-492">Delete All Rules</span></span>
| <span data-ttu-id="f2215-493">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-493">HTTP Method</span></span> | <span data-ttu-id="f2215-494">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-495">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-496">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-497">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-497">Parameter Name</span></span> | <span data-ttu-id="f2215-498">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-499">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-499">modelId</span></span> |<span data-ttu-id="f2215-500">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-501">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-501">apiVersion</span></span> |<span data-ttu-id="f2215-502">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-502">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-503">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-503">Request Body</span></span> |<span data-ttu-id="f2215-504">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-504">NONE</span></span> |

<span data-ttu-id="f2215-505">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-505">**Response**:</span></span>

<span data-ttu-id="f2215-506">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="f2215-507">8. Каталог</span><span class="sxs-lookup"><span data-stu-id="f2215-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="f2215-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-508">8.1.</span></span>    <span data-ttu-id="f2215-509">Импорт данных каталога</span><span class="sxs-lookup"><span data-stu-id="f2215-509">Import Catalog Data</span></span>
<span data-ttu-id="f2215-510">При передаче нескольких каталогов файлы toohello же модель с несколькими вызовами, будет вставлен только hello новые элементы каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="f2215-511">Существующие элементы останутся на основе исходных значений hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="f2215-512">С помощью этого метода нельзя обновлять данные каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="f2215-513">данные каталога Hello следовать hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f2215-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="f2215-514">Без характеристик: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="f2215-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="f2215-515">С характеристиками: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="f2215-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="f2215-516">Примечание: hello максимальный размер файла — 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="f2215-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="f2215-517">** Сведения о формате **</span><span class="sxs-lookup"><span data-stu-id="f2215-517">** Format details **</span></span>

| <span data-ttu-id="f2215-518">Имя</span><span class="sxs-lookup"><span data-stu-id="f2215-518">Name</span></span> | <span data-ttu-id="f2215-519">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f2215-519">Mandatory</span></span> | <span data-ttu-id="f2215-520">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-520">Type</span></span> | <span data-ttu-id="f2215-521">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f2215-522">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="f2215-522">Item Id</span></span> |<span data-ttu-id="f2215-523">Да</span><span class="sxs-lookup"><span data-stu-id="f2215-523">Yes</span></span> |<span data-ttu-id="f2215-524">[A–z], [a–z], [0–9], [_] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;</span><span class="sxs-lookup"><span data-stu-id="f2215-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="f2215-525">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-525">Max length: 50</span></span> |<span data-ttu-id="f2215-526">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="f2215-527">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="f2215-527">Item Name</span></span> |<span data-ttu-id="f2215-528">Да</span><span class="sxs-lookup"><span data-stu-id="f2215-528">Yes</span></span> |<span data-ttu-id="f2215-529">Любые алфавитно-цифровые символы</span><span class="sxs-lookup"><span data-stu-id="f2215-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="f2215-530">Максимальная длина: 255</span><span class="sxs-lookup"><span data-stu-id="f2215-530">Max length: 255</span></span> |<span data-ttu-id="f2215-531">Имя элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-531">Item name.</span></span> |
| <span data-ttu-id="f2215-532">Категория элемента</span><span class="sxs-lookup"><span data-stu-id="f2215-532">Item Category</span></span> |<span data-ttu-id="f2215-533">Да</span><span class="sxs-lookup"><span data-stu-id="f2215-533">Yes</span></span> |<span data-ttu-id="f2215-534">Любые алфавитно-цифровые символы</span><span class="sxs-lookup"><span data-stu-id="f2215-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="f2215-535">Максимальная длина: 255</span><span class="sxs-lookup"><span data-stu-id="f2215-535">Max length: 255</span></span> |<span data-ttu-id="f2215-536">Категория toowhich этот элемент принадлежит (например кулинарии книг, Драма...); может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="f2215-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="f2215-537">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-537">Description</span></span> |<span data-ttu-id="f2215-538">Нет, если только нет характеристик (но может быть пустым)</span><span class="sxs-lookup"><span data-stu-id="f2215-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="f2215-539">Любые алфавитно-цифровые символы</span><span class="sxs-lookup"><span data-stu-id="f2215-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="f2215-540">Максимальная длина: 4000</span><span class="sxs-lookup"><span data-stu-id="f2215-540">Max length: 4000</span></span> |<span data-ttu-id="f2215-541">Описание элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-541">Description of this item.</span></span> |
| <span data-ttu-id="f2215-542">Список характеристик</span><span class="sxs-lookup"><span data-stu-id="f2215-542">Features list</span></span> |<span data-ttu-id="f2215-543">Нет</span><span class="sxs-lookup"><span data-stu-id="f2215-543">No</span></span> |<span data-ttu-id="f2215-544">Любые алфавитно-цифровые символы</span><span class="sxs-lookup"><span data-stu-id="f2215-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="f2215-545">Максимальная длина: 4000; максимальное число компонентов: 20</span><span class="sxs-lookup"><span data-stu-id="f2215-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="f2215-546">Список разделенных запятыми имя функции = функция значение, которое может быть рекомендация модели используется tooenhance; в разделе [дополнительные разделы](#2-advanced-topics) раздела.</span><span class="sxs-lookup"><span data-stu-id="f2215-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="f2215-547">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-547">HTTP Method</span></span> | <span data-ttu-id="f2215-548">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-549">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-550">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="f2215-551">ЗАГОЛОВОК</span><span class="sxs-lookup"><span data-stu-id="f2215-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="f2215-552">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-552">Parameter Name</span></span> | <span data-ttu-id="f2215-553">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-554">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-554">modelId</span></span> |<span data-ttu-id="f2215-555">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-556">filename</span><span class="sxs-lookup"><span data-stu-id="f2215-556">filename</span></span> |<span data-ttu-id="f2215-557">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="f2215-558">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="f2215-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f2215-559">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-559">Max length: 50</span></span> |
| <span data-ttu-id="f2215-560">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-560">apiVersion</span></span> |<span data-ttu-id="f2215-561">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-561">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-562">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-562">Request Body</span></span> |<span data-ttu-id="f2215-563">Пример (с компонентами):</span><span class="sxs-lookup"><span data-stu-id="f2215-563">Example (with features):</span></span><br/><span data-ttu-id="f2215-564">2406e770-769c-4189-89de-1c9283f93a96, Callan Клара, книгу, название книги hello, создавать = Wright Ричард publisher = Harper Flamingo Канада, год = 2001 г.</span><span class="sxs-lookup"><span data-stu-id="f2215-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="f2215-565">hello 21bf8088-b6c0-4509-870c-e1c7ac78304a, Forgetting комнате: фантастики (Byzantium книга), книга, создавать = Bantock ник publisher = Harpercollins, год = 1997</span><span class="sxs-lookup"><span data-stu-id="f2215-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="f2215-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="f2215-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="f2215-567">552a1940-21e4-4399-82bb-594b46d7ed54, солидарности ответ, книгу, название книги hello, создавать = фабрики Magnus издателя публикации галереей = год = 1998</span><span class="sxs-lookup"><span data-stu-id="f2215-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="f2215-568">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-568">**Response**:</span></span>

<span data-ttu-id="f2215-569">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-569">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-570">Hello API возвращает отчет hello импорта.</span><span class="sxs-lookup"><span data-stu-id="f2215-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="f2215-571">`feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="f2215-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="f2215-572">`feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.</span><span class="sxs-lookup"><span data-stu-id="f2215-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="f2215-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="f2215-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-574">8.2.</span></span>    <span data-ttu-id="f2215-575">Получение каталога</span><span class="sxs-lookup"><span data-stu-id="f2215-575">Get Catalog</span></span>
<span data-ttu-id="f2215-576">Извлекает все элементы каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="f2215-577">Hello каталога будут получены одной странице одновременно.</span><span class="sxs-lookup"><span data-stu-id="f2215-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="f2215-578">Для поиска элементов tooget с определенного индекса, можно использовать параметр hello $skip odata.</span><span class="sxs-lookup"><span data-stu-id="f2215-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="f2215-579">Для экземпляра tooget элементов, начиная с позиции 100 следует добавить параметр hello $skip = 100 toohello запрос.</span><span class="sxs-lookup"><span data-stu-id="f2215-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="f2215-580">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-580">HTTP Method</span></span> | <span data-ttu-id="f2215-581">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-582">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-583">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-584">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-584">Parameter Name</span></span> | <span data-ttu-id="f2215-585">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-586">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-586">modelId</span></span> |<span data-ttu-id="f2215-587">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-588">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-588">apiVersion</span></span> |<span data-ttu-id="f2215-589">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-589">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-590">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-590">Request Body</span></span> |<span data-ttu-id="f2215-591">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-591">NONE</span></span> |

<span data-ttu-id="f2215-592">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-592">**Response**:</span></span>

<span data-ttu-id="f2215-593">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-593">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-594">Hello ответ включает одной записи для каждого элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="f2215-595">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-596">`feed/entry/content/properties/ExternalId`-Каталога внешний идентификатор элемента, одно — предоставляемое клиента hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="f2215-597">`feed/entry/content/properties/InternalId`-Каталога внутренний идентификатор элемента, hello, создавший Azure Machine Learning рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="f2215-598">`feed/entry/content/properties/Name` — имя элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="f2215-599">`feed/entry/content/properties/Category` — категория элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="f2215-600">`feed/entry/content/properties/Description` — описание элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="f2215-601">`feed/entry/content/properties/Metadata` — метаданные элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="f2215-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="f2215-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-603">8.3.</span></span>    <span data-ttu-id="f2215-604">Получение элементов каталога по токену</span><span class="sxs-lookup"><span data-stu-id="f2215-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="f2215-605">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-605">HTTP Method</span></span> | <span data-ttu-id="f2215-606">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-607">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-608">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-609">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-609">Parameter Name</span></span> | <span data-ttu-id="f2215-610">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-611">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-611">modelId</span></span> |<span data-ttu-id="f2215-612">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-613">token</span><span class="sxs-lookup"><span data-stu-id="f2215-613">token</span></span> |<span data-ttu-id="f2215-614">Имя элемента каталога hello маркер.</span><span class="sxs-lookup"><span data-stu-id="f2215-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="f2215-615">Должен содержать не менее трех символов.</span><span class="sxs-lookup"><span data-stu-id="f2215-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="f2215-616">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-616">apiVersion</span></span> |<span data-ttu-id="f2215-617">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-617">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-618">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-618">Request Body</span></span> |<span data-ttu-id="f2215-619">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-619">NONE</span></span> |

<span data-ttu-id="f2215-620">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-620">**Response**:</span></span>

<span data-ttu-id="f2215-621">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-621">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-622">Hello ответ включает одной записи для каждого элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="f2215-623">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-624">`feed/entry/content/properties/InternalId`-Каталога внутренний идентификатор элемента, hello, создавший Azure Machine Learning рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="f2215-625">`feed/entry/content/properties/Name` — имя элемента каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="f2215-626">`feed/entry/content/properties/Rating` — (для будущего использования).</span><span class="sxs-lookup"><span data-stu-id="f2215-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="f2215-627">`feed/entry/content/properties/Reasoning` — (для будущего использования).</span><span class="sxs-lookup"><span data-stu-id="f2215-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="f2215-628">`feed/entry/content/properties/Metadata` — (для будущего использования).</span><span class="sxs-lookup"><span data-stu-id="f2215-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="f2215-629">`feed/entry/content/properties/FormattedRating` — (для будущего использования).</span><span class="sxs-lookup"><span data-stu-id="f2215-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="f2215-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="f2215-631">9. Данные об использовании</span><span class="sxs-lookup"><span data-stu-id="f2215-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="f2215-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-632">9.1.</span></span>    <span data-ttu-id="f2215-633">Импорт данных по использованию</span><span class="sxs-lookup"><span data-stu-id="f2215-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="f2215-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-634">9.1.1.</span></span> <span data-ttu-id="f2215-635">Передача файла</span><span class="sxs-lookup"><span data-stu-id="f2215-635">Uploading File</span></span>
<span data-ttu-id="f2215-636">В этом разделе показано, как данные об использовании tooupload с помощью файла.</span><span class="sxs-lookup"><span data-stu-id="f2215-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="f2215-637">Можно вызывать этот API несколько раз с данными об использовании.</span><span class="sxs-lookup"><span data-stu-id="f2215-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="f2215-638">Для всех вызовов сохранятся все данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="f2215-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="f2215-639">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-639">HTTP Method</span></span> | <span data-ttu-id="f2215-640">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-641">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-642">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-643">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-643">Parameter Name</span></span> | <span data-ttu-id="f2215-644">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-645">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-645">modelId</span></span> |<span data-ttu-id="f2215-646">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-647">filename</span><span class="sxs-lookup"><span data-stu-id="f2215-647">filename</span></span> |<span data-ttu-id="f2215-648">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="f2215-649">Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="f2215-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f2215-650">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-650">Max length: 50</span></span> |
| <span data-ttu-id="f2215-651">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-651">apiVersion</span></span> |<span data-ttu-id="f2215-652">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-652">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-653">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-653">Request Body</span></span> |<span data-ttu-id="f2215-654">Данные об использовании.</span><span class="sxs-lookup"><span data-stu-id="f2215-654">Usage data.</span></span> <span data-ttu-id="f2215-655">Формат:</span><span class="sxs-lookup"><span data-stu-id="f2215-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="f2215-656">Имя</span><span class="sxs-lookup"><span data-stu-id="f2215-656">Name</span></span></th><th><span data-ttu-id="f2215-657">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f2215-657">Mandatory</span></span></th><th><span data-ttu-id="f2215-658">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-658">Type</span></span></th><th><span data-ttu-id="f2215-659">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-659">Description</span></span></th></tr><tr><td><span data-ttu-id="f2215-660">Идентификатор пользователя</span><span class="sxs-lookup"><span data-stu-id="f2215-660">User Id</span></span></td><td><span data-ttu-id="f2215-661">Да</span><span class="sxs-lookup"><span data-stu-id="f2215-661">Yes</span></span></td><td><span data-ttu-id="f2215-662">[A–z], [a–z], [0–9], [_] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;</span><span class="sxs-lookup"><span data-stu-id="f2215-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="f2215-663">Максимальная длина: 255</span><span class="sxs-lookup"><span data-stu-id="f2215-663">Max length: 255</span></span> </td><td><span data-ttu-id="f2215-664">Уникальный идентификатор пользователя</span><span class="sxs-lookup"><span data-stu-id="f2215-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="f2215-665">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="f2215-665">Item Id</span></span></td><td><span data-ttu-id="f2215-666">Да</span><span class="sxs-lookup"><span data-stu-id="f2215-666">Yes</span></span></td><td><span data-ttu-id="f2215-667">[A-z], [a-z], [0-9], [&#95;] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;</span><span class="sxs-lookup"><span data-stu-id="f2215-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="f2215-668">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-668">Max length: 50</span></span></td><td><span data-ttu-id="f2215-669">Уникальный идентификатор элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="f2215-670">Время</span><span class="sxs-lookup"><span data-stu-id="f2215-670">Time</span></span></td><td><span data-ttu-id="f2215-671">Нет</span><span class="sxs-lookup"><span data-stu-id="f2215-671">No</span></span></td><td><span data-ttu-id="f2215-672">Дата в формате: ГГГГ/ММ/ДДТЧЧ:ММ:СС (например, 2013/06/20Т10:00:00)</span><span class="sxs-lookup"><span data-stu-id="f2215-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="f2215-673">Время данных</span><span class="sxs-lookup"><span data-stu-id="f2215-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="f2215-674">Событие</span><span class="sxs-lookup"><span data-stu-id="f2215-674">Event</span></span></td><td><span data-ttu-id="f2215-675">Нет. Если указано, необходимо также указать дату</span><span class="sxs-lookup"><span data-stu-id="f2215-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="f2215-676">Одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="f2215-676">One of hello following:</span></span><br><span data-ttu-id="f2215-677">• Click</span><span class="sxs-lookup"><span data-stu-id="f2215-677">• Click</span></span><br><span data-ttu-id="f2215-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="f2215-678">• RecommendationClick</span></span><br><span data-ttu-id="f2215-679">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="f2215-679">•    AddShopCart</span></span><br><span data-ttu-id="f2215-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="f2215-680">• RemoveShopCart</span></span><br><span data-ttu-id="f2215-681">• Покупка</span><span class="sxs-lookup"><span data-stu-id="f2215-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="f2215-682">Максимальный размер файла: 200 МБ.</span><span class="sxs-lookup"><span data-stu-id="f2215-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="f2215-683">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="f2215-684">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-684">**Response**:</span></span>

<span data-ttu-id="f2215-685">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="f2215-686">`Feed\entry\content\properties\LineCount` — количество принятых строк.</span><span class="sxs-lookup"><span data-stu-id="f2215-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="f2215-687">`Feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.</span><span class="sxs-lookup"><span data-stu-id="f2215-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="f2215-688">`Feed\entry\content\properties\FileId` — идентификатор файла.</span><span class="sxs-lookup"><span data-stu-id="f2215-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="f2215-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="f2215-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-690">9.1.2.</span></span> <span data-ttu-id="f2215-691">Использование функции сбора данных</span><span class="sxs-lookup"><span data-stu-id="f2215-691">Using Data Acquisition</span></span>
<span data-ttu-id="f2215-692">В этом разделе показано, как toosend событий в реальном времени tooAzure машины обучения рекомендации, обычно с веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="f2215-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="f2215-693">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-693">HTTP Method</span></span> | <span data-ttu-id="f2215-694">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-695">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="f2215-696">ЗАГОЛОВОК</span><span class="sxs-lookup"><span data-stu-id="f2215-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="f2215-697">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-697">Parameter Name</span></span> | <span data-ttu-id="f2215-698">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-699">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-699">apiVersion</span></span> |<span data-ttu-id="f2215-700">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-700">1.0</span></span> |
| <span data-ttu-id="f2215-701">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-701">Request body</span></span> |<span data-ttu-id="f2215-702">Записи данных событий для каждого события необходимо toosend.</span><span class="sxs-lookup"><span data-stu-id="f2215-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="f2215-703">Для hello одного сеанса пользователя или браузера hello таким же Идентификатором hello SessionId поля, необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="f2215-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="f2215-704">(Пример текста события см. ниже.)</span><span class="sxs-lookup"><span data-stu-id="f2215-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="f2215-705">Пример события Click:</span><span class="sxs-lookup"><span data-stu-id="f2215-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="f2215-706">Пример события RecommendationClick:</span><span class="sxs-lookup"><span data-stu-id="f2215-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="f2215-707">Пример события AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="f2215-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="f2215-708">Пример события RemoveShopCart:</span><span class="sxs-lookup"><span data-stu-id="f2215-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="f2215-709">Пример события Purchase:</span><span class="sxs-lookup"><span data-stu-id="f2215-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="f2215-710">Пример отправки событий двух типов, Click и AddShopCart:</span><span class="sxs-lookup"><span data-stu-id="f2215-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="f2215-711">**Ответ**. Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="f2215-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-712">9.2.</span></span>    <span data-ttu-id="f2215-713">Вывод списка файлов использования модели</span><span class="sxs-lookup"><span data-stu-id="f2215-713">List Model Usage Files</span></span>
<span data-ttu-id="f2215-714">Извлекает метаданные из всех файлов использования модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="f2215-715">Hello об использовании файлы будут получены одной странице одновременно.</span><span class="sxs-lookup"><span data-stu-id="f2215-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="f2215-716">Каждая страница содержит 100 элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-716">Each page containes 100 items.</span></span> <span data-ttu-id="f2215-717">Для поиска элементов tooget с определенного индекса, можно использовать параметр hello $skip odata.</span><span class="sxs-lookup"><span data-stu-id="f2215-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="f2215-718">Для экземпляра tooget элементов, начиная с позиции 100 следует добавить параметр hello $skip = 100 toohello запрос.</span><span class="sxs-lookup"><span data-stu-id="f2215-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="f2215-719">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-719">HTTP Method</span></span> | <span data-ttu-id="f2215-720">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-721">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-722">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-723">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-723">Parameter Name</span></span> | <span data-ttu-id="f2215-724">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="f2215-725">forModelId</span></span> |<span data-ttu-id="f2215-726">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-727">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-727">apiVersion</span></span> |<span data-ttu-id="f2215-728">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-728">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-729">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-729">Request Body</span></span> |<span data-ttu-id="f2215-730">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-730">NONE</span></span> |

<span data-ttu-id="f2215-731">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-731">**Response**:</span></span>

<span data-ttu-id="f2215-732">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-732">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-733">Hello ответ содержит одну запись для использования файла.</span><span class="sxs-lookup"><span data-stu-id="f2215-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="f2215-734">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-735">`feed\entry\content\properties\Id` — идентификатор файла использования.</span><span class="sxs-lookup"><span data-stu-id="f2215-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="f2215-736">`feed\entry\content\properties\Length` — размер файла использования в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="f2215-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="f2215-737">`feed\entry\content\properties\DateModified`-Дата создания файла использования hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="f2215-738">`feed\entry\content\properties\UseInModel`-Файл для использования hello использование в модели hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="f2215-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="f2215-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-740">9.3.</span></span>    <span data-ttu-id="f2215-741">Получение статистики использования</span><span class="sxs-lookup"><span data-stu-id="f2215-741">Get Usage Statistics</span></span>
<span data-ttu-id="f2215-742">Получает статистику использования.</span><span class="sxs-lookup"><span data-stu-id="f2215-742">Gets usage statistics.</span></span>

| <span data-ttu-id="f2215-743">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-743">HTTP Method</span></span> | <span data-ttu-id="f2215-744">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-745">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-746">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-747">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-747">Parameter Name</span></span> | <span data-ttu-id="f2215-748">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-749">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-749">modelId</span></span> |<span data-ttu-id="f2215-750">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-751">startDate</span><span class="sxs-lookup"><span data-stu-id="f2215-751">startDate</span></span> |<span data-ttu-id="f2215-752">Дата начала.</span><span class="sxs-lookup"><span data-stu-id="f2215-752">Start date.</span></span> <span data-ttu-id="f2215-753">Формат: гггг/ММ/ддТЧЧ:мм:сс</span><span class="sxs-lookup"><span data-stu-id="f2215-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="f2215-754">endDate</span><span class="sxs-lookup"><span data-stu-id="f2215-754">endDate</span></span> |<span data-ttu-id="f2215-755">Дата окончания.</span><span class="sxs-lookup"><span data-stu-id="f2215-755">End date.</span></span> <span data-ttu-id="f2215-756">Формат: гггг/ММ/ддТЧЧ:мм:сс</span><span class="sxs-lookup"><span data-stu-id="f2215-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="f2215-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="f2215-757">eventTypes</span></span> |<span data-ttu-id="f2215-758">Строки с разделителями запятыми события типы или null tooget все события</span><span class="sxs-lookup"><span data-stu-id="f2215-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="f2215-759">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-759">apiVersion</span></span> |<span data-ttu-id="f2215-760">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-760">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-761">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-761">Request Body</span></span> |<span data-ttu-id="f2215-762">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-762">NONE</span></span> |

<span data-ttu-id="f2215-763">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-763">**Response**:</span></span>

<span data-ttu-id="f2215-764">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-764">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-765">Коллекция элементов "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="f2215-765">A collection of key/value elements.</span></span> <span data-ttu-id="f2215-766">Каждый из них содержит сумму hello событий для определенного типа событий группируются по часам.</span><span class="sxs-lookup"><span data-stu-id="f2215-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="f2215-767">`feed\entry[i]\content\properties\Key`— Содержит время hello (сгруппированный по часам) и типа события hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="f2215-768">`feed\entry[i]\content\properties\Value` — общее число событий.</span><span class="sxs-lookup"><span data-stu-id="f2215-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="f2215-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="f2215-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-770">9.4.</span></span>    <span data-ttu-id="f2215-771">Получение образца файла использования</span><span class="sxs-lookup"><span data-stu-id="f2215-771">Get Usage File Sample</span></span>
<span data-ttu-id="f2215-772">Извлекает hello первый 2 КБ, использование содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="f2215-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="f2215-773">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-773">HTTP Method</span></span> | <span data-ttu-id="f2215-774">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-775">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-776">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-777">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-777">Parameter Name</span></span> | <span data-ttu-id="f2215-778">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-779">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-779">modelId</span></span> |<span data-ttu-id="f2215-780">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-781">fileId</span><span class="sxs-lookup"><span data-stu-id="f2215-781">fileId</span></span> |<span data-ttu-id="f2215-782">Уникальный идентификатор hello модель использования файла</span><span class="sxs-lookup"><span data-stu-id="f2215-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="f2215-783">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-783">apiVersion</span></span> |<span data-ttu-id="f2215-784">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-784">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-785">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-785">Request Body</span></span> |<span data-ttu-id="f2215-786">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-786">NONE</span></span> |

<span data-ttu-id="f2215-787">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-787">**Response**:</span></span>

<span data-ttu-id="f2215-788">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-788">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-789">Ответ возвращается в формате необработанного текста.</span><span class="sxs-lookup"><span data-stu-id="f2215-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="f2215-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="f2215-790">9.5.</span></span>    <span data-ttu-id="f2215-791">Получение файла использования модели</span><span class="sxs-lookup"><span data-stu-id="f2215-791">Get Model Usage File</span></span>
<span data-ttu-id="f2215-792">Извлекает полное содержимое hello hello использования файла.</span><span class="sxs-lookup"><span data-stu-id="f2215-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="f2215-793">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-793">HTTP Method</span></span> | <span data-ttu-id="f2215-794">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-795">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-796">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-797">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-797">Parameter Name</span></span> | <span data-ttu-id="f2215-798">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-799">mid</span><span class="sxs-lookup"><span data-stu-id="f2215-799">mid</span></span> |<span data-ttu-id="f2215-800">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-801">fid</span><span class="sxs-lookup"><span data-stu-id="f2215-801">fid</span></span> |<span data-ttu-id="f2215-802">Уникальный идентификатор hello модель использования файла</span><span class="sxs-lookup"><span data-stu-id="f2215-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="f2215-803">загрузить</span><span class="sxs-lookup"><span data-stu-id="f2215-803">download</span></span> |<span data-ttu-id="f2215-804">1</span><span class="sxs-lookup"><span data-stu-id="f2215-804">1</span></span> |
| <span data-ttu-id="f2215-805">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-805">apiVersion</span></span> |<span data-ttu-id="f2215-806">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-806">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-807">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-807">Request Body</span></span> |<span data-ttu-id="f2215-808">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-808">NONE</span></span> |

<span data-ttu-id="f2215-809">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-809">**Response**:</span></span>

<span data-ttu-id="f2215-810">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-810">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-811">Ответ возвращается в формате необработанного текста.</span><span class="sxs-lookup"><span data-stu-id="f2215-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="f2215-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="f2215-812">9.6.</span></span>    <span data-ttu-id="f2215-813">Удаление файла использования</span><span class="sxs-lookup"><span data-stu-id="f2215-813">Delete Usage File</span></span>
<span data-ttu-id="f2215-814">Удаляет файл использования hello указанной модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="f2215-815">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-815">HTTP Method</span></span> | <span data-ttu-id="f2215-816">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-817">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-818">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-819">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-819">Parameter Name</span></span> | <span data-ttu-id="f2215-820">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-821">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-821">modelId</span></span> |<span data-ttu-id="f2215-822">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-823">fileId</span><span class="sxs-lookup"><span data-stu-id="f2215-823">fileId</span></span> |<span data-ttu-id="f2215-824">Уникальный идентификатор hello файл toobe удалена</span><span class="sxs-lookup"><span data-stu-id="f2215-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="f2215-825">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-825">apiVersion</span></span> |<span data-ttu-id="f2215-826">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-826">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-827">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-827">Request Body</span></span> |<span data-ttu-id="f2215-828">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-828">NONE</span></span> |

<span data-ttu-id="f2215-829">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-829">**Response**:</span></span>

<span data-ttu-id="f2215-830">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="f2215-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="f2215-831">9.7.</span></span>    <span data-ttu-id="f2215-832">Удаление всех файлов использования</span><span class="sxs-lookup"><span data-stu-id="f2215-832">Delete All Usage Files</span></span>
<span data-ttu-id="f2215-833">Удаляет все файлы использования модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="f2215-834">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-834">HTTP Method</span></span> | <span data-ttu-id="f2215-835">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-836">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-837">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-838">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-838">Parameter Name</span></span> | <span data-ttu-id="f2215-839">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-840">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-840">modelId</span></span> |<span data-ttu-id="f2215-841">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-842">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-842">apiVersion</span></span> |<span data-ttu-id="f2215-843">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-843">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-844">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-844">Request Body</span></span> |<span data-ttu-id="f2215-845">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-845">NONE</span></span> |

<span data-ttu-id="f2215-846">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-846">**Response**:</span></span>

<span data-ttu-id="f2215-847">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="f2215-848">10. Функции</span><span class="sxs-lookup"><span data-stu-id="f2215-848">10. Features</span></span>
<span data-ttu-id="f2215-849">В этом разделе показано, как tooretrieve функции сведения, такие как функции hello импортирован и их значения, рангу, и при этом ранг был выделен.</span><span class="sxs-lookup"><span data-stu-id="f2215-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="f2215-850">Функции, импортируются как часть данных каталога hello, а затем рангу связанного при завершения rank сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="f2215-851">Функция rank можно изменить соответствующим toohello модель данных об использовании и типа элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="f2215-852">Но ранг hello согласованное использование/элементы должны быть только небольшие отклонения.</span><span class="sxs-lookup"><span data-stu-id="f2215-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="f2215-853">Ранг Hello функций является неотрицательным числом.</span><span class="sxs-lookup"><span data-stu-id="f2215-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="f2215-854">Hello с номером 0 означает не присваивается ранг этой функции hello (происходит при вызове этого API завершения предыдущего toohello первого построения rank hello).</span><span class="sxs-lookup"><span data-stu-id="f2215-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="f2215-855">Дата Hello, по которому отмеченное ранг hello называется актуальность оценка hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="f2215-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-856">10.1.</span></span> <span data-ttu-id="f2215-857">Получение информации о характеристиках (для последней сборки рейтинга)</span><span class="sxs-lookup"><span data-stu-id="f2215-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="f2215-858">Извлекает сведения о функции hello, включая ранжирования для последней hello успешной rank сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="f2215-859">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-859">HTTP Method</span></span> | <span data-ttu-id="f2215-860">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-861">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-862">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-863">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-863">Parameter Name</span></span> | <span data-ttu-id="f2215-864">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-865">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-865">modelId</span></span> |<span data-ttu-id="f2215-866">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="f2215-867">samplingSize</span></span> |<span data-ttu-id="f2215-868">Количество tooinclude значения для каждого компонента, в соответствии с toohello данных, содержащихся в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="f2215-869">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="f2215-869">Possible values are:</span></span><br> <span data-ttu-id="f2215-870">-1 — все образцы;</span><span class="sxs-lookup"><span data-stu-id="f2215-870">-1 - All samples.</span></span> <br><span data-ttu-id="f2215-871">0 — ни одного образца;</span><span class="sxs-lookup"><span data-stu-id="f2215-871">0 - No sampling.</span></span> <br><span data-ttu-id="f2215-872">N — возвращается N образцов для каждого имени компонента.</span><span class="sxs-lookup"><span data-stu-id="f2215-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="f2215-873">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-873">apiVersion</span></span> |<span data-ttu-id="f2215-874">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-874">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-875">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-875">Request Body</span></span> |<span data-ttu-id="f2215-876">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-876">NONE</span></span> |

<span data-ttu-id="f2215-877">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-877">**Response**:</span></span>

<span data-ttu-id="f2215-878">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-878">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-879">Hello ответ содержит список записей сведения о функции.</span><span class="sxs-lookup"><span data-stu-id="f2215-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="f2215-880">Каждая запись содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f2215-880">Each entry contains:</span></span>

* <span data-ttu-id="f2215-881">`feed/entry/content/m:properties/d:Name` — название характеристики.</span><span class="sxs-lookup"><span data-stu-id="f2215-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="f2215-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Дата в какой hello ранг функция выделенный toothis так называемый</span><span class="sxs-lookup"><span data-stu-id="f2215-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="f2215-883">актуальность оценки.</span><span class="sxs-lookup"><span data-stu-id="f2215-883">score freshness feature.</span></span> <span data-ttu-id="f2215-884">Историческая дата ("0001-01-01T00:00:00") означает, что сборка рейтинга еще не выполнялась.</span><span class="sxs-lookup"><span data-stu-id="f2215-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="f2215-885">`feed/entry/content/m:properties/d:Rank` — рейтинг характеристики (число с плавающей запятой).</span><span class="sxs-lookup"><span data-stu-id="f2215-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="f2215-886">При рейтинге не менее 2,0 характеристика считается значимой.</span><span class="sxs-lookup"><span data-stu-id="f2215-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="f2215-887">`feed/entry/content/m:properties/d:SampleValues`-Запятыми список значений, размер выборки toohello на запросе.</span><span class="sxs-lookup"><span data-stu-id="f2215-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="f2215-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="f2215-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-889">10.2.</span></span> <span data-ttu-id="f2215-890">Получение информации о характеристиках (для определенной сборки рейтинга)</span><span class="sxs-lookup"><span data-stu-id="f2215-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="f2215-891">Извлекает сведения о функции hello, включая релевантности для конкретного построения rank hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="f2215-892">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-892">HTTP Method</span></span> | <span data-ttu-id="f2215-893">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-894">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-895">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-896">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-896">Parameter Name</span></span> | <span data-ttu-id="f2215-897">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-898">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-898">modelId</span></span> |<span data-ttu-id="f2215-899">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="f2215-900">samplingSize</span></span> |<span data-ttu-id="f2215-901">Количество tooinclude значения для каждого компонента, в соответствии с toohello данных, содержащихся в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="f2215-902">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="f2215-902">Possible values are:</span></span><br> <span data-ttu-id="f2215-903">-1 — все образцы;</span><span class="sxs-lookup"><span data-stu-id="f2215-903">-1 - All samples.</span></span> <br><span data-ttu-id="f2215-904">0 — ни одного образца;</span><span class="sxs-lookup"><span data-stu-id="f2215-904">0 - No sampling.</span></span> <br><span data-ttu-id="f2215-905">N — возвращается N образцов для каждого имени компонента.</span><span class="sxs-lookup"><span data-stu-id="f2215-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="f2215-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="f2215-906">rankBuildId</span></span> |<span data-ttu-id="f2215-907">Уникальный идентификатор сборки rank hello или -1 для последнего построения rank hello</span><span class="sxs-lookup"><span data-stu-id="f2215-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="f2215-908">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-908">apiVersion</span></span> |<span data-ttu-id="f2215-909">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-909">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-910">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-910">Request Body</span></span> |<span data-ttu-id="f2215-911">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-911">NONE</span></span> |

<span data-ttu-id="f2215-912">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-912">**Response**:</span></span>

<span data-ttu-id="f2215-913">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-913">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-914">Hello ответ содержит список записей сведения о функции.</span><span class="sxs-lookup"><span data-stu-id="f2215-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="f2215-915">Каждая запись содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f2215-915">Each entry contains:</span></span>

* <span data-ttu-id="f2215-916">`feed/entry/content/m:properties/d:Name` — название характеристики.</span><span class="sxs-lookup"><span data-stu-id="f2215-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="f2215-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Дата в какой hello ранг функция выделенный toothis так называемый</span><span class="sxs-lookup"><span data-stu-id="f2215-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="f2215-918">актуальность оценки.</span><span class="sxs-lookup"><span data-stu-id="f2215-918">score freshness feature.</span></span> <span data-ttu-id="f2215-919">Историческая дата ("0001-01-01T00:00:00") означает, что сборка рейтинга еще не выполнялась.</span><span class="sxs-lookup"><span data-stu-id="f2215-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="f2215-920">`feed/entry/content/m:properties/d:Rank` — рейтинг характеристики (число с плавающей запятой).</span><span class="sxs-lookup"><span data-stu-id="f2215-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="f2215-921">При рейтинге не менее 2,0 характеристика считается значимой.</span><span class="sxs-lookup"><span data-stu-id="f2215-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="f2215-922">`feed/entry/content/m:properties/d:SampleValues`-Запятыми список значений, размер выборки toohello на запросе.</span><span class="sxs-lookup"><span data-stu-id="f2215-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="f2215-923">OData</span><span class="sxs-lookup"><span data-stu-id="f2215-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="f2215-924">11. Создание</span><span class="sxs-lookup"><span data-stu-id="f2215-924">11. Build</span></span>
  <span data-ttu-id="f2215-925">В этом разделе описывается hello различные интерфейсы API, связанные с toobuilds.</span><span class="sxs-lookup"><span data-stu-id="f2215-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="f2215-926">Существует три типа сборок: сборка рекомендаций, сборка рейтингов и сборка FBT (часто покупаемая вместе с ними).</span><span class="sxs-lookup"><span data-stu-id="f2215-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="f2215-927">Назначение Hello рекомендация сборки — toogenerate модели рекомендаций, использовать для составления прогнозов.</span><span class="sxs-lookup"><span data-stu-id="f2215-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="f2215-928">Прогнозы (для сборок этого типа) бывают двух типов:</span><span class="sxs-lookup"><span data-stu-id="f2215-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="f2215-929">I2I — т. н.</span><span class="sxs-lookup"><span data-stu-id="f2215-929">I2I - a.k.a.</span></span> <span data-ttu-id="f2215-930">Элемент рекомендации tooItem - заданный элемент или список элементов, этот параметр будет прогнозироваться список элементов, которые, скорее всего, toobe высокий интерес.</span><span class="sxs-lookup"><span data-stu-id="f2215-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="f2215-931">U2I — т. н.</span><span class="sxs-lookup"><span data-stu-id="f2215-931">U2I - a.k.a.</span></span> <span data-ttu-id="f2215-932">Рекомендации tooItem пользователя - заданы идентификатор пользователя (а при необходимости список элементов) этот параметр будет прогнозироваться список элементов, которые, скорее всего, toobe высокий интерес для hello заданным пользователем (и его выбора дополнительных элементов).</span><span class="sxs-lookup"><span data-stu-id="f2215-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="f2215-933">Hello U2I рекомендации основываются на историю hello элементы, представляющие интерес для пользователя hello toohello время построения модели hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="f2215-934">Rank построение, которое технические, позволяющий toolearn о hello полезность ваши возможности.</span><span class="sxs-lookup"><span data-stu-id="f2215-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="f2215-935">Как правило в порядке tooget hello добиться наилучших результатов для модели рекомендаций, включающие функции, должен выполнить hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="f2215-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="f2215-936">Активация rank сборки (если оценка hello ваши возможности стабильна) и подождите, пока вы получаете оценка функции hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="f2215-937">Получить ваши возможности ранг hello, вызывающему Привет [получить сведения о функции](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="f2215-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="f2215-938">Настройте сборки рекомендация hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f2215-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="f2215-939">`useFeatureInModel`-Set tooTrue.</span><span class="sxs-lookup"><span data-stu-id="f2215-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="f2215-940">`ModelingFeatureList`-Set tooa запятыми список функций со скоростью не менее 2.0 (в соответствии с toohello рангов, полученный в предыдущем шаге hello).</span><span class="sxs-lookup"><span data-stu-id="f2215-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="f2215-941">`AllowColdItemPlacement`-Set tooTrue.</span><span class="sxs-lookup"><span data-stu-id="f2215-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="f2215-942">При необходимости можно задать `EnableFeatureCorrelation` tooTrue и `ReasoningFeatureList` toohello список компонентов, которые вы хотите toouse объяснение (обычно hello же список компонентов, используются для моделирования или подчиненный список).</span><span class="sxs-lookup"><span data-stu-id="f2215-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="f2215-943">Активация сборки hello рекомендации с параметрами настройки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="f2215-944">Примечание: Если не задан, все параметры (например, вызов сборки рекомендация hello без параметров) или явно не отключайте hello использования функций (например `UseFeatureInModel` задать tooFalse), системы hello описывается настройка параметров, связанных с функции hello toohello описано выше значения, в случае, если существует rank сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="f2215-945">Не существует ограничения на выполнении rank построения и рекомендации построить одновременно для hello же модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="f2215-946">Тем не менее не может запустить две сборки hello того же типа на hello же модели в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="f2215-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="f2215-947">Сборка FBT (Frequently Bought Together, "С этим товаром часто покупают") — это еще один алгоритм рекомендаций, иногда называемый консервативным. Он подходит для каталогов, которые по своему характеру являются неоднородными (однородные каталоги: книги, фильмы, продукты питания, одежда; неоднородные: компьютеры и устройства, товары из разных областей, большое многообразие).</span><span class="sxs-lookup"><span data-stu-id="f2215-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="f2215-948">Примечание: Если hello использования файлы, загруженные содержат hello необязательное поле «Тип событий» нажмите для взноса по моделирования только события «Покупки» будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="f2215-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="f2215-949">Если тип события не указан, все события будут рассматриваться как покупки.</span><span class="sxs-lookup"><span data-stu-id="f2215-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="f2215-950">11.1. Параметры сборки</span><span class="sxs-lookup"><span data-stu-id="f2215-950">11.1 Build parameters</span></span>
<span data-ttu-id="f2215-951">Каждый тип сборки можно настроить с помощью набора параметров (описанных ниже).</span><span class="sxs-lookup"><span data-stu-id="f2215-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="f2215-952">Если не настроить параметры hello, hello системы будет автоматически атрибута toohello сведения присутствуют во время hello запустить сборку в соответствии с параметрами toohello значения.</span><span class="sxs-lookup"><span data-stu-id="f2215-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="f2215-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-953">11.1.1.</span></span> <span data-ttu-id="f2215-954">Уплотнение данных по использованию</span><span class="sxs-lookup"><span data-stu-id="f2215-954">Usage condenser</span></span>
<span data-ttu-id="f2215-955">Пользователи и элементы с небольшим числом точек использования могут создавать больше шума, чем информации.</span><span class="sxs-lookup"><span data-stu-id="f2215-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="f2215-956">Hello система пытается toopredict hello минимальное число точек использования каждого toobe пользователя или элемента, используемого в модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="f2215-957">Это число будет находиться в пределах диапазона hello, определенных hello ItemCutoffLowerBound и параметрах ItemCutoffUpperBound для hello диапазона, определенные hello UserCutOffLowerBound и UserCutoffUpperBound параметров для пользователей и элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="f2215-958">Hello конденсатор влияет на элементы или пользователей можно минимизировать путем настройки по крайней мере один из соответствующих границ toozero hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="f2215-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-959">11.1.2.</span></span> <span data-ttu-id="f2215-960">Параметры сборки рейтингов</span><span class="sxs-lookup"><span data-stu-id="f2215-960">Rank build parameters</span></span>
<span data-ttu-id="f2215-961">в следующей таблице Hello описывается hello параметров построения для ранжирования сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="f2215-962">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-962">Key</span></span> | <span data-ttu-id="f2215-963">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-963">Description</span></span> | <span data-ttu-id="f2215-964">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-964">Type</span></span> | <span data-ttu-id="f2215-965">Допустимое значение</span><span class="sxs-lookup"><span data-stu-id="f2215-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f2215-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="f2215-966">NumberOfModelIterations</span></span> |<span data-ttu-id="f2215-967">hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="f2215-968">большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени.</span><span class="sxs-lookup"><span data-stu-id="f2215-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="f2215-969">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-969">Integer</span></span> |<span data-ttu-id="f2215-970">10–50</span><span class="sxs-lookup"><span data-stu-id="f2215-970">10-50</span></span> |
| <span data-ttu-id="f2215-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="f2215-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="f2215-972">Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных.</span><span class="sxs-lookup"><span data-stu-id="f2215-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="f2215-973">Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры.</span><span class="sxs-lookup"><span data-stu-id="f2215-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="f2215-974">Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами.</span><span class="sxs-lookup"><span data-stu-id="f2215-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="f2215-975">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-975">Integer</span></span> |<span data-ttu-id="f2215-976">10-40</span><span class="sxs-lookup"><span data-stu-id="f2215-976">10-40</span></span> |
| <span data-ttu-id="f2215-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="f2215-978">Определяет нижнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-979">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-979">See usage condenser above.</span></span> |<span data-ttu-id="f2215-980">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-980">Integer</span></span> |<span data-ttu-id="f2215-981">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="f2215-983">Определяет верхнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-984">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-984">See usage condenser above.</span></span> |<span data-ttu-id="f2215-985">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-985">Integer</span></span> |<span data-ttu-id="f2215-986">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="f2215-988">Определяет hello пользователя нижнюю границу конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-989">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-989">See usage condenser above.</span></span> |<span data-ttu-id="f2215-990">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-990">Integer</span></span> |<span data-ttu-id="f2215-991">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="f2215-993">Определяет верхнюю границу пользователя hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-994">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-994">See usage condenser above.</span></span> |<span data-ttu-id="f2215-995">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-995">Integer</span></span> |<span data-ttu-id="f2215-996">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="f2215-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-997">11.1.3.</span></span> <span data-ttu-id="f2215-998">Параметры сборки рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-998">Recommendation build parameters</span></span>
<span data-ttu-id="f2215-999">в следующей таблице Hello описывается hello параметров построения для построения рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="f2215-1000">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-1000">Key</span></span> | <span data-ttu-id="f2215-1001">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-1001">Description</span></span> | <span data-ttu-id="f2215-1002">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-1002">Type</span></span> | <span data-ttu-id="f2215-1003">Допустимое значение</span><span class="sxs-lookup"><span data-stu-id="f2215-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f2215-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="f2215-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="f2215-1005">hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="f2215-1006">большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени.</span><span class="sxs-lookup"><span data-stu-id="f2215-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="f2215-1007">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1007">Integer</span></span> |<span data-ttu-id="f2215-1008">10–50</span><span class="sxs-lookup"><span data-stu-id="f2215-1008">10-50</span></span> |
| <span data-ttu-id="f2215-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="f2215-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="f2215-1010">Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных.</span><span class="sxs-lookup"><span data-stu-id="f2215-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="f2215-1011">Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры.</span><span class="sxs-lookup"><span data-stu-id="f2215-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="f2215-1012">Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами.</span><span class="sxs-lookup"><span data-stu-id="f2215-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="f2215-1013">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1013">Integer</span></span> |<span data-ttu-id="f2215-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="f2215-1014">10-40</span></span> |
| <span data-ttu-id="f2215-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="f2215-1016">Определяет нижнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-1017">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1017">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1018">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1018">Integer</span></span> |<span data-ttu-id="f2215-1019">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="f2215-1021">Определяет верхнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-1022">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1022">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1023">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1023">Integer</span></span> |<span data-ttu-id="f2215-1024">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="f2215-1026">Определяет hello пользователя нижнюю границу конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-1027">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1027">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1028">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1028">Integer</span></span> |<span data-ttu-id="f2215-1029">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="f2215-1031">Определяет верхнюю границу пользователя hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-1032">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1032">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1033">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1033">Integer</span></span> |<span data-ttu-id="f2215-1034">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1035">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-1035">Description</span></span> |<span data-ttu-id="f2215-1036">Описание сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1036">Build description.</span></span> |<span data-ttu-id="f2215-1037">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1037">String</span></span> |<span data-ttu-id="f2215-1038">Любой текст, максимум 512 символов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="f2215-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="f2215-1039">EnableModelingInsights</span></span> |<span data-ttu-id="f2215-1040">Позволяет toocompute метрики в модели рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="f2215-1041">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1041">Boolean</span></span> |<span data-ttu-id="f2215-1042">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1042">True/False</span></span> |
| <span data-ttu-id="f2215-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="f2215-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="f2215-1044">Указывает, если функции могут использоваться в модели рекомендаций hello tooenhance заказа.</span><span class="sxs-lookup"><span data-stu-id="f2215-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="f2215-1045">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1045">Boolean</span></span> |<span data-ttu-id="f2215-1046">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1046">True/False</span></span> |
| <span data-ttu-id="f2215-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="f2215-1047">ModelingFeatureList</span></span> |<span data-ttu-id="f2215-1048">Список разделенных запятыми toobe имена компонентов, используемых в построении hello рекомендация, в порядке tooenhance hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="f2215-1049">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1049">String</span></span> |<span data-ttu-id="f2215-1050">Имена компонентов, копирование too512 символов</span><span class="sxs-lookup"><span data-stu-id="f2215-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="f2215-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="f2215-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="f2215-1052">Указывает, если рекомендация hello также будет принудительно новых элементов через компонент подобия.</span><span class="sxs-lookup"><span data-stu-id="f2215-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="f2215-1053">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1053">Boolean</span></span> |<span data-ttu-id="f2215-1054">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1054">True/False</span></span> |
| <span data-ttu-id="f2215-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="f2215-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="f2215-1056">Указывает, можно ли использовать характеристику в обосновании.</span><span class="sxs-lookup"><span data-stu-id="f2215-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="f2215-1057">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1057">Boolean</span></span> |<span data-ttu-id="f2215-1058">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1058">True/False</span></span> |
| <span data-ttu-id="f2215-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="f2215-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="f2215-1060">Список разделенных запятыми toobe имена компонентов для рассуждения предложения (например описания рекомендации).</span><span class="sxs-lookup"><span data-stu-id="f2215-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="f2215-1061">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1061">String</span></span> |<span data-ttu-id="f2215-1062">Имена компонентов, копирование too512 символов</span><span class="sxs-lookup"><span data-stu-id="f2215-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="f2215-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="f2215-1063">EnableU2I</span></span> |<span data-ttu-id="f2215-1064">Разрешить так называемый hello персонализированных рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="f2215-1065">U2I (рекомендациями tooitem пользователя).</span><span class="sxs-lookup"><span data-stu-id="f2215-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="f2215-1066">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1066">Boolean</span></span> |<span data-ttu-id="f2215-1067">True или False (по умолчанию True)</span><span class="sxs-lookup"><span data-stu-id="f2215-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="f2215-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-1068">11.1.4.</span></span> <span data-ttu-id="f2215-1069">Параметры сборки FBT</span><span class="sxs-lookup"><span data-stu-id="f2215-1069">FBT build parameters</span></span>
<span data-ttu-id="f2215-1070">в следующей таблице Hello описывается hello параметров построения для построения рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="f2215-1071">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-1071">Key</span></span> | <span data-ttu-id="f2215-1072">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-1072">Description</span></span> | <span data-ttu-id="f2215-1073">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-1073">Type</span></span> | <span data-ttu-id="f2215-1074">Допустимое значение (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="f2215-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f2215-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="f2215-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="f2215-1076">Как модель консервативной hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1076">How conservative hello model is.</span></span> <span data-ttu-id="f2215-1077">Количество вхождений совместно для моделирования toobe элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="f2215-1078">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1078">Integer</span></span> |<span data-ttu-id="f2215-1079">3–50 (6)</span><span class="sxs-lookup"><span data-stu-id="f2215-1079">3-50 (6)</span></span> |
| <span data-ttu-id="f2215-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="f2215-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="f2215-1081">Количество элементов в наборе часто Здравствуйте, границ.</span><span class="sxs-lookup"><span data-stu-id="f2215-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="f2215-1082">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1082">Integer</span></span> |<span data-ttu-id="f2215-1083">2–3 (2)</span><span class="sxs-lookup"><span data-stu-id="f2215-1083">2-3 (2)</span></span> |
| <span data-ttu-id="f2215-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="f2215-1084">FbtMinimalScore</span></span> |<span data-ttu-id="f2215-1085">Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результаты.</span><span class="sxs-lookup"><span data-stu-id="f2215-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="f2215-1086">Hello выше hello лучше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1086">hello higher hello better.</span></span> |<span data-ttu-id="f2215-1087">Double</span><span class="sxs-lookup"><span data-stu-id="f2215-1087">Double</span></span> |<span data-ttu-id="f2215-1088">0 и выше (0)</span><span class="sxs-lookup"><span data-stu-id="f2215-1088">0 and above (0)</span></span> |
| <span data-ttu-id="f2215-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="f2215-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="f2215-1090">Определяет toobe функция подобия hello, используемые сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="f2215-1091">Serendipity, повышает вероятность точности прогнозов и сопутствующих вхождения повышает вероятность предсказуемость Жаккарда является хорошо компромисс между двумя hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="f2215-1092">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1092">String</span></span> |<span data-ttu-id="f2215-1093">cooccurrence, точность, jaccard (точность)</span><span class="sxs-lookup"><span data-stu-id="f2215-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="f2215-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-1094">11.2.</span></span> <span data-ttu-id="f2215-1095">Запуск сборки рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="f2215-1096">По умолчанию этот интерфейс API запускает сборку модели рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="f2215-1097">tootrigger ранг сборки (в порядке tooscore функции), следует использовать вариант API hello сборки с параметром типа сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="f2215-1098">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1098">HTTP Method</span></span> | <span data-ttu-id="f2215-1099">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1100">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1101">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="f2215-1102">ЗАГОЛОВОК</span><span class="sxs-lookup"><span data-stu-id="f2215-1102">HEADER</span></span> |<span data-ttu-id="f2215-1103">`"Content-Type", "text/xml"` (при отправке текста запроса)</span><span class="sxs-lookup"><span data-stu-id="f2215-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="f2215-1104">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1104">Parameter Name</span></span> | <span data-ttu-id="f2215-1105">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1106">modelId</span></span> |<span data-ttu-id="f2215-1107">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="f2215-1108">userDescription</span></span> |<span data-ttu-id="f2215-1109">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="f2215-1110">Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См.</span><span class="sxs-lookup"><span data-stu-id="f2215-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="f2215-1111">пример выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1111">See example above.</span></span><br><span data-ttu-id="f2215-1112">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-1112">Max length: 50</span></span> |
| <span data-ttu-id="f2215-1113">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1113">apiVersion</span></span> |<span data-ttu-id="f2215-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-1115">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-1115">Request Body</span></span> |<span data-ttu-id="f2215-1116">Если оставить пустым hello построения будет выполняться с параметры сборки по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="f2215-1117">Параметры сборки hello tooset следует отправьте параметры hello в XML-ФАЙЛЕ в текст hello как следующий образец hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="f2215-1118">(См. раздел hello «параметры построения» объяснение параметров hello).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="f2215-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="f2215-1119">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1119">**Response**:</span></span>

<span data-ttu-id="f2215-1120">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1121">Это асинхронный интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="f2215-1121">This is an asynchronous API.</span></span> <span data-ttu-id="f2215-1122">В качестве ответа вы получите идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="f2215-1123">tooknow после окончания сборки hello, следует вызвать API hello «Получить строит состояние из модели» и найдите этот идентификатор построения в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="f2215-1124">Обратите внимание, что сборка может занять от toohours минут в зависимости от размера данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="f2215-1125">Пока hello сборки завершается, не должны занимать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="f2215-1126">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1126">Valid build status:</span></span>

* <span data-ttu-id="f2215-1127">Create — запрос сборки был создан;</span><span class="sxs-lookup"><span data-stu-id="f2215-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="f2215-1128">Queued — запрос сборки был отправлен и поставлен в очередь;</span><span class="sxs-lookup"><span data-stu-id="f2215-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="f2215-1129">Building — выполняется сборка;</span><span class="sxs-lookup"><span data-stu-id="f2215-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="f2215-1130">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="f2215-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="f2215-1131">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="f2215-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="f2215-1132">Cancelled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="f2215-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="f2215-1133">Отмена - был отправлен запрос на отмену для построения hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="f2215-1134">Обратите внимание, hello пути не удается найти идентификатор сборки hello.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="f2215-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="f2215-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="f2215-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-1136">11.3.</span></span> <span data-ttu-id="f2215-1137">Запуск сборки (рекомендаций, рейтингов или FBT)</span><span class="sxs-lookup"><span data-stu-id="f2215-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="f2215-1138">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1138">HTTP Method</span></span> | <span data-ttu-id="f2215-1139">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1140">ПУБЛИКАЦИЯ</span><span class="sxs-lookup"><span data-stu-id="f2215-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1141">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="f2215-1142">ЗАГОЛОВОК</span><span class="sxs-lookup"><span data-stu-id="f2215-1142">HEADER</span></span> |<span data-ttu-id="f2215-1143">`"Content-Type", "text/xml"` (при отправке текста запроса)</span><span class="sxs-lookup"><span data-stu-id="f2215-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="f2215-1144">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1144">Parameter Name</span></span> | <span data-ttu-id="f2215-1145">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1146">modelId</span></span> |<span data-ttu-id="f2215-1147">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="f2215-1148">userDescription</span></span> |<span data-ttu-id="f2215-1149">Текстовому идентификатору hello каталога.</span><span class="sxs-lookup"><span data-stu-id="f2215-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="f2215-1150">Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См.</span><span class="sxs-lookup"><span data-stu-id="f2215-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="f2215-1151">пример выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1151">See example above.</span></span><br><span data-ttu-id="f2215-1152">Максимальная длина: 50</span><span class="sxs-lookup"><span data-stu-id="f2215-1152">Max length: 50</span></span> |
| <span data-ttu-id="f2215-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="f2215-1153">buildType</span></span> |<span data-ttu-id="f2215-1154">Тип tooinvoke hello сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="f2215-1155">– Recommendation — для сборки рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="f2215-1156">– Ranking — для сборки рейтинга.</span><span class="sxs-lookup"><span data-stu-id="f2215-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="f2215-1157">– Fbt — для сборки FBT.</span><span class="sxs-lookup"><span data-stu-id="f2215-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="f2215-1158">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1158">apiVersion</span></span> |<span data-ttu-id="f2215-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-1160">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-1160">Request Body</span></span> |<span data-ttu-id="f2215-1161">Если оставить пустым hello построения будет выполняться с параметры сборки по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="f2215-1162">Параметры сборки tooset, отправьте их в XML-ФАЙЛЕ в текст hello, как и в следующий образец hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="f2215-1163">(См. раздел hello «параметры построения» содержатся пояснения и полный список параметров hello).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="f2215-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="f2215-1164">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1164">**Response**:</span></span>

<span data-ttu-id="f2215-1165">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1166">Это асинхронный интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="f2215-1166">This is an asynchronous API.</span></span> <span data-ttu-id="f2215-1167">В качестве ответа вы получите идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="f2215-1168">tooknow после окончания сборки hello, следует вызвать API hello «Получить строит состояние из модели» и найдите этот идентификатор построения в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="f2215-1169">Обратите внимание, что сборка может занять от toohours минут в зависимости от размера данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="f2215-1170">Пока hello сборки завершается, не должны занимать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="f2215-1171">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1171">Valid build status:</span></span>

* <span data-ttu-id="f2215-1172">Create — модель создана;</span><span class="sxs-lookup"><span data-stu-id="f2215-1172">Create - Model was created.</span></span>
* <span data-ttu-id="f2215-1173">Queued — сборка модели запущена и поставлена в очередь;</span><span class="sxs-lookup"><span data-stu-id="f2215-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="f2215-1174">Building — сборка модели выполняется;</span><span class="sxs-lookup"><span data-stu-id="f2215-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="f2215-1175">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="f2215-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="f2215-1176">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="f2215-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="f2215-1177">Cancelled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="f2215-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="f2215-1178">Cancelling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="f2215-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="f2215-1179">Обратите внимание, hello пути не удается найти идентификатор сборки hello.`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="f2215-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="f2215-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="f2215-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-1181">11.4.</span></span> <span data-ttu-id="f2215-1182">Получение статусов сборок модели</span><span class="sxs-lookup"><span data-stu-id="f2215-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="f2215-1183">Извлекает сборки определенной модели с указанием их состояния.</span><span class="sxs-lookup"><span data-stu-id="f2215-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="f2215-1184">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1184">HTTP Method</span></span> | <span data-ttu-id="f2215-1185">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1186">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1187">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1188">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1188">Parameter Name</span></span> | <span data-ttu-id="f2215-1189">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1190">modelId</span></span> |<span data-ttu-id="f2215-1191">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="f2215-1192">onlyLastBuild</span></span> |<span data-ttu-id="f2215-1193">Указывает ли все hello tooreturn строить журнал hello модели или только hello состояние последнего построения hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="f2215-1194">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1194">apiVersion</span></span> |<span data-ttu-id="f2215-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1195">1.0</span></span> |

<span data-ttu-id="f2215-1196">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1196">**Response**:</span></span>

<span data-ttu-id="f2215-1197">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1198">Hello ответ включает одной записи для каждого построения.</span><span class="sxs-lookup"><span data-stu-id="f2215-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="f2215-1199">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1200">`feed/entry/content/properties/UserName`— Имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="f2215-1201">`feed/entry/content/properties/ModelName`-Имя модели hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="f2215-1202">`feed/entry/content/properties/ModelId` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="f2215-1203">`feed/entry/content/properties/IsDeployed`-Сборки hello развернут ли (так)</span><span class="sxs-lookup"><span data-stu-id="f2215-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="f2215-1204">активная сборка).</span><span class="sxs-lookup"><span data-stu-id="f2215-1204">active build).</span></span>
* <span data-ttu-id="f2215-1205">`feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="f2215-1206">`feed/entry/content/properties/BuildType`-Тип сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="f2215-1207">`feed/entry/content/properties/Status` — состояние сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="f2215-1208">Может принимать одно из следующих hello: ошибка, построение, в очереди, отменяется, отменено, успех.</span><span class="sxs-lookup"><span data-stu-id="f2215-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="f2215-1209">`feed/entry/content/properties/StatusMessage`-Сообщение сведения о состоянии (применяется только toospecific состояния).</span><span class="sxs-lookup"><span data-stu-id="f2215-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="f2215-1210">`feed/entry/content/properties/Progress` — ход выполнения сборки (%).</span><span class="sxs-lookup"><span data-stu-id="f2215-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="f2215-1211">`feed/entry/content/properties/StartTime` — время начала сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="f2215-1212">`feed/entry/content/properties/EndTime` — время окончания сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="f2215-1213">`feed/entry/content/properties/ExecutionTime` — длительность сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="f2215-1214">`feed/entry/content/properties/ProgressStep`— Сведения о текущей стадии hello построения выполняется.</span><span class="sxs-lookup"><span data-stu-id="f2215-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="f2215-1215">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1215">Valid build status:</span></span>

* <span data-ttu-id="f2215-1216">Created — запись запроса сборки создана;</span><span class="sxs-lookup"><span data-stu-id="f2215-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="f2215-1217">Queued — запрос сборки инициирован и помещен в очередь;</span><span class="sxs-lookup"><span data-stu-id="f2215-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="f2215-1218">Building — сборка выполняется;</span><span class="sxs-lookup"><span data-stu-id="f2215-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="f2215-1219">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="f2215-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="f2215-1220">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="f2215-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="f2215-1221">Cancelled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="f2215-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="f2215-1222">Cancelling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="f2215-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="f2215-1223">Допустимые значения типа сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1223">Valid values for build type:</span></span>

* <span data-ttu-id="f2215-1224">Rank — сборка рейтинга;</span><span class="sxs-lookup"><span data-stu-id="f2215-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="f2215-1225">Recommendation — сборка рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="f2215-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="f2215-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="f2215-1227">11.5.</span></span> <span data-ttu-id="f2215-1228">Получение состояний сборок</span><span class="sxs-lookup"><span data-stu-id="f2215-1228">Get Builds Status</span></span>
<span data-ttu-id="f2215-1229">Извлекает состояния сборок всех моделей пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="f2215-1230">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1230">HTTP Method</span></span> | <span data-ttu-id="f2215-1231">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1232">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1233">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1234">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1234">Parameter Name</span></span> | <span data-ttu-id="f2215-1235">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="f2215-1236">onlyLastBuild</span></span> |<span data-ttu-id="f2215-1237">Указывает ли все hello tooreturn строить журнал hello модели или только состояние hello hello последнюю сборку.</span><span class="sxs-lookup"><span data-stu-id="f2215-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="f2215-1238">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1238">apiVersion</span></span> |<span data-ttu-id="f2215-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1239">1.0</span></span> |

<span data-ttu-id="f2215-1240">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1240">**Response**:</span></span>

<span data-ttu-id="f2215-1241">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1242">Hello ответ включает одной записи для каждого построения.</span><span class="sxs-lookup"><span data-stu-id="f2215-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="f2215-1243">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1244">`feed/entry/content/properties/UserName`— Имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="f2215-1245">`feed/entry/content/properties/ModelName`-Имя модели hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="f2215-1246">`feed/entry/content/properties/ModelId` — уникальный идентификатор модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="f2215-1247">`feed/entry/content/properties/IsDeployed`-Ли hello сборка развертывается.</span><span class="sxs-lookup"><span data-stu-id="f2215-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="f2215-1248">`feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="f2215-1249">`feed/entry/content/properties/BuildType`-Тип сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="f2215-1250">`feed/entry/content/properties/Status` — состояние сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="f2215-1251">Может принимать одно из следующих hello: ошибка, построение, в очереди, отменено, отменяется, успех.</span><span class="sxs-lookup"><span data-stu-id="f2215-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="f2215-1252">`feed/entry/content/properties/StatusMessage`-Сообщение сведения о состоянии (применяется только toospecific состояния).</span><span class="sxs-lookup"><span data-stu-id="f2215-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="f2215-1253">`feed/entry/content/properties/Progress` — ход выполнения сборки (%).</span><span class="sxs-lookup"><span data-stu-id="f2215-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="f2215-1254">`feed/entry/content/properties/StartTime` — время начала сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="f2215-1255">`feed/entry/content/properties/EndTime` — время окончания сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="f2215-1256">`feed/entry/content/properties/ExecutionTime` — длительность сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="f2215-1257">`feed/entry/content/properties/ProgressStep`— Сведения о текущей стадии hello построения выполняется.</span><span class="sxs-lookup"><span data-stu-id="f2215-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="f2215-1258">Допустимые состояния сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1258">Valid build status:</span></span>

* <span data-ttu-id="f2215-1259">Created — запись запроса сборки создана;</span><span class="sxs-lookup"><span data-stu-id="f2215-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="f2215-1260">Queued — запрос сборки инициирован и помещен в очередь;</span><span class="sxs-lookup"><span data-stu-id="f2215-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="f2215-1261">Building — сборка выполняется;</span><span class="sxs-lookup"><span data-stu-id="f2215-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="f2215-1262">Success — сборка успешно завершилась;</span><span class="sxs-lookup"><span data-stu-id="f2215-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="f2215-1263">Error — сборка завершилась сбоем;</span><span class="sxs-lookup"><span data-stu-id="f2215-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="f2215-1264">Cancelled — сборка отменена;</span><span class="sxs-lookup"><span data-stu-id="f2215-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="f2215-1265">Cancelling — сборка отменяется.</span><span class="sxs-lookup"><span data-stu-id="f2215-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="f2215-1266">Допустимые значения типа сборки:</span><span class="sxs-lookup"><span data-stu-id="f2215-1266">Valid values for build type:</span></span>

* <span data-ttu-id="f2215-1267">Rank — сборка рейтинга;</span><span class="sxs-lookup"><span data-stu-id="f2215-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="f2215-1268">Recommendation — сборка рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="f2215-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="f2215-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="f2215-1270">11.6.</span></span> <span data-ttu-id="f2215-1271">Удаление сборки</span><span class="sxs-lookup"><span data-stu-id="f2215-1271">Delete Build</span></span>
<span data-ttu-id="f2215-1272">Удаление сборки</span><span class="sxs-lookup"><span data-stu-id="f2215-1272">Deletes a build.</span></span>

<span data-ttu-id="f2215-1273">Примечание.</span><span class="sxs-lookup"><span data-stu-id="f2215-1273">NOTE:</span></span> <br><span data-ttu-id="f2215-1274">Активные сборки не удаляются.</span><span class="sxs-lookup"><span data-stu-id="f2215-1274">You cannot delete an active build.</span></span> <span data-ttu-id="f2215-1275">Hello модели должен быть обновлен tooa другого активного построения перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="f2215-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="f2215-1276">Выполняющуюся сборку нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="f2215-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="f2215-1277">Сначала отмените hello сборки путем вызова <strong>отменить построение</strong>.</span><span class="sxs-lookup"><span data-stu-id="f2215-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="f2215-1278">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1278">HTTP Method</span></span> | <span data-ttu-id="f2215-1279">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1280">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1281">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1282">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1282">Parameter Name</span></span> | <span data-ttu-id="f2215-1283">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1284">buildId</span></span> |<span data-ttu-id="f2215-1285">Уникальный идентификатор сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="f2215-1286">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1286">apiVersion</span></span> |<span data-ttu-id="f2215-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1287">1.0</span></span> |

<span data-ttu-id="f2215-1288">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1288">**Response:**</span></span>

<span data-ttu-id="f2215-1289">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="f2215-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="f2215-1290">11.7.</span></span> <span data-ttu-id="f2215-1291">Отмена сборки</span><span class="sxs-lookup"><span data-stu-id="f2215-1291">Cancel Build</span></span>
<span data-ttu-id="f2215-1292">Отменяет выполняющуюся сборку.</span><span class="sxs-lookup"><span data-stu-id="f2215-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="f2215-1293">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1293">HTTP Method</span></span> | <span data-ttu-id="f2215-1294">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1295">ОТПРАВКА</span><span class="sxs-lookup"><span data-stu-id="f2215-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1296">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1297">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1297">Parameter Name</span></span> | <span data-ttu-id="f2215-1298">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1299">buildId</span></span> |<span data-ttu-id="f2215-1300">Уникальный идентификатор сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="f2215-1301">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1301">apiVersion</span></span> |<span data-ttu-id="f2215-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1302">1.0</span></span> |

<span data-ttu-id="f2215-1303">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1303">**Response:**</span></span>

<span data-ttu-id="f2215-1304">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="f2215-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="f2215-1305">11.8.</span></span> <span data-ttu-id="f2215-1306">Получение параметров сборки</span><span class="sxs-lookup"><span data-stu-id="f2215-1306">Get Build Parameters</span></span>
<span data-ttu-id="f2215-1307">Извлекает параметры сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="f2215-1308">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1308">HTTP Method</span></span> | <span data-ttu-id="f2215-1309">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1310">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1311">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1312">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1312">Parameter Name</span></span> | <span data-ttu-id="f2215-1313">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1314">buildId</span></span> |<span data-ttu-id="f2215-1315">Уникальный идентификатор сборки hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="f2215-1316">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1316">apiVersion</span></span> |<span data-ttu-id="f2215-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1317">1.0</span></span> |

<span data-ttu-id="f2215-1318">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1318">**Response:**</span></span>

<span data-ttu-id="f2215-1319">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1320">Этот интерфейс API возвращает коллекцию элементов "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="f2215-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="f2215-1321">Каждый элемент представляет параметр и его значение:</span><span class="sxs-lookup"><span data-stu-id="f2215-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="f2215-1322">`feed/entry/content/properties/Key` — имя параметра сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="f2215-1323">`feed/entry/content/properties/Value` — значение параметра сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="f2215-1324">в следующей таблице Hello описывается hello значение, представляющее каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="f2215-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="f2215-1325">Ключ</span><span class="sxs-lookup"><span data-stu-id="f2215-1325">Key</span></span> | <span data-ttu-id="f2215-1326">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-1326">Description</span></span> | <span data-ttu-id="f2215-1327">Тип</span><span class="sxs-lookup"><span data-stu-id="f2215-1327">Type</span></span> | <span data-ttu-id="f2215-1328">Допустимое значение</span><span class="sxs-lookup"><span data-stu-id="f2215-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f2215-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="f2215-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="f2215-1330">hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="f2215-1331">большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени.</span><span class="sxs-lookup"><span data-stu-id="f2215-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="f2215-1332">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1332">Integer</span></span> |<span data-ttu-id="f2215-1333">10–50</span><span class="sxs-lookup"><span data-stu-id="f2215-1333">10-50</span></span> |
| <span data-ttu-id="f2215-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="f2215-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="f2215-1335">Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных.</span><span class="sxs-lookup"><span data-stu-id="f2215-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="f2215-1336">Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры.</span><span class="sxs-lookup"><span data-stu-id="f2215-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="f2215-1337">Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами.</span><span class="sxs-lookup"><span data-stu-id="f2215-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="f2215-1338">Целое число </span><span class="sxs-lookup"><span data-stu-id="f2215-1338">Integer</span></span> |<span data-ttu-id="f2215-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="f2215-1339">10-40</span></span> |
| <span data-ttu-id="f2215-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="f2215-1341">Определяет нижнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-1342">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1342">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1343">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1343">Integer</span></span> |<span data-ttu-id="f2215-1344">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="f2215-1346">Определяет верхнюю границу элемента hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-1347">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1347">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1348">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1348">Integer</span></span> |<span data-ttu-id="f2215-1349">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="f2215-1351">Определяет hello пользователя нижнюю границу конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="f2215-1352">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1352">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1353">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1353">Integer</span></span> |<span data-ttu-id="f2215-1354">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="f2215-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="f2215-1356">Определяет верхнюю границу пользователя hello конденсатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="f2215-1357">См. раздел, посвященный уплотнению данных по использованию, выше.</span><span class="sxs-lookup"><span data-stu-id="f2215-1357">See usage condenser above.</span></span> |<span data-ttu-id="f2215-1358">Число</span><span class="sxs-lookup"><span data-stu-id="f2215-1358">Integer</span></span> |<span data-ttu-id="f2215-1359">2 или более (0 — отключить уплотнение)</span><span class="sxs-lookup"><span data-stu-id="f2215-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="f2215-1360">Описание</span><span class="sxs-lookup"><span data-stu-id="f2215-1360">Description</span></span> |<span data-ttu-id="f2215-1361">Описание сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1361">Build description.</span></span> |<span data-ttu-id="f2215-1362">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1362">String</span></span> |<span data-ttu-id="f2215-1363">Любой текст, максимум 512 символов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="f2215-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="f2215-1364">EnableModelingInsights</span></span> |<span data-ttu-id="f2215-1365">Позволяет toocompute метрики в модели рекомендаций hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="f2215-1366">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1366">Boolean</span></span> |<span data-ttu-id="f2215-1367">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1367">True/False</span></span> |
| <span data-ttu-id="f2215-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="f2215-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="f2215-1369">Указывает, если функции могут использоваться в модели рекомендаций hello tooenhance заказа.</span><span class="sxs-lookup"><span data-stu-id="f2215-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="f2215-1370">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1370">Boolean</span></span> |<span data-ttu-id="f2215-1371">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1371">True/False</span></span> |
| <span data-ttu-id="f2215-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="f2215-1372">ModelingFeatureList</span></span> |<span data-ttu-id="f2215-1373">Список разделенных запятыми toobe имена компонентов, используемых в построении hello рекомендация, в порядке tooenhance hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="f2215-1374">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1374">String</span></span> |<span data-ttu-id="f2215-1375">Имена компонентов, копирование too512 символов</span><span class="sxs-lookup"><span data-stu-id="f2215-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="f2215-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="f2215-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="f2215-1377">Указывает, если рекомендация hello также будет принудительно новых элементов через компонент подобия.</span><span class="sxs-lookup"><span data-stu-id="f2215-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="f2215-1378">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1378">Boolean</span></span> |<span data-ttu-id="f2215-1379">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1379">True/False</span></span> |
| <span data-ttu-id="f2215-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="f2215-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="f2215-1381">Указывает, можно ли использовать характеристику в обосновании.</span><span class="sxs-lookup"><span data-stu-id="f2215-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="f2215-1382">Логический</span><span class="sxs-lookup"><span data-stu-id="f2215-1382">Boolean</span></span> |<span data-ttu-id="f2215-1383">True или False</span><span class="sxs-lookup"><span data-stu-id="f2215-1383">True/False</span></span> |
| <span data-ttu-id="f2215-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="f2215-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="f2215-1385">Список разделенных запятыми toobe имена компонентов для рассуждения предложения (например описания рекомендации).</span><span class="sxs-lookup"><span data-stu-id="f2215-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="f2215-1386">Строка</span><span class="sxs-lookup"><span data-stu-id="f2215-1386">String</span></span> |<span data-ttu-id="f2215-1387">Имена компонентов, копирование too512 символов</span><span class="sxs-lookup"><span data-stu-id="f2215-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="f2215-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="f2215-1389">12. Рекомендации</span><span class="sxs-lookup"><span data-stu-id="f2215-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="f2215-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1390">12.1.</span></span> <span data-ttu-id="f2215-1391">Получение рекомендаций по элементам (для активной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="f2215-1392">Узнать hello active построения типа «Рекомендации» или «Взноса по» на основе списка элементов начальные значения (input).</span><span class="sxs-lookup"><span data-stu-id="f2215-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="f2215-1393">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1393">HTTP Method</span></span> | <span data-ttu-id="f2215-1394">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1395">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1396">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1397">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1397">Parameter Name</span></span> | <span data-ttu-id="f2215-1398">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1399">modelId</span></span> |<span data-ttu-id="f2215-1400">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="f2215-1401">itemIds</span></span> |<span data-ttu-id="f2215-1402">Список разделенных запятыми hello toorecommend элементы для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="f2215-1403">Если активный сборки hello имеет тип взноса по, затем можно передать только один элемент.</span><span class="sxs-lookup"><span data-stu-id="f2215-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="f2215-1404">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1404">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1405">numberOfResults</span></span> |<span data-ttu-id="f2215-1406">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1406">Number of required results</span></span> <br> <span data-ttu-id="f2215-1407">Макс. 150</span><span class="sxs-lookup"><span data-stu-id="f2215-1407">Max: 150</span></span> |
| <span data-ttu-id="f2215-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1408">includeMetatadata</span></span> |<span data-ttu-id="f2215-1409">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1409">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1410">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1410">apiVersion</span></span> |<span data-ttu-id="f2215-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1411">1.0</span></span> |

<span data-ttu-id="f2215-1412">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1412">**Response:**</span></span>

<span data-ttu-id="f2215-1413">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1414">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1415">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1416">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1417">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1418">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1419">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1420">Пример ответа Hello ниже включает 10 рекомендуемые элементы.</span><span class="sxs-lookup"><span data-stu-id="f2215-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="f2215-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="f2215-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-1422">12.2.</span></span> <span data-ttu-id="f2215-1423">Получение рекомендаций по элементам (для определенной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="f2215-1424">Получение рекомендаций определенной сборки типа Recommendation или Fbt.</span><span class="sxs-lookup"><span data-stu-id="f2215-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="f2215-1425">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1425">HTTP Method</span></span> | <span data-ttu-id="f2215-1426">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1427">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1428">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1429">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1429">Parameter Name</span></span> | <span data-ttu-id="f2215-1430">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1431">modelId</span></span> |<span data-ttu-id="f2215-1432">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="f2215-1433">itemIds</span></span> |<span data-ttu-id="f2215-1434">Список разделенных запятыми hello toorecommend элементы для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="f2215-1435">Если активный сборки hello имеет тип взноса по, затем можно передать только один элемент.</span><span class="sxs-lookup"><span data-stu-id="f2215-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="f2215-1436">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1436">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1437">numberOfResults</span></span> |<span data-ttu-id="f2215-1438">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1438">Number of required results</span></span> <br> <span data-ttu-id="f2215-1439">Макс. 150</span><span class="sxs-lookup"><span data-stu-id="f2215-1439">Max: 150</span></span> |
| <span data-ttu-id="f2215-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1440">includeMetatadata</span></span> |<span data-ttu-id="f2215-1441">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1441">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1442">buildId</span></span> |<span data-ttu-id="f2215-1443">Hello построения toouse идентификатор для этого запроса рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="f2215-1444">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1444">apiVersion</span></span> |<span data-ttu-id="f2215-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1445">1.0</span></span> |

<span data-ttu-id="f2215-1446">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1446">**Response:**</span></span>

<span data-ttu-id="f2215-1447">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1448">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1449">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1450">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1451">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1452">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1453">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1454">Пример ответа см. в подразделе 12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="f2215-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-1455">12.3.</span></span> <span data-ttu-id="f2215-1456">Получение рекомендаций FBT (для активной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="f2215-1457">Получите рекомендации hello active построения типа взноса» по» на основе начального значения (input) элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="f2215-1458">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1458">HTTP Method</span></span> | <span data-ttu-id="f2215-1459">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1460">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1461">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1462">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1462">Parameter Name</span></span> | <span data-ttu-id="f2215-1463">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1464">modelId</span></span> |<span data-ttu-id="f2215-1465">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="f2215-1466">itemId</span></span> |<span data-ttu-id="f2215-1467">Элемент toorecommend для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="f2215-1468">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1468">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1469">numberOfResults</span></span> |<span data-ttu-id="f2215-1470">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1470">Number of required results</span></span> <br><span data-ttu-id="f2215-1471">Макс. 150</span><span class="sxs-lookup"><span data-stu-id="f2215-1471">Max: 150</span></span> |
| <span data-ttu-id="f2215-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="f2215-1472">minimalScore</span></span> |<span data-ttu-id="f2215-1473">Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результатов</span><span class="sxs-lookup"><span data-stu-id="f2215-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="f2215-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1474">includeMetatadata</span></span> |<span data-ttu-id="f2215-1475">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1475">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1476">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1476">apiVersion</span></span> |<span data-ttu-id="f2215-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1477">1.0</span></span> |

<span data-ttu-id="f2215-1478">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1478">**Response:**</span></span>

<span data-ttu-id="f2215-1479">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1480">Hello ответ включает одной записи для каждого набора рекомендуемых элементов (набор элементов, которые обычно купил вместе с элемента начального значения и входных hello).</span><span class="sxs-lookup"><span data-stu-id="f2215-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="f2215-1481">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1482">`Feed\entry\content\properties\Id1` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1483">`Feed\entry\content\properties\Name1`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1484">`Feed\entry\content\properties\Id2` — идентификатор второго рекомендованного элемента (необязательно).</span><span class="sxs-lookup"><span data-stu-id="f2215-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="f2215-1485">`Feed\entry\content\properties\Name2`-Имя hello 2-й элемент (необязательно).</span><span class="sxs-lookup"><span data-stu-id="f2215-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="f2215-1486">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1487">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1488">Пример ответа Hello ниже включает три набора рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="f2215-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="f2215-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="f2215-1490">12.4.</span></span> <span data-ttu-id="f2215-1491">Получение рекомендаций FBT (для определенной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="f2215-1492">Получение рекомендаций типа Fbt для определенной сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="f2215-1493">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1493">HTTP Method</span></span> | <span data-ttu-id="f2215-1494">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1495">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1496">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1497">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1497">Parameter Name</span></span> | <span data-ttu-id="f2215-1498">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1499">modelId</span></span> |<span data-ttu-id="f2215-1500">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="f2215-1501">itemId</span></span> |<span data-ttu-id="f2215-1502">Элемент toorecommend для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="f2215-1503">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1503">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1504">numberOfResults</span></span> |<span data-ttu-id="f2215-1505">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1505">Number of required results</span></span> <br><span data-ttu-id="f2215-1506">Макс. 150</span><span class="sxs-lookup"><span data-stu-id="f2215-1506">Max: 150</span></span> |
| <span data-ttu-id="f2215-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="f2215-1507">minimalScore</span></span> |<span data-ttu-id="f2215-1508">Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результатов</span><span class="sxs-lookup"><span data-stu-id="f2215-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="f2215-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1509">includeMetatadata</span></span> |<span data-ttu-id="f2215-1510">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1510">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1511">buildId</span></span> |<span data-ttu-id="f2215-1512">Hello построения toouse идентификатор для этого запроса рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="f2215-1513">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1513">apiVersion</span></span> |<span data-ttu-id="f2215-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1514">1.0</span></span> |

<span data-ttu-id="f2215-1515">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1515">**Response:**</span></span>

<span data-ttu-id="f2215-1516">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1517">Hello ответ включает одной записи для каждого набора рекомендуемых элементов (набор элементов, которые обычно купил вместе с элемента начального значения и входных hello).</span><span class="sxs-lookup"><span data-stu-id="f2215-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="f2215-1518">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1519">`Feed\entry\content\properties\Id1` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1520">`Feed\entry\content\properties\Name1`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1521">`Feed\entry\content\properties\Id2` — идентификатор второго рекомендованного элемента (необязательно).</span><span class="sxs-lookup"><span data-stu-id="f2215-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="f2215-1522">`Feed\entry\content\properties\Name2`-Имя hello 2-й элемент (необязательно).</span><span class="sxs-lookup"><span data-stu-id="f2215-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="f2215-1523">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1524">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1525">Пример ответа см. в подразделе 12.3.</span><span class="sxs-lookup"><span data-stu-id="f2215-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="f2215-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="f2215-1526">12.5.</span></span> <span data-ttu-id="f2215-1527">Получение пользовательских рекомендаций (для активной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="f2215-1528">Получение пользовательских рекомендаций для сборки типа Recommendation, отмеченной как активная сборка.</span><span class="sxs-lookup"><span data-stu-id="f2215-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="f2215-1529">Возвращает список прогнозируемый элемент, историю использования toohello hello пользователя в соответствии с Hello API.</span><span class="sxs-lookup"><span data-stu-id="f2215-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="f2215-1530">Примечания:</span><span class="sxs-lookup"><span data-stu-id="f2215-1530">Notes:</span></span> 

1. <span data-ttu-id="f2215-1531">Для сборки FBT нет пользовательских рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="f2215-1532">Если построение hello active — взноса по, этот метод завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f2215-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="f2215-1533">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1533">HTTP Method</span></span> | <span data-ttu-id="f2215-1534">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1535">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1536">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1537">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1537">Parameter Name</span></span> | <span data-ttu-id="f2215-1538">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1539">modelId</span></span> |<span data-ttu-id="f2215-1540">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1541">userId</span><span class="sxs-lookup"><span data-stu-id="f2215-1541">userId</span></span> |<span data-ttu-id="f2215-1542">Уникальный идентификатор пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="f2215-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1543">numberOfResults</span></span> |<span data-ttu-id="f2215-1544">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1544">Number of required results</span></span> |
| <span data-ttu-id="f2215-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1545">includeMetatadata</span></span> |<span data-ttu-id="f2215-1546">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1546">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1547">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1547">apiVersion</span></span> |<span data-ttu-id="f2215-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1548">1.0</span></span> |

<span data-ttu-id="f2215-1549">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1549">**Response:**</span></span>

<span data-ttu-id="f2215-1550">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1551">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1552">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1553">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1554">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1555">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1556">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1557">Пример ответа см. в подразделе 12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="f2215-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="f2215-1558">12.6.</span></span> <span data-ttu-id="f2215-1559">Получение пользовательских рекомендаций со списком элементов (для активной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="f2215-1560">Получение пользовательских рекомендаций для сборки типа Recommendation, отмеченной как активная сборка, с дополнительным списком элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="f2215-1561">Hello API вернет список прогнозируемый элемент, в соответствии с Хронология использования toohello пользователя hello и hello дополнительных указанных элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="f2215-1562">Примечания:</span><span class="sxs-lookup"><span data-stu-id="f2215-1562">Notes:</span></span> 

1. <span data-ttu-id="f2215-1563">Для сборки FBT нет пользовательских рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="f2215-1564">Если построение hello active — взноса по, этот метод завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="f2215-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="f2215-1565">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1565">HTTP Method</span></span> | <span data-ttu-id="f2215-1566">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1567">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1568">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1569">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1569">Parameter Name</span></span> | <span data-ttu-id="f2215-1570">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1571">modelId</span></span> |<span data-ttu-id="f2215-1572">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1573">userId</span><span class="sxs-lookup"><span data-stu-id="f2215-1573">userId</span></span> |<span data-ttu-id="f2215-1574">Уникальный идентификатор пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="f2215-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="f2215-1575">itemsIds</span></span> |<span data-ttu-id="f2215-1576">Список разделенных запятыми hello toorecommend элементы для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="f2215-1577">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1577">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1578">numberOfResults</span></span> |<span data-ttu-id="f2215-1579">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1579">Number of required results</span></span> |
| <span data-ttu-id="f2215-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1580">includeMetatadata</span></span> |<span data-ttu-id="f2215-1581">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1581">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1582">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1582">apiVersion</span></span> |<span data-ttu-id="f2215-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1583">1.0</span></span> |

<span data-ttu-id="f2215-1584">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1584">**Response:**</span></span>

<span data-ttu-id="f2215-1585">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1586">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1587">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1588">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1589">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1590">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1591">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1592">Пример ответа см. в подразделе 12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="f2215-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="f2215-1593">12.7.</span></span> <span data-ttu-id="f2215-1594">Получение пользовательских рекомендаций (для определенной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="f2215-1595">Получение пользовательских рекомендаций для определенной сборки типа Recommendation.</span><span class="sxs-lookup"><span data-stu-id="f2215-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="f2215-1596">Возвращает список прогнозируемый элемент, историю использования toohello hello пользователя (используется в конкретной сборке hello) в соответствии с Hello API.</span><span class="sxs-lookup"><span data-stu-id="f2215-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="f2215-1597">Примечание. Для сборки FBT нет пользовательских рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="f2215-1598">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1598">HTTP Method</span></span> | <span data-ttu-id="f2215-1599">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1600">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1601">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1602">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1602">Parameter Name</span></span> | <span data-ttu-id="f2215-1603">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1604">modelId</span></span> |<span data-ttu-id="f2215-1605">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1606">userId</span><span class="sxs-lookup"><span data-stu-id="f2215-1606">userId</span></span> |<span data-ttu-id="f2215-1607">Уникальный идентификатор пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="f2215-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1608">numberOfResults</span></span> |<span data-ttu-id="f2215-1609">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1609">Number of required results</span></span> |
| <span data-ttu-id="f2215-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1610">includeMetatadata</span></span> |<span data-ttu-id="f2215-1611">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1611">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1612">buildId</span></span> |<span data-ttu-id="f2215-1613">Hello построения toouse идентификатор для этого запроса рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="f2215-1614">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1614">apiVersion</span></span> |<span data-ttu-id="f2215-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1615">1.0</span></span> |

<span data-ttu-id="f2215-1616">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1616">**Response:**</span></span>

<span data-ttu-id="f2215-1617">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1618">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1619">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1620">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1621">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1622">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1623">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1624">Пример ответа см. в подразделе 12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="f2215-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="f2215-1625">12.8.</span></span> <span data-ttu-id="f2215-1626">Получение пользовательских рекомендаций со списком элементов (для определенной сборки)</span><span class="sxs-lookup"><span data-stu-id="f2215-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="f2215-1627">Получите рекомендации пользователя определенного построения типа «Рекомендации» и hello список дополнительных элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="f2215-1628">Возвращает список прогнозируемого товара, журнал использования toohello пользователя hello и hello дополнительный список из элементов в соответствии с Hello API.</span><span class="sxs-lookup"><span data-stu-id="f2215-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="f2215-1629">Примечание. Для сборки FBT нет пользовательских рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="f2215-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="f2215-1630">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1630">HTTP Method</span></span> | <span data-ttu-id="f2215-1631">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1632">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1633">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1634">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1634">Parameter Name</span></span> | <span data-ttu-id="f2215-1635">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1636">modelId</span></span> |<span data-ttu-id="f2215-1637">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1638">userId</span><span class="sxs-lookup"><span data-stu-id="f2215-1638">userId</span></span> |<span data-ttu-id="f2215-1639">Уникальный идентификатор пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="f2215-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="f2215-1640">itemIds</span></span> |<span data-ttu-id="f2215-1641">Список разделенных запятыми hello toorecommend элементы для.</span><span class="sxs-lookup"><span data-stu-id="f2215-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="f2215-1642">Максимальная длина: 1024</span><span class="sxs-lookup"><span data-stu-id="f2215-1642">Max length: 1024</span></span> |
| <span data-ttu-id="f2215-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f2215-1643">numberOfResults</span></span> |<span data-ttu-id="f2215-1644">Требуемое число результатов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1644">Number of required results</span></span> |
| <span data-ttu-id="f2215-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f2215-1645">includeMetatadata</span></span> |<span data-ttu-id="f2215-1646">Для использования в будущем, всегда имеет значение false</span><span class="sxs-lookup"><span data-stu-id="f2215-1646">Future use, always false</span></span> |
| <span data-ttu-id="f2215-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1647">buildId</span></span> |<span data-ttu-id="f2215-1648">Hello построения toouse идентификатор для этого запроса рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2215-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="f2215-1649">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1649">apiVersion</span></span> |<span data-ttu-id="f2215-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1650">1.0</span></span> |

<span data-ttu-id="f2215-1651">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1651">**Response:**</span></span>

<span data-ttu-id="f2215-1652">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1653">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1654">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1655">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1656">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1657">`Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.</span><span class="sxs-lookup"><span data-stu-id="f2215-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f2215-1658">`Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).</span><span class="sxs-lookup"><span data-stu-id="f2215-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="f2215-1659">Пример ответа см. в подразделе 12.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="f2215-1660">13. Журнал работы пользователей</span><span class="sxs-lookup"><span data-stu-id="f2215-1660">13. User Usage History</span></span>
<span data-ttu-id="f2215-1661">После построения модели рекомендаций был hello система позволит tooretrieve hello журнал пользователей (элементов связанного tooa пользователя) используется для построения hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="f2215-1662">Этот API разрешить tooretrieve hello пользовательского журнала</span><span class="sxs-lookup"><span data-stu-id="f2215-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="f2215-1663">Примечание: hello журнал пользователей сейчас доступен только для сборок рекомендации.</span><span class="sxs-lookup"><span data-stu-id="f2215-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="f2215-1664">13.1 Получения журнала пользователя</span><span class="sxs-lookup"><span data-stu-id="f2215-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="f2215-1665">Получить список hello элемента используется в активных hello построения или в указанный hello сборки для hello указанный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2215-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="f2215-1666">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1666">HTTP Method</span></span> | <span data-ttu-id="f2215-1667">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1668">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1668">GET</span></span> |<span data-ttu-id="f2215-1669">Просмотреть журнал hello пользователя для построения active hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="f2215-1670">Просмотреть журнал hello пользователей для заданного построения hello`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="f2215-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="f2215-1671">Пример:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="f2215-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="f2215-1672">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1672">Parameter Name</span></span> | <span data-ttu-id="f2215-1673">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1674">modelId</span></span> |<span data-ttu-id="f2215-1675">Уникальный идентификатор Hello hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="f2215-1676">userId</span><span class="sxs-lookup"><span data-stu-id="f2215-1676">userId</span></span> |<span data-ttu-id="f2215-1677">Hello уникальный идентификатор hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="f2215-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="f2215-1678">buildId</span></span> |<span data-ttu-id="f2215-1679">Необязательный параметр Разрешить tooindicate, из какой сборке hello журнал пользователей должно быть выборки</span><span class="sxs-lookup"><span data-stu-id="f2215-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="f2215-1680">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1680">apiVersion</span></span> |<span data-ttu-id="f2215-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1681">1.0</span></span> |

<span data-ttu-id="f2215-1682">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1682">**Response:**</span></span>

<span data-ttu-id="f2215-1683">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1684">Hello ответ включает одной записи для каждого рекомендуемых элементов.</span><span class="sxs-lookup"><span data-stu-id="f2215-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="f2215-1685">Каждая запись имеет hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="f2215-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="f2215-1686">`Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.</span><span class="sxs-lookup"><span data-stu-id="f2215-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f2215-1687">`Feed\entry\content\properties\Name`-Имя элемента hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="f2215-1688">`Feed\entry\content\properties\Rating` — Недоступно.</span><span class="sxs-lookup"><span data-stu-id="f2215-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="f2215-1689">`Feed\entry\content\properties\Reasoning` — Недоступно.</span><span class="sxs-lookup"><span data-stu-id="f2215-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="f2215-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="f2215-1691">14. Уведомления</span><span class="sxs-lookup"><span data-stu-id="f2215-1691">14. Notifications</span></span>
<span data-ttu-id="f2215-1692">Рекомендации обучения Azure машины создает уведомления при возникновении вызваны ошибками в системе hello.</span><span class="sxs-lookup"><span data-stu-id="f2215-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="f2215-1693">Существует 3 типа уведомлений:</span><span class="sxs-lookup"><span data-stu-id="f2215-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="f2215-1694">Сбой сборки — срабатывает при каждом сбое сборки.</span><span class="sxs-lookup"><span data-stu-id="f2215-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="f2215-1695">Получение данных, обрабатывающий сбой - это уведомление срабатывает, когда у нас есть более 100 ошибок в hello последние 5 минут в hello обработки событий использования в модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="f2215-1696">Сбой потребления рекомендации — это уведомление срабатывает, когда у нас есть более 100 ошибок в hello последние 5 минут в hello обработки запросов рекомендацию в модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="f2215-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="f2215-1697">14.1.</span></span> <span data-ttu-id="f2215-1698">Получение уведомлений</span><span class="sxs-lookup"><span data-stu-id="f2215-1698">Get Notifications</span></span>
<span data-ttu-id="f2215-1699">Получает все уведомления hello для всех моделей или для одной модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="f2215-1700">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1700">HTTP Method</span></span> | <span data-ttu-id="f2215-1701">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1702">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="f2215-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1703">Получение всех уведомлений для всех моделей:</span><span class="sxs-lookup"><span data-stu-id="f2215-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1704">Пример получения уведомлений для определенной модели:</span><span class="sxs-lookup"><span data-stu-id="f2215-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="f2215-1705">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1705">Parameter Name</span></span> | <span data-ttu-id="f2215-1706">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1707">modelId</span></span> |<span data-ttu-id="f2215-1708">Необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="f2215-1708">Optional parameter.</span></span> <span data-ttu-id="f2215-1709">Если он не указан, вы получите все уведомления для всех моделей.</span><span class="sxs-lookup"><span data-stu-id="f2215-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="f2215-1710">Допустимое значение: Уникальный идентификатор hello модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="f2215-1711">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1711">apiVersion</span></span> |<span data-ttu-id="f2215-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-1713">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-1713">Request Body</span></span> |<span data-ttu-id="f2215-1714">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-1714">NONE</span></span> |

<span data-ttu-id="f2215-1715">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="f2215-1715">**Response:**</span></span>

<span data-ttu-id="f2215-1716">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="f2215-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="f2215-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="f2215-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-1718">14.2.</span></span> <span data-ttu-id="f2215-1719">Удаление уведомлений модели</span><span class="sxs-lookup"><span data-stu-id="f2215-1719">Delete Model Notifications</span></span>
<span data-ttu-id="f2215-1720">Удаляет все прочитанные уведомления для модели.</span><span class="sxs-lookup"><span data-stu-id="f2215-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="f2215-1721">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1721">HTTP Method</span></span> | <span data-ttu-id="f2215-1722">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1723">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f2215-1724">Пример:</span><span class="sxs-lookup"><span data-stu-id="f2215-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1725">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1725">Parameter Name</span></span> | <span data-ttu-id="f2215-1726">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="f2215-1727">modelId</span></span> |<span data-ttu-id="f2215-1728">Уникальный идентификатор модели hello</span><span class="sxs-lookup"><span data-stu-id="f2215-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="f2215-1729">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1729">apiVersion</span></span> |<span data-ttu-id="f2215-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-1731">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-1731">Request Body</span></span> |<span data-ttu-id="f2215-1732">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-1732">NONE</span></span> |

<span data-ttu-id="f2215-1733">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1733">**Response**:</span></span>

<span data-ttu-id="f2215-1734">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="f2215-1735">14.2.</span><span class="sxs-lookup"><span data-stu-id="f2215-1735">14.3.</span></span> <span data-ttu-id="f2215-1736">Удаление уведомлений пользователя</span><span class="sxs-lookup"><span data-stu-id="f2215-1736">Delete User Notifications</span></span>
<span data-ttu-id="f2215-1737">Удаляет все уведомления для всех моделей.</span><span class="sxs-lookup"><span data-stu-id="f2215-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="f2215-1738">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f2215-1738">HTTP Method</span></span> | <span data-ttu-id="f2215-1739">URI</span><span class="sxs-lookup"><span data-stu-id="f2215-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1740">УДАЛИТЬ</span><span class="sxs-lookup"><span data-stu-id="f2215-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="f2215-1741">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f2215-1741">Parameter Name</span></span> | <span data-ttu-id="f2215-1742">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="f2215-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2215-1743">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2215-1743">apiVersion</span></span> |<span data-ttu-id="f2215-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="f2215-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="f2215-1745">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f2215-1745">Request Body</span></span> |<span data-ttu-id="f2215-1746">НЕТ</span><span class="sxs-lookup"><span data-stu-id="f2215-1746">NONE</span></span> |

<span data-ttu-id="f2215-1747">**Ответ**:</span><span class="sxs-lookup"><span data-stu-id="f2215-1747">**Response**:</span></span>

<span data-ttu-id="f2215-1748">Код состояния HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f2215-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="f2215-1749">15. Юридическая информация</span><span class="sxs-lookup"><span data-stu-id="f2215-1749">15. Legal</span></span>
<span data-ttu-id="f2215-1750">Данный документ предоставляется "как есть".</span><span class="sxs-lookup"><span data-stu-id="f2215-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="f2215-1751">Сведения и мнения, содержащиеся в этом документе, включая URL-адреса и другие ссылки на веб-сайты, могут быть изменены без предварительного уведомления.</span><span class="sxs-lookup"><span data-stu-id="f2215-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="f2215-1752">Некоторые примеры, содержащиеся в данном документе, являются вымышленными и приводятся исключительно в демонстрационных целях.</span><span class="sxs-lookup"><span data-stu-id="f2215-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="f2215-1753">Любое сходство с реальными ситуациями случайно.</span><span class="sxs-lookup"><span data-stu-id="f2215-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="f2215-1754">Этот документ не предоставляет никаких законных прав интеллектуальной собственности tooany в продуктах корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f2215-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="f2215-1755">Вы можете скопировать и использовать данный документ для внутренних справочных целей.</span><span class="sxs-lookup"><span data-stu-id="f2215-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="f2215-1756">© Корпорация Майкрософт (Microsoft Corporation), 2015 г.</span><span class="sxs-lookup"><span data-stu-id="f2215-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="f2215-1757">Все права защищены.</span><span class="sxs-lookup"><span data-stu-id="f2215-1757">All rights reserved.</span></span>

