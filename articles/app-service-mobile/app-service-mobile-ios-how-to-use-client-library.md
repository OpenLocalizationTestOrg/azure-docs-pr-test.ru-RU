---
title: "aaaHow tooUse iOS SDK для мобильных приложений Azure"
description: "Как tooUse iOS SDK для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="1006a-103">Как tooUse iOS клиентскую библиотеку для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1006a-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="1006a-104">Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [пакет SDK для iOS мобильные приложения Azure][1].</span><span class="sxs-lookup"><span data-stu-id="1006a-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="1006a-105">Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части, создайте таблицу и загрузить проект Xcode готовые iOS.</span><span class="sxs-lookup"><span data-stu-id="1006a-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="1006a-106">В этом руководстве сосредоточиться на стороне клиента hello iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="1006a-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="1006a-107">Дополнительные сведения о toolearn Здравствуйте серверные SDK для hello внутреннего, см. инструкции пакета SDK сервера hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="1006a-108">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="1006a-108">Reference documentation</span></span>
<span data-ttu-id="1006a-109">Hello справочная документация для клиента hello iOS SDK находится здесь: [мобильных приложений Azure iOS Справочник по клиентским][2].</span><span class="sxs-lookup"><span data-stu-id="1006a-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="1006a-110">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="1006a-110">Supported Platforms</span></span>
<span data-ttu-id="1006a-111">пакет SDK для iOS Hello поддерживает проекты Objective-C, Swift 2.2 проектов и проектов Swift 2.3 для iOS версии 8.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1006a-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="1006a-112">Проверка подлинности «сервер потока» Hello использует WebView для hello, представленных пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1006a-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="1006a-113">Если устройство hello не может toopresent пользовательского интерфейса и веб-представление, другой метод проверки подлинности не требуются это внешнюю область hello hello продукта.</span><span class="sxs-lookup"><span data-stu-id="1006a-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="1006a-114">Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.</span><span class="sxs-lookup"><span data-stu-id="1006a-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="1006a-115"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="1006a-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="1006a-116">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="1006a-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="1006a-117">В этом руководстве предполагается, что этой таблицы hello имеет ту же схему, как таблицы hello в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="1006a-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="1006a-118">Кроме того, в данном руководстве предполагается, что в коде можно ссылаться на `MicrosoftAzureMobile.framework` и импортировать `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="1006a-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="1006a-119"><a name="create-client"></a>Создание клиента</span><span class="sxs-lookup"><span data-stu-id="1006a-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="1006a-120">Создание tooaccess серверной части мобильных приложений Azure в проекте `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="1006a-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="1006a-121">Замените `AppUrl` с URL-адреса приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="1006a-122">Параметры `gatewayURLString` и `applicationKey` можно оставить пустыми.</span><span class="sxs-lookup"><span data-stu-id="1006a-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="1006a-123">Если вы настроили шлюз для проверки подлинности, заполнение `gatewayURLString` с URL-адресом шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="1006a-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="1006a-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="1006a-126"><a name="table-reference"></a>Практическое руководство. Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="1006a-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="1006a-127">tooaccess или обновления данных, создать таблицу внутренних toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="1006a-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="1006a-128">Замените `TodoItem` с именем hello таблицы</span><span class="sxs-lookup"><span data-stu-id="1006a-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="1006a-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="1006a-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="1006a-131"><a name="querying"></a>Практическое руководство. Запрос данных</span><span class="sxs-lookup"><span data-stu-id="1006a-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="1006a-132">toocreate запроса к базе данных, запрос hello `MSTable` объекта.</span><span class="sxs-lookup"><span data-stu-id="1006a-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="1006a-133">Hello следующий запрос возвращает все элементы hello в `TodoItem` и журналы hello текст каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="1006a-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="1006a-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1006a-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="1006a-136"><a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="1006a-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="1006a-137">результаты toofilter существует много доступных параметров.</span><span class="sxs-lookup"><span data-stu-id="1006a-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="1006a-138">с помощью предиката, используйте toofilter `NSPredicate` и `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="1006a-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="1006a-139">возвращаемые данные toofind только неполные Todo элементы фильтруются следующие Hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="1006a-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1006a-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="1006a-142"><a name="query-object"></a>Практическое руководство. Использование MSQuery</span><span class="sxs-lookup"><span data-stu-id="1006a-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="1006a-143">tooperform сложного запроса (включая сортировку и разбиение по страницам), создание `MSQuery` объекта напрямую или с помощью предиката:</span><span class="sxs-lookup"><span data-stu-id="1006a-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="1006a-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="1006a-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="1006a-146">`MSQuery` позволяет контролировать некоторые настройки запросов.</span><span class="sxs-lookup"><span data-stu-id="1006a-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="1006a-147">Задание порядка результатов</span><span class="sxs-lookup"><span data-stu-id="1006a-147">Specify order of results</span></span>
* <span data-ttu-id="1006a-148">Ограничить tooreturn какие поля</span><span class="sxs-lookup"><span data-stu-id="1006a-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="1006a-149">Ограничить число записей, tooreturn</span><span class="sxs-lookup"><span data-stu-id="1006a-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="1006a-150">Указание общего количества в ответе</span><span class="sxs-lookup"><span data-stu-id="1006a-150">Specify total count in response</span></span>
* <span data-ttu-id="1006a-151">Указание в запросе настраиваемых параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="1006a-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="1006a-152">Применение дополнительных функций</span><span class="sxs-lookup"><span data-stu-id="1006a-152">Apply additional functions</span></span>

<span data-ttu-id="1006a-153">Выполнение `MSQuery` запроса путем вызова `readWithCompletion` hello объекта.</span><span class="sxs-lookup"><span data-stu-id="1006a-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="1006a-154"><a name="sorting"></a>Практическое руководство. Сортировка данных с помощью MSQuery</span><span class="sxs-lookup"><span data-stu-id="1006a-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="1006a-155">результаты toosort, давайте рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="1006a-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="1006a-156">вызов toosort по возрастанию поле «текст», а затем по убыванию «полный» `MSQuery` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1006a-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="1006a-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1006a-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="1006a-159"><a name="selecting"></a><a name="parameters"></a>Практическое руководство. Ограничение возвращаемых полей и развертывание строковых параметров запроса с помощью MSQuery</span><span class="sxs-lookup"><span data-stu-id="1006a-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="1006a-160">toobe toolimit полей, возвращаемых в запросе, укажите имена hello hello полей в hello **selectFields** свойство.</span><span class="sxs-lookup"><span data-stu-id="1006a-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="1006a-161">Этот пример возвращает только текст hello и завершенных поля:</span><span class="sxs-lookup"><span data-stu-id="1006a-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="1006a-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="1006a-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="1006a-164">tooinclude Дополнительные параметры строк запроса в hello server запроса (например, так как пользовательский серверный сценарий использует их), заполнение `query.parameters` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1006a-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="1006a-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="1006a-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="1006a-167"><a name="paging"></a>Практическое руководство. Настройка размера страницы</span><span class="sxs-lookup"><span data-stu-id="1006a-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="1006a-168">С помощью мобильных приложений Azure элементы управления размер страницы приветствия hello количество записей, которые извлекаются из внутренних таблиц hello одновременно.</span><span class="sxs-lookup"><span data-stu-id="1006a-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="1006a-169">Вызов слишком`pull` данных может затем выполнить пакетное копирование данных, на основе этого размера страницы, пока они не дополнительные toopull записей.</span><span class="sxs-lookup"><span data-stu-id="1006a-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="1006a-170">Это возможно tooconfigure размер страницы с помощью **MSPullSettings** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1006a-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="1006a-171">размер страницы по умолчанию Hello равно 50 и hello приведенном ниже примере изменяется too3.</span><span class="sxs-lookup"><span data-stu-id="1006a-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="1006a-172">Можно изменить размер страницы для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="1006a-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="1006a-173">Если имеется большое количество записей данных небольшого размера высокого уровня страницы уменьшает hello число проходов сигнала сервера.</span><span class="sxs-lookup"><span data-stu-id="1006a-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="1006a-174">Этот параметр управляет hello размер страницы на стороне клиента hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="1006a-175">Если hello клиент запрашивает больший размер страницы, чем поддерживается серверной мобильные приложения hello, размер страницы приветствия — повысить производительность hello максимальное hello серверной — настроенное toosupport.</span><span class="sxs-lookup"><span data-stu-id="1006a-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="1006a-176">Этот параметр также находится hello *номер* записей данных не hello *размер в байтах*.</span><span class="sxs-lookup"><span data-stu-id="1006a-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="1006a-177">При увеличении размера страницы приветствия клиента, следует также увеличить размер страницы приветствия на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="1006a-178">В разделе [» как: размер подкачки hello таблицы»](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello шагов toodo это.</span><span class="sxs-lookup"><span data-stu-id="1006a-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="1006a-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="1006a-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="1006a-181"><a name="inserting"></a>Практическое руководство. Вставка данных</span><span class="sxs-lookup"><span data-stu-id="1006a-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="1006a-182">Создание новой строки, tooinsert `NSDictionary` и вызова `table insert`.</span><span class="sxs-lookup"><span data-stu-id="1006a-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="1006a-183">Если [Динамическая схема] — включена, hello мобильной службы приложений Azure серверной части. автоматически формирует новые столбцы на основании hello `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="1006a-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="1006a-184">Если `id` не указан, серверной hello автоматически создает новый уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1006a-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="1006a-185">Предоставить свой собственный `id` toouse электронной почты адреса, имена пользователей или пользовательские значения как идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1006a-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="1006a-186">Наличие собственного идентификатора может упростить операции соединения и бизнес-логику базы данных.</span><span class="sxs-lookup"><span data-stu-id="1006a-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="1006a-187">Hello `result` содержит hello новый элемент, который был вставлен.</span><span class="sxs-lookup"><span data-stu-id="1006a-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="1006a-188">В зависимости от логики сервера может иметь дополнительные или измененных данных по сравнению toowhat был передан toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="1006a-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="1006a-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1006a-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="1006a-191"><a name="modifying"></a>Практическое руководство. Изменение данных</span><span class="sxs-lookup"><span data-stu-id="1006a-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="1006a-192">tooupdate существующей строки, измените элемент и вызова `update`:</span><span class="sxs-lookup"><span data-stu-id="1006a-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="1006a-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1006a-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="1006a-195">Кроме того можно укажите идентификатор строки hello и hello обновить поля:</span><span class="sxs-lookup"><span data-stu-id="1006a-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="1006a-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1006a-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="1006a-198">Как минимум, hello `id` атрибут должен быть задан при выполнении обновлений.</span><span class="sxs-lookup"><span data-stu-id="1006a-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="1006a-199"><a name="deleting"></a>Практическое руководство. Удаление данных</span><span class="sxs-lookup"><span data-stu-id="1006a-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="1006a-200">вызов toodelete элемент, `delete` с элементом hello:</span><span class="sxs-lookup"><span data-stu-id="1006a-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="1006a-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="1006a-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="1006a-203">Кроме того, для удаления элемента можно указать идентификатор строки:</span><span class="sxs-lookup"><span data-stu-id="1006a-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="1006a-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="1006a-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="1006a-206">Как минимум, hello `id` атрибут должен быть задан при внесении удаляет.</span><span class="sxs-lookup"><span data-stu-id="1006a-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="1006a-207"><a name="customapi"></a>Практическое руководство. Вызов настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="1006a-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="1006a-208">С помощью настраиваемого API можно включить любые функциональные возможности серверной части.</span><span class="sxs-lookup"><span data-stu-id="1006a-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="1006a-209">Это не обязательно toomap tooa табличной операции.</span><span class="sxs-lookup"><span data-stu-id="1006a-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="1006a-210">Не только получить больший контроль над обмена сообщениями, можно даже чтения и set заголовки и изменить формат текста ответа hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="1006a-211">как считывать toocreate пользовательского API на серверной hello toolearn [пользовательских API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="1006a-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="1006a-212">вызов пользовательского API toocall `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="1006a-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="1006a-213">содержимого Hello запроса и ответа, рассматриваются как JSON.</span><span class="sxs-lookup"><span data-stu-id="1006a-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="1006a-214">toouse другие типы носителей [используйте hello другая перегрузка метода `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="1006a-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="1006a-215">toomake `GET` запроса вместо `POST` запрос, параметр набора `HTTPMethod` слишком`"GET"` и параметр `body` слишком`nil` (поскольку запросы GET не имеют тел сообщений.) Если настраиваемый API поддерживает другие команды HTTP, измените `HTTPMethod` соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="1006a-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="1006a-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="1006a-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="1006a-218"><a name="templates"></a>Как: Register извещающих шаблоны toosend кросс платформенных уведомлений</span><span class="sxs-lookup"><span data-stu-id="1006a-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="1006a-219">шаблоны tooregister передать шаблоны с вашего **client.push registerDeviceToken** метод в клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="1006a-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="1006a-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="1006a-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="1006a-222">Шаблоны относятся к типу NSDictionary и может содержать несколько шаблонов в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1006a-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="1006a-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="1006a-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="1006a-225">Все теги будут удалены из hello запрос безопасности.</span><span class="sxs-lookup"><span data-stu-id="1006a-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="1006a-226">теги tooadd tooinstallations или шаблоны в установках см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][4].</span><span class="sxs-lookup"><span data-stu-id="1006a-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="1006a-227">toosend уведомления с помощью этих зарегистрированных шаблонов, работать с [API-интерфейсов концентраторы уведомлений][3].</span><span class="sxs-lookup"><span data-stu-id="1006a-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="1006a-228"><a name="errors"></a>Практическое руководство. Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="1006a-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="1006a-229">При вызове службы приложений Azure мобильной серверной части, содержит блок завершения hello `NSError` параметра.</span><span class="sxs-lookup"><span data-stu-id="1006a-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="1006a-230">Если возникает ошибка, этот параметр не является пустым.</span><span class="sxs-lookup"><span data-stu-id="1006a-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="1006a-231">В коде необходимо проверить этот параметр и обрабатывать ошибки hello, при необходимости, как показано в предшествующих фрагменты кода hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="1006a-232">файл Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] определяет константы hello `MSErrorResponseKey`, `MSErrorRequestKey`, и `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="1006a-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="1006a-233">tooget дополнительные данные, связанные ошибки toohello:</span><span class="sxs-lookup"><span data-stu-id="1006a-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="1006a-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="1006a-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="1006a-236">Кроме того файл hello определяет константы для каждого кода ошибки.</span><span class="sxs-lookup"><span data-stu-id="1006a-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="1006a-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="1006a-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="1006a-239"><a name="adal"></a>Как: проверять подлинность пользователей с hello библиотеку аутентификации Active Directory</span><span class="sxs-lookup"><span data-stu-id="1006a-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="1006a-240">Пользователи toosign hello библиотеку проверки подлинности Active Directory (ADAL) можно использовать в приложении с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1006a-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="1006a-241">Поток проверки подлинности клиента, с помощью пакета SDK поставщика удостоверений является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метод.</span><span class="sxs-lookup"><span data-stu-id="1006a-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="1006a-242">Клиентский поток аутентификации обеспечивает более удобный пользовательский интерфейс входа и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="1006a-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1006a-243">Настройте внутренний сервер мобильных приложений для входа в AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] [ 7] учебника.</span><span class="sxs-lookup"><span data-stu-id="1006a-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="1006a-244">Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="1006a-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="1006a-245">Для iOS, мы рекомендуем перенаправления, hello, URI имеет вид hello `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="1006a-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="1006a-246">Дополнительные сведения см. в разделе hello [ADAL iOS краткое руководство][8].</span><span class="sxs-lookup"><span data-stu-id="1006a-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="1006a-247">Установите ADAL с помощью Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="1006a-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="1006a-248">Изменить ваш hello tooinclude Podfile следующие определения, заменив **ВАШ ПРОЕКТ** с именем hello проекта Xcode:</span><span class="sxs-lookup"><span data-stu-id="1006a-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="1006a-249">и hello Pod.</span><span class="sxs-lookup"><span data-stu-id="1006a-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="1006a-250">С помощью hello терминалов, запустите `pod install` из каталога hello, содержащее проект, а затем откройте созданный hello рабочей области Xcode (не проект hello).</span><span class="sxs-lookup"><span data-stu-id="1006a-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="1006a-251">Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="1006a-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="1006a-252">Выполните следующие замены:</span><span class="sxs-lookup"><span data-stu-id="1006a-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="1006a-253">Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения.</span><span class="sxs-lookup"><span data-stu-id="1006a-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="1006a-254">Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com. Это значение можно скопировать с вкладки hello домена в Azure Active Directory в hello [классический портал Azure].</span><span class="sxs-lookup"><span data-stu-id="1006a-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="1006a-255">Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="1006a-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="1006a-256">Идентификатор клиента можно получить из hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.</span><span class="sxs-lookup"><span data-stu-id="1006a-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="1006a-257">Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="1006a-258">Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1006a-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="1006a-259">Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="1006a-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="1006a-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="1006a-261">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="1006a-262"><a name="facebook-sdk"></a>Как: проверять подлинность пользователей с hello Facebook SDK для iOS</span><span class="sxs-lookup"><span data-stu-id="1006a-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="1006a-263">Hello Facebook SDK для пользователей iOS toosign можно использовать в приложении с помощью Facebook.</span><span class="sxs-lookup"><span data-stu-id="1006a-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="1006a-264">Использование потока проверки подлинности клиента является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метод.</span><span class="sxs-lookup"><span data-stu-id="1006a-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="1006a-265">Проверка подлинности для потока клиента Hello обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="1006a-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1006a-266">Настройте внутренний сервер мобильных приложений для входа в Facebook, следуя [как tooconfigure приложения службы для имени входа Facebook] [ 9] учебника.</span><span class="sxs-lookup"><span data-stu-id="1006a-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="1006a-267">Установка hello Facebook SDK для iOS, следующие hello [Facebook SDK для iOS — начало работы] [ 10] документации.</span><span class="sxs-lookup"><span data-stu-id="1006a-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="1006a-268">Вместо того чтобы создавать приложения, можно добавить существующую регистрацию платформы iOS tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="1006a-269">Facebook Документация включает код Objective-C в делегат приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="1006a-270">Если вы используете **Swift**, можно использовать следующие преобразования для AppDelegate.swift hello:</span><span class="sxs-lookup"><span data-stu-id="1006a-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="1006a-271">В дополнение tooadding `FBSDKCoreKit.framework` tooyour проекта, добавьте ссылку слишком`FBSDKLoginKit.framework` в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="1006a-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="1006a-272">Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="1006a-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="1006a-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="1006a-274">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="1006a-275"><a name="twitter-fabric"></a>Практическое руководство: проверка подлинности пользователей с помощью структуры Twitter для iOS</span><span class="sxs-lookup"><span data-stu-id="1006a-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="1006a-276">Для пользователей iOS toosign можно использовать структуры в приложение с помощью Twitter.</span><span class="sxs-lookup"><span data-stu-id="1006a-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="1006a-277">Проверка подлинности клиента потока является более предпочтительным, чем toousing hello `loginWithProvider:completion:` метода, как он обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.</span><span class="sxs-lookup"><span data-stu-id="1006a-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1006a-278">Настройте внутренний сервер мобильных приложений для входа в Twitter, следуя hello [как tooconfigure приложения службы для имени входа Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="1006a-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="1006a-279">Добавление проекта tooyour структуры по следующей hello [структуры для iOS — начало работы] документация и настройка TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="1006a-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1006a-280">По умолчанию структура создаст приложение Twitter.</span><span class="sxs-lookup"><span data-stu-id="1006a-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="1006a-281">Можно избежать создания приложения путем регистрации hello ключ клиента и секрет пользователя, созданной ранее с помощью hello следующие фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="1006a-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="1006a-282">Кроме того, можно заменить hello ключ потребителя и предоставить значения tooApp службы с hello значения секрет пользователя см. в hello [панель структуры].</span><span class="sxs-lookup"><span data-stu-id="1006a-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="1006a-283">Если этот параметр выбран, быть убедиться, что tooset hello обратного вызова URL-адрес tooa заполнитель значения, такие как `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="1006a-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="1006a-284">При выборе toouse секреты hello, созданную ранее, добавьте следующий код tooyour делегат приложения hello:</span><span class="sxs-lookup"><span data-stu-id="1006a-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="1006a-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="1006a-286">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="1006a-287">Добавьте hello следующие приложения tooyour кода, в соответствии с toohello язык, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="1006a-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="1006a-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="1006a-289">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="1006a-290"><a name="google-sdk"></a>Как: проверять подлинность пользователей с hello Google входа в пакет SDK для iOS</span><span class="sxs-lookup"><span data-stu-id="1006a-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="1006a-291">Hello Google вход SDK можно использовать для пользователей iOS toosign в приложение с помощью учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="1006a-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="1006a-292">Google недавно объявила о политики безопасности изменения tootheir OAuth.</span><span class="sxs-lookup"><span data-stu-id="1006a-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="1006a-293">Эти изменения политики будет необходимо использовать пакет SDK для Google в будущем hello hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="1006a-294">Настройте внутренний сервер мобильных приложений для входа в Google, следующие hello [как tooconfigure приложения службы для имени входа Google](app-service-mobile-how-to-configure-google-authentication.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="1006a-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="1006a-295">Установка hello Google SDK для iOS, следующие hello [Google вход для iOS — интеграцией](https://developers.google.com/identity/sign-in/ios/start-integrating) документации.</span><span class="sxs-lookup"><span data-stu-id="1006a-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="1006a-296">Раздел «Проверка подлинности с сервером» hello, можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="1006a-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="1006a-297">Добавьте следующие tooyour делегат hello `signIn:didSignInForUser:withError:` метода, в соответствии с toohello языка.</span><span class="sxs-lookup"><span data-stu-id="1006a-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="1006a-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="1006a-299">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="1006a-300">Убедитесь, что также добавить hello следующие слишком`application:didFinishLaunchingWithOptions:` в вашем приложении делегат, заменив «SERVER_CLIENT_ID» hello таким же ИДЕНТИФИКАТОРОМ, вы использовали tooconfigure приложения службы на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1006a-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="1006a-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="1006a-302">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="1006a-303">Добавьте следующий код приложения tooyour в UIViewController, который реализует hello hello `GIDSignInUIDelegate` протокола, используемого языка toohello в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="1006a-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="1006a-304">Прежде чем снова вход выхода и несмотря на то, что вам не требуется tooenter учетные данные снова, появится диалоговое окно согласия.</span><span class="sxs-lookup"><span data-stu-id="1006a-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="1006a-305">Этот метод следует вызывайте только при истечении срока действия маркера сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="1006a-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="1006a-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1006a-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="1006a-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="1006a-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[быстрого запуска Azure мобильных приложений]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[Динамическая схема]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[панель структуры]: https://www.fabric.io/home
[структуры для iOS — начало работы]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
