---
title: "aaaList ресурсов хранилища Azure с hello клиентская библиотека хранилища для C++ | Документы Microsoft"
description: "Узнайте, как toouse hello список интерфейсов API в клиентской библиотеке хранилища Microsoft Azure для C++ tooenumerate контейнеров больших двоичных объектов, очередей, таблиц и сущностей."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="9dac0-103">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="9dac0-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="9dac0-104">Листинг операции выполняются сценарии разработки toomany ключа хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9dac0-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="9dac0-105">В этой статье описывается, как toomost эффективно перечисления объектов в хранилище Azure с помощью hello список интерфейсов API, входящих в hello клиентская библиотека хранилища Microsoft Azure для C++.</span><span class="sxs-lookup"><span data-stu-id="9dac0-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="9dac0-106">В этом руководстве обращается hello клиентская библиотека хранилища Azure для C++ версии 2.x, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="9dac0-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="9dac0-107">Hello клиентской библиотеки хранилища предоставляет разнообразные методы toolist или запроса объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="9dac0-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="9dac0-108">В этой статье рассматриваются hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="9dac0-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="9dac0-109">перечисление контейнеров в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="9dac0-109">List containers in an account</span></span>
* <span data-ttu-id="9dac0-110">перечисление больших двоичных объектов в контейнере или виртуальном каталоге больших двоичных объектов;</span><span class="sxs-lookup"><span data-stu-id="9dac0-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="9dac0-111">перечисление очередей в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="9dac0-111">List queues in an account</span></span>
* <span data-ttu-id="9dac0-112">перечисление таблиц в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="9dac0-112">List tables in an account</span></span>
* <span data-ttu-id="9dac0-113">запрос сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="9dac0-113">Query entities in a table</span></span>

