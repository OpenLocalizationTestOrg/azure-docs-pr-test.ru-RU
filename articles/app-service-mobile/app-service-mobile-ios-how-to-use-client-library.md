---
title: "Использование пакета iOS SDK для мобильных приложений Azure"
description: "Использование пакета iOS SDK для мобильных приложений Azure"
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
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="b78bc-103">Использование клиентской библиотеки iOS для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b78bc-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="b78bc-104">В данном руководстве показано, как реализовать типичные сценарии с использованием последней версии [пакета SDK iOS для мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="b78bc-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="b78bc-105">Если вы не знакомы с мобильными приложениями Azure, изучите статью [Быстрый запуск мобильного приложения Azure], чтобы создать серверную часть и таблицу, а также скачать предварительно собранный проект Xcode для iOS.</span><span class="sxs-lookup"><span data-stu-id="b78bc-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="b78bc-106">В данном руководстве мы сосредоточимся на клиентской части пакета iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="b78bc-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="b78bc-107">Дополнительные сведения о серверном пакете SDK для внутреннего сервера см. практических руководствах по пакету SDK для сервера.</span><span class="sxs-lookup"><span data-stu-id="b78bc-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="b78bc-108">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="b78bc-108">Reference documentation</span></span>
<span data-ttu-id="b78bc-109">Справочная документация по пакету SDK для клиента iOS находится здесь: [Справочник по клиенту iOS мобильных приложений Azure][2].</span><span class="sxs-lookup"><span data-stu-id="b78bc-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b78bc-110">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="b78bc-110">Supported Platforms</span></span>
<span data-ttu-id="b78bc-111">Пакет SDK для iOS поддерживает проекты Objective-C, проекты Swift 2.2 и проекты Swift 2.3 для iOS 8.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b78bc-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="b78bc-112">"Серверная" аутентификация использует WebView для представляемого пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b78bc-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="b78bc-113">Если устройство не может представить пользовательский интерфейс WebView, потребуется применить другие способы аутентификации, которые выходят за рамки данного продукта.</span><span class="sxs-lookup"><span data-stu-id="b78bc-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="b78bc-114">Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.</span><span class="sxs-lookup"><span data-stu-id="b78bc-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="b78bc-115"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="b78bc-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="b78bc-116">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="b78bc-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="b78bc-117">В этом руководстве предполагается, что в таблице используется та же схему, что и в таблицах, приведенных в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="b78bc-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="b78bc-118">Кроме того, в данном руководстве предполагается, что в коде можно ссылаться на `MicrosoftAzureMobile.framework` и импортировать `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="b78bc-119"><a name="create-client"></a>Создание клиента</span><span class="sxs-lookup"><span data-stu-id="b78bc-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="b78bc-120">Чтобы получить доступ к серверной части мобильных приложений Azure в вашем проекте, создайте `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="b78bc-121">Замените `AppUrl` на URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="b78bc-122">Параметры `gatewayURLString` и `applicationKey` можно оставить пустыми.</span><span class="sxs-lookup"><span data-stu-id="b78bc-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="b78bc-123">Если вы настроите шлюз для проверки подлинности, укажите в параметре `gatewayURLString` его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b78bc-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="b78bc-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="b78bc-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="b78bc-126"><a name="table-reference"></a>Практическое руководство. Создание ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="b78bc-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="b78bc-127">Для доступа к данным или их обновления создайте ссылку на таблицу серверной части.</span><span class="sxs-lookup"><span data-stu-id="b78bc-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="b78bc-128">Замените `TodoItem` на имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="b78bc-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="b78bc-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="b78bc-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="b78bc-131"><a name="querying"></a>Практическое руководство. Запрос данных</span><span class="sxs-lookup"><span data-stu-id="b78bc-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="b78bc-132">Чтобы создать запрос к базе данных, отправьте запрос объекта `MSTable` .</span><span class="sxs-lookup"><span data-stu-id="b78bc-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="b78bc-133">Следующий запрос возвращает все элементы в `TodoItem` и регистрирует в журнале текст каждого из них.</span><span class="sxs-lookup"><span data-stu-id="b78bc-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="b78bc-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-134">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-135">**Swift**:</span></span>

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

## <span data-ttu-id="b78bc-136"><a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="b78bc-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="b78bc-137">Есть множество способов фильтрации результатов.</span><span class="sxs-lookup"><span data-stu-id="b78bc-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="b78bc-138">Для фильтрации данных с использованием предиката используйте `NSPredicate` и `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="b78bc-139">Следующие фильтры позволяют возвращать только незавершенные элементы Todo.</span><span class="sxs-lookup"><span data-stu-id="b78bc-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="b78bc-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
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

<span data-ttu-id="b78bc-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
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

## <span data-ttu-id="b78bc-142"><a name="query-object"></a>Практическое руководство. Использование MSQuery</span><span class="sxs-lookup"><span data-stu-id="b78bc-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="b78bc-143">Чтобы выполнить сложный запрос (в том числе на сортировку и подкачку), создайте объект `MSQuery` непосредственно или с помощью предиката:</span><span class="sxs-lookup"><span data-stu-id="b78bc-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="b78bc-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="b78bc-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="b78bc-146">`MSQuery` позволяет контролировать некоторые настройки запросов.</span><span class="sxs-lookup"><span data-stu-id="b78bc-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="b78bc-147">Задание порядка результатов</span><span class="sxs-lookup"><span data-stu-id="b78bc-147">Specify order of results</span></span>
* <span data-ttu-id="b78bc-148">Ограничение возвращаемых полей</span><span class="sxs-lookup"><span data-stu-id="b78bc-148">Limit which fields to return</span></span>
* <span data-ttu-id="b78bc-149">Ограничение количества возвращаемых записей</span><span class="sxs-lookup"><span data-stu-id="b78bc-149">Limit how many records to return</span></span>
* <span data-ttu-id="b78bc-150">Указание общего количества в ответе</span><span class="sxs-lookup"><span data-stu-id="b78bc-150">Specify total count in response</span></span>
* <span data-ttu-id="b78bc-151">Указание в запросе настраиваемых параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="b78bc-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="b78bc-152">Применение дополнительных функций</span><span class="sxs-lookup"><span data-stu-id="b78bc-152">Apply additional functions</span></span>

<span data-ttu-id="b78bc-153">Выполнение `MSQuery` запроса путем вызова `readWithCompletion` для объекта.</span><span class="sxs-lookup"><span data-stu-id="b78bc-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="b78bc-154"><a name="sorting"></a>Практическое руководство. Сортировка данных с помощью MSQuery</span><span class="sxs-lookup"><span data-stu-id="b78bc-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="b78bc-155">На примере ниже показано, как сортировать результаты.</span><span class="sxs-lookup"><span data-stu-id="b78bc-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="b78bc-156">Для сортировки по возрастанию значений поля text, а затем по убыванию по значению complete, вызовите `MSQuery` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b78bc-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="b78bc-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-157">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-158">**Swift**:</span></span>

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


## <span data-ttu-id="b78bc-159"><a name="selecting"></a><a name="parameters"></a>Практическое руководство. Ограничение возвращаемых полей и развертывание строковых параметров запроса с помощью MSQuery</span><span class="sxs-lookup"><span data-stu-id="b78bc-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="b78bc-160">Чтобы ограничить поля, возвращаемые в запросе, укажите имена полей в свойстве **selectFields** .</span><span class="sxs-lookup"><span data-stu-id="b78bc-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="b78bc-161">Данный пример возвращает только текст и заполненные поля.</span><span class="sxs-lookup"><span data-stu-id="b78bc-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="b78bc-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="b78bc-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="b78bc-164">Чтобы включить дополнительные строковые параметры в запрос сервера (например, так как они используются в настраиваемом серверном скрипте), заполните `query.parameters` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b78bc-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="b78bc-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="b78bc-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="b78bc-167"><a name="paging"></a>Практическое руководство. Настройка размера страницы</span><span class="sxs-lookup"><span data-stu-id="b78bc-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="b78bc-168">При использовании мобильных приложений Azure размер страницы определяет количество записей, одновременно извлекаемых из таблиц серверной части.</span><span class="sxs-lookup"><span data-stu-id="b78bc-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="b78bc-169">Вызов данных `pull` приведет к пакетному извлечению данных на основе этого размера страницы до тех пор, пока не будут извлечены все соответствующие записи.</span><span class="sxs-lookup"><span data-stu-id="b78bc-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="b78bc-170">Можно настроить размер страницы с помощью **MSPullSettings**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b78bc-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="b78bc-171">Размер страницы по умолчанию равен 50, а в приведенном ниже примере он изменен на 3.</span><span class="sxs-lookup"><span data-stu-id="b78bc-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="b78bc-172">Можно изменить размер страницы для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="b78bc-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="b78bc-173">Если имеется большое количество записей данных небольшого размера, то большой размер страницы уменьшит число круговых путей сервера.</span><span class="sxs-lookup"><span data-stu-id="b78bc-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="b78bc-174">Этот параметр определяет размер страницы только на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="b78bc-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="b78bc-175">Если клиент запрашивает больший размер страницы, чем поддерживает серверная часть мобильных приложений, то используется максимальный размер страницы, допускаемый серверной частью.</span><span class="sxs-lookup"><span data-stu-id="b78bc-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="b78bc-176">Этот параметр также определяет *число* записей данных, а не *размер в байтах*.</span><span class="sxs-lookup"><span data-stu-id="b78bc-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="b78bc-177">Если увеличить размер страницы клиента, также следует увеличить размер страницы на сервере.</span><span class="sxs-lookup"><span data-stu-id="b78bc-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="b78bc-178">Инструкции см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b78bc-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="b78bc-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="b78bc-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="b78bc-181"><a name="inserting"></a>Практическое руководство. Вставка данных</span><span class="sxs-lookup"><span data-stu-id="b78bc-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="b78bc-182">Чтобы вставить новую строку таблицы, создайте `NSDictionary` и вызовите `table insert`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="b78bc-183">Если включена [динамическая схема], то серверная часть мобильной службы службы приложений Azure автоматически создает столбцы на основе `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="b78bc-184">Если не указано значение параметра `id` , на внутреннем сервере автоматически создается уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b78bc-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="b78bc-185">Укажите собственное значение параметра `id` , чтобы в качестве идентификатора использовать адреса электронной почты, имена пользователей или настраиваемые значения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="b78bc-186">Наличие собственного идентификатора может упростить операции соединения и бизнес-логику базы данных.</span><span class="sxs-lookup"><span data-stu-id="b78bc-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="b78bc-187">`result` содержит новый элемент, который был вставлен.</span><span class="sxs-lookup"><span data-stu-id="b78bc-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="b78bc-188">В зависимости от логики вашего сервера он может иметь дополнительные или измененные данные, по сравнению с теми, которые были переданы на сервер.</span><span class="sxs-lookup"><span data-stu-id="b78bc-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="b78bc-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-189">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-190">**Swift**:</span></span>

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

## <span data-ttu-id="b78bc-191"><a name="modifying"></a>Практическое руководство. Изменение данных</span><span class="sxs-lookup"><span data-stu-id="b78bc-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="b78bc-192">Чтобы обновить существующую строку, измените элемент и вызовите `update`:</span><span class="sxs-lookup"><span data-stu-id="b78bc-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="b78bc-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-193">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-194">**Swift**:</span></span>

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

<span data-ttu-id="b78bc-195">Можно также указать идентификатор строки и обновляемое поле:</span><span class="sxs-lookup"><span data-stu-id="b78bc-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="b78bc-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="b78bc-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="b78bc-198">При обновлении необходимо по крайней мере задать атрибут `id` .</span><span class="sxs-lookup"><span data-stu-id="b78bc-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="b78bc-199"><a name="deleting"></a>Практическое руководство. Удаление данных</span><span class="sxs-lookup"><span data-stu-id="b78bc-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="b78bc-200">Чтобы удалить элемент, вызовите `delete` с элементом:</span><span class="sxs-lookup"><span data-stu-id="b78bc-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="b78bc-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="b78bc-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="b78bc-203">Кроме того, для удаления элемента можно указать идентификатор строки:</span><span class="sxs-lookup"><span data-stu-id="b78bc-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="b78bc-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="b78bc-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="b78bc-206">При удалении необходимо по крайней мере задать атрибут `id` .</span><span class="sxs-lookup"><span data-stu-id="b78bc-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="b78bc-207"><a name="customapi"></a>Практическое руководство. Вызов настраиваемого интерфейса API</span><span class="sxs-lookup"><span data-stu-id="b78bc-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="b78bc-208">С помощью настраиваемого API можно включить любые функциональные возможности серверной части.</span><span class="sxs-lookup"><span data-stu-id="b78bc-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="b78bc-209">Они не должны совпадать с операциями с таблицами.</span><span class="sxs-lookup"><span data-stu-id="b78bc-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="b78bc-210">Вы не только расширяете контроль над процессом обмена сообщениями, но также получаете возможность читать и задавать заголовки и изменять формат текста ответа.</span><span class="sxs-lookup"><span data-stu-id="b78bc-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="b78bc-211">Сведения о создании настраиваемого API в серверной части см. в разделе [Настраиваемые интерфейсы API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis).</span><span class="sxs-lookup"><span data-stu-id="b78bc-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="b78bc-212">Для вызова настраиваемого API вызовите `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="b78bc-213">Содержимое запроса и ответа содержимого рассматривается как JSON.</span><span class="sxs-lookup"><span data-stu-id="b78bc-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="b78bc-214">Чтобы использовать другие типы носителей, [воспользуйтесь другой перегрузкой `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="b78bc-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="b78bc-215">Чтобы вместо запроса `POST` выполнить запрос `GET`, задайте параметру `HTTPMethod` значение `"GET"`, а параметру `body` — значение `nil` (поскольку запросы GET не имеют текста сообщений). Если настраиваемый API поддерживает другие команды HTTP, измените `HTTPMethod` соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b78bc-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="b78bc-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-216">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-217">**Swift**:</span></span>

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

## <span data-ttu-id="b78bc-218"><a name="templates"></a>Использование шаблонов для отправки кроссплатформенных push- уведомлений</span><span class="sxs-lookup"><span data-stu-id="b78bc-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="b78bc-219">Чтобы зарегистрировать шаблоны, передайте их с помощью метода **client.push registerDeviceToken** в свое клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="b78bc-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="b78bc-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="b78bc-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="b78bc-222">Шаблоны относятся к типу NSDictionary и могут содержать несколько шаблонов в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="b78bc-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="b78bc-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="b78bc-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="b78bc-225">Все теги будут удалены из запроса в целях безопасности.</span><span class="sxs-lookup"><span data-stu-id="b78bc-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="b78bc-226">В статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure][4] показано, как добавлять теги для установки или шаблоны в пределах установки.</span><span class="sxs-lookup"><span data-stu-id="b78bc-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="b78bc-227">Для отправки уведомлений с использованием зарегистрированных шаблонов используйте [API центров уведомлений][3].</span><span class="sxs-lookup"><span data-stu-id="b78bc-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="b78bc-228"><a name="errors"></a>Практическое руководство. Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="b78bc-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="b78bc-229">При вызове серверной части мобильной службы службы приложений Azure блок завершения содержит параметр `NSError`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="b78bc-230">Если возникает ошибка, этот параметр не является пустым.</span><span class="sxs-lookup"><span data-stu-id="b78bc-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="b78bc-231">В коде необходимо проверить этот параметр и обработать ошибку по мере необходимости, как показано во фрагментах кода выше.</span><span class="sxs-lookup"><span data-stu-id="b78bc-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="b78bc-232">Файл [`<WindowsAzureMobileServices/MSError.h>`][6] определяет константы `MSErrorResponseKey`, `MSErrorRequestKey` и `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="b78bc-233">Вот как можно получить дополнительные данные об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b78bc-233">To get more data related to the error:</span></span>

<span data-ttu-id="b78bc-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="b78bc-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="b78bc-236">Кроме того, этот файл определяет константы для каждого кода ошибки.</span><span class="sxs-lookup"><span data-stu-id="b78bc-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="b78bc-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="b78bc-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="b78bc-239"><a name="adal"></a>Практическое руководство. Проверка подлинности пользователей с помощью библиотеки проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="b78bc-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="b78bc-240">Библиотеку проверки подлинности Active Directory (ADAL) можно использовать для входа пользователей в приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b78bc-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="b78bc-241">Клиентский поток аутентификации с использованием пакета SDK поставщика удостоверений предпочтительнее использования метода `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="b78bc-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="b78bc-242">Клиентский поток аутентификации обеспечивает более удобный пользовательский интерфейс входа и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="b78bc-243">Настройте серверную часть мобильного приложения для входа с помощью AAD, следуя указаниям в руководстве [Настройка приложения службы приложений для использования службы входа Azure Active Directory][7].</span><span class="sxs-lookup"><span data-stu-id="b78bc-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="b78bc-244">Обязательно выполните дополнительный этап регистрации собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="b78bc-245">Для iOS мы рекомендуем использовать универсальный код ресурса (URI) перенаправления следующего вида: `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="b78bc-246">Чтобы узнать больше, ознакомьтесь с [кратким руководством по ADAL для iOS][8].</span><span class="sxs-lookup"><span data-stu-id="b78bc-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="b78bc-247">Установите ADAL с помощью Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="b78bc-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="b78bc-248">Измените файл Podfile: добавьте в него следующее определение, заменив **YOUR-PROJECT** именем проекта Xcode.</span><span class="sxs-lookup"><span data-stu-id="b78bc-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="b78bc-249">и Pod:</span><span class="sxs-lookup"><span data-stu-id="b78bc-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="b78bc-250">С помощью приложения Terminal запустите `pod install` из каталога, содержащего проект, а затем откройте созданную рабочую область Xcode (не проект).</span><span class="sxs-lookup"><span data-stu-id="b78bc-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="b78bc-251">Добавьте в приложение приведенный ниже код, соответствующий используемому языку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="b78bc-252">Выполните следующие замены:</span><span class="sxs-lookup"><span data-stu-id="b78bc-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="b78bc-253">Замените строку **INSERT-AUTHORITY-HERE** именем клиента, в котором подготовлено приложение.</span><span class="sxs-lookup"><span data-stu-id="b78bc-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="b78bc-254">Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b78bc-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="b78bc-255">Это значение можно скопировать на вкладке "Домен" в разделе Azure Active Directory на [классическом портале Azure].</span><span class="sxs-lookup"><span data-stu-id="b78bc-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="b78bc-256">Замените текст **INSERT-RESOURCE-ID-HERE** идентификатором клиента для серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="b78bc-257">Идентификатор клиента можно скопировать на портале в разделе **Настройки Azure Active Directory** на вкладке **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="b78bc-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="b78bc-258">Замените текст **INSERT-CLIENT-ID-HERE** идентификатором клиента, скопированным из собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="b78bc-259">Замените текст **INSERT-REDIRECT-URI-HERE** конечной точкой сайта */.auth/login/done* , используя схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b78bc-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="b78bc-260">Это значение должно быть похоже на *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="b78bc-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="b78bc-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-261">**Objective-C**:</span></span>

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


<span data-ttu-id="b78bc-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
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

## <span data-ttu-id="b78bc-263"><a name="facebook-sdk"></a>Практическое руководство: проверка подлинности пользователей с помощью пакета SDK Facebook для iOS</span><span class="sxs-lookup"><span data-stu-id="b78bc-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="b78bc-264">Пакет SDK Facebook для iOS можно использовать для входа пользователей в приложение с помощью Facebook.</span><span class="sxs-lookup"><span data-stu-id="b78bc-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="b78bc-265">Использование клиентского потока аутентификации предпочтительнее использования метода `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="b78bc-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="b78bc-266">Клиентский поток аутентификации обеспечивает более удобный пользовательский интерфейс входа и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="b78bc-267">Настройте серверную часть мобильного приложения для входа с помощью Facebook, следуя указаниям в руководстве [Как настроить приложение службы приложений для использования имени для входа Facebook][9].</span><span class="sxs-lookup"><span data-stu-id="b78bc-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="b78bc-268">Установите пакет SDK Facebook для iOS, как описано в документе [Facebook SDK for iOS - Getting Started][10] (Пакет SDK Facebook для iOS. Приступая к работе).</span><span class="sxs-lookup"><span data-stu-id="b78bc-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="b78bc-269">Вместо создания приложения можно добавить платформу iOS в имеющуюся регистрацию.</span><span class="sxs-lookup"><span data-stu-id="b78bc-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="b78bc-270">Документация Facebook содержит код Objective-C в делегате приложения.</span><span class="sxs-lookup"><span data-stu-id="b78bc-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="b78bc-271">При использовании **Swift** можно использовать следующие переводы для AppDelegate.swift.</span><span class="sxs-lookup"><span data-stu-id="b78bc-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
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
4. <span data-ttu-id="b78bc-272">Кроме добавления в проект `FBSDKCoreKit.framework` необходимо таким же образом добавить ссылку на `FBSDKLoginKit.framework`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="b78bc-273">Добавьте в приложение приведенный ниже код, соответствующий используемому языку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="b78bc-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-274">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
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

## <span data-ttu-id="b78bc-276"><a name="twitter-fabric"></a>Практическое руководство: проверка подлинности пользователей с помощью структуры Twitter для iOS</span><span class="sxs-lookup"><span data-stu-id="b78bc-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="b78bc-277">Структуру для iOS можно использовать для входа пользователей в приложение с помощью Twitter.</span><span class="sxs-lookup"><span data-stu-id="b78bc-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="b78bc-278">Использование клиентского потока аутентификации является более предпочтительным, чем использование метода `loginWithProvider:completion:` , так как он обеспечивает более удобный пользовательский интерфейс входа и позволяет выполнять дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="b78bc-279">Настройте серверную часть мобильного приложения для входа с помощью Twitter, следуя указаниям в учебнике [Как настроить приложение службы приложений для использования имени для входа Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="b78bc-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="b78bc-280">Добавьте структуру в проект, как описано в документе [Fabric for iOS - Getting Started] (Структура для iOS. Приступая к работе), а также установите TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="b78bc-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b78bc-281">По умолчанию структура создаст приложение Twitter.</span><span class="sxs-lookup"><span data-stu-id="b78bc-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="b78bc-282">Чтобы избежать создания этого приложения, можно зарегистрировать ключ клиента и секрет клиента, которые вы создали ранее, с помощью фрагментов кода ниже.</span><span class="sxs-lookup"><span data-stu-id="b78bc-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="b78bc-283">Кроме того, можно заменить значения ключа клиента и секрета клиента, которые предоставляются службе приложений, на значения, отображаемые на [панели мониторинга структуры].</span><span class="sxs-lookup"><span data-stu-id="b78bc-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="b78bc-284">Если выбран этот параметр, не забудьте задать URL-адрес обратного вызова для значения заполнителя, например `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="b78bc-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="b78bc-285">Если вы решили использовать ранее созданные секреты, добавьте в делегат приложения следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="b78bc-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="b78bc-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-286">**Objective-C**:</span></span>

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

    <span data-ttu-id="b78bc-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="b78bc-288">Добавьте в приложение приведенный ниже код, соответствующий используемому языку.</span><span class="sxs-lookup"><span data-stu-id="b78bc-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="b78bc-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-289">**Objective-C**:</span></span>

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

<span data-ttu-id="b78bc-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-290">**Swift**:</span></span>

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

## <span data-ttu-id="b78bc-291"><a name="google-sdk"></a>Практическое руководство: проверка подлинности пользователей с помощью пакета SDK Google Sign-In для iOS</span><span class="sxs-lookup"><span data-stu-id="b78bc-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="b78bc-292">Пакет SDK Google Sign-In для iOS можно использовать для входа пользователей в приложение с помощью учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="b78bc-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="b78bc-293">Недавно компания Google объявила о внесении изменений в свои политики безопасности OAuth.</span><span class="sxs-lookup"><span data-stu-id="b78bc-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="b78bc-294">Эти изменения политик в дальнейшем потребуют использовать пакет SDK для Google.</span><span class="sxs-lookup"><span data-stu-id="b78bc-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="b78bc-295">Настройте серверную часть мобильного приложения для входа с помощью Google Sign-In, следуя указаниям в руководстве [Как настроить приложение службы приложений для использования имени для входа Google](app-service-mobile-how-to-configure-google-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="b78bc-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="b78bc-296">Установите пакет SDK Google для iOS, следуя инструкциям в статье [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) (Google Sign-In для iOS — начало интеграции).</span><span class="sxs-lookup"><span data-stu-id="b78bc-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="b78bc-297">Раздел "Authenticate with a Backend Server" (Аутентификация на внутреннем сервере) можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="b78bc-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="b78bc-298">Добавьте в метод `signIn:didSignInForUser:withError:` делегата код, приведенный ниже (в соответствии с используемым языком).</span><span class="sxs-lookup"><span data-stu-id="b78bc-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="b78bc-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="b78bc-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="b78bc-301">Добавьте также показанный ниже код в `application:didFinishLaunchingWithOptions:` в делегате приложения, заменив SERVER_CLIENT_ID тем же идентификатором, с помощью которого вы настроили службу приложений на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="b78bc-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="b78bc-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="b78bc-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="b78bc-304">Добавьте приведенный ниже код в приложение в UIViewController, который реализует протокол `GIDSignInUIDelegate` (в соответствии с используемым языком).</span><span class="sxs-lookup"><span data-stu-id="b78bc-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="b78bc-305">Вы вышли перед повторным входом, и хотя вам не нужно повторно вводить учетные данные, вы увидите диалоговое окно согласия.</span><span class="sxs-lookup"><span data-stu-id="b78bc-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="b78bc-306">Вызывайте этот метод, только когда истек срок маркера сеанса.</span><span class="sxs-lookup"><span data-stu-id="b78bc-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="b78bc-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="b78bc-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b78bc-308">**Swift**:</span></span>

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
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="b78bc-309">[Быстрый запуск мобильного приложения Azure]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b78bc-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="b78bc-310">[динамическая схема]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="b78bc-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="b78bc-311">[панели мониторинга структуры]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="b78bc-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="b78bc-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="b78bc-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
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
