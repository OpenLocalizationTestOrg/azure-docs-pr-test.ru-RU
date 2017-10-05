---
title: "Вывод списка ресурсов службы хранилища Azure с помощью клиентской библиотеки службы хранилища для C++ | Документация Майкрософт"
description: "Узнайте, как использовать API-интерфейсов перечисления в клиентской библиотеке для службы хранилища Microsoft Azure для C++ для получения списка контейнеров, больших двоичных объектов, очередей, таблиц и сущностей."
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
ms.openlocfilehash: 9844412739f4f6f95416f81347f0f2eeeca62bea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="e9046-103">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="e9046-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="e9046-104">Операции перечисления необходимы для многих сценариев разработки с использованием хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e9046-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="e9046-105">В этой статье описано, как наиболее эффективно перечислять объекты в хранилище Azure с помощью API-интерфейсов, предоставленных в клиентской библиотеке для службы хранилища Microsoft Azure для C++.</span><span class="sxs-lookup"><span data-stu-id="e9046-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="e9046-106">Это руководство предназначено для клиентской библиотеки хранилища Azure для С++ версии 2.x, которая доступна в [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="e9046-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="e9046-107">Клиентская библиотека хранилища предоставляет разнообразные методы перечисления или запроса объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="e9046-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="e9046-108">В этой статье рассматриваются следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="e9046-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="e9046-109">перечисление контейнеров в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="e9046-109">List containers in an account</span></span>
* <span data-ttu-id="e9046-110">перечисление больших двоичных объектов в контейнере или виртуальном каталоге больших двоичных объектов;</span><span class="sxs-lookup"><span data-stu-id="e9046-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="e9046-111">перечисление очередей в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="e9046-111">List queues in an account</span></span>
* <span data-ttu-id="e9046-112">перечисление таблиц в учетной записи;</span><span class="sxs-lookup"><span data-stu-id="e9046-112">List tables in an account</span></span>
* <span data-ttu-id="e9046-113">запрос сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="e9046-113">Query entities in a table</span></span>

<span data-ttu-id="e9046-114">Каждый из этих методов продемонстрирован с использованием различных перегрузок для разных сценариев.</span><span class="sxs-lookup"><span data-stu-id="e9046-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="e9046-115">Асинхронный или синхронный</span><span class="sxs-lookup"><span data-stu-id="e9046-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="e9046-116">Так как клиентская библиотека хранилища для C++ основана на [библиотеке C++ REST](https://github.com/Microsoft/cpprestsdk), мы поддерживаем асинхронные операции с использованием [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="e9046-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="e9046-117">Например:</span><span class="sxs-lookup"><span data-stu-id="e9046-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="e9046-118">Синхронные операции создают оболочку для соответствующих асинхронных операций:</span><span class="sxs-lookup"><span data-stu-id="e9046-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="e9046-119">При работе с несколькими потоковыми приложениями или службами мы рекомендуем напрямую использовать асинхронные интерфейсы API, а не создавать поток для вызова API синхронизации, что существенно влияет на производительность.</span><span class="sxs-lookup"><span data-stu-id="e9046-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="e9046-120">Сегментированное перечисление</span><span class="sxs-lookup"><span data-stu-id="e9046-120">Segmented listing</span></span>
<span data-ttu-id="e9046-121">Из-за масштаба облачного хранилища требуется сегментированное перечисление.</span><span class="sxs-lookup"><span data-stu-id="e9046-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="e9046-122">Например, в контейнере больших двоичных объектов Azure может быть больше миллиона больших двоичных объектов, а в таблице Azure может быть больше миллиарда сущностей.</span><span class="sxs-lookup"><span data-stu-id="e9046-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="e9046-123">Это не теоретические значения, а фактические примеры реальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e9046-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="e9046-124">Поэтому нецелесообразно получать список всех объектов в одном ответе.</span><span class="sxs-lookup"><span data-stu-id="e9046-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="e9046-125">Вместо этого можно получить список объектов с разбиением на страницы.</span><span class="sxs-lookup"><span data-stu-id="e9046-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="e9046-126">Каждый из API-интерфейсов перечисления содержит *сегментированную* перегрузку.</span><span class="sxs-lookup"><span data-stu-id="e9046-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="e9046-127">Ответ для операции сегментированного перечисления включает в себя:</span><span class="sxs-lookup"><span data-stu-id="e9046-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="e9046-128"><i>_segment</i>, который содержит набор результатов, возвращаемых для одного вызова API перечисления;</span><span class="sxs-lookup"><span data-stu-id="e9046-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="e9046-129">*continuation_token*, который передается в следующий вызов для получения следующей страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="e9046-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="e9046-130">Если дополнительных результатов для возврата нет, маркер продолжения имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="e9046-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="e9046-131">Типичный вызов для перечисления всех больших двоичных объектов в контейнере указан в приведенном ниже фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="e9046-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="e9046-132">Этот кода можно найти в наших [примерах](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="e9046-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="e9046-133">Обратите внимание, что количество результатов, возвращаемых на странице, определяется параметром *max_results* в перегрузке каждого интерфейса API, например:</span><span class="sxs-lookup"><span data-stu-id="e9046-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="e9046-134">Если вы не укажете параметр *max_results*, то по умолчанию на одной странице возвращается до 5000 результатов.</span><span class="sxs-lookup"><span data-stu-id="e9046-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="e9046-135">Также обратите внимание, что запрос к хранилищу таблиц Azure может не вернуть ни одной записи или число возвращенных записей может быть меньше указанного значения параметра *max_results*, даже если маркер продолжения не пуст.</span><span class="sxs-lookup"><span data-stu-id="e9046-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="e9046-136">Одной из причин может быть то, что запрос не удалось выполнить в течение пяти секунд.</span><span class="sxs-lookup"><span data-stu-id="e9046-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="e9046-137">Если маркер продолжения не пуст, запрос следует продолжить, а ваш код не должен предполагать размер результатов сегмента.</span><span class="sxs-lookup"><span data-stu-id="e9046-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="e9046-138">Рекомендуемый шаблон для большинства сценариев таков — сегментированное перечисление, которое предоставляет явные сведения о ходе выполнения перечисления или запроса и указывает, как служба отвечает на каждый запрос.</span><span class="sxs-lookup"><span data-stu-id="e9046-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="e9046-139">В частности, для приложений и служб на C++ низкоуровневое управление ходом выполнения перечисления может помочь контролировать память и производительность.</span><span class="sxs-lookup"><span data-stu-id="e9046-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="e9046-140">Каскадное перечисление</span><span class="sxs-lookup"><span data-stu-id="e9046-140">Greedy listing</span></span>
<span data-ttu-id="e9046-141">Более ранние версии клиентской библиотеки хранилища для C++ (предварительные версии 0.5.0 и более ранние) содержали интерфейсы API несегментированного перечисления для таблиц и очередей, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e9046-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="e9046-142">Эти методы были реализованы в виде оболочки сегментированных API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e9046-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="e9046-143">Для каждого ответа сегментированного перечисления код дополнил результаты до вектора и вернул все результаты после проверки полных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="e9046-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="e9046-144">Этот подход может работать, если учетная запись хранения или таблица содержит небольшое количество объектов.</span><span class="sxs-lookup"><span data-stu-id="e9046-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="e9046-145">Однако с увеличением числа объектов, объем необходимой памяти может расти без ограничений, так как все результаты остаются в памяти.</span><span class="sxs-lookup"><span data-stu-id="e9046-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="e9046-146">Одна операция перечисления может занять очень много времени, в течение которого у вызывающего объекта не будет информации о ходе ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="e9046-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="e9046-147">Таких API каскадного перечисления нет в пакете SDK для C#, Java и JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="e9046-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="e9046-148">Чтобы избежать потенциальных проблем при использовании каскадных API, мы удалили их в предварительной версии 0.6.0.</span><span class="sxs-lookup"><span data-stu-id="e9046-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="e9046-149">Если ваш код вызывает эти каскадные API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="e9046-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="e9046-150">Затем следует изменить код, чтобы использовать API сегментированного перечисления:</span><span class="sxs-lookup"><span data-stu-id="e9046-150">Then you should modify your code to use the segmented listing APIs:</span></span>

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

<span data-ttu-id="e9046-151">Указывая параметр *max_results* сегмента, можно балансировать между количеством запросов и объемом памяти для удовлетворения требований к производительности вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e9046-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="e9046-152">Кроме того, если вы используете API сегментированного перечисления, но храните данные в локальной коллекции в каскадном стиле, мы также настоятельно рекомендуем переработать код так, чтобы осторожно обрабатывать хранение данных в локальной коллекции при масштабировании.</span><span class="sxs-lookup"><span data-stu-id="e9046-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="e9046-153">Отложенное перечисление</span><span class="sxs-lookup"><span data-stu-id="e9046-153">Lazy listing</span></span>
<span data-ttu-id="e9046-154">Хотя каскадное перечисление может вызывать проблемы, оно удобно, если в контейнере не слишком много объектов.</span><span class="sxs-lookup"><span data-stu-id="e9046-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="e9046-155">Если вы также используете пакеты SDK C# или Oracle Java, то вам необходимо ознакомиться с перечисляемой моделью программирования, которая реализует отложенное перечисление, когда данные извлекаются по определенному смещению только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e9046-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="e9046-156">В C++ шаблон на основе итератора также предоставляет подобный подход.</span><span class="sxs-lookup"><span data-stu-id="e9046-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="e9046-157">Типичный API отложенного перечисления, использующий **list_blobs**, например, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9046-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="e9046-158">Фрагмент типичного кода, использующего отложенное перечисление, может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9046-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
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

<span data-ttu-id="e9046-159">Обратите внимание, что отложенное перечисление доступно только в синхронном режиме.</span><span class="sxs-lookup"><span data-stu-id="e9046-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="e9046-160">По сравнению с каскадным перечислением отложенное перечисление извлекает данные только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e9046-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="e9046-161">На самом деле этот метод извлекает данные из хранилища Azure, только когда следующий итератор переходит в следующий сегмент.</span><span class="sxs-lookup"><span data-stu-id="e9046-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="e9046-162">Таким образом использование памяти контролируется на основе предельного размера, а операция выполняется быстро.</span><span class="sxs-lookup"><span data-stu-id="e9046-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="e9046-163">API-интерфейсы отложенного перечисления включены в клиентскую библиотеку хранилища C++ версии 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="e9046-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e9046-164">Заключение</span><span class="sxs-lookup"><span data-stu-id="e9046-164">Conclusion</span></span>
<span data-ttu-id="e9046-165">В этой статье мы рассмотрели различные перегрузки для API-интерфейсов перечисления для различных объектов в клиентской библиотеке хранилища C++.</span><span class="sxs-lookup"><span data-stu-id="e9046-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="e9046-166">Итог:</span><span class="sxs-lookup"><span data-stu-id="e9046-166">To summarize:</span></span>

* <span data-ttu-id="e9046-167">Настоятельно рекомендуется использовать асинхронные интерфейсы API в сценариях с несколькими потоками.</span><span class="sxs-lookup"><span data-stu-id="e9046-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="e9046-168">Для большинства сценариев рекомендуется сегментированное перечисление.</span><span class="sxs-lookup"><span data-stu-id="e9046-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="e9046-169">Отложенное перечисление представлено в библиотеке как удобная оболочка для синхронных сценариев.</span><span class="sxs-lookup"><span data-stu-id="e9046-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="e9046-170">Мы не рекомендуем использовать каскадное перечисление — оно было удалено из библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e9046-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9046-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9046-171">Next steps</span></span>
<span data-ttu-id="e9046-172">Для получения дополнительной информации о хранилище Azure и клиентской библиотеке для C++ см. следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e9046-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="e9046-173">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="e9046-173">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="e9046-174">Использование табличного хранилища из C++</span><span class="sxs-lookup"><span data-stu-id="e9046-174">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="e9046-175">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="e9046-175">How to use Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="e9046-176">Документация по API-интерфейсам клиентской библиотеки хранилища Azure для C++.</span><span class="sxs-lookup"><span data-stu-id="e9046-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="e9046-177">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e9046-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="e9046-178">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="e9046-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