<span data-ttu-id="9dac0-114">Каждый из этих методов продемонстрирован с использованием различных перегрузок для разных сценариев.</span><span class="sxs-lookup"><span data-stu-id="9dac0-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="9dac0-115">Асинхронный или синхронный</span><span class="sxs-lookup"><span data-stu-id="9dac0-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="9dac0-116">Поскольку hello клиентская библиотека хранилища для C++ является надстройкой hello [библиотеки C++ REST](https://github.com/Microsoft/cpprestsdk), мы поддерживаем по своей природе асинхронных операций с помощью [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="9dac0-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="9dac0-117">Например:</span><span class="sxs-lookup"><span data-stu-id="9dac0-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="9dac0-118">Синхронные операции wrap hello соответствующих асинхронных операций:</span><span class="sxs-lookup"><span data-stu-id="9dac0-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="9dac0-119">При работе с несколькими приложениями или службами потоков, рекомендуется использовать hello асинхронные интерфейсы API, напрямую вместо создания синхронизации hello toocall поток API, которые существенно влияет на производительность.</span><span class="sxs-lookup"><span data-stu-id="9dac0-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="9dac0-120">Сегментированное перечисление</span><span class="sxs-lookup"><span data-stu-id="9dac0-120">Segmented listing</span></span>
<span data-ttu-id="9dac0-121">Масштаб Hello облачного хранилища требуется листинг Сегментированные.</span><span class="sxs-lookup"><span data-stu-id="9dac0-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="9dac0-122">Например, в контейнере больших двоичных объектов Azure может быть больше миллиона больших двоичных объектов, а в таблице Azure может быть больше миллиарда сущностей.</span><span class="sxs-lookup"><span data-stu-id="9dac0-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="9dac0-123">Это не теоретические значения, а фактические примеры реальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9dac0-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="9dac0-124">Именно поэтому нецелесообразным toolist все объекты в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="9dac0-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="9dac0-125">Вместо этого можно получить список объектов с разбиением на страницы.</span><span class="sxs-lookup"><span data-stu-id="9dac0-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="9dac0-126">Каждый список API-интерфейсы hello имеет *сегментированных* перегрузки.</span><span class="sxs-lookup"><span data-stu-id="9dac0-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="9dac0-127">Hello ответ для операции листинг Сегментированные включает:</span><span class="sxs-lookup"><span data-stu-id="9dac0-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="9dac0-128"><i>_segment</i>, который содержит набор результатов, возвращенных за один вызов toohello, перечисление API hello.</span><span class="sxs-lookup"><span data-stu-id="9dac0-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="9dac0-129">*continuation_token*, который передается следующему вызову toohello в порядке tooget hello следующей страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="9dac0-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="9dac0-130">Если нет дополнительных результатов tooreturn, токен продолжения hello имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="9dac0-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="9dac0-131">Например типичный вызов toolist все большие двоичные объекты в контейнере может выглядеть как следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="9dac0-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="9dac0-132">Hello код находится в нашем [образцы](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="9dac0-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="9dac0-133">Обратите внимание, что hello количество результатов, возвращаемых на странице можно управлять параметром hello *max_results* в перегрузке hello каждый API, например:</span><span class="sxs-lookup"><span data-stu-id="9dac0-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="9dac0-134">Если вы не укажете hello *max_results* параметр, по умолчанию hello возвращается максимальное значение too5000 результатов на одной странице.</span><span class="sxs-lookup"><span data-stu-id="9dac0-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="9dac0-135">Также Обратите внимание, что запрос к хранилищу таблиц Azure может возвращать нет записей или записей меньше, чем значение hello hello *max_results* параметр, который вы указали, даже если токен продолжения hello не является пустым.</span><span class="sxs-lookup"><span data-stu-id="9dac0-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="9dac0-136">Одна из причин может быть hello запроса не удалось завершить в течение пяти секунд.</span><span class="sxs-lookup"><span data-stu-id="9dac0-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="9dac0-137">При условии, что токен продолжения hello не пуста, следует продолжить запрос hello и код не должен предполагать hello размер сегмента результатов.</span><span class="sxs-lookup"><span data-stu-id="9dac0-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="9dac0-138">Hello рекомендуется шаблона для большинства сценариев кодирования разбито перечисление, предоставляющее явную хода выполнения со списком или запросов, а также службы hello реакция tooeach запроса.</span><span class="sxs-lookup"><span data-stu-id="9dac0-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="9dac0-139">Особенно для C++ приложений или служб управление hello со списком выполняется более низкого уровня могут помочь управления памятью и производительностью.</span><span class="sxs-lookup"><span data-stu-id="9dac0-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="9dac0-140">Каскадное перечисление</span><span class="sxs-lookup"><span data-stu-id="9dac0-140">Greedy listing</span></span>
<span data-ttu-id="9dac0-141">Более ранних версиях hello клиентская библиотека хранилища для C++ (Предварительный просмотр версий 0.5.0 и более ранних версий) включены несегментированный список API-интерфейсы для таблиц и очередей, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9dac0-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="9dac0-142">Эти методы были реализованы в виде оболочки сегментированных API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="9dac0-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="9dac0-143">В каждом ответе листинг Сегментированные кода hello добавлено вектор tooa результаты hello и вернуть все результаты, после полного контейнеры hello сканировались.</span><span class="sxs-lookup"><span data-stu-id="9dac0-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="9dac0-144">Этот подход может работать при hello учетной записи хранилища или таблица содержит небольшое количество объектов.</span><span class="sxs-lookup"><span data-stu-id="9dac0-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="9dac0-145">Тем не менее увеличение hello число объектов, требуемый объем памяти hello удалось увеличить без ограничения, так как все результаты остаются в памяти.</span><span class="sxs-lookup"><span data-stu-id="9dac0-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="9dac0-146">Одной операцией получения листинга может занять очень много времени, в которой hello вызывающего объекта, необходимо было отсутствует информация о ходе своего выполнения.</span><span class="sxs-lookup"><span data-stu-id="9dac0-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="9dac0-147">Эти жадном список интерфейсов API в hello SDK не существует в C#, Java, и hello среды JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="9dac0-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="9dac0-148">tooavoid hello потенциальных проблем с помощью этих жадном API, мы удалили их в версии 0.6.0 предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="9dac0-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="9dac0-149">Если ваш код вызывает эти каскадные API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="9dac0-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="9dac0-150">Необходимо изменить код, а затем toouse hello сегментированных список API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="9dac0-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="9dac0-151">Указав hello *max_results* параметр hello сегмента можно распределить между номерами hello запросов и использования памяти toomeet вопросы производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="9dac0-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="9dac0-152">Кроме того, если выполняется с помощью листинг Сегментированные API-интерфейсы, но сохранить данные hello в локальную коллекцию в стиле «жадного», также настоятельно рекомендуется выполнить рефакторинг toohandle вашего кода, хранение данных в локальную коллекцию тщательно в масштабе.</span><span class="sxs-lookup"><span data-stu-id="9dac0-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="9dac0-153">Отложенное перечисление</span><span class="sxs-lookup"><span data-stu-id="9dac0-153">Lazy listing</span></span>
<span data-ttu-id="9dac0-154">Несмотря на то, что жадном листинг возникает потенциальные проблемы, его удобно, если не слишком много объектов в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="9dac0-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="9dac0-155">Если вы также используете C# или Oracle Java SDK, необходимо ознакомиться с hello перечисляемую модель программирования, обеспечивающую отложенной стиля списка, где hello данные с определенным смещением только доставляются при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9dac0-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="9dac0-156">В C++ шаблон на основе итератора hello также предоставляет подобный подход.</span><span class="sxs-lookup"><span data-stu-id="9dac0-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="9dac0-157">Типичный API отложенного перечисления, использующий **list_blobs**, например, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dac0-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="9dac0-158">Фрагмент обычного кода, который использует шаблон отложенной листинг hello может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dac0-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="9dac0-159">Обратите внимание, что отложенное перечисление доступно только в синхронном режиме.</span><span class="sxs-lookup"><span data-stu-id="9dac0-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="9dac0-160">По сравнению с каскадным перечислением отложенное перечисление извлекает данные только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9dac0-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="9dac0-161">На деле hello он выбирает данные из хранилища Azure, только в том случае, когда перемещает hello следующего итератора в следующего сегмента.</span><span class="sxs-lookup"><span data-stu-id="9dac0-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="9dac0-162">Таким образом использование памяти контролируется с помощью предельный размер и hello операция выполняется быстро.</span><span class="sxs-lookup"><span data-stu-id="9dac0-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="9dac0-163">Листинг отложенной API-интерфейсы, включаются в hello клиентская библиотека хранилища C++ в версии 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="9dac0-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9dac0-164">Заключение</span><span class="sxs-lookup"><span data-stu-id="9dac0-164">Conclusion</span></span>
<span data-ttu-id="9dac0-165">В этой статье мы рассмотрели разные перегрузки для перечисления API-интерфейсы для различных объектов в hello клиентской библиотеки хранилища для C++.</span><span class="sxs-lookup"><span data-stu-id="9dac0-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="9dac0-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="9dac0-166">toosummarize:</span></span>

* <span data-ttu-id="9dac0-167">Настоятельно рекомендуется использовать асинхронные интерфейсы API в сценариях с несколькими потоками.</span><span class="sxs-lookup"><span data-stu-id="9dac0-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="9dac0-168">Для большинства сценариев рекомендуется сегментированное перечисление.</span><span class="sxs-lookup"><span data-stu-id="9dac0-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="9dac0-169">Отложенная список приведен в библиотеке hello как удобный оболочка в синхронные сценарии.</span><span class="sxs-lookup"><span data-stu-id="9dac0-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="9dac0-170">Жадное список не рекомендуется и был удален из библиотеки hello.</span><span class="sxs-lookup"><span data-stu-id="9dac0-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dac0-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dac0-171">Next steps</span></span>
<span data-ttu-id="9dac0-172">Дополнительные сведения о хранилище Azure и клиентскую библиотеку C++ см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="9dac0-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="9dac0-173">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="9dac0-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="9dac0-174">Как toouse хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="9dac0-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="9dac0-175">Как toouse хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="9dac0-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="9dac0-176">Документация по API-интерфейсам клиентской библиотеки хранилища Azure для C++.</span><span class="sxs-lookup"><span data-stu-id="9dac0-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="9dac0-177">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="9dac0-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="9dac0-178">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="9dac0-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

